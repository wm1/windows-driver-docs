---
title: NDIS\_STATUS\_DOT11\_INCOMING\_ASSOC\_REQUEST\_RECEIVED
author: windows-driver-content
description: NDIS\_STATUS\_DOT11\_INCOMING\_ASSOC\_REQUEST\_RECEIVED
ms.assetid: 03210984-acf8-40b7-8414-1b984cef9dc7
ms.author: windowsdriverdev
ms.date: 08/08/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
keywords: 
 -NDIS_STATUS_DOT11_INCOMING_ASSOC_REQUEST_RECEIVED Network Drivers Starting with Windows Vista
---

# NDIS\_STATUS\_DOT11\_INCOMING\_ASSOC\_REQUEST\_RECEIVED


**Important**  The [Native 802.11 Wireless LAN](https://msdn.microsoft.com/library/windows/hardware/ff560690) interface is deprecated in Windows 10 and later. Please use the WLAN Device Driver Interface (WDI) instead. For more information about WDI, see [WLAN Universal Windows driver model](https://msdn.microsoft.com/library/windows/hardware/dn897672).

 

A miniport driver must make an NDIS\_STATUS\_DOT11\_INCOMING\_ASSOC\_REQUEST\_RECEIVED status indication after the NIC receives an incoming association request frame from a peer station on an infrastructure BSS.

The data type for this indication is the [**DOT11\_INCOMING\_ASSOC\_REQUEST\_RECEIVED\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/ff548655) structure.

The NIC should validate the association request and determine whether to accept the request, following IEEE 802.11 standards. The NIC can also use its own proprietary logic to examine proprietary fields in the request. The miniport driver should issue this indication after it and the NIC have validated the association request and have accepted the request based on their own internal logic. When the operating system receives this indication, it assumes that the NIC has accepted the association request.

If the association request packet is not valid, or if the NIC decides to reject the request, the NIC should send an association response packet that rejects the request and should not present this indication to the operating system.

The miniport driver calls [**NdisMIndicateStatusEx**](https://msdn.microsoft.com/library/windows/hardware/ff563600) to make an NDIS\_STATUS\_DOT11\_INCOMING\_ASSOC\_REQUEST\_RECEIVED indication, and must pass a pointer to an [**NDIS\_STATUS\_INDICATION**](https://msdn.microsoft.com/library/windows/hardware/ff567373) structure through the *StatusIndication* parameter. When making this indication, the driver must set the following members of the NDIS\_STATUS\_INDICATION structure:

-   **StatusCode** must be set to NDIS\_STATUS\_DOT11\_INCOMING\_ASSOC\_REQUEST\_RECEIVED.

-   **StatusBuffer** must be set to the address of a DOT11\_INCOMING\_ASSOC\_REQUEST\_RECEIVED\_PARAMETERS structure.

-   **StatusBufferSize** must be set to sizeof(DOT11\_INCOMING\_ASSOC\_REQUEST\_RECEIVED\_PARAMETERS) + AssociationRequest\_Frame\_size.

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
<td><p>Available in Windows 7 and later versions of the Windows operating systems.</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Windot11.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## See also


[**DOT11\_INCOMING\_ASSOC\_REQUEST\_RECEIVED\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/ff548655)

 

 


--------------------
[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bnetvista\netvista%5D:%20NDIS_STATUS_DOT11_INCOMING_ASSOC_REQUEST_RECEIVED%20%20RELEASE:%20%288/8/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")


