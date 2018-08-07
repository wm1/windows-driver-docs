---
title: NetConfigurationQueryString method
topic_type:
- apiref
api_name:
- NetConfigurationQueryString
api_location:
- NetAdapterCxStub.lib
- NetAdapterCxStub.dll
api_type:
- LibDef
---

# NetConfigurationQueryString method


[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

Retrieves the specified string value from the adapter configuration object and assigns the string to a specified framework string object.

Syntax
------

```cpp
NTSTATUS NetConfigurationQueryString(
  _In_     NETCONFIGURATION       Configuration,
  _In_     PCUNICODE_STRING       ValueName,
  _In_opt_ PWDF_OBJECT_ATTRIBUTES StringAttributes,
  _Out_    WDFSTRING              *WdfString
);
```

Parameters
----------

*Configuration* [in]  
Handle to a NETCONFIGURATION object that represents an opened registry key.

*ValueName* [in]  
A pointer to a **UNICODE_STRING** structure that contains a name for string value.

*StringAttributes* [in, optional]  
A pointer to a [**WDF_OBJECT_ATTRIBUTES**](https://msdn.microsoft.com/library/windows/hardware/ff552400) structure that contains driver-supplied attributes for the new WDFSTRING object. This parameter is optional and can be WDF_NO_OBJECT_ATTRIBUTES.

*WdfString* [out]  
A handle to a framework string object. NetAdapterCx will assign the registry value's string data to this object.

Return value
------------

The method returns STATUS_SUCCESS if the operation succeeds. Otherwise, this method may return an appropriate NTSTATUS error code.

Remarks
-------
The client driver obtains a handle to a NETCONFIGURATION object by calling  [**NetAdapterOpenConfiguration**](netadapteropenconfiguration.md) or [**NetConfigurationOpenSubConfiguration**](netconfigurationopensubconfiguration.md).

By default, the framework string object is parented to the collection object. The client driver can change this by setting the **ParentObject** member of the [**WDF_OBJECT_ATTRIBUTES**](https://msdn.microsoft.com/library/windows/hardware/ff552400) structure.

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
<td align="left">Netconfiguration.h (include Netadaptercx.h)</td>
</tr>
<tr class="odd">
<td align="left"><p>Library</p></td>
<td align="left">NetAdapterCxStub.lib</td>
</tr>
<tr class="even">
<td align="left"><p>IRQL</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
</tr>
</tbody>
</table>

 

 





