---
layout: page
title: Alarm
parent: Messages
nav_order: 4
permalink: /messages/alarm/
---

# Alarm
```
alarm/<module>/<code>/<sender>[/<component>]
````

Examples:
```
alarm/tlc/1/45fe   # A0001 serious hardware error (for main component) on node 45fe
alarm/tlc/301/45fe/dl.7   # A0301 serious deteector error for component dl.7 on node 45fe
```

For example, a traffic light `bb35` that has a hardware error in detector logic 4 might publish to:
`alarm/tlc/1/bb35/dl/4`


## Subscribing
Supervisors can subscribe to all alarm from all devices using:
`alarm/#`

Or if you only want alarms from a certain module:
`alarm/sensor/#`

