---
title: NET_BUFFER_LIST_NEXT_NBL macro
author: windows-driver-content
description: NET_BUFFER_LIST_NEXT_NBL is a macro that NDIS drivers use to get the next NET_BUFFER_LIST structure in a linked list of NET_BUFFER_LIST structures.
ms.assetid: 5f0fc110-5e17-4030-b25b-e00d25b60b14
ms.author: windowsdriverdev 
ms.date: 07/18/2017 
ms.topic: article 
ms.prod: windows-hardware 
ms.technology: windows-devices 
keywords:
 - NET_BUFFER_LIST_NEXT_NBL macro Network Drivers Starting with Windows Vista
---

# NET\_BUFFER\_LIST\_NEXT\_NBL macro


NET\_BUFFER\_LIST\_NEXT\_NBL is a macro that NDIS drivers use to get the next [**NET\_BUFFER\_LIST**](https://msdn.microsoft.com/library/windows/hardware/ff568388) structure in a linked list of NET\_BUFFER\_LIST structures.

Syntax
------

```ManagedCPlusPlus
PNET_BUFFER_LIST NET_BUFFER_LIST_NEXT_NBL(
   PNET_BUFFER_LIST _NBL
);
```

Parameters
----------

*\_NBL*   
A pointer to a NET\_BUFFER\_LIST structure.

Return value
------------

NET\_BUFFER\_LIST\_NEXT\_NBL returns a pointer to the next NET\_BUFFER\_LIST structure in the linked list of NET\_BUFFER\_LIST structures, or it returns **NULL** if the end of the linked list is reached.

Remarks
-------

NET\_BUFFER\_LIST\_NEXT\_NBL gets the return value from the **Next** member of the [**NET\_BUFFER\_LIST\_DATA**](https://msdn.microsoft.com/library/windows/hardware/ff568393) structure in the [**NET\_BUFFER\_LIST**](https://msdn.microsoft.com/library/windows/hardware/ff568388) structure that the *\_NBL* parameter points to.

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
</tbody>
</table>

## See also


[**NET\_BUFFER\_LIST**](https://msdn.microsoft.com/library/windows/hardware/ff568388)

[**NET\_BUFFER\_LIST\_DATA**](https://msdn.microsoft.com/library/windows/hardware/ff568393)

 

 


--------------------
[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bnetvista\netvista%5D:%20NET_BUFFER_LIST_NEXT_NBL%20macro%20%20RELEASE:%20%287/10/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")


