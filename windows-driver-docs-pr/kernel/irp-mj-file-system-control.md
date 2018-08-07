---
title: IRP\_MJ\_FILE\_SYSTEM\_CONTROL
author: windows-driver-content
description: Only file system drivers process IRP\_MJ\_FILE\_SYSTEM\_CONTROL requests.
ms.author: windowsdriverdev
ms.date: 08/12/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.assetid: 695ed61b-7082-44be-ae82-ddc3e4a0b8d0
keywords:
 - IRP_MJ_FILE_SYSTEM_CONTROL Kernel-Mode Driver Architecture
---

# IRP\_MJ\_FILE\_SYSTEM\_CONTROL


Only file system drivers process **IRP\_MJ\_FILE\_SYSTEM\_CONTROL** requests. For more information about the use of this IRP major function code by file system drivers, see [**IRP\_MJ\_FILE\_SYSTEM\_CONTROL**](https://msdn.microsoft.com/library/windows/hardware/ff548670). For more information about file system drivers, see [File System Drivers](https://msdn.microsoft.com/library/windows/hardware/ff540376).

Requirements
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Wdm.h (include Wdm.h, Ntddk.h, or Ntifs.h)</td>
</tr>
</tbody>
</table>

 

 


--------------------
[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bkernel\kernel%5D:%20IRP_MJ_FILE_SYSTEM_CONTROL%20%20RELEASE:%20%288/10/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")


