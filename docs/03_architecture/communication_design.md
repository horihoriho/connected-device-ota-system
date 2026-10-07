# Communication Design

## 1. Overview

This document defines the communication design between the connected device, the management server, and the MQTT broker, and the OTA package server.

The communication design specifies the detailed communication specification for MQTT, TCP, and HTTP based on system architecture and component design.
It also defines communication roles of each system components and the communication matrix which describe communication relationships between components.


## 2. Communication Roles

The system uses MQTT, TCP, and HTTP for different communication.

**MQTT**

MQTT is used for remote monitoring. 
The publish/subscribe model allows multiple connected devices to communicate monitoring messages with the management server through the MQTT broker.  
This model is suitable for asynchronous monitoring communication.

**TCP**
TCP is used for remote control and OTA control between the connected device and the management server.
The bidirectional communication allows the connected device to communicate directly and reliably with the management server. 
A TCP connection is suitable for exchanging control requests and their corresponding results between the two.

**HTTP**
HTTP is used for downloading OTA packages from the OTA package server.
The OTA package can contain large data compared with others. HTTP provides a standard request/response protocol for transferring files and allows the connected device to download OTA packages directly form the OTA package server.

## 3. Communication Matrix

| Function | Sender | Receiver | Protocol | Message |
| --- | --- | --- | --- | --- |
| periodic monitoring | connected device | management server | MQTT | device status |
| on-demand monitoring | management server | connected device | MQTT | status request | 
| on-demand monitoring | cennected device | management server | MQTT | device status |
| remote control | management server | connected device | TCP | control request |
| remote control | connected device | management server | TCP | control result |
| OTA update checking | connected device | management server | TCP | update information request | 
| OTA update checking | management server | connected device | TCP | update information result |
| OTA update result | connected device | management server | TCP | update result |
| OTA package downloading | connected device | OTA package server | HTTP | package download request |
| OTA package downloading | OTA package server | connected device | HTTP | OTA package |


## 4. MQTT Communication Design

### 4.1 Overview
MQTT is used for exchanging remote monitoring messages, including periodic device status reports, on-demand status requests, and on-demand status responses, between the connected device and management server through the MQTT broker. 

### 4.2 Topic Design
| Topic | Publisher | Subscriber | Purpose | 
| --- | --- | --- | --- |
| device/{device_id}/status | connected device | management server | report the latest device status for both periodic and on-demand monitoring |
| device/{device_id}/status/request | management server | connected device | request the latest device status for on-demand monitoring |

### 4.3 Message Design

   4.4 QoS Design
   4.5 Connection Management
   4.6 Monitoring Communication Flow

## 5. TCP Communication Design

### 5.1 Overview
TCP is used for exchanging remote control and OTA management messages, including ....

5.2 Connection Design
   5.3 Message Types
   5.4 Message Framing
   5.5 Request / Response Mapping
   5.6 Connection Failure and Reconnection
   5.7 Remote Control Communication Flow
   5.8 OTA Control Communication Flow

## 6. HTTP Communication Design
   6.1 Overview
   6.2 Request / Response Design
   6.3 OTA Package Download
   6.4 Download Failure Handling

## 7. Communication Design Summary
