---
title: Bug Check 0x129 WORKER_THREAD_RETURNED_WITH_BAD_PAGING_IO_PRIORITY
description: The WORKER_THREAD_RETURNED_WITH_BAD_PAGING_IO_PRIORITY bug check has a value of 0x00000129 that indicates that a worker threads Paging IOPriority was wrongly modified.
ms.assetid: E662D301-6B4D-4E92-BED3-4BB0731DBFD0
keywords: ["Bug Check 0x129 WORKER_THREAD_RETURNED_WITH_BAD_PAGING_IO_PRIORITY", "WORKER_THREAD_RETURNED_WITH_BAD_PAGING_IO_PRIORITY"]
ms.author: windowsdriverdev
ms.date: 05/23/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
topic_type:
- apiref
api_name:
- WORKER_THREAD_RETURNED_WITH_BAD_PAGING_IO_PRIORITY
api_type:
- NA
---

# Bug Check 0x129: WORKER\_THREAD\_RETURNED\_WITH\_BAD\_PAGING\_IO\_PRIORITY


The WORKER\_THREAD\_RETURNED\_WITH\_BAD\_PAGING\_IO\_PRIORITY bug check has a value of 0x00000129. This indicates that a worker threads Paging IOPriority was wrongly modified by the called worker routine.

**Important** This topic is for programmers. If you are a customer who has received a blue screen error code while using your computer, see [Troubleshoot blue screen errors](http://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors).

## WORKER\_THREAD\_RETURNED\_WITH\_BAD\_PAGING\_IO\_PRIORITY Parameters


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Parameter</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">1</td>
<td align="left"><p>Address of worker routine</p>
<p>Use the [<strong>ln (List Nearest Symbols)</strong>](ln--list-nearest-symbols-.md) command on this address to find the offending driver.</p></td>
</tr>
<tr class="even">
<td align="left">2</td>
<td align="left">Current Paging IoPrioirity value</td>
</tr>
<tr class="odd">
<td align="left">3</td>
<td align="left">Workitem parameter</td>
</tr>
<tr class="even">
<td align="left">4</td>
<td align="left">Workitem address</td>
</tr>
</tbody>
</table>

 

 

 




