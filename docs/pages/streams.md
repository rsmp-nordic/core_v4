---
title: Streams
permalink: /streams/
nav_order: 7
---

# Streams
Status updates are delivered via _streams_.

A stream defines how data is delived, including:

- attribute set
- update rate
- aggregation, e.g. sum and average
- chunking. ie. gather multiple events in a single message
- activation defaults
- timeouts

A node can have ome or more streams configured for each status type. 

Unlike RSMP 3, you don't specify subscription settings when you start fetching data.
Instead you choose between the already defined streams.

```mermaid
graph LR
A[Service A]-->|traffic/1/live| Broker
A[Service A] -->|traffic/1/hourly| Broker
Broker-->|traffic/1/live| B[Manager A]
Broker-->|traffic/1/hourly| B[Manager A]
Broker -->|traffic/1/live| C[Manager B]
Broker -->|traffic/1/hourly| D[Manager C]
```

If the node allows stream administration, consumers can add/edit streams.

## Starting and stopping streams
When you start a stream on a node, the starts publishing data to the associated topic path.

Consumers still have to subscribe to the associated topic path to receive data.

When you stop a stream on a node, the node stops publishing data to the associated topic path.

### Off by default
Streams can be configured to be off by default, in which case a consumer must start the 
stream before the ndoe starts publishing to the associated  topic path

### On by default
Streams can be configured to be on by default, in which case the node starts publishing
as soon as it starts, and you don't need to explicitly start the stream.

You can still stop the stream, in case you don't need the data anymore.

### Always-on
Streams can be configured to be always-on, in which case the node starts publishing
as soon as it starts up. The stream cannot be stopped.

The benefit is that you're garanteed that the data is always send to the broker.

## Listing Streams
The node provides a list of streams available, with information about attribute set,
update rate, aggregation, etc.

## Stream Administration
Streams are configured on a node.

If the node supports stream administration, consumers can edit/add/remove steams.

- add new stream
- edit existing stream
- remove existing stream

Access to stream administration can be managed by access control lists on the broker.

## Stream
A streams can be configured to automatically stop when consumers disappear, or have
been offline for a predefined period.
This is useful for streams that take up significant bandwidth, and you want to be sure
that they are stopped when not used anymore.
Automatic stopping can be based on timeouts and `presence` message, which informs the node
when other nodes go online/offline.
[To be expanded.]




