# Protocol specification

* Transport: UDP, multicast
* Short
* Unreliable
* Messaging

## Channel

Indexed by number from [0-65535].

## Topic
* 1 byte  - size of topic
* up to 63 - content

## Message

* 2 byte (network order) - size of content
* up to 442 - payload

