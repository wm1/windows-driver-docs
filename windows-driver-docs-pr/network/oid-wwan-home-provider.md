---
title: OID\_WWAN\_HOME\_PROVIDER
author: windows-driver-content
description: OID\_WWAN\_HOME\_PROVIDER is used to set and retrieve information about the home provider of the cellular service subscription.
ms.assetid: f7bea146-261d-4d01-9fd5-ae512a1ac083
ms.author: windowsdriverdev
ms.date: 08/08/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
keywords: 
 -OID_WWAN_HOME_PROVIDER Network Drivers Starting with Windows Vista
---

# OID\_WWAN\_HOME\_PROVIDER


OID\_WWAN\_HOME\_PROVIDER is used to set and retrieve information about the home provider of the cellular service subscription. For GSM-based devices and CDMA-based device with U-RIM, this information should be stored on the Subscriber Identity Module (SIM card). For CDMA-based devices without U-RIM, this information should be stored in auxiliary device memory.

Windows 8 supports both *set* and *query* requests. Windows 7 supports only *query* requests.

Miniport drivers must process both *set* and *query* requests asynchronously, initially returning NDIS\_STATUS\_INDICATION\_REQUIRED to the original request and later sending a [**NDIS\_STATUS\_WWAN\_HOME\_PROVIDER**](ndis-status-wwan-home-provider.md) status notification, for a *query*, or NDIS\_STATUS\_WWAN\_SET\_HOME\_PROVIDER\_COMPLETE status notification, for *set*, containing an [**NDIS\_WWAN\_HOME\_PROVIDER**](https://msdn.microsoft.com/library/windows/hardware/ff567909) structure to return information about the home network provider with the **Provider.ProviderState** member of the NDIS\_WWAN\_HOME\_PROVIDER structure set to WWAN\_PROVIDER\_STATE\_HOME.

*Set* operations are only required to be supported by multi-carrier capable devices. The MB service will only *set* the home provider to multi-carrier providers reported by the miniport via OID\_WWAN\_PREFERRED\_MULTICARRIER\_PROVIDERS or OID\_WWAN\_VISIBLE\_PROVIDERS. *Set* operations have an input buffer of NDIS\_WWAN\_SET\_HOME\_PROVIDER.

Remarks
-------

A *set* operation should not require the user to unlock the device regardless if the current SIM or target SIM is in a locked state.

| Current Provider SIM | Target Provider SIM | Result of *set* HOME\_PROVIDER                               |
|----------------------|---------------------|--------------------------------------------------------------|
| -                    | Locked              | Target PIN not required for setting home provider            |
| Locked               | -                   | Source PIN not required for setting home provider            |
| Locked               | Locked              | Source and Target PIN not required for setting home provider |

 

For more information about using this OID, see [WWAN Provider Operations](https://msdn.microsoft.com/library/windows/hardware/ff559101).

Miniport drivers can access the Subscriber Identity Module (SIM card) when processing query operations, but should not access the provider network.

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


[**NDIS\_WWAN\_HOME\_PROVIDER**](https://msdn.microsoft.com/library/windows/hardware/ff567909)

[**NDIS\_STATUS\_WWAN\_HOME\_PROVIDER**](ndis-status-wwan-home-provider.md)

[WWAN Provider Operations](https://msdn.microsoft.com/library/windows/hardware/ff559101)

 

 


--------------------
[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bnetvista\netvista%5D:%20OID_WWAN_HOME_PROVIDER%20%20RELEASE:%20%288/8/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")


