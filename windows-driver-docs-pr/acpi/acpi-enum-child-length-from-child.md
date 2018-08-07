---
title: ACPI_ENUM_CHILD_LENGTH_FROM_CHILD macro
author: windows-driver-content
description: The ACPI_ENUM_CHILD_LENGTH_FROM_CHILD macro calculates the size, in bytes, of a variable-length ACPI_ENUM_CHILD structure.
ms.assetid: 62be7cb5-4b71-4b8e-bad5-807623cd812a
keywords: 
- ACPI_ENUM_CHILD_LENGTH_FROM_CHILD macro ACPI Devices
ms.author: windowsdriverdev
ms.date: 07/18/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

# ACPI\_ENUM\_CHILD\_LENGTH\_FROM\_CHILD macro


The ACPI\_ENUM\_CHILD\_LENGTH\_FROM\_CHILD macro calculates the size, in bytes, of a variable-length [**ACPI\_ENUM\_CHILD**](https://msdn.microsoft.com/library/windows/hardware/ff536109) structure.

Syntax
------

```ManagedCPlusPlus
void ACPI_ENUM_CHILD_LENGTH_FROM_CHILD(
    Child
);
```

Parameters
----------

*Child*   
A pointer to a structure of type ACPI\_ENUM\_CHILD for which to calculate the size, in bytes, of the structure.

Return value
------------

The size, in bytes, of the ACPI\_ENUM\_CHILD structure that *Child* points to.

Remarks
-------

A driver can use this macro to calculate the size, in bytes, of the ACPI\_ENUM\_CHILD structures in an [**ACPI\_ENUM\_CHILDREN\_OUTPUT\_BUFFER**](https://msdn.microsoft.com/library/windows/hardware/ff536112) structure.

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
<td><p>Windows Vista and later versions of Windows.</p></td>
</tr>
<tr class="odd">
<td><p>Header</p></td>
<td>Acpiioct.h (include Acpiioct.h)</td>
</tr>
</tbody>
</table>

## See also


[**ACPI\_ENUM\_CHILD**](https://msdn.microsoft.com/library/windows/hardware/ff536109)

[**ACPI\_ENUM\_CHILDREN\_OUTPUT\_BUFFER**](https://msdn.microsoft.com/library/windows/hardware/ff536112)

 

 


--------------------
[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bacpi\acpi%5D:%20ACPI_ENUM_CHILD_LENGTH_FROM_CHILD%20macro%20%20RELEASE:%20%287/18/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")


