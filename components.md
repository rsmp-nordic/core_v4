# Components
A devices or system has one or more components, representing physical of logical parts.

Each component has a specific type, for eaxample a traffic light controller might haave signal groups and detector logics.

## Component Paths
Components are referenced using component paths. A component path consists of one or more parts, separated by slashes. For example, a  traffic light controller with two signal groups (sg) and four detector logics (dl) might have these paths:

```
tc
sg/1
sg/2
dl/video/1
dl/video/2
dl/loop/1
dl/loop/2
```

Note that component paths does not include the site id.

## Component Groups
You can address groups of component by pointing to intermediate levels. For example:

All detector logics: `dl`  
All video detectors: `dl/video`  
All signal groups: `sg`  

## Main component
Exactly one component at root leve must be configured to the main comnponent, and this component can be used to refer to the device as a whole.
As a shorthand, an empty component path can be used to refer to the main component. In RSMP 4 topic path this is done by leaving out the component path entirely.
 
## Component Names
Component names is what is used in RSMP 3 and consist of strings. For example, a traffic light controller might have these components:

```
KK+AG0105=000TC000
KK+AG0105=000DL001
KK+AG0105=000DL002
KK+AG0105=000SG001
KK+AG0105=000SG002
```

In this example, TC is the main component, DL is a detector logics, and SG is a signal group. There is no grouping, except what's implied by the names.

Note that component names include the site id. This causes some redundancy when sending messages.

## Migration from RMSP 3
In RSMP 4, you can stil use RSMP 3 component names, assuming they are configured on the device. However we recommend  using Component Paths.

Component path can be used alongside component names, as long as component names do not include `/`.

Devices migrating from RSMP 3 to RSMP 4 should continue to support the existing component names if they are configured. Component paths can be added when desired, in which case the corresponding name and path should adress the same component, e.g. `KK+AG0105=000DL001` and `/dl/1` would refer to the same component.

After configuring paths, can you choose to remove component names to simplify the setup, or leave them for compatibility.


