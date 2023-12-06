## Command
All devices subscribe to a command topic that includes their id, which the supervisor can publish to. 

Device subscribe to  `command/<id>/<component>/<module>/<cmd>`

id: the id of the device itself
module: the sxl module (category of command)
cmd: the command

The payload contains the parameters in JSON format.

For example, a traffic light with id 45fe might subscribe to all command for all components using either single level wildcards with:
`command/45fe/+/+/+` 

Or using a multi-level wildcard:
`command/45fe/#`

Now the supervisor can send commands to this particular traffic light and component by publishing to `command/45ef/<component>/...`

Suppose the traffic light has these components:

- main: the main controller, handles, eg. signal program changes
- sg1: signal group 1
- sg2: signal group 2
- dl1: detector logic 1
- dl2: detector logic 2

And let's suppose the traffic light supports these modules:
- tlc: traffic light controller commands
- detector: traffic detectors used for local traffic control


### Change signal plan
`command/45fe/main/tlc/plan`

We send the command to the `main` component.
We use `plan` command in the `tlc` module.

The payload would include the arguments, like what plan to switch to.

### Set detector sensibility
`command/45fe/dl1/detector/sensibility`

We send the command to the `dl1` component.
We use `sensibility` command in the `detector` module.

The payload would include the arguments, like the sensibility value.

### Sending to many devices
A traffic light with id 45fe could subscribe to a topic with the id 'all':
`command/all/#`

Or a bit more selectively:
`command/all/main/tlc/+` 
`command/all/+/detector/+` 

The supervisor can publish to this topic to e.g. change the signal plan on all traffic lights at the same:
`command/all/main/tlc/plan`

Or change the detector sensibility on all detector logics in a particular traffic lights:
`command/45fe/all/detector/plan`

Or change the detector sensibility on all detector logics in all traffic lights:
`command/all/all/detector/sensibility`


## Response
How would command responses be handled? We would use the request-response pattern, which is based on Response Topics. When you send a command, you pass a topic that would want to response to be published to. A supervisor sending a command could pass the response topic:
`response/<supervisor_id>/component/module/command`.

When a supervisor with id 22ba changing plan with `command/45fe/main/tlc/plan`, the respons would be send to `response/22ba/main/tlc/plan`.

All supervisor can receive response if the just subscribe to `response/+/main/tlc/plan`.
