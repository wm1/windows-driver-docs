---
title: usb3kd.ucx_controller
description: The usb3kd.ucx_controller command displays information about a USB 3.0 host controller. The display is based on data structures maintained by UcxVersion.sys.
ms.assetid: A2768E47-C8D7-4A01-80AC-98FB5AAA17BD
keywords: ["usb3kd.ucx_controller Windows Debugging"]
ms.author: windowsdriverdev
ms.date: 05/23/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
topic_type:
- apiref
api_name:
- usb3kd.ucx_controller
api_type:
- NA
---

# !usb3kd.ucx\_controller


The [**!usb3kd.ucx\_controller**](-usb3kd-device-info.md) command displays information about a USB 3.0 host controller. The display is based on data structures maintained by the USB host controller extension driver (Ucx*Version*.sys).

```
!usb3kd.ucx_controller UcxControllerPrivContext
```

## <span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>Parameters


<span id="_______UcxControllerPrivContext______"></span><span id="_______ucxcontrollerprivcontext______"></span><span id="_______UCXCONTROLLERPRIVCONTEXT______"></span> *UcxControllerPrivContext*   
Address of the \_UCXCONTROLLER\_PRIVCONTEXT structure that represents the controller.

## <span id="DLL"></span><span id="dll"></span>DLL


Usb3kd.dll

Remarks
-------

The USB host controller extension driver (Ucx*Version*.sys) provides a layer of abstraction between the USB 3.0 hub driver and the USB 3.0 host controller driver. The extension driver has its own representation of host controllers, devices, and endpoints. The output the [**!ucx\_controller**](-usb3kd-device-info.md) command is based on the data structures maintained by the extension driver. For more information about the USB host controller extension driver and the USB 3.0 host controller driver, see [USB Driver Stack Architecture](https://msdn.microsoft.com/library/windows/hardware/hh406256).

Examples
--------

To obtain the address of the UCX controller private context, look at the output of the [**!ucx\_controller\_list**](-usb3kd-ucx-controller-list.md) command. In the following example, the address of the private context is 0xfffffa80052da050.

```
3: kd> !ucx_controller_list

## Dumping List of UCX controller objects
--------------------------------------
[1] !ucx_controller 0xfffffa80052da050 (dt ucx01000!_UCXCONTROLLER_PRIVCONTEXT fffffa80052da050)
    !ucx_device 0xfffffa8005a41840
        .!ucx_endpoint 0xfffffa800533f3d0 [Blk In ], UcxEndpointStateEnabled
        ...
    !ucx_device 0xfffffa8005bd9680
        .!ucx_endpoint 0xfffffa8003694860 [Blk Out], UcxEndpointStateEnabled
        ...
```

Now you can pass the address of the UCX controller private context to the [**!ucx\_controller**](-usb3kd-device-info.md) command.

```
3: kd> !ucx_controller 0xfffffa80052da050

## Dumping Ucx Controller Information fffffa80052da050
---------------------------------------------------
dt ucx01000!_UCXCONTROLLER_PRIVCONTEXT 0xfffffa80052da050
Parent Device: !wdfdevice 0x57ffac91fd8
Controller Queues:
    Default               : !wdfqueue 0x57ffacc5fd8
    Address'0'Ownership   : !wdfqueue 0x57ffad5ad88
    DeviceManagement      : !wdfqueue 0x57ffacd6fd8
    ... pend on Ctrl Reset: !wdfqueue 0x57ffad48fd8

Controller Reset State History: <Event> NewState 
    [ 2] <ControllerResetEventOperationSuccess> ControllerResetStateRHPdoInD0
    [ 1] <ControllerResetEventRHPdoEnteredD0> ControllerResetStateStopBlockingResetComplete1
    [ 0] <SmEngineEventStart> ControllerResetStateRhPdoInDx

Controller Reset Event History:
    [ 1] ControllerResetEventRHPdoEnteredD0
    [ 0] SmEngineEventStart

Root Hub PDO: !wdfdevice 0x57ffaf4daa8
Number of 2.0 Ports: 2
Number of 3.0 Ports: 2
RootHub Control !wdfqueue 0x57ffacb4798
RootHub Interrupt !wdfqueue 0x57ffad033f8, pending !wdfequest 0x57ffa5fe998

Device Tree:
    !ucx_device 0xfffffa8005a41840
        .!ucx_endpoint 0xfffffa800533f3d0 [Blk In ], UcxEndpointStateEnabled
        .!ucx_endpoint 0xfffffa80053405d0 [Blk Out], UcxEndpointStateEnabled
        .!ucx_endpoint 0xfffffa8005a3f710 [Control], UcxEndpointStateEnabled
        .!ucx_endpoint 0xfffffa8005bbe4e0 [Blk Out], UcxEndpointStateStale
        .!ucx_endpoint 0xfffffa8005ac4810 [Blk In ], UcxEndpointStateStale
    !ucx_device 0xfffffa8005bd9680
        .!ucx_endpoint 0xfffffa8003694860 [Blk Out], UcxEndpointStateEnabled
        .!ucx_endpoint 0xfffffa8003686820 [Blk In ], UcxEndpointStateEnabled
        .!ucx_endpoint 0xfffffa8005be0550 [Control], UcxEndpointStateEnabled
        .!ucx_endpoint 0xfffffa8003695580 [Blk In ], UcxEndpointStateStale
        .!ucx_endpoint 0xfffffa80036a20c0 [Blk Out], UcxEndpointStateStale
```

## <span id="see_also"></span>See also


[USB 3.0 Extensions](usb-3-extensions.md)

[**!usb3kd.ucx\_controller\_list**](-usb3kd-ucx-controller-list.md)

[Universal Serial Bus (USB) Drivers](http://go.microsoft.com/fwlink/p?LinkID=227351)

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[debugger\debugger]:%20!usb3kd.ucx_controller%20%20RELEASE:%20%285/15/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")





