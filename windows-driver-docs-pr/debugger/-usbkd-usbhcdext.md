---
title: usbkd.usbhcdext
description: The usbkd.usbhcdext command displays information from the device extension of a USB host controller or a USB root hub.
ms.assetid: 83811F9F-5899-4EC8-83D7-39EE884C0A01
keywords: ["usbkd.usbhcdext Windows Debugging"]
ms.author: windowsdriverdev
ms.date: 05/23/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
topic_type:
- apiref
api_name:
- usbkd.usbhcdext
api_type:
- NA
---

# !usbkd.usbhcdext


The [**!usbkd.usbhcdext**](https://msdn.microsoft.com/library/windows/hardware/dn367072) command displays information from the device extension of a USB host controller or a USB root hub.

```
!usbkd.usbhcdext DeviceExtension
```

## <span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>Parameters


<span id="_______DeviceExtension______"></span><span id="_______deviceextension______"></span><span id="_______DEVICEEXTENSION______"></span> *DeviceExtension*   
Address of one of the following:

-   The device extension for the functional device object (FDO) of a USB host controller.
-   The device extension for the physical device object (PDO) a USB root hub.

## <span id="DLL"></span><span id="dll"></span>DLL


Usbkd.dll

Examples
--------

Here is one way to find the address of the device extension for the FDO of an EHCI host controller. First enter [**!usbkd.usb2tree**](-usbkd-usb2tree.md).

```
0: kd> !usbkd.usb2tree

EHCI MINIPORT(s) dt usbport!_USBPORT_MINIPORT_DRIVER ffffe00001f48bd0

1)!ehci_info ffffe00001ca11a0 !devobj ffffe00001ca1050 PCI: VendorId 8086 DeviceId 293c RevisionId 0002 
 ...
```

In the preceding output, the address of the device extension of the FDO is displayed as the argument of the [DML](debugger-markup-language-commands.md) command **!ehci\_info ffffe00001ca11a0**.

Now pass the address of the device extension to the [**!usbhcdext**](https://msdn.microsoft.com/library/windows/hardware/dn367072) command.

```
0: kd> !usbkd.usbhcdext ffffe00001ca11a0

HC Flavor 1000  FDO ffffe00001ca1050
Root Hub: FDO ffffe00002320050 !hub2_info ffffe000023201a0
Operational Registers ffffd000228bf020
Device Data ffffe00001ca2da0
dt USBPORT!_FDO_EXTENSION ffffe00001ca15a0
DM Timer Flags ffffe00001ca16d4
FDO Flags ffffe00001ca16d0
HCD Log ffffe00001ca11a0

DeviceHandleList: !usblist ffffe00001ca23b8, DL 
DeviceHandleDeletedList: !usblist ffffe00001ca23c8, DL [Empty]
GlobalEndpointList: !usblist ffffe00001ca2388, EP 
EpNeoStateChangeList: !usblist ffffe00001ca2370, SC [Empty]
GlobalTtListHead: !usblist ffffe00001ca23a8, TT [Empty]
BusContextHead: !usblist ffffe00001ca16b0, BC 

## Pending Requests

[001] dt USBPORT!_USB_IOREQUEST_CONTEXT ffffe00001ca1450 Tag: AddD Obj: ffffe00001ca11a0
...

## XDPC List

01) dt USBPORT!_XDPC_CONTEXT ffffe00001ca1f18
...
```

Here is one way to find the address of the device extension for the PDO of a root hub. First enter [**!usbkd.usb2tree**](-usbkd-usb2tree.md).

```
0: kd> !usbkd.usb2tree

EHCI MINIPORT(s) dt usbport!_USBPORT_MINIPORT_DRIVER ffffe00001f48bd0

1)!ehci_info ffffe00001ca11a0 !devobj ffffe00001ca1050 PCI: VendorId 8086 DeviceId 293c RevisionId 0002 
    RootHub !hub2_info ffffe000023201a0 !devstack ffffe00002320050
 ...
```

In the preceding output, you can see the address of the FDO of the root hub displayed as the argument to the command **!devstack ffffe00002320050**. Use the [**!devstack**](-devstack.md) command to find the address of the PDO and the PDO device extension.

```
0: kd> !kdexts.devstack ffffe00002320050
  !DevObj           !DrvObj            !DevExt           ObjectName
> ffffe00002320050  \Driver\usbhub     ffffe000023201a0  0000002d
  ffffe0000213c050  \Driver\usbehci    ffffe0000213c1a0  USBPDO-3
...
```

In the preceding output, you can see that the address of the device extension for the PDO of the root hub is `ffffe0000213c1a0`.

Now pass the address of the device extension to the [**!usbhcdext**](https://msdn.microsoft.com/library/windows/hardware/dn367072) command.

```
0: kd> !usbkd.usbhcdext ffffe0000213c1a0

Root Hub PDO Extension
Parent HC: FDO ffffe00001ca1050 !ehci_info ffffe00001ca11a0
HUB FDO ffffe00002320050 !hub2_info ffffe000023201a0
dt USBPORT!_PDO_EXTENSION ffffe0000213c5a0

## Pending Requests

[001] dt USBPORT!_USB_IOREQUEST_CONTEXT ffffe0000213c450 Tag: RHcr Obj: ffffe0000213c1a0
[002] dt USBPORT!_USB_IOREQUEST_CONTEXT ffffe00003ce5800 Tag: iIRP Obj: ffffe00002182210

## POWER FUNC HISTORY (latest at bottom)

[00] IRP_MN_WAIT_WAKE (PowerSystemHibernate)
...

## PnP STATE LOG (latest at bottom)

##      EVENT                         STATE               NEXT

[01] EvPDO_IRP_MN_START_DEVICE      PnpNotStarted       PnpStarted 
```

## <span id="see_also"></span>See also


[USB 2.0 Debugger Extensions](usb-2-0-extensions.md)

[Universal Serial Bus (USB) Drivers](http://go.microsoft.com/fwlink/p?LinkID=227351)

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[debugger\debugger]:%20!usbkd.usbhcdext%20%20RELEASE:%20%285/15/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")





