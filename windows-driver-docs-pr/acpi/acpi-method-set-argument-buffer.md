---
title: ACPI_METHOD_SET_ARGUMENT_BUFFER macro
author: windows-driver-content
description: The ACPI_METHOD_SET_ARGUMENT_BUFFER macro sets the members of an ACPI_METHOD_ARGUMENT structure for custom data that is supplied in a data buffer.
ms.assetid: 1f335814-fa9f-45c6-b970-10884e971ec1
keywords: 
- ACPI_METHOD_SET_ARGUMENT_BUFFER macro ACPI Devices
ms.author: windowsdriverdev
ms.date: 07/18/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

# ACPI\_METHOD\_SET\_ARGUMENT\_BUFFER macro


The ACPI\_METHOD\_SET\_ARGUMENT\_BUFFER macro sets the members of an [**ACPI\_METHOD\_ARGUMENT**](https://msdn.microsoft.com/library/windows/hardware/ff536125) structure for custom data that is supplied in a data buffer.

Syntax
------

```ManagedCPlusPlus
void ACPI_METHOD_SET_ARGUMENT_BUFFER(
    Argument,
    BuffData,
    BuffLength
);
```

Parameters
----------

*Argument*   
A pointer to an ACPI\_METHOD\_ARGUMENT structure.

*BuffData*   
A pointer to a data buffer that contains custom data.

*BuffLength*   
The size, in bytes, of the custom data.

Return value
------------

This macro does not return a value.

Remarks
-------

A driver can use this macro to set the members of an ACPI\_METHOD\_ARGUMENT structure that supplies custom data.

Requirements
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Target platform</p></td>
<td>Desktop</td>
</tr>
<tr class="even">
<td><p>Version</p></td>
<td><p>Windows 2000 and later versions of Windows.</p></td>
</tr>
<tr class="odd">
<td><p>Header</p></td>
<td>Acpiioct.h (include Acpiioct.h)</td>
</tr>
</tbody>
</table>

## See also


[**ACPI\_METHOD\_ARGUMENT**](https://msdn.microsoft.com/library/windows/hardware/ff536125) 

 

 


--------------------
[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bacpi\acpi%5D:%20ACPI_METHOD_SET_ARGUMENT_BUFFER%20macro%20%20RELEASE:%20%287/18/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")


