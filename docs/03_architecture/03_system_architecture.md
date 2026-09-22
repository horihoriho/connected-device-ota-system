# System Architecture

## 1. Overview

The system consists of a Connected Device, Management Server, MQTT Broker, and OTA Package Server.

The system provides remote monitoring, remote control, and software update through MQTT, TCP, and HTTP communication.


## 2. System Components

### 2.1 Connected Device

The connected device is a Linux-based device implemented mainly C++.

This device provides following functions:

- *Remote Monitoring*
    - collects device status
    - reports device status through MQTT 
    - responds to on-demand requests

- *Remote Control*
    - receives remote control requests through TCP
    - executes supported commands
    - responds command results

- *OTA(over the air)*
    - check for software updates through TCP
    - downloads OTA packages through HTTP
    - verifies and applies OTA packages
    - reports OTA results through TCP


### 2.2 Management Server

The management server connects with the connected device.

This server provides following functions:

- *Remote Monitoring*
    - receives device status through MQTT
    - sends on-demand device status requests

- *Remote Control*
    - sends remote control requests through TCP
    - receives command execution results

- OTA Management
    - receives software update check request through TCP
    - determines whether a software update is available
    - sends OTA package information to the device
    - receives OTA results through TCP


### 2.3 MQTT Broker

The MQTT broker provides asynchronous messages between the connected device and the management server.

This is mainly used for remote monitoring.


### 2.4 OTA Package Server

The OTA package server stores and distributes software update packages.
The connected device downloads OTA packages from the server through HTTP.

This server is basically separated from the management server, although both servers run on the same physical host in the initial implementation.
 

## 3. Communication Architecture

### 3.1 Remote Monitoring
### 3.2 Remote Control
### 3.3 OTA

## 4. System Architecture Diagram

## 5. Requirement Mapping
