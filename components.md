# Components
A devices or system has one or more components, representing physical of logical parts.

Each component has a specific type, for eaxample a traffic light controller might haave signal groups and detector logics.

## Component Paths
Components are referenced using component paths. A component path consists of one or more parts, separated by dots. For example, a  traffic light controller with two signal groups (sg) and four detector logics (dl) might have these paths:

```
tc
sg.1
sg.2
dl.video.1
dl.video.2
dl.loop.1
dl.loop.2
```

Note that component paths does not include the site id.

## Component Groups
You can address groups of component by pointing to intermediate levels. For example:

All detector logics: `dl`  
All video detectors: `dl.vide.`  
All signal groups: `sg`  

## Main component
Exactly one root level component must be configured as the main comnponent. This component is used to refer to the device as a whole.

As a shorthand, you can use an empty component path, or leave it out, to refer to the main component.
 

