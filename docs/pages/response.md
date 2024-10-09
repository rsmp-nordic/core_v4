---
layout: page
title: Response
parent: Message Types
nav_order: 3
permalink: /messages/response/
---

## Command Response
```
response/<module>/<code>/<sender>[/<component>]
````

Examples:
```
response/tlc/2/45fe             # responde to M0002 set signal plan status (for main component) on node 45fe
response/traffic/17/45fe/sg.1   # response to hyopthetical M0017 set detector treshold for sigmal group 1 on node 45fe
```
