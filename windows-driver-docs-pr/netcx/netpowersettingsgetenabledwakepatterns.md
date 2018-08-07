---
title: NetPowerSettingsGetEnabledWakePatterns method
topic_type:
- apiref
api_name:
- NetPowerSettingsGetEnabledWakePatterns
api_location:
- NetAdapterCxStub.lib
- NetAdapterCxStub.dll
api_type:
- LibDef
---

# NetPowerSettingsGetEnabledWakePatterns method


[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

Retrieves flags representing currently enabled wake pattern types that a network adapter supports.

Syntax
------

```cpp
ULONG NetPowerSettingsGetEnabledWakePatterns(
  _In_ NETPOWERSETTINGS NetPowerSettings
);
```

Parameters
----------

*NetPowerSettings* [in]  
A handle to the NETPOWERSETTINGS object associated with the NETADAPTER. To retrieve the handle, call [**NetAdapterGetPowerSettings**](netadaptergetpowersettings.md).

Return value
------------

A ULONG value that contains a bitwise **OR** of [**NET_ADAPTER_WAKE_PATTERN_FLAGS**](net-adapter-wake-pattern-flags.md)-typed flags that correspond to capabilities that the client driver reported in the **SupportedWakePacketPatterns** member of the [**NET_ADAPTER_POWER_CAPABILITIES**](net-adapter-power-capabilities.md) structure. NDIS uses these flags to enable the wake-on-LAN (WOL) patterns that a network adapter uses to wake the local computer from a low power state. For more information about WOL patterns, see [**NDIS_PM_WOL_PATTERN**](https://msdn.microsoft.com/library/windows/hardware/ff566768).

Remarks
-------

The client driver must only call **NetPowerSettingsGetEnabledWakePatterns** during a power transition, typically from its [*EVT_WDF_DEVICE_ARM_WAKE_FROM_SX*](https://msdn.microsoft.com/library/windows/hardware/ff540844) or [*EVT_WDF_DEVICE_ARM_WAKE_FROM_S0*](https://msdn.microsoft.com/library/windows/hardware/ff540843) callback function.  Otherwise, the call results in a system bugcheck.

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

* [**NetPowerSettingsGetWakePatternCount**](netpowersettingsgetwakepatterncount.md)
* [**NDIS_PM_CAPABILITIES**](https://msdn.microsoft.com/library/windows/hardware/ff566748)
* [**NDIS_PM_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/ff566759)
* [**NDIS_PM_WOL_PATTERN**](https://msdn.microsoft.com/library/windows/hardware/ff566768)
