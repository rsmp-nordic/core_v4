# Alarms

## Publishing
Devices publish to:

`alarm/<id>/<component>/<module>/<alarm>`

id: unique id of the device
component: component delivering the data
module: the module containing the alarm type
alarm: the type of alarm

For example, a traffic light `bb35` that has a hardware error might publish to:
`alarm/bb35/tlc/hardware`


## Subscribing
Supervisors can subscribe to all alarm from all devices using:
`alarm/#`

Or if you only want alarms from a certain module:
`alarm/+/sensor/#`

