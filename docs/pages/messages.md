---
title: Messages
permalink: /messages/
nav_order: 100
has_children: true
has_toc: false
---

# Messages
RSMP 4 defines the following messages with coresponding topic paths structures:


| Message type | Topic path |
|-|-|
| [Presence](presence.md) | `presence/<sender>` |
| [Status](status.md) | `status/<module>/<code>/<sender>/<component>` |
| [Command](command.md) | `command/<module>/<code>/<receiver>/<component>` |
| [Result](result.md) | `result/<module>/<code>/<sender>/<component>` |
| [Alarm](alarm.md) | `alarm/<module>/<code>/<sender>/<component>` |
| [Reaction](reaction.md) | `reaction/<module>/<code>/<receiver>/<component>` |


All these topic paths (except presence) follow this layout:

```
<type>/<module>/<code>/<node>[/<component>]
```

- type: the type of message, either presence, statuss, command, resposne, alarm or reaction.
- module: the name of the module.
- code: the code of command/status/alarm within the module.
- node: the id of the sender or receiver, depending on the message type.
- component: indentifies one or more [components](components.md).

The component can be left out as a shortcut to refer to the main component.

The component is includes as part of the topic path (except for presence messages) to ensure that you can retain status, commands an alarms for each component.

## Payload CBOR Encoding
Message payloads consist of JSON encoded in binary format using [CBOR (Concise Binary Object Representation)](https://cbor.io).

Using CBOR encoding saves space, while still retaining the JSON data model, which is very easy to work with.

CBOR is natively supported in many MQTT tools, making it painless to interact with RMSP 4 messages encoded with CBOR. 
