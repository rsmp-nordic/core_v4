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

MQTT allows a retained value per topic path. The component is includes as part of the topic path (except for presence messages) to ensure that you can retain status, commands an alarms for each component.

## Presence
```
presence/<sender>
````

Examples:
```
presence/45fe   # node 45fe went online/offline
```

## Status
```
status/<module>/<sender>/<node>[/<component>]
````

Examples:
```
status/tlc/14/45fe        # S0014 current signal plan for the main component on node 45fe
status/tlc/25/45fe/sg.1   # S0025 time-of-green for signal group 1 on node 45fe
```

## Command
```
command/<module>/<code>/<receiver>[/<component>]
````

Examples:
```
comamand/tlc/2/45fe             # M0002 set signal plan status (for main component) on node 45fe
comamand/traffic/17/45fe/sg.1   # hyopthetical M0017 set detector treshold for sigmal group 1 on node 45fe
```

## Command Response
```
response/<module>/<code>/<sender>[/<component>]
````

Examples:
```
response/tlc/2/45fe             # responde to M0002 set signal plan status (for main component) on node 45fe
response/traffic/17/45fe/sg.1   # response to hyopthetical M0017 set detector treshold for sigmal group 1 on node 45fe
```

## Alarm
```
alarm/<module>/<code>/<sender>[/<component>]
````

Examples:
```
alarm/tlc/1/45fe   # A0001 serious hardware error (for main component) on node 45fe
alarm/tlc/301/45fe/dl.7   # A0301 serious deteector error for component dl.7 on node 45fe
```

## Alarm Reaction
```
reaction/<module>/<code>/<receiver>[/<component>]
````

Examples:
```
reaction/tlc/1/45fe   # reaction to A0001 serious hardware error (for main component) on node 45fe
reaction/tlc/301/45fe/dl.7   # reaction A0301 serious deteector error for component dl.7 on node 45fe
```
