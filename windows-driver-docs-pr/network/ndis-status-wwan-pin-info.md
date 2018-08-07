---
title: NDIS\_STATUS\_WWAN\_PIN\_INFO
author: windows-driver-content
description: Miniport drivers use the NDIS\_STATUS\_WWAN\_PIN\_INFO notification to respond to OID query and set requests of OID\_WWAN\_PIN. Miniport drivers cannot use this notification to send unsolicited events.This notification uses the NDIS\_WWAN\_PIN\_INFO structure.
ms.assetid: fa3c2467-2240-423b-b91b-f7e19d5be353
ms.author: windowsdriverdev
ms.date: 08/08/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
keywords: 
 -NDIS_STATUS_WWAN_PIN_INFO Network Drivers Starting with Windows Vista
---

# NDIS\_STATUS\_WWAN\_PIN\_INFO


Miniport drivers use the NDIS\_STATUS\_WWAN\_PIN\_INFO notification to respond to OID query and set requests of [OID\_WWAN\_PIN](oid-wwan-pin.md).

Miniport drivers cannot use this notification to send unsolicited events.

This notification uses the [**NDIS\_WWAN\_PIN\_INFO**](https://msdn.microsoft.com/library/windows/hardware/ff567911) structure.

Remarks
-------

Miniport drivers should return information about the Personal Identity Number (PIN) that the MB device currently expects in response to a query request. Miniport drivers should return the status notification filled in as described in sections below in response to a set request.

**Responding to WwanPinOperationEnter Requests**

When miniport drivers use the NDIS\_STATUS\_WWAN\_PIN\_INFO notification to respond to **WwanPinOperationEnter** requests, they should implement these procedures:

-   For successful **WwanPinOperationEnter** query requests, when the MB device no longer requires a PIN, miniport drivers must set **uStatus** to WWAN\_STATUS\_SUCCESS and **PinType** to **WwanPinTypeNone**.

-   For failed **WwanPinOperationEnter** requests, miniport drivers must set **uStatus** to WWAN\_STATUS\_FAILURE and include applicable data as per the following details:

    -   PIN Disabled or PIN Not Expected: For **WwanPinOperationEnter** set requests, when the corresponding PIN is either disabled or currently not expected by the MB device, miniport drivers must set **PinType** to **WwanPinTypeNone**. All other members are ignored.

    -   PIN Not Supported: If the given PIN is not supported by the MB device, miniport drivers must set **uStatus** to WWAN\_STATUS\_NO\_DEVICE\_SUPPORT.

    -   PIN Retrial: In this mode, the MB device requires the PIN to be re-entered as the **AttemptsRemaining** value is still non-zero for this particular type of PIN. Miniport drivers must set **PinType** to the same value as that of **PinType** in NDIS\_WWAN\_SET\_PIN.

    -   PIN Blocking: The PIN is blocked when **AttemptsRemaining** is zero. If the PIN unblock operation is not available, miniport drivers must set **uStatus** to WWAN\_STATUS\_FAILURE and **PinType** to **WwanPinTypeNone**. All the other members are ignored.

        **Note**  If the MB device supports PIN unblock operations, miniport drivers should follow the PIN Unblocking step to respond to the request.

         

    -   PIN Unblocking: The PIN is blocked when **AttemptsRemaining** is zero. To unblock the PIN, the MB device may request a corresponding PIN Unlock Key (PUK), if applicable. In this case, miniport drivers must set **PinType** to the corresponding WwanPinType*Xxx*PUK with the relevant details.

    -   Blocked PUK: If the number of failed trials exceeds the preset value for entering the WwanPinType*Xxx*PUK, then the PUK becomes blocked. Miniport drivers must signal this by setting **uStatus** to WWAN\_STATUS\_FAILURE and **PinType** to **WwanPinTypeNone**. In case PUK1 is blocked, miniport drivers must send an NDIS\_STATUS\_WWAN\_READY\_INFO with **ReadyState** set to **WwanReadyStateBadSim**.

**Responding to WwanPinOperationEnable, WwanPinOperationDisable, or WwanPinOperationChange Requests**

When miniport drivers use the NDIS\_STATUS\_WWAN\_PIN\_INFO notification to respond to **WwanPinOperationEnable**, **WwanPinOperationDisable**, and **WwanPinOperationChange**, they should implement the following operations:

-   For successful requests, miniport drivers must set **uStatus** to WWAN\_STATUS\_SUCCESS. Other members are ignored.

-   Miniport drivers must set **uStatus** to WWAN\_STATUS\_SUCCESS for PIN-enable and PIN-disable operations when the PIN is already in the requested state. Miniport drivers must set **PinType** to **WwanPinTypeNone**. Other members are ignored.

-   When a PIN mode is changed from disabled to enabled the PIN state should be WwanPinStateNone.

-   If PIN1 is enabled, the PIN state shall become WwanPinStateEnter when power is cycled to the MB device.

-   For all other PINs, the PIN state can change from WwanPinStateNone to WwanPinStateEnter depending on MB device specific conditions.

-   PIN Not Supported: If a PIN operation is not supported by the MB device, miniport drivers must set **uStatus** to WWAN\_STATUS\_NO\_DEVICE\_SUPPORT. For example, enabling and disabling PIN2 is not typically supported by MB devices so the above error code must be returned. All other members are ignored.

-   PIN Must be Entered: If a PIN operation requires a PIN to be entered, miniport drivers must set **uStatus** to WWAN\_STATUS\_PIN\_REQUIRED and **PinType** to WwanPinType*Xxx*. Other members are ignored.

-   PIN Change Operation: If the MB device restricts the change of PIN value only when it is in enabled state, a request to change in disabled state must be returned with WWAN\_STATUS\_PIN\_DISABLED.

-   PIN Retrial: On failure, miniport drivers must set **uStatus** to WWAN\_STATUS\_FAILURE, and **PinType** to the same value as specified in NDIS\_WWAN\_SET\_PIN. Other members are ignored except for **AttemptsRemaining**. This may occur when an incorrect PIN is entered.

-   PIN Blocking: The PIN is blocked when the number of **AttemptsRemaining** is zero. If the PIN unblock operation is not available, miniport drivers must set **uStatus** to WWAN\_STATUS\_FAILURE and **PinType** to **WwanPinTypeNone**. **AttemptsRemaining** should be set to 0 and all the other members are ignored.

    **Note**  If the MB device supports PIN unblock operations, miniport drivers should follow the PIN Unblocking step to respond to the request.

     

-   Unblocking PIN: The PIN is blocked when **AttemptsRemaining** is zero. To unblock the PIN, the MB device may request a corresponding PUK, if applicable. In this case, miniport drivers must set **uStatus** to WWAN\_STATUS\_FAILURE, **PinType** to the corresponding WwanPinType*Xxx*PUK, **PinState** to **WwanPinStateEnter**, and **AttemptsRemaining** should have the number of attempts allowed to enter a valid PUK.

    If PIN blocking results in the MB device or SIM becomes blocked, miniport drivers must send an event notification with **ReadyState** set to **WwanReadyStateDeviceLocked**.

-   If there is an active PDP context at the time of PIN1 blocking, miniport drivers must deactivate the PDP context and send notifications to the operating system about the PDP deactivation and link state change.

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


[OID\_WWAN\_PIN](oid-wwan-pin.md)

[**NDIS\_STATUS\_WWAN\_PIN\_INFO**](ndis-status-wwan-pin-info.md)

 

 


--------------------
[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bnetvista\netvista%5D:%20NDIS_STATUS_WWAN_PIN_INFO%20%20RELEASE:%20%288/8/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")


