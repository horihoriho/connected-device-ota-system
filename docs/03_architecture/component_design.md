# Component Design

## Connected Device Components 

The connected device software is divided into application components and communication components.

### Application Components

The Application components consists of the following components:
- Remote Monitoring Component
- Remote Control Component
- OTA Manager Component

#### Remote Monitoring Component

**Responsibilities**
- collect and report status periodically
- handle on-demand status requests and report them
- Always maintain the latest status 

**Input**
- device status
- periodic reporting trigger 
- on-demand status request

**Output**
- device status for periodic reporting
- device status for on-demand reporting

**Dependencies**
- MQTT communication component
- System Information component

#### Remote Control Component

**Responsibilities**
- receive and execute remote control request
- report remote control results

**Input**
- remote control requests

**Output**
- remote control results 

**Dependencies**
- TCP communication component

#### OTA Manager Component

**Responsiblities**
- check whether software updates is available or not  
- inquire software update requests
- download, verify, and apply an software
- report the software update results

**Input**
- software Information
- update software

**Output**
- software update requests
- software update results

**Dependencies**
- TCP communication component
- HTTP communication component
- System information component


### Communication Components

The communication components provide network communication services which is used for application components.

It consists of the following components:
- MQTT communication component
- TCP communication component
- HTTP communication component


### Platform Components



