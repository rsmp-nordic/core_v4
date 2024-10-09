---
layout: page
title: Aggregated Status
parent: Message Types
nav_order: 6
permalink: /messages/aggregate/
---
## Aggregated Status
We would perhaps consider this a status like any other, just defined to indicate the overall status of all components. It would be linked to the main component. Eg:

`status/<id>/main/system/aggregated`

An option would also be to split each aggregated status part into topics:
`status/<id>/main/system/aggregated/high`
`status/<id>/main/system/aggregated/low`
`status/<id>/main/system/aggregated/local_mode`