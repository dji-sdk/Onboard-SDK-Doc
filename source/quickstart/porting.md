---
title: Porting
date: 2020-05-8
version: 4.0.0
keywords: [Porting, OSDK, Hal, Osal]
---
> **NOTE** This article is **Machine-Translated**. If you have any questions about this article, please send an <a href="mailto:dev@dji.com">E-mail </a>to DJI, we will correct it in time. DJI appreciates your support and attention.

Port the application developed based on OSDK to the different OS and Platforms, OSDK offered the Hal and Osal layer libs.

> **NOTE** Those [sample](https://github.com/dji-sdk/Onboard-SDK)，use <a href="https://www.stmicroelectronics.com.cn/en/evaluation-tools/stm3241g-eval.html"><b>STM3241G-EVAL</b></a> for example to introduce howe to porting the application in other OS and hardware platforms

## Overview 
Port the application developed based on OSDK to different OS and Platforms, developer need to adapted the Hal (Hardware Abstraction Layer, hardware interface layer), and the Osal (Operating System Abstraction Layer) ), as shown in Figure 1.   
<div>
<div style="text-align: center"><p>Figure 1.Porting  </p>
</div>
<div style="text-align: center"><p><span>
      <img src="../images/OSDK-en.png" width="300" alt/></span></p>
</div></div>

> **NOTE**
> * Applications developed on STM32 using **OSDK 4.0 and above must** run on FreeRTOS;
> * Applications developed on STM32 using **OSDK 4.0 or least**, **can only run on the bare**.

## Concepts
### Hal
Hal (Hardware Abstraction Layer, hardware interface layer) is an OSDK hardware interface abstraction layer, located between the operating system, the application and hardware interface. Developers need to implement and adapt the functions of the Hal layer according to the function prototype in the specified interface Register to the application, so that the application developed based on OSDK can directly access the underlying resources of different computing platform hardware through the Hal layer and communicate with the drone.

* Don‘t use advanced visual functions
When not using advanced vision functions, the onboard computer only needs to communicate with the drone through the UART interface. Developers need to follow the function prototype in the `OsdkPlatform_RegHalUartHandler()` to implement and register the function that adapting the Hal to the application.

* Use advanced visual functions
When using advanced vision functions, the onboard computer needs to obtain the image data of the drone camera through the USB interface. Developers need to follow the function prototype in the `OsdkPlatform_RegHalUSBBulkHandler()` to implement and register the function that fits the Hal layer into the application.

### Osal
Osal (Operating System Abstraction Layer) is an OSDK operating system abstraction layer, located between the application and the operating system. Developers need to follow the function prototype in the `PsdkPlatform_RegOsalHandler()` interface to implement and register the functions that adapt the Osal layer to the application, so that applications developed based on OSDK can directly access the operating system and operating system kernel resources through the Osal layer To port applications to different operating systems.

#### Thread
To use the thread mechanism to manage the application to perform the corresponding tasks, developers need to implement the functions of creating threads, destroying threads, and thread sleep.

* Create thread:

```c
E_OsdkStat (*TaskCreate)(T_OsdkTaskHandle *task, 
                        void *(*taskFunc)(void *), 
                        uint32_t stackSize, void *arg)
```

* Destruction thread: `E_OsdkStat (*TaskDestroy)(T_OsdkTaskHandle task)`
* Thread sleep: `E_OsdkStat (*TaskSleepMs)(uint32_t timeMs)`

#### Mutex
Mutex is a mechanism used to prevent multiple threads from reading and writing to common resources (such as shared memory, etc.) on the same queue, counter, and interrupt handler at the same time. Use the mutex mechanism to manage the payload control program，developer needs to develop functions such as the mutex create, mutex destroys, mutex lock, and unlock.

* Mutex Create:`E_OsdkStat (*MutexCreate)(T_OsdkMutexHandle *mutex)`  
* Mutex Destroy:`E_OsdkStat (*MutexDestroy)(T_OsdkMutexHandle mutex)`  
* Mutex Lock:`E_OsdkStat (*MutexLock)(T_OsdkMutexHandle mutex)` 
* Mutex Unlock:`E_OsdkStat (*MutexUnlock)(T_OsdkMutexHandle mutex);`


#### Semaphore
The semaphore is a mechanism that prevents multiple threads from operating on the same code segment at the same time. Use the semaphore mechanism to manage the payload control program, the developer needs to develop functions such as semaphores creat, semaphores destroy, semaphores wait, semaphores timed wait and semaphores post.

* Semaphore Create: `E_OsdkStat (*SemaphoreCreate)(T_OsdkSemHandle *semaphore, uint32_t initValue)`
     > **NOTE** When using this interface, please set the initial value of the `initValue` semaphore.
* Semaphore Destroy : `E_OsdkStat OsdkOsal_SemaphoreDestroy (T_OsdkSemHandle semaphore)`
* Semaphore Wait: `E_OsdkStat OsdkOsal_SemaphoreWait (T_OsdkSemHandle semaphore);`
     > **NOTE** The maximum value of the wait time for the semaphore interface is **32767 ms**.

