---
title: usbkd._ehciep
description: The usbkd._ehciep command displays information from a usbehci _ENDPOINT_DATA structure. Use this command to display information about asynchronous endpoints (that is, control and bulk endpoints).
ms.assetid: 0DA42FDD-41D6-4234-9D9C-36872F0CE0C1
keywords: ["usbkd._ehciep Windows Debugging"]
ms.author: windowsdriverdev
ms.date: 05/23/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
topic_type:
- apiref
api_name:
- usbkd._ehciep
api_type:
- NA
---

# !usbkd.\_ehciep


The **!usbkd.\_ehciep** command displays information from a **usbehci!\_ENDPOINT\_DATA** structure. Use this command to display information about asynchronous endpoints (that is, control and bulk endpoints).

```
!usbkd._ehciep StructAddr
```

## <span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>Parameters


<span id="_______StructAddr______"></span><span id="_______structaddr______"></span><span id="_______STRUCTADDR______"></span> *StructAddr*   
Address of a **usbehci!\_ENDPOINT\_DATA** structure. To find addresses of **usbehci!\_ENDPOINT\_DATA** structures, use [**!usbhcdext**](-usbkd-usbhcdext.md) and [**!usblist**](-usbkd-usblist.md).

## <span id="DLL"></span><span id="dll"></span>DLL


Usbkd.dll

Examples
--------

This example shows one way to get the address of a **usbehci!\_ENDPOINT\_DATA** structure. Start with the [**!usb2tree**](-usbkd-usb2tree.md) command.

```
0: kd> !usbkd.usb2tree
...
2)!ehci_info ffffe0000206e1a0 !devobj ffffe0000206e050 PCI: VendorId 8086 DeviceId 293c RevisionId 0002 
    RootHub !hub2_info ffffe000024a61a0 !devstack ffffe000024a6050
        Port 1: !port2_info ffffe000026dd000 
        Port 2: !port2_info ffffe000026ddb40 
        Port 3: !port2_info ffffe000026de680 !devstack ffffe00001ec3060
            !device2_info ffffe00001ec31b0 (USB Mass Storage Device: Xxx Corporation)
        Port 4: !port2_info ffffe000026df1c0 
```

In the preceding output, the address of the device extension of the FDO is displayed as the argument of the [DML](debugger-markup-language-commands.md) command **!ehci\_info ffffe0000206e1a0**. Either click the DML command or pass the address of the device extension to [**!usbhcdext**](https://msdn.microsoft.com/library/windows/hardware/dn367072).

```
0: kd> !usbkd.usbhcdext ffffe0000206e1a0
...
DeviceHandleList: !usblist ffffe0000206f3b8, DL 
DeviceHandleDeletedList: !usblist ffffe0000206f3c8, DL [Empty]
GlobalEndpointList: !usblist ffffe0000206f388, EP 
...
```

The preceding output displays the command **!usblist ffffe0000206f388, EP**. Use this command to display a list of endpoints.

```
0: kd> !usblist ffffe0000206f388, EP 
list: ffffe0000206f388 EP
...
dt usbport!_HCD_ENDPOINT ffffe000026dc970  !usbep ffffe000026dc970
common buffer bytes 0x00003000 (12288) @ va 0000000021e6e000 pa 00000000d83c9000
Device Address: 0x01, ep 0x81 Bulk In Flags: 00000041 dt _USB_ENDPOINT_FLAGS ffffe000026dc990
... usbehci!_ENDPOINT_DATA ffffe000026dcc38
...
```

In the preceding output, `ffffe000026dcc38` is the address of a **usbehci!\_ENDPOINT\_DATA** structure. Pass this address to **!\_ehciep**.

```
0: kd> !usbkd._ehciep ffffe000026dcc38
*USBEHCI
dt usbehci!_ENDPOINT_DATA ffffe000026dcc38
Flags: 0x00000000
dt usbehci!_HCD_QUEUEHEAD_DESCRIPTOR ffffd00021e6e080
*HwQH ffffd00021e6e080
HwQH
     HwQH.HLink dea2e002
     HwQH.EpChars 02002101
         DeviceAddress: 0x1
         IBit: 0x0
         EndpointNumber: 0x1
         EndpointSpeed: 0x2 HcEPCHAR_HighSpeed
         DataToggleControl: 0x0
         HeadOfReclimationList: 0x0
         MaximumPacketLength: 0x200 - 512
   ...
current slot 0000000000000000
slot[0] dt usbehci!_ENDPOINT_SLOT ffffe000026dcdb8 - slot_NotBusy
----
     ffffd00021e6e100
     dt usbehci!_HCD_TRANSFER_DESCRIPTOR ffffd00021e6e100
    tdphys: d83c9100'200 txlen 00000000 tx ffffd00000000041 flags 6d4e695d  _BUSY _SLOT_RESET
    Next_qTD: d83c9200'd83c9180 AltNext_qTD 77423c00'41 
    NextTD: ffffd00021e6e200 AltNextTD ffffd00021e6e180 SlotNextTd ffffd00021e6e200 tok 00000c00  Xbytes x0 (0)
.
     ffffd00021e6e200
     dt usbehci!_HCD_TRANSFER_DESCRIPTOR ffffd00021e6e200
    tdphys: d83c9200'5000 txlen 00000000 tx ffffd00000000041 flags 6d4e695d  _BUSY _SLOT_RESET
    Next_qTD: d83c9280'd83c9180 AltNext_qTD 77423c00'41 
    NextTD: ffffd00021e6e280 AltNextTD ffffd00021e6e180 SlotNextTd ffffd00021e6e280 tok 00000c00  Xbytes x0 (0)
...
```

## <span id="see_also"></span>See also


[USB 2.0 Debugger Extensions](usb-2-0-extensions.md)

[Universal Serial Bus (USB) Drivers](http://go.microsoft.com/fwlink/p?LinkID=227351)

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[debugger\debugger]:%20!usbkd._ehciep%20%20RELEASE:%20%285/15/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")





