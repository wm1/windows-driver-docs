---
title: OID\_WWAN\_READY\_INFO
author: windows-driver-content
description: OID\_WWAN\_READY\_INFO returns the device ready-state, which includes its Subscriber Identity Module (SIM card).
ms.assetid: 3e6f6cb7-14fc-4eee-b5d6-d5e0cad46ea2
ms.author: windowsdriverdev
ms.date: 08/08/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
keywords: 
 -OID_WWAN_READY_INFO Network Drivers Starting with Windows Vista
---

# OID\_WWAN\_READY\_INFO


OID\_WWAN\_READY\_INFO returns the device ready-state, which includes its Subscriber Identity Module (SIM card). This typically occurs at the beginning of any session.

Set requests are not supported.

Miniport drivers must process query requests asynchronously, initially returning NDIS\_STATUS\_INDICATION\_REQUIRED to the original request, and later sending an [**NDIS\_STATUS\_WWAN\_READY\_INFO**](ndis-status-wwan-ready-info.md) status notification containing an [**NDIS\_WWAN\_READY\_INFO**](https://msdn.microsoft.com/library/windows/hardware/ff567916) structure that indicates the MB device's ready-state when completing query requests.

Remarks
-------

For more information about using this OID, see [MB device Readiness](https://msdn.microsoft.com/library/windows/hardware/ff557164).

Miniport drivers can access device memory or the SIM card when processing query operations, but should not access the provider network.

Miniport drivers should wait until the PIN is cleared (if required) and then read the subscriber's identity and telephone number(s) (TNs), and then set the ReadyInfo.ReadyState member of the NDIS\_WWAN\_READY\_INFO structure to WwanReadyStateInitialized.

Miniport drivers must never fail OID\_WWAN\_READY\_INFO and must always return the correct device ready-state.

Miniport drivers must always notify the MB Service whenever the device ready-state changes.

Miniport drivers should follow these steps to provide a good user experience:

-   If PIN1 is locked, miniport drivers must first send a ready-state event notification with **ReadyInfo.ReadyState** set to *WwanReadyStateDeviceLocked*. The MB Service then sends the miniport driver an OID set request of OID\_WWAN\_PIN. After the device unlocks then the miniport driver must send another ready-state event notification with **ReadyInfo.ReadyState** set to *WwanReadyStateInitialized*. Until PIN1 is successfully unlocked, miniport drivers must not change the device ready-state to *WwanReadyStateInitialized*.

-   Miniport drivers must first send an event notification with **ReadyInfo.ReadyState** set to *WwanReadyStateSimNotInserted* when the MB Service loads the miniport driver if no SIM card is present, as may be the case with devices that allow SIM cards to be inserted or removed. If the device has the capability to detect a hot insertion of a SIM card, the miniport driver must send another event notification with **ReadyInfo.ReadyState** set to *WwanReadyStateInitialized* when the user inserts a SIM.

-   Devices that have the capability to detect service activation state must set **ReadyInfo.ReadyState** to *WwanReadyStateNotActivated*. Furthermore, if the miniport driver supports service activation, the miniport driver will receive an OID set request of OID\_WWAN\_SERVICE\_ACTIVATION. On successful completion of service activation, miniport drivers must send another event notification with **ReadyInfo.ReadyState** set to *WwanReadyStateInitialized*.

-   Miniport drivers that require a specific firmware revision must ensure that the correct firmware revision is available. If the firmware revision is not available, the miniport driver should complete the event notification transaction by setting **ReadyInfo.ReadyState** to *WwanReadyStateFailure*.

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


[**NDIS\_WWAN\_READY\_INFO**](https://msdn.microsoft.com/library/windows/hardware/ff567916)

[**NDIS\_STATUS\_WWAN\_READY\_INFO**](ndis-status-wwan-ready-info.md)

[MB device Readiness](https://msdn.microsoft.com/library/windows/hardware/ff557164)

 

 


--------------------
[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bnetvista\netvista%5D:%20OID_WWAN_READY_INFO%20%20RELEASE:%20%288/8/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")


