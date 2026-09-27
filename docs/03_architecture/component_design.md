# Component Design

## Connected Device Components 

The connected device software is divided into application, communication, and platform components.

### Application Components

The Application components consists of the following components:
- Remote Monitoring Component
- Remote Control Component
- OTA Management Component

#### Remote Monitoring Component

**Responsibilities**
- collect and report device status periodically
- handle on-demand status requests and report the latest status
- maintain the latest device status 

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
- receive and execute remote control requests
- report remote control results

**Input**
- remote control requests

**Output**
- remote control results 

**Dependencies**
- TCP communication component

#### OTA Management Component

**Responsibilities**
- request software update information
- download, verify, and apply an OTA package
- verify the update software version
- report the software update results

**Input**
- software update information
- OTA package

**Output**
- software update information requests
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

#### MQTT Communication Component

**Responsibilities**
- manage the connection with MQTT broker
- publish messages
- subscribe to topics
- handle connection failures

**Input**
- published messages 

**Output**
- received MQTT messages
- connection status

**Dependencies**
- None

#### TCP Communication Component

**Responsibilities**
- manage the connection with TCP server
- receive and send messages
- handle connection failures

**Input**
- messages to be sent 

**Output**
- received TCP messages
- connection status

**Dependencies**
- None

#### HTTP Communication Component

**Responsibilities**
- manage the connection with the OTA package server
- send HTTP requests
- receive HTTP responses
- handle the connection failures

**Input**
- OTA package download request

**Output**
- downloaded OTA package
- download result

**Dependencies**
- None

### Platform Components


The platform components provide device system information which is used for application components.

It consists of the system information component.

#### System Information Component

**Responsibilities**
- collect real-time system information from the device
- provide device information required by Applications

**Input**
- system information request 

**Output**
- device system information

**Dependencies**
- None


## Management Server Components

The management server is divided into application and communication components.

### Application Components

The Application components consists of the following components:
- Remote Monitoring Component
- Remote Control Component
- OTA Management Component

#### Remote Monitoring Component

**Responsibilities**
- receive periodic device status
- request and receive on-demand device status

**Input**
- device status
- on-demand monitoring trigger

Output
- on-demand device status request

**Dependencies**
- MQTT communication component

#### Remote Control Component

**Responsibilities**
- send remote control requests
- receive remote control results

**Input**
- remote control trigger
- remote control results

**Output**
- remote control requests

**Dependencies**
- TCP communication component


####  OTA Management Component

**Responsibilities**
- receive software information requests
- determine whether a software update is available
- provide software update information
- receive software update results

**Input**
- software information requests
- software update results

**Output**
- software update information

**Dependencies**
- TCP communication component


### Communication Components

The communication components provide network communication services which is used for application components.

It consists of the following components:
- MQTT communication component
- TCP communication component

#### MQTT communication component

**Responsibilities**
- manage the connection with MQTT broker
- publish messages
- subscribe to topics
- handle connection failures

**Input**
- published messages 

**Output**
- received MQTT messages
- connection status

**Dependencies**
- None

#### TCP Communication Component

**Responsibilities**
- manage the connection with TCP client
- receive and send messages
- handle connection failures

**Input**
- messages to be sent 

**Output**
- received TCP messages
- connection status

**Dependencies**
- None


## MQTT broker Component

**Responsibilities**
- accept connection with MQTT client
- route published message to subscribed clients
- manage MQTT subscriptions

**Connected Interface**
- Connected Device
- Management Server


## OTA Package Server Component

**Responsibilities**
- store OTA packages
- provide OTA package to connected devices through HTTP

**Connected Interface**
- Connected Device


## Component Interaction Diagram

```mermaid
```
flowchart LR

    %% =====================================================
    %% Connected Device
    %% =====================================================
    subgraph DEVICE["Connected Device"]

        subgraph D_APP["Application Components"]
            D_RM["Remote Monitoring"]
            D_RC["Remote Control"]
            D_OTA["OTA Management"]
        end

        subgraph D_COMM["Communication Components"]
            D_MQTT["MQTT Communication"]
            D_TCP["TCP Communication"]
            D_HTTP["HTTP Communication"]
        end

        subgraph D_PLATFORM["Platform Components"]
            D_SYS["System Information"]
        end

        D_SYS -->|"Device Status"| D_RM
        D_SYS -->|"Software Information"| D_OTA

        D_RM -->|"Device Status"| D_MQTT
        D_MQTT -->|"On-demand Status Request"| D_RM

        D_TCP -->|"Remote Control Request"| D_RC
        D_RC -->|"Remote Control Result"| D_TCP

        D_OTA -->|"Update Information Request / OTA Result"| D_TCP
        D_TCP -->|"Software Update Information"| D_OTA

        D_OTA -->|"Package Download Request"| D_HTTP
        D_HTTP -->|"OTA Package / Download Result"| D_OTA
    end


    %% =====================================================
    %% MQTT Broker
    %% =====================================================
    subgraph BROKER["MQTT Broker"]
        B["Broker"]
    end


    %% =====================================================
    %% Management Server
    %% =====================================================
    subgraph SERVER["Management Server"]

        subgraph S_APP["Application Components"]
            S_RM["Remote Monitoring"]
            S_RC["Remote Control"]
            S_OTA["OTA Management"]
        end

        subgraph S_COMM["Communication Components"]
            S_MQTT["MQTT Communication"]
            S_TCP["TCP Communication"]
        end

        S_MQTT -->|"Device Status"| S_RM
        S_RM -->|"On-demand Status Request"| S_MQTT

        S_RC -->|"Remote Control Request"| S_TCP
        S_TCP -->|"Remote Control Result"| S_RC

        S_TCP -->|"Update Information Request / OTA Result"| S_OTA
        S_OTA -->|"Software Update Information"| S_TCP
    end


    %% =====================================================
    %% OTA Package Server
    %% =====================================================
    subgraph OTA_SERVER["OTA Package Server"]
        P["Package Server"]
    end


    %% =====================================================
    %% Communication Protocols
    %% =====================================================
    MQTT_D(["MQTT"])
    MQTT_S(["MQTT"])
    TCP(["TCP"])
    HTTP(["HTTP"])


    %% =====================================================
    %% System-Level Connections
    %% =====================================================
    D_MQTT <--> MQTT_D
    MQTT_D <--> B

    B <--> MQTT_S
    MQTT_S <--> S_MQTT

    D_TCP <--> TCP
    TCP <--> S_TCP

    D_HTTP <--> HTTP
    HTTP <--> P
```


```
