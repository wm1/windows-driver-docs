---
title: NDIS\_STATUS\_WWAN\_HOME\_PROVIDER
author: windows-driver-content
description: Miniport drivers use the NDIS\_STATUS\_WWAN\_HOME\_PROVIDER notification to inform the MB Service about the completion of OID\_WWAN\_HOME\_PROVIDER \ 160; query requests.
ms.assetid: a5733c62-be4e-4f86-9639-6addd31baf0c
ms.author: windowsdriverdev
ms.date: 08/08/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
keywords: 
 -NDIS_STATUS_WWAN_HOME_PROVIDER Network Drivers Starting with Windows Vista
---

# NDIS\_STATUS\_WWAN\_HOME\_PROVIDER


Miniport drivers use the NDIS\_STATUS\_WWAN\_HOME\_PROVIDER notification to inform the MB Service about the completion of [OID\_WWAN\_HOME\_PROVIDER](oid-wwan-home-provider.md)  query requests.

Miniport drivers cannot use this notification to send unsolicited events.

This notification uses the [**NDIS\_WWAN\_HOME\_PROVIDER**](https://msdn.microsoft.com/library/windows/hardware/ff567909) structure.

Remarks
-------

Miniport drivers must comply with the following rules when responding to OID\_WWAN\_HOME\_PROVIDER query requests:

-   GSM-Based Devices: The home provider name can be retrieved from the Subscriber Identity Module (SIM) using several methods, such as from the EFSPN elementary file in the SIM (EFSPN is defined in the 3GPP TS 31.102 under section Service Provider Name), or from the operator-specific extensions when the EFSPN is not provisioned. You should refer to the operator-specific requirements specifications for obtaining the home provider name, extracting MCC-MNC from IMSI, and performing a look up in the GSMA SE.13 database. Contact the operator when retrieving operator-specific home provider names if the EFSPN is not provisioned. If a SIM is not provisioned with a home provider name through EFSPN or any other mechanism, miniport drivers should set the provider name to **NULL**.

    For details about a SIM card's file system, see the 3GPP TS 11.11 specification. If the provider identification is not provisioned in the Subscriber Identity Module (SIM card), miniport drivers should return WWAN\_STATUS\_READ\_FAILURE.

-   CDMA-Based Devices: Returning the home provider name is mandatory. It is recommended that IHVs provide this information in their device as part of network personalization. If the provider identity is not available, miniport drivers for CDMA-based providers must set the **Provider.ProviderId** member of the NDIS\_WWAN\_HOME\_PROVIDER structure to WWAN\_CDMA\_DEFAULT\_PROVIDER\_ID.

Miniport drivers must return this information when the device ready-state changes to **WwanReadyStateInitialized** and format all the members of the WWAN\_PROVIDER structure, as appropriate.

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


[OID\_WWAN\_HOME\_PROVIDER](oid-wwan-home-provider.md)

[**NDIS\_WWAN\_HOME\_PROVIDER**](https://msdn.microsoft.com/library/windows/hardware/ff567909)

 

 


--------------------
[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bnetvista\netvista%5D:%20NDIS_STATUS_WWAN_HOME_PROVIDER%20%20RELEASE:%20%288/8/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")


