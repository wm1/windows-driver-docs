---
title: NDIS\_STATUS\_WWAN\_SMS\_CONFIGURATION
author: windows-driver-content
description: Miniport drivers use the NDIS\_STATUS\_WWAN\_SMS\_CONFIGURATION notification to inform the MB Service about either the completion of a previous OID\_WWAN\_SMS\_CONFIGURATION \ 160;query or set request, or an event notification in the case of change in SMS configuration. Miniport drivers can also send unsolicited events with this notification.This notification uses the NDIS\_WWAN\_SMS\_CONFIGURATION structure.
ms.assetid: 86dfe2dc-070b-43d9-b6fa-54dee985c65d
ms.author: windowsdriverdev
ms.date: 08/08/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
keywords: 
 -NDIS_STATUS_WWAN_SMS_CONFIGURATION Network Drivers Starting with Windows Vista
---

# NDIS\_STATUS\_WWAN\_SMS\_CONFIGURATION


Miniport drivers use the NDIS\_STATUS\_WWAN\_SMS\_CONFIGURATION notification to inform the MB Service about either the completion of a previous [OID\_WWAN\_SMS\_CONFIGURATION](oid-wwan-sms-configuration.md) query or set request, or an event notification in the case of change in SMS configuration.

Miniport drivers can also send unsolicited events with this notification.

This notification uses the [**NDIS\_WWAN\_SMS\_CONFIGURATION**](https://msdn.microsoft.com/library/windows/hardware/ff567935) structure.

Remarks
-------

The miniport driver must send this unsolicited indication when the MB device's SMS subsystem is ready for SMS operation.

Requirements
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Version</p></td>
<td><p>Available in Windows 7 and later versions of Windows.</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## See also


[OID\_WWAN\_SMS\_CONFIGURATION](oid-wwan-sms-configuration.md)

[**NDIS\_WWAN\_SMS\_CONFIGURATION**](https://msdn.microsoft.com/library/windows/hardware/ff567935)

 

 


--------------------
[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bnetvista\netvista%5D:%20NDIS_STATUS_WWAN_SMS_CONFIGURATION%20%20RELEASE:%20%288/8/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")


