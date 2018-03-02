
# Protocol specification

* Transport: UDP, multicast
* Short
* Unreliable
* Messaging

## Size

Maximum size of all packet (without IP headers) - **508** bytes

## Channel

Channel is a identification of shared bus for communication.

Channel can be converted to multicast address by following rule: `multicast_ip = channel_idx % 16777215 + 4009754625`.
Where 

* 4009754625 is start multicast ip address (`239.0.0.1`)
* `channel_idx` - unsigned 64-bit integer, that identify shared channel
* `multicast_ip` - result multicast ip

Channel number must be in network order after [magic](#magic) bytes. If message arrives without channel number, it must be dropped

## Magic

Each packet must contains four octets in the begin: `0x4d 0x54 0x4c 0x4b`, that means 'MTLK' in ASCII. If packet not contains this prefix it must be dropped.


## Message

Anything else after topic is payload


## Packet

| Magic  | Topic    | Data
|--------|--------- |-----------|
| 4 byte | 4 bytes  | 0 - 500   |
