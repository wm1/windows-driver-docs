---
title: NDIS_LOWER_IRQL macro
author: windows-driver-content
description: The NDIS_LOWER_IRQL macro sets the IRQL on the current processor to the specified value.
ms.assetid: fd6b57a1-cd6f-4d30-b2b6-0c9842706855
ms.author: windowsdriverdev 
ms.date: 07/18/2017 
ms.topic: article 
ms.prod: windows-hardware 
ms.technology: windows-devices 
keywords:
- NDIS_LOWER_IRQL macro Network Drivers Starting with Windows Vista
---

# NDIS\_LOWER\_IRQL macro


The NDIS\_LOWER\_IRQL macro sets the IRQL on the current processor to the specified value.

Syntax
------

```ManagedCPlusPlus
VOID NDIS_LOWER_IRQL(
   KIRQL _OldIrql_,
   KIRQL _CurIrql_
);
```

Parameters
----------

*\_OldIrql\_*   
The original (that is, unraised) IRQL value from before the driver called the [**NDIS\_RAISE\_IRQL\_TO\_DISPATCH**](ndis-raise-irql-to-dispatch.md) macro. NDIS\_LOWER\_IRQL sets the IRQL to this value.

*\_CurIrql\_*   
The current IRQL value that is active before the call to NDIS\_LOWER\_IRQL.

Return value
------------

None

Remarks
-------

NDIS network drivers should use the NDIS\_LOWER\_IRQL macro to restore the IRQL setting that existed before a call to the [**NDIS\_RAISE\_IRQL\_TO\_DISPATCH**](ndis-raise-irql-to-dispatch.md) macro.

If the value that the *\_OldIrql\_* parameter specifies is not equal to the current IRQL, the NDIS\_LOWER\_IRQL macro attempts to lower the IRQL to the value that the *\_OldIrql\_* parameter specifies.

It is a fatal error to call NDIS\_LOWER\_IRQL and use a value for *\_OldIrql\_* that was not returned from an immediately preceding call to the [**NDIS\_RAISE\_IRQL\_TO\_DISPATCH**](ndis-raise-irql-to-dispatch.md) macro.

NDIS\_LOWER\_IRQL is an NDIS wrapper for the [**KeLowerIrql**](https://msdn.microsoft.com/library/windows/hardware/ff552968) routine.

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
<td>[Universal](http://go.microsoft.com/fwlink/p/?linkid=531356)</td>
</tr>
<tr class="even">
<td><p>Version</p></td>
<td><p>Supported in NDIS 6.0 and later.</p></td>
</tr>
<tr class="odd">
<td><p>Header</p></td>
<td>Ndis.h (include Ndis.h)</td>
</tr>
<tr class="even">
<td><p>IRQL</p></td>
<td><p>Any level (see Remarks section)</p></td>
</tr>
<tr class="odd">
<td><p>DDI compliance rules</p></td>
<td>[<strong>Irql_IrqlSetting_Function</strong>](https://msdn.microsoft.com/library/windows/hardware/ff547962)</td>
</tr>
</tbody>
</table>

## See also


[**KeLowerIrql**](https://msdn.microsoft.com/library/windows/hardware/ff552968)

[**NDIS\_RAISE\_IRQL\_TO\_DISPATCH**](ndis-raise-irql-to-dispatch.md)

 

 


--------------------
[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bnetvista\netvista%5D:%20NDIS_LOWER_IRQL%20macro%20%20RELEASE:%20%287/10/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")