* Semaphore Timeout : `E_OsdkStat OsdkOsal_SemaphoreTimedWait (T_OsdkSemHandle semaphore, uint32_t waitTimeMs)`
* Semaphore Post: `E_OsdkStat OsdkOsal_SemaphorePost (T_OsdkSemHandle semaphore)`

#### System Time
Get the time of the system (ms):`E_OsdkStat OsdkOsal_GetTimeMs(uint32_t *ms);`

#### Memory Management
* Apply：`void *OsdkOsal_Malloc(uint32_t size);`
* Free：`void OsdkOsal_Free(void *ptr)`

## Develop With The Porting
### 1. Initialization
After creating the project file, please call the following interface to register the interface functions of the hardware platform and operating system to the application developed based on OSDK, **otherwise** the application developed using OSDK **will not be portable to other hardware platforms And on the operating system**.

```c++
E_OsdkStat OsdkPlatform_RegOsalHandler(const T_OsdkOsalHandler *osalHandler);
/*don't use advanced visual functions*/
E_OsdkStat OsdkPlatform_RegHalUartHandler(const T_OsdkHalUartHandler *halUartHandler);
/*use advanced visual functions*/
E_OsdkStat OsdkPlatform_RegHalUSBBulkHandler(const T_OsdkHalUSBBulkHandler *halUSBBulkHandler);
```


### 2. Load Files
#### Hal
* Linux/ROS：osdkhal_linux.c  
* STM32F4：osdkhal_stm32.c
#### Osal
* Linux/ROS：osdkosal_linux.c  
* STM32F4：osdkosal_stm32.c

### 3. Register The Port Module
#### Hal 
```c++
#ifdef ADVANCED_SENSING
  if(DJI_REG_USB_BULK_HANDLER(&halUSBBulkHandler) != true) {
    throw std::runtime_error("USB Bulk handler register fail");
  };
#endif
```

#### Osal
```c++
if(DJI_REG_OSAL_HANDLER(&osalHandler) != true) {
  throw std::runtime_error("Osal handler register fail");
}
```

## FreeRTOS
To port applications developed based on OSDK to the FreeRTOS platform, you need to obtain the kernel source code of FreeRTOS first.

#### 1. Get The Porting Code

* Download and unzip the FreeRTOS compressed package [V10.2.1](https://www.freertos.org/a00104.html), the main directory after the code is decompressed is shown below.
<div>
<div style="text-align: center"><p>Figure 2.FreeRTOS Main Directory  </p>
</div>
<div style="text-align: center"><p><span>
      <img src="../images/FreeRTOS_code1.png" width="500" alt/></span></p>
</div></div>


* Key files
   * Porting FreeRTOS core code     
   Copy all files under `/FreeRTOS/Source/` to `onboard-sdk/sample/platform/STM32/OnBoardSDK_STM32/OS/FreeRTOS/`.        
   <div>
<div style="text-align: center"><p>Figure 3. FreeRTOS Porting Files   </p>
</div>
<div style="text-align: center"><p><span>
      <img src="../images/FreeRTOS1.png" width="500" alt/></span></p>
</div></div>
    
   * Copy the configuration files       
    copy the `FreeRTOSConfig.h` file in`/FreeRTOS/Demo/CORTEX_M4F_STM32F407ZG-SK/`to` onboard-sdk/sample/platform/STM32/OnBoardSDK_STM32/OS/FreeRTOS/include` directory.       
   The file location of `FreeRTOSConfig.h`:     
<div>
<div style="text-align: center"><p>Figure 4. FreeRTOS Config File</p>
</div>
<div style="text-align: center"><p><span>
      <img src="../images/FreeRTOS_config1.png" width="500" alt/></span></p>
</div></div>


#### 2. Modify Key Config Information
Modify key information in `FreeRTOSConfig.h`   
  * Change`#ifdef __ICCARM__` to `#if defined (__ICCARM__) || defined (__CC_ARM) || defined (__GNUC__)`     
  * Change`#defined configUSE_IDLE_HOOK    2`to`#defined configUSE_IDLE_HOOK    2`     
  * Change`#define configTOTAL_HEAP_SIZE     ((size_t)(75*1024))`to`#define configTOTAL_HEAP_SIZE      ((size_t)(60*1024))`   
  * Change`#define configCHECK_FOR_STACK_OVERFLOW      2`to`#define configCHECK_FOR_STACK_OVERFLOW      0`    
  * Change`#define configUSE_MALLOC_FAILED_HOOK       1`to`#define configUSE_MALLOC_FAILED_HOOK       0`    
  The comparison of the FreeRTOSConfig.h is as below:
        <div>
<div style="text-align: center"><p>Figure 5. Modification Comparison
</p>
</div>
<div style="text-align: center"><p><span>
      <img src="../images/porting1.png" alt/></span></p>
</div></div>
