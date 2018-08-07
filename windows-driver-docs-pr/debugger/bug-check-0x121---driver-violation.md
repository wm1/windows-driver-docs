---
title: Bug Check 0x121 DRIVER_VIOLATION
description: The DRIVER_VIOLATION bug check has a value of 0x00000121. This bug check indicates that a driver has caused a violation.
ms.assetid: 4a5d1d84-a958-45a6-9511-b5b4ecd4c067
keywords: ["Bug Check 0x121 DRIVER_VIOLATION", "DRIVER_VIOLATION"]
ms.author: windowsdriverdev
ms.date: 05/23/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
topic_type:
- apiref
api_name:
- DRIVER_VIOLATION
api_type:
- NA
---

# Bug Check 0x121: DRIVER\_VIOLATION


The DRIVER\_VIOLATION bug check has a value of 0x00000121. This bug check indicates that a driver has caused a violation.

**Important** This topic is for programmers. If you are a customer who has received a blue screen error code while using your computer, see [Troubleshoot blue screen errors](http://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors).

## DRIVER\_VIOLATION Parameters


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
<td align="left"><p>1</p></td>
<td align="left"><p>Describes the type of violation</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>Reserved</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>Reserved</p></td>
</tr>
</tbody>
</table>

 

Remarks
-------

Use a kernel debugger and view the call stack to determine the name of the driver that caused the violation.

 

 




