---
title: rcdrkd.rcdrloglist
description: The rcdrkd.rcdrloglist extension displays a list of the recorder logs owned by a driver or a set of drivers.
ms.assetid: D4D3C313-EFD4-482B-B4A3-307F2407D2BA
keywords: ["rcdrkd.rcdrloglist Windows Debugging"]
ms.author: windowsdriverdev
ms.date: 05/23/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
topic_type:
- apiref
api_name:
- rcdrkd.rcdrloglist
api_type:
- NA
---

# !rcdrkd.rcdrloglist


The **!rcdrkd.rcdrloglist** extension displays a list of the recorder logs owned by a driver or a set of drivers.

```
!rcdrkd.rcdrloglist DriverName [DriverName ...]
```

## <span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>Parameters


<span id="_______DriverName______"></span><span id="_______drivername______"></span><span id="_______DRIVERNAME______"></span> *DriverName*   
The name of a driver, not including the .sys extension.

## <span id="DLL"></span><span id="dll"></span>DLL


Rcdrkd.dll

Remarks
-------

This command is relevant only for drivers that log messages to different logs by using the WppRecorder API.

Examples
--------

The following example displays a list of all recorder logs owned by the USB 3.0 host controller driver (usbxhci.sys).

```
3: kd> !rcdrloglist usbxhci
Log dump command                           Log ID                   Size
================                           ======                   ====
!rcdrlogdump  usbxhci -a fffffa8005ff2b60  03 SLT02 DCI04           1024
!rcdrlogdump  usbxhci -a fffffa8005ff2010  03 SLT02 DCI03           1024
!rcdrlogdump  usbxhci -a fffffa8005b36010  03 SLT01 DCI03           1024
!rcdrlogdump  usbxhci -a fffffa8005b379e0  03 SLT01 DCI04           1024
!rcdrlogdump  usbxhci -a fffffa8005b33350  03 SLT02 DCI01           1024
!rcdrlogdump  usbxhci -a fffffa8005b2bb60  03 SLT01 DCI01           1024
!rcdrlogdump  usbxhci -a fffffa8005a2bb60  03 CMD                   1024
!rcdrlogdump  usbxhci -a fffffa8005a1ab60  03 INT00                 1024
!rcdrlogdump  usbxhci -a fffffa8005085330  03 RUNDOWN               512
!rcdrlogdump  usbxhci -a fffffa8005311780  03 1033 0194             1024
```

## <span id="see_also"></span>See also


[RCDRKD Extensions](rcdrkd-extensions.md)

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[debugger\debugger]:%20!rcdrkd.rcdrloglist%20%20RELEASE:%20%285/15/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")





