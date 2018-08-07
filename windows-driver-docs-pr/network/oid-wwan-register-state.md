---
title: OID\_WWAN\_REGISTER\_STATE
author: windows-driver-content
description: OID\_WWAN\_REGISTER\_STATE selects a network provider to register with.
ms.assetid: 564de5bf-10d9-47fe-a4c1-3409d9b2aee8
ms.author: windowsdriverdev
ms.date: 08/08/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
keywords: 
 -OID_WWAN_REGISTER_STATE Network Drivers Starting with Windows Vista
---

# OID\_WWAN\_REGISTER\_STATE


OID\_WWAN\_REGISTER\_STATE selects a network provider to register with.

Miniport drivers must process set and query requests asynchronously, initially returning NDIS\_STATUS\_INDICATION\_REQUIRED to the original request, and later sending an [**NDIS\_STATUS\_WWAN\_REGISTER\_STATE**](ndis-status-wwan-register-state.md) status notification containing an [**NDIS\_WWAN\_REGISTRATION\_STATE**](https://msdn.microsoft.com/library/windows/hardware/ff567917) structure to provide information about the registered network provider regardless of completing set or query requests.

Callers requesting to set the network provider to register with provide an [**NDIS\_WWAN\_SET\_REGISTER\_STATE**](https://msdn.microsoft.com/library/windows/hardware/ff567926) structure to the miniport driver with the appropriate information.

Remarks
-------

For more information about using this OID, see [WWAN Registration Operations](https://msdn.microsoft.com/library/windows/hardware/ff559116).

Miniport drivers can access the provider network when processing query or set operations, but should not access the Subscriber Identity Module (SIM card).

The MB driver model supports two registration methods--automatic and manual. For CDMA-based networks, the MB driver model supports only automatic registration.

Devices supporting manual registration must set the **WwanControlCaps** member in [**WWAN\_DEVICE\_CAPS**](https://msdn.microsoft.com/library/windows/hardware/ff571204) structure to WWAN\_CTRL\_CAPS\_REG\_MANUAL. Be aware that GSM-based devices must support manual registration.

If the registration state is automatic, miniport drivers must instruct their device to select a network provider based on the selection algorithm specific to the cellular technology and proceed with registration.

The semantics of RegisterAction values are defined as follows:

-   The *WwanRegisterActionAutomatic* flag is used by the MB Service to instruct the miniport driver to set the device to automatic register mode and let the device select the best provider network. The miniport driver must ignore **ProviderId** parameter. This setting is persistent across radio states (ON/OFF), and device power cycles, until it is explicitly change by the MB Service.

-   The *WwanRegisterActionManual* flag is used by the MB Service to instruct the miniport driver to register with the provider network identified by the **ProviderId** parameter. The **ProviderId** value shall come from the **ProviderId** member of WWAN\_PROVIDER data structure of one of the visible providers. This setting is persistent across radio states (ON/OFF), and device power cycles, until it is explicitly changed by the MB Service.

-   Changing between the different RegisterAction values are allowed even if the device is currently registered to a provider. If the device need to deregister before switching between the Automatic and Manual registration modes, the miniport driver must ensure that the device is set to deregistration before setting to the new registration mode.

-   The *Manual* and *Automatic* registration mode only affects the network selection mode. The MB device should try to register to selected network whenever the radio is turned on.

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


[**NDIS\_WWAN\_SET\_REGISTER\_STATE**](https://msdn.microsoft.com/library/windows/hardware/ff567926)

[**NDIS\_STATUS\_WWAN\_REGISTER\_STATE**](ndis-status-wwan-register-state.md)

[WWAN Registration Operations](https://msdn.microsoft.com/library/windows/hardware/ff559116)

 

 


--------------------
[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bnetvista\netvista%5D:%20OID_WWAN_REGISTER_STATE%20%20RELEASE:%20%288/8/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")


