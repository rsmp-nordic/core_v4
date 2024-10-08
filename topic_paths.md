# Topic Paths
All messages follow this topic path layout:

```
<type>/<module>/<code>/<node>[/<component>]
```

- type: the type of message, either presence, statuss, command, resposne, alarm or reaction.
- module: the name of the module
- code: the code of command/status/alarm within the module
- node: the id if sender or receiver, depending on the mesage type
- component: component path indentifying one or more components, can be left out as a shortcut to refer to the main component.

Attributes and data are send in the payload, not as part of the topic path.

The node id represents wither a sender or a receiver, depending on the message type.

The [Component path](components.md) consists or zero, one or more parts separate with slashes.

MQTT allows a retained value per topic path. The component is includes as part of the topic path (except for presence messages) to ensure that you can retain status, commands an alarms for each component.

## Messages summary

| Message type | Topic path |
|-|-|
| [Presence](presence.md) | `presence/<sender>` |
| [Status](status.md) | `status/<module>/<code>/<sender>/<component>` |
| [Command](command.md) | `command/<module>/<code>/<receiver>/<component>` |
| [Response](response.md) | `response/<module>/<code>/<sender>/<component>` |
| [Alarm](alarm.md) | `alarm/<module>/<code>/<sender>/<component>` |
| [Reaction](reaction.md) | `reaction/<module>/<code>/<receiver>/<component>` |

