---
title: minipkd.adapters
description: The minipkd.adapters extension displays all of the adapters that work with the SCSI Port driver that have been identified in the system, and the individual devices associated with each adapter.
ms.assetid: 8571b9ec-1ec9-4adb-8a65-5306e45c3aa6
keywords: ["minipkd.adapters Windows Debugging"]
ms.author: windowsdriverdev
ms.date: 05/23/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
topic_type:
- apiref
api_name:
- minipkd.adapters
api_type:
- NA
---

# !minipkd.adapters


The **!minipkd.adapters** extension displays all of the adapters that work with the SCSI Port driver that have been identified in the system, and the individual devices associated with each adapter.

```
!minipkd.adapters 
```

### <span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Unavailable</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP and later</strong></p></td>
<td align="left"><p>Minipkd.dll</p></td>
</tr>
</tbody>
</table>

 

### <span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>Additional Information

For more information, see [SCSI Miniport Debugging](scsi-miniport-debugging.md).

Remarks
-------

The display includes the driver name, the device object address, and the device extension address for each adapter. The display for each adapter also includes a list of each device on the adapter. The display for each device includes the device extension address, the SCSI address, the device object address, and some flags for the device. Information about the Plug and Play state and the power state is also included.

The flags in the display are explained in the following table:

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Flag</th>
<th align="left">Meaning</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>c</p></td>
<td align="left"><p>Claimed. Indicates that the device has a driver on it.</p></td>
</tr>
<tr class="even">
<td align="left"><p>m</p></td>
<td align="left"><p>Missing. Indicates that the device was present on the bus in a prior scan but was not present during the latest scan.</p></td>
</tr>
<tr class="odd">
<td align="left"><p>e</p></td>
<td align="left"><p>Enumerated. Indicates that the device has been reported to the Plug and Play manager.</p></td>
</tr>
<tr class="even">
<td align="left"><p>v</p></td>
<td align="left"><p>Visible. Indicates that the device has been enumerated by the system. This flag is more significant when it is not present for a device.</p></td>
</tr>
<tr class="odd">
<td align="left"><p>p</p></td>
<td align="left"><p>Paging. Indicates that the device is in the paging path.</p></td>
</tr>
<tr class="even">
<td align="left"><p>d</p></td>
<td align="left"><p>Dump. Indicates that the device is in the crash dump path and will be used for a crash dump.</p></td>
</tr>
<tr class="odd">
<td align="left"><p>h</p></td>
<td align="left"><p>Hibernate. Indicates that the device is hibernating.</p></td>
</tr>
</tbody>
</table>

 

Here is an example of the **!minipkd.adapters** display:

```
0: kd> !minipkd.adapters
Adapter \Driver\lp6nds35     DO 86334a70         DevExt 86334b28
Adapter \Driver\adpu160m     DO 8633da70         DevExt 8633db28
 LUN 862e60f8 @(0,0,0) c ev     pnp(00/ff) pow(0,0) DevObj 862e6040
 LUN 863530f8 @(0,1,0) c ev p d pnp(00/ff) pow(0,0) DevObj 86353040
 LUN 862e50f8 @(0,2,0) c ev     pnp(00/ff) pow(0,0) DevObj 862e5040
 LUN 863520f8 @(0,6,0)   ev     pnp(00/ff) pow(0,0) DevObj 86352040
Adapter \Driver\adpu160m     DO 86376040         DevExt 863760f8
```

An error message similar to the following indicates that either the symbol path is incorrect and does not point to the correct version of the Scsiport.sys symbols, or that Windows has not identified any adapters that work with the SCSI Port driver.

```
minipkd error (0) <path> ... \minipkd\minipkd.c @ line 435
```

If the [**!minipkd.help**](-minipkd-help.md) extension command returns help information successfully, the SCSI Port symbols are correct.

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[debugger\debugger]:%20!minipkd.adapters%20%20RELEASE:%20%285/15/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")




