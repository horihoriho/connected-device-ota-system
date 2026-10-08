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
| `device/{device_id}/status` | connected device | management server | report the latest device status for both periodic and on-demand monitoring |
| `device/{device_id}/status/request` | management server | connected device | request the latest device status for on-demand monitoring |

### 4.3 Message Design

#### 4.3.1 Device Status

**Purpose**
To report the latest device status for both periodic and on-demand remote monitoring

**Topic**
`device/{device_id}/status`

**Payload Format**
JSON (UTF-8)

**Payload Definition**
The device status message contains device identification, device health, and metadata information. 
All status should be sent if some fields are unavailable. 

| Field | Type | Format | Unit | Default | On Failure | Description |
| --- | --- | --- | --- | --- | --- | --- |
| `device_identification.device_id` | string | - | - | configured value | invalid message | unique ID of the device |
| `device_identification.hardware_model` | string | - | - | `null` | `null` | hardware model of the device |
| `device_identification.software_version` | string | - | - | configured value | invalid message | software version of the device |
| `device_identification.os_version` | string | - | - | `null` | `null` | os version of the device |
| `device_health.uptime` | integer | - | seconds | `null` | `null` | time elapsed since the system startup |
| `device_health.cpu_temperature` | number | - | celsius | `null` | `null` | current cpu temperature |
| `device_health.cpu_usage` | number | - | percent | `null`  | `null` | current cpu usage |
| `device_health.memory_usage` | number | - | percent | `null`  | `null` | current memory usage |
| `device_health.disk_usage` | number | - | percent | `null`  | `null` | current disk usage |
| `metadata.timestamp` | string | RFC3339 | - | `null` | `null` | timestamp when the device correct the device status |

**Example**
```Json
{
  "device_identification": {
    "device_id": "device01",
    "hardware_model": "Raspberry Pi 4 Model B",
    "software_version": "1.0.0",
    "os_version": "Raspberry Pi OS"
  },
  "device_health": {
    "uptime": 86400,
    "cpu_temperature": 48.2,
    "cpu_usage": 23.5,
    "memory_usage": 41.8,
    "disk_usage": 32.1
  },
  "metadata": {
    "timestamp": "2026-10-07T15:00:00Z"
  }
}
```

#### 4.3.2 Device Status Request

**Purpose**
To request the latest device status for on-demand remote monitoring

**Topic**
`device/{device_id}/status/request`

**Payload Format**
None (zero-length payload)

**Notes**
In general, request messages should contain request id to check the correlation between request and response.
Request/Response correlation is not supported based on the project scope.


### 4.4 QoS Design

MQTT QoS levels are selected based on message reliability, duplicate delivery tolerance, and communication overhead.

| Message | Publish QoS | Subscribe QoS |
| --- | --- | --- |
| Device Status | 1 | 1 |
| Device Status Request | 1 | 1 |

#### Design Considerations

- QoS 1 is used to improve message delivery reliability.
- QoS 1 allows the publisher to confirm message acceptance through PUBACK.
- Duplicate messages may occur with QoS 1.
- The Connected Device shall tolerate duplicate status requests.
- The Management Server shall tolerate duplicate device status messages.
- QoS 1 does not guarantee successful application-level process.

### 4.5 Connection Management

This section describes MQTT connection establishment, disconnection detection, reconnection, message retransmission, and session management between MQTT clients and the MQTT broker.

#### 4.5.1 Connection Establishment

The connected device and the management server shall establish MQTT connection with the MQTT broker.

The connection establishment process is defined as follows:

1. The MQTT client sends CONNECT packet to the MQTT broker
2. The MQTT broker responses CONNACK packet to the MQTT broker
3. The MQTT client confirms successful connection based on the CONNACK packet

If connection fails, the MQTT client shall initialize and retry establishment process.

#### 4.5.2 Disconnection Detection

The connected device and the management server shall detect the MQTT disconnection with the MQTT broker.

The disconnection detections are defined as follows:

- MQTT Keep Alive timeout
- MQTT client library error notifications

If disconnection is detected, the MQTT client shall initialize and retry connection process

#### 4.5.3 Reconnection 

The connected device and the management server shall reconnect to the MQTT broker when the MQTT connection is lost.

The reconnection process is defined as follows:

1. The MQTT client tries to reconnect to the MQTT broker once
2. If reconnection fails, the MQTT client retries after configured interval based on an exponential backoff strategy
3. After reconnection succeeds, the MQTT client reset the retry interval to initial value

The ecponential backoff strategy is adopt to reduce resource consumption.

#### 4.5.4 Message Retransmission



### 4.6 Monitoring Communication Flow




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
