
# Protocol specification

* Transport: UDP, multicast
* Short
* Unreliable
* Messaging

## Size

Maximum size of all packet (without IP headers) - **508** bytes

## Channel

Channel is a 'physical' identification of shared bus for communication.

Channel can be converted to multicast address by following rule: `multicast_ip = channel_idx % 16777215 + 4009754625`.
Where 

* 4009754625 is start multicast ip address (`239.0.0.1`)
* `channel_idx` - unsigned 32-bit integer, that identify shared channel
* `multicast_ip` - result multicast ip


## Magic

Each packet must contains four octets in the begin: `0x4d 0x54 0x4c 0x4b`, that means 'MTLK' in ASCII. If packet not contains this prefix it must be dropped

## Topic

Topic - logical identification of shared communication.

It's simple byte array up to 255 bytes.


| Payload size | Payload   |
|--------------|-----------|
| 1 bytes      | up to 255 |

Listening topics must be explicitly set by receiver. If receiver get topic, that not in subscription list, it must drop it silently.

## Auto channel

Calculates by hash of topic. It is not strictly unique hash function and used only for reducing collision. Mutalk using CRC-32-IEEE 802.3


## Message

Anything else after topic is payload


## Packet

| Magic  | Topic   size | Topic     | Data
|--------|--------------|-----------|---------|
| 4 byte | 1 bytes      | up to 255 | 0 - 503*

\* - total size of packet must be not more then 508 bytes


