## Status
```
status/<module>/<sender>/<node>[/<component>]
````

Examples:
```
status/tlc/14/45fe        # S0014 current signal plan for the main component on node 45fe
status/tlc/25/45fe/sg.1   # S0025 time-of-green for signal group 1 on node 45fe
```

Sites publish status to:
`status/<id>/<component>/<module>/<status>`

- id: unique id of the device
- component: component delivering the data
- module: module containing this type of status
- status: the type of status
- the payload contains the status attributes.

For example, a traffic sensor with the id `12d9` which reports traffic counts from the component `dl1`, using the status `volume` in the module `traffic`, would publish to the topic
`status/12d9/dl1/traffic/volume`.

The payload would contain the actual data.

### Is anyone listening?
One of the ideas of MQTT is that clients don't have to know anything about each other. They just need the address of the broker, and some topic to publish/subscribe to. This means that a sensor, e.g. a thermometer, starts publishing data as soon as it connects to the broker, regardless of whether anyone is listening.

A benefit of this is that the broker can be set up to persists data to a database, regardless of which clients (supervisors) are connected.
But if the data has a significant size, a downside might be that you spend bandwidth for no reason, in case nobody is listening.

This could also be an issue if the device can deliver the data in several formats, aggregation intervals, etc. Instead of having to publish in all formats, only what's asked by supervisor should be send.

In RSMP 3 you can set the status interval, either a fixed interval, or send on change. Some settings might result if high data bandwidth, like signal group status for all groups every second, or some traffic sensor that has a lot of very frequent changes.

How could this be handled in MQTT?

It should be possible to use topics for building our own subscription mechanism on top of MQTT if we need to.

Subscriber count: Devices could subscribe to a 'subscribe' channel, and supervisor would post to them when they want data.
The device would keep count of who subscribed to the data. If at least one is subscribed, the device starts publishing data. Last Will can be used by supervisor to inform devices in case they go offline, and the device can update the subscribe count. If nobody is listening anymore, it can stop publishing data. To avoid 'dead listeners' we could require supervisor to resubscribe within some period, like 1 minute/hour/day.

Timed: Supervisors could also inform a device that it would like data to be send for some interval. A supervisor would have to ask for more before the current interval times out. If the supervisor dies, the device will then stop sending data at some point.

### Update intervals
If we want a supervisor to be able to subscribe to data at arbitrary intervals, device could publish to topics that include the update interval in the topic name e.g an interval of once per minute:
`status/12d9/traffic/volume/1m`

A device could perhaps offer some fixed interval that you can use, e.g. 1s, 10s, 1m, 10m,  1h, 24h

### Subscriptions
If we need to provide different data stream to each supervisor, another approach would be for each supervisor to subscribe to a topic that include the id of the supervisor. The supervisor informs the device about what data it wants, and the device then starts publishing to a topic that includes the id of the supervisor, which only that particular supervisor reads.

Example:

A traffic sensor with the id 6b41 can deliver traffic speeds and other metrics. The device subscribes to:
`subscribe/6b41/traffic/+`
`unsubscribe/6b41/traffic/+`

These topics are used to receive status subscribe/unsubscribe requests.

A supervisor with id 299c wants to receive traffic volumes once per 10s.
It posts to `subscribe/6b41/traffic/speed`, passing it's id and the desired update interval.
It then subscribes to `status/6b41/to/299c/traffic/speed` to receive data at the desired interval.

The device receives the request, and starts publishing every 10s to `status/6b41/to/299c/traffic/speed`

When the supervisor does not want to receive data anymore, it send a message to `unsubscribe/6b41/traffic/speed`, passing it's id. The device then stops publishing to `status/6b41/to/299c/traffic/speed`.

If the supervisor dies ungracefully, a Last Will can be send to `died/299c` to inform the device that the supervisor wet away.
The device could either:
- Keep publishing. Pro: data is retained by the broker, and send to the supervisor once it reconnects: Con: if the supervisor never comes back, data is still being send by the device and retained on the broker, and could take up a bandwidth and storage.
- Stop publishing (perhaps after some timeout): Pro: no bandwidth or storage is used in case the supervisor doet not come back. Con: data is lost unless is is stored locally on the device and retransmitted using some custom mechanics we would need to design.


## Aggregation
A question is whether a device should be able to provide data in several different aggregations at the same time (to different supervisor) or just one.

Or whether we want to move to model where devices send just raw data, and aggregation is handled later in the chain.
