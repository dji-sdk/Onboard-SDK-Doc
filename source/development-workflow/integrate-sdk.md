---
title: Integrate The SDK Into Your Own Application
date: 2017-06-01
version: 3.3
keywords: [write apps, developemtn, SDK, integrate, DJI]
---

## Project Structure

This diagram shows the structure of the SDK in the context of writing apps:

![integrate-sdk](../images/workflow/djiosdk_integrate_into_app.png)


## Including DJI OSDK Headers in Your Code

The [hierarchy diagram](../introduction/sdk-architectural-overview.html#hierarchy) in the SDK Architectural Overview shows that the Vehicle class contains references to all components available through the OSDK.
Thus, `Vehicle` acts as an entry point for user code.

Let's take an example - `mission_sample` provided as part of the Linux samples. Here is a snippet of `mission_sample.hpp`:

![integrate-sdk-sample](../images/workflow/integrate_sdk_includes.png)

- L17-19: Includes that your application needs for the code you are writing
- L22: DJI OSDK Include. This is the only DJI OSDK header you need to include in your application.
- L25: Helper functions that read User Configuration files on the Linux platform, and execute activation of the drone.
       You may re-use these functions in your code if you are developing standalone applications for a Linux platform.

## Setting Up Dependencies

This section assumes you are using the CMake build system on Linux; the steps however are general enough to be
conceptually reused with different platforms/build systems.



The DJI OSDK library is self-contained, and to build against the library you have two options:

- Build the `djiosdk-core` target locally
