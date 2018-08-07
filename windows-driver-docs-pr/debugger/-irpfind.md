---
title: irpfind
description: The irpfind extension displays information about all I/O request packets (IRP) currently allocated in the target system, or about those IRPs matching the specified search criteria.
ms.assetid: f0d850d9-8804-40df-90a3-b9c6a6b4540f
keywords: ["irpfind Windows Debugging"]
ms.author: windowsdriverdev
ms.date: 05/23/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
topic_type:
- apiref
api_name:
- irpfind
api_type:
- NA
---

# !irpfind


The **!irpfind** extension displays information about all I/O request packets (IRP) currently allocated in the target system, or about those IRPs matching the specified search criteria.

Syntax

```
!irpfind [-v][PoolType[RestartAddress[CriteriaData]]]
```

## <span id="ddk__irpfind_dbg"></span><span id="DDK__IRPFIND_DBG"></span>Parameters


<span id="_______-v______"></span><span id="_______-V______"></span> **-v**   
Displays verbose information.

<span id="_______PoolType______"></span><span id="_______pooltype______"></span><span id="_______POOLTYPE______"></span> *PoolType*   
Specifies the type of pool to be searched. The following values are permitted:

<span id="0"></span>0  
Specifies nonpaged memory pool. This is the default.

<span id="1"></span>1  
Specifies paged memory pool.

<span id="2"></span>2  
Specifies the special pool.

<span id="4"></span>4  
Specifies the session pool.

<span id="_______RestartAddress______"></span><span id="_______restartaddress______"></span><span id="_______RESTARTADDRESS______"></span> *RestartAddress*   
Specifies the hexadecimal address at which to begin the search. This is useful if the previous search was terminated prematurely. The default is zero.

<span id="_______Criteria______"></span><span id="_______criteria______"></span><span id="_______CRITERIA______"></span> *Criteria*   
Specifies the criteria for the search. Only those IRPs that satisfy the given match will be displayed.

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Criteria</th>
<th align="left">Match</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>arg</strong></p></td>
<td align="left"><p>Finds all IRPs with a stack location where one of the arguments equals <em>Data</em>.</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>device</strong></p></td>
<td align="left"><p>Finds all IRPs with a stack location where <strong>DeviceObject</strong> equals <em>Data</em>.</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>fileobject</strong></p></td>
<td align="left"><p>Finds all IRPs whose <strong>Irp.Tail.Overlay.OriginalFileObject</strong> equals <em>Data</em>.</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>mdlprocess</strong></p></td>
<td align="left"><p>Finds all IRPs whose <strong>Irp.MdlAddress.Process</strong> equals <em>Data</em>.</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>thread</strong></p></td>
<td align="left"><p>Finds all IRPs whose <strong>Irp.Tail.Overlay.Thread</strong> equals <em>Data</em>.</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>userevent</strong></p></td>
<td align="left"><p>Finds all IRPs whose <strong>Irp.UserEvent</strong> equals <em>Data</em>.</p></td>
</tr>
</tbody>
</table>

 

<span id="_______Data______"></span><span id="_______data______"></span><span id="_______DATA______"></span> *Data*   
Specifies the data to be matched in the search.

### <span id="DLL"></span><span id="dll"></span>DLL

Kdexts.dll

### <span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>Additional Information

See [Plug and Play Debugging](plug-and-play-debugging.md) for applications of this extension command. For information about IRPs, see the Windows Driver Kit (WDK) documentation and *Microsoft Windows Internals* by Mark Russinovich and David Solomon.

Remarks
-------

This example finds the IRP in the nonpaged pool that is going to set user event FF9E4F48 upon completion:

```
kd> !irpfind 0 0 userevent ff9e4f48
```

The following example produces a full listing of all IRPs in the nonpaged pool:

```
kd> !irpfind
Searching NonPaged pool (8090c000 : 8131e000) for Tag: Irp
8097c008 Thread 8094d900 current stack belongs to  \Driver\symc810
8097dec8 Thread 8094dda0 current stack belongs to  \FileSystem\Ntfs
809861a8 Thread 8094dda0 current stack belongs to  \Driver\symc810
809864e8 Thread 80951ba0 current stack belongs to  \Driver\Mouclass
80986608 Thread 80951ba0 current stack belongs to  \Driver\Kbdclass
80986728 Thread 8094dda0 current stack belongs to  \Driver\symc810
```

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[debugger\debugger]:%20!irpfind%20%20RELEASE:%20%285/15/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")




