---
title: Messages
permalink: /messages/
nav_order: 100
has_children: true
---

# Messages
RSMP 4 is based on MQTT. Messages are  send by publishing to a topic path and passing a payload.


## Payload
Message payloads consist of JSON encoded in binary format using [CBOR (Concise Binary Object Representation)](https://cbor.io).

Using CBOR encoding saves space, while still retaining the JSON data model, which is very easy to work with.

CBOR is natively supported in many MQTT tools, making it painless to interact with RMSP 4 messages encoded with CBOR. 
