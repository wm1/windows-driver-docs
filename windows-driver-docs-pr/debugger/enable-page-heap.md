---
title: Enable page heap
description: Enable page heap
ms.assetid: b889b7b7-721c-4ecf-bf59-c1ccc0bc735d
keywords: ["Enable page heap (global flag)"]
ms.author: windowsdriverdev
ms.date: 05/23/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

# Enable page heap


## <span id="ddk_enable_page_heap_dtools"></span><span id="DDK_ENABLE_PAGE_HEAP_DTOOLS"></span>


The **Enable page heap** flag turns on page heap verification, which monitors dynamic heap memory operations, including allocate and free operations, and causes a debugger break when the verifier detects a heap error.

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Abbreviation</strong></p></td>
<td align="left"><p>hpa</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Hexadecimal value</strong></p></td>
<td align="left"><p>0x02000000</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>Symbolic Name</strong></p></td>
<td align="left"><p>FLG_HEAP_PAGE_ALLOCS</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Destination</strong></p></td>
<td align="left"><p>System-wide registry entry, kernel flag, image file registry entry</p></td>
</tr>
</tbody>
</table>

 

### <span id="comments"></span><span id="COMMENTS"></span>Comments

This option enables full page heap verification when set for image files and standard page heap verification when set in the system registry or as a kernel flag.

-   *Full page heap verification* (for **/i**) places a zone of reserved virtual memory at the end of each allocation.

-   *Standard page heap verification* (for **/r** or **/k**) places random patterns at the end of an allocation and examines the patterns when a heap block is freed.

Setting this flag for an image file is the same as typing **gflags /p /enable** *ImageFile* **/full** for the image file at the command line.

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[debugger\debugger]:%20Enable%20page%20heap%20%20RELEASE:%20%285/15/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")




