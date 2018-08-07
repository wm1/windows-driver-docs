---
title: NetPowerSettingsGetProtocolOffload method
topic_type:
- apiref
api_name:
- NetPowerSettingsGetProtocolOffload
api_location:
- NetAdapterCxStub.lib
- NetAdapterCxStub.dll
api_type:
- LibDef
---

# NetPowerSettingsGetProtocolOffload method


[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

Retrieves a structure that specifies parameters for a low power protocol offload to a network adapter.

Syntax
------

```cpp
PNDIS_PM_PROTOCOL_OFFLOAD NetPowerSettingsGetProtocolOffload(
  _In_ NETPOWERSETTINGS NetPowerSettings,
  _In_ ULONG            Index
);
```

Parameters
----------

*NetPowerSettings* [in]  
A handle to the NETPOWERSETTINGS object associated with the NETADAPTER. To retrieve the handle, call [**NetAdapterGetPowerSettings**](netadaptergetpowersettings.md).

*Index* [in]  
A zero-based value that is used as an index into the protocol offload structures associated with the NETPOWERSETTINGS object. This value must be less than the value returned by [**NetPowerSettingsGetProtocolOffloadCount**](netpowersettingsgetprotocoloffloadcount.md).

Return value
------------

Returns a pointer to the [**NDIS_PM_PROTOCOL_OFFLOAD**](https://msdn.microsoft.com/library/windows/hardware/ff566760) structure at the specified index, or **NULL** if the index value is invalid.

Remarks
-------

The client driver must only call **NetPowerSettingsGetProtocolOffload** during a power transition, typically from its [*EVT_WDF_DEVICE_ARM_WAKE_FROM_SX*](https://msdn.microsoft.com/library/windows/hardware/ff540844) or [*EVT_WDF_DEVICE_ARM_WAKE_FROM_S0*](https://msdn.microsoft.com/library/windows/hardware/ff540843) callback function, or from the [*EVT_NET_ADAPTER_PREVIEW_PROTOCOL_OFFLOAD*](evt-net-adapter-preview-protocol-offload.md) callback function.  Otherwise, the call results in a system bugcheck.

The client driver can use the pointer to examine the [**NDIS_PM_PROTOCOL_OFFLOAD**](https://msdn.microsoft.com/library/windows/hardware/ff566760) structure, but should not retain it. NetAdapterCx automatically releases the protocol offload structure during offload removal.

Requirements
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Target platform</p></td>
<td align="left">Universal</td>
</tr>
<tr class="even">
<td align="left"><p>Minimum KMDF version</p></td>
<td align="left"><p>1.21</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Minimum NetAdapterCx version</p></td>
<td align="left"><p>1.0</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Netpowersettings.h (include Netadaptercx.h)</td>
</tr>
<tr class="odd">
<td align="left"><p>Library</p></td>
<td align="left">NetAdapterCxStub.lib</td>
</tr>
<tr class="even">
<td align="left"><p>IRQL</p></td>
<td align="left"><p>DISPATCH_LEVEL</p></td>
</tr>
</tbody>
</table>

## See also


[**NDIS_PM_PROTOCOL_OFFLOAD**](https://msdn.microsoft.com/library/windows/hardware/ff566760)

 

 






