---
title: usb3kd.ucx_endpoint
description: The usb3kd.ucx_endpoint command displays information about an endpoint on a USB device in the USB 3.0 tree. The display is based on data maintained by UcxVersion.sys.
ms.assetid: 37667665-ACA1-48D3-B79E-5B9BBD689034
keywords: ["usb3kd.ucx_endpoint Windows Debugging"]
ms.author: windowsdriverdev
ms.date: 05/23/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
topic_type:
- apiref
api_name:
- usb3kd.ucx_endpoint
api_type:
- NA
---

# !usb3kd.ucx\_endpoint


The [**!usb3kd.ucx\_endpoint**](-usb3kd-device-info.md) command displays information about an endpoint on a USB device in the [USB 3.0 tree](usb-3-extensions.md#usb-3-tree). The display is based on data structures maintained by the USB host controller extension driver (Ucx*Version*.sys).

```
!usb3kd.ucx_endpoint UcxEndpointPrivContext
```

## <span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>Parameters


<span id="_______UcxEndpointPrivContext______"></span><span id="_______ucxendpointprivcontext______"></span><span id="_______UCXENDPOINTPRIVCONTEXT______"></span> *UcxEndpointPrivContext*   
Address of the \_UCXENDPOINT\_PRIVCONTEXT structure that represents the endpoint.

## <span id="DLL"></span><span id="dll"></span>DLL


Usb3kd.dll

Remarks
-------

The USB host controller extension driver (Ucx*Version*.sys) provides a layer of abstraction between the USB 3.0 hub driver and the USB 3.0 host controller driver. The extension driver has its own representation of host controllers, devices, and endpoints. The output the **!ucx\_endpoint** command is based on the data structures maintained by the extension driver. For more information about the USB host controller extension driver and the USB 3.0 host controller driver, see [USB Driver Stack Architecture](https://msdn.microsoft.com/library/windows/hardware/hh406256).

Examples
--------

To obtain the address of the UCX endpoint private context, look at the output of the [**!ucx\_controller\_list**](-usb3kd-ucx-controller-list.md) command. In the following example, the address of the private context for the first endpoint on the second device is 0xfffffa8003694860.

```
3: kd> !ucx_controller_list

## Dumping List of UCX controller objects
--------------------------------------
[1] !ucx_controller 0xfffffa80052da050 (dt ucx01000!_UCXCONTROLLER_PRIVCONTEXT fffffa80052da050)
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

Now you can pass the address of the UCX endpoint private context to the **!ucx\_endpoint** command.

```
3: kd> !ucx_endpoint 0xfffffa8003694860

## Dumping Ucx USB Endpoint Information fffffa8003694860
-----------------------------------------------------
dt ucx01000!_UCXENDPOINT_PRIVCONTEXT 0xfffffa8003694860
[Blk Out], UcxEndpointStateEnabled, MaxTransferSize: 4194304
Endpoint Address: 0x02
Endpoint Queue: !wdfqueue 0x57ffc969888

UcxEndpoint State History: <Event> NewState 
    [ 3] <UcxEndpointEventOperationSuccess> UcxEndpointStateEnabled
    [ 2] <UcxEndpointEventYes> UcxEndpointStateCompletingPendingOperation1
    [ 1] <UcxEndpointEventEnableComplete> UcxEndpointStateIsAbleToStart2
    [ 0] <SmEngineEventStart> UcxEndpointStateCreated

UcxEndpoint Event History:
    [ 1] UcxEndpointEventEnableComplete
    [ 0] SmEngineEventStart

EventCallbacks:
    EvtEndpointPurge: (0xfffff880044ba6e8) USBXHCI!Endpoint_UcxEvtEndpointPurge
    EvtEndpointAbort: (0xfffff880044ba94c) USBXHCI!Endpoint_UcxEvtEndpointAbort
    EvtEndpointReset: (0xfffff880044bb854) USBXHCI!Endpoint_UcxEvtEndpointReset
```

## <span id="see_also"></span>See also


[USB 3.0 Extensions](usb-3-extensions.md)

[**!usb3kd.ucx\_controller\_list**](-usb3kd-ucx-controller-list.md)

[Universal Serial Bus (USB) Drivers](http://go.microsoft.com/fwlink/p?LinkID=227351)

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[debugger\debugger]:%20!usb3kd.ucx_endpoint%20%20RELEASE:%20%285/15/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")





