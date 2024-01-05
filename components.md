# Components

A devices has one or more components, representing physical of logical parts of the equipment or system. Each component has a specific type.

A specific component must be the main component, representing the entire device.

For example, a traffic light will have a main "traffic controller" component, plus one for each signal group and detector logic.

## Component Names
In RSMP 3, each component has a unique name and there is no grouping, except what's implied by the names. For example, a traffic light controller might have these components:

```
KK+AG0105=000TC000
KK+AG0105=000DL001
KK+AG0105=000DL002
KK+AG0105=000SG001
KK+AG0105=000SG002
```
In this example, TC is the main component, DL is a detector logics, and SG is a signal group.

This is known as component names. With RSMP 4, you can continue to use component names (assuming they are configured on the device).

## Component Paths
RSMP 4 allows you to organize components hierarchically and address both individidual components and groups of components using paths. A path starts with `.` and uses `.` as the delimiter.

For example, a traffic light controller might have these components configured:

```
dl
  1, 2
sg
  1, 2
```

Individual components are adresssed using the path , e.g. signal group 1 is addressed as `.sg.1`.

You can address groups of components e.g. to send a command to them. For example, all detector logics can be addressed with `.dl`.

The main component can always be adresses with `.`. There is no need to explicitly configure a main component. 

### Nested Component Paths
You can use deeper nested component paths if you want, for example to organize different types of detectors or signal groups:

```
dl
  radar
    1, 2
  video
    1, 2
sg
  1, 2
  ```

Here, the second video detector would be addresss as `.dl.video.2`.

Nesting could also be used to handle multiple sub-interections in a single traffic light controller:

```
a
  sg
    1, 2
  dl
    1, 2
b
  sg
    1, 2, 3
  ```

`.` would adress a main component, which  would not be a signal controller, but rather something that coordinates several intersection controllers.

To address a specific sub-controller you would use `.a` or `.b`.

You would address the second detector logic of intersection a as `.a.dl.2`, and the 3rd signal group of intersection b as `.b.sg.3`.

## Migration from RMSP 3
RSMP 4 component path can be used alongside RMSP 3 component names, as long as component names do not start with a dot.

Devices migrating from RSMP 3 to RSMP 4 should continue to support the existing component names if they are configured. Component paths can be added when desired, in which case the corresponding name and path should adress the same component, e.g. `KK+AG0105=000DL001` and `.dl.1` might address the same component.

After configuring paths, can you choose to remove component names to simplify the setup, or leave them for compatibility.


