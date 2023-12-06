## Alarms
Devices could publish to
`alarm/<id>/<component>/<module>/<alarm>`

Where:
id: unique id of the device
component: component delivering the data
module: the module containing the alarm
alarm: the type of alarm

Supervisors could subscribe to all alarm from all devices using:
`alarm/#`

Or if you only want certain modules of alarms:
`alarm/+/sensor/+`

For example, a traffic light bb35 that has a hardware error might publish to:
`alarm/bb35/tlc/hardware`
