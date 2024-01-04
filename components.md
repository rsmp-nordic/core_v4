# Components

A devices has one or more components, representing physical of logical parts of the equipment or system. Each component has a specific type.

A specific component must be the main component, representing the entire device.

For example, a traffic light will have a main "traffic controller" component, plus one for each signal group and detector logic.

## Component Names
In RSMP 3, each component has a unique name and there is no grouping, except what's implied by the names. For example, a traffic light controller might have these components:

```
TC000
DL001, DL002
SG001, SG002
```
Here TC000 is the main component, DL means a detector logics, and SG means a signal group.

This is known as component names.

With RSMP 4, you can continue to use component names (assuming they are configured on the device). For example you can address signal group 1 as `KK+AG0105/SG001`, or the main component as `KK+AG0105/TC000`.

## Component Paths
RSMP 4 allows you to organize components hierarchically and address then using paths. A path starts with `.` and uses `.` as the delimiter.

For example, a traffic light controller might have these components configured:

```
dl
  1
  2
sg
  1
  2
```

Paths make it possible to address all components of a specific type, e.g. to send a command to them all, or to requeest status from them. For example, all detector logics can be addressed as `.dl`.

An individual component is is adressse it's path, e.g. signal group 1 is addressed as `.sg.1`.

Note that there is no need to explicitly configure a name for the main component. The main component can always be adresses with `.`.

### Nesting
You can use deeper nesting if you want, for example to organize different types of detectors or signal groups:

```
dl
  radar
    1
    2
  video
    1
    2
sg
  1
  2
  ```

Here, the second video detector would be addresss as `.dl.video.2`.

Nesting could also be used to handle multiple sub-interections in a single traffic light controller:

```
sub
  a
    sg
      1
      2
    dl
      1
      2
  b
    sg
      1
      2
      3
  ```

`.` would adress a main component, which pressumably would not a a signal controller, but rather something that coordinates several intersections.

`.sub` would addres both intersections together. To address a specifici sub-controller you would use `.sub.a` or `.sub.b`.
You would address the second detector logic of intersection 1 as `.sub.a.dl.2`.


## Migration from RMSP 3
RSMP 4 component path can be used alongside RMSP 3 component names, as long as component names do not start with a dot.

Devices migrating from RSMP 3 to RSMP 4 should continue to support the existing component names if they are configured. Component paths can be added when desired, in which case the corresponding name and path should adress the same component, e.g. `KK+AG0105/DL0001` and `KK+AG0105/dl.1` will address the same component.

After confiuring paths, can you choose to remove flat names to simplify the setup, or leave them for compatibility.


