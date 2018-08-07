---
title: Power-Down Sequence for an Network Adapter WDF Client Driver
---

# Power-Down Sequence for an Network Adapter WDF Client Driver

[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

The following figure shows the order in which NetAdapterCx calls a client driver's event callback functions when powering down and removing the device. The sequence starts at the top of the figure with an operational device that is in the working power state (D0):

![device enumeration and power-down sequence for NetAdapter client driver](images/powerdown.png)

The broad horizontal lines mark the steps that are involved in powering down a device. The column on the left side of the figure describes the step, and the column on the right lists the event callbacks that accomplish it.

As the figure shows, the power-down and removal sequence involves calling the corresponding "undo" callbacks in the reverse order in which the framework called the functions that are involved in making the device operational. The framework deletes the device object after it deletes the device object context area.
