---
layout: page
title: Response
parent: Message Types
nav_order: 3
permalink: /messages/response/
---

## Command Response
A command reponses is published after handling a command.

```
response/<module>/<code>/<sender>[/<component>]
````

Examples:
```
response/tlc/2/45fe             # TLC M0002 (for main component) response from node 45fe
response/sensor/17/45fe/dl/3    # Sensor M0017 for detector logic 3 from node 45fe
```
