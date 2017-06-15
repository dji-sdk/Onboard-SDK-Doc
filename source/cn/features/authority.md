#Authority

## Version control

**All OSDK only have technical support for latest product Firmware version**


| Product 	| Latest FW 	 |Drone Version| OSDK V2.3  | OSDK V3.2.1 		   | OSDKV3.3 	 	|
|:-------------:|:--------------:|:-----------:|:----------:|:----------------------------:|:------------------:|
| M100    	|		 | 	       |EOL         | Support latest FW 	   | Not support  	|
| A3 	 	|		 | 	       |N/A         | Version below 3.2.36.00	   | Support latest FW 	|
| N3 	  	|  		 | 	       |N/A         | Version below 3.2.36.00	   | Support latest FW	|
| M600 Pro 	|  		 | 	       |N/A 	    | Version below 3.2.36.00	   | Support latest FW	|
| M210 	  	|  		 | 	       |N/A         | N/A			   | Support latest FW	|
| M210-RTK 	|  		 | 	       |N/A         | N/A			   | Support latest FW	|

##Get Versions

### SDK version

SDK version is only a tag for distinguish different SDK releases, you could check them by:

* github branch names
* github release tags

### Drone version

each FW have a internal version called Drone version to show which components of Open Protocal it supported.

you could chech the Drong version by invoke API: 

`DJI::OSDK::Vehicle::getDroneVersion`

it is an overloaded API, you could check more details through the [doxygen doc](../../doxygen/index.html)