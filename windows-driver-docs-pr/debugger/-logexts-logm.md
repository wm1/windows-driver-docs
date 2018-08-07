---
title: logexts.logm
description: The logexts.logm extension creates or displays a module inclusion list or a module exclusion list.
ms.assetid: 1037ba25-ffa6-4edd-99fd-bd0e249f4b37
keywords: ["logexts.logm Windows Debugging"]
ms.author: windowsdriverdev
ms.date: 05/23/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
topic_type:
- apiref
api_name:
- logexts.logm
api_type:
- NA
---

# !logexts.logm


The **!logexts.logm** extension creates or displays a module inclusion list or a module exclusion list.

```
!logexts.logm i Modules 
!logexts.logm x Modules 
!logexts.logm 
```

## <span id="ddk__logexts_logm_dbg"></span><span id="DDK__LOGEXTS_LOGM_DBG"></span>Parameters


<span id="_______i______"></span><span id="_______I______"></span> **i**   
Causes Logger to use a module inclusion list. It will consist of the specified *Modules*.

<span id="_______x______"></span><span id="_______X______"></span> **x**   
Causes Logger to use a module exclusion list. It will consist of Logexts.dll, kernel32.dll, and the specified *Modules*.

<span id="_______Modules______"></span><span id="_______modules______"></span><span id="_______MODULES______"></span> *Modules*   
Specifies the modules to be included or excluded. This list is not cumulative; each use of this command creates an entirely new list. If multiple modules are listed, separate them with spaces. An asterisk (\*) can be used to indicate all modules.

### <span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Logexts.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP and later</strong></p></td>
<td align="left"><p>Logexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>Additional Information

For more information, see [Logger and LogViewer](logger-and-logviewer.md).

Remarks
-------

With no parameters, the **!logexts.logm** extension displays the current inclusion list or exclusion list.

The extensions **!logexts.logm x \*** and **!logexts.logm i** are equivalent: they result in a completely empty inclusion list.

The extensions **!logexts.logm i \*** and **!logexts.logm x** are equivalent: they result in an exclusion list that contains only Logexts.dll and kernel32.dll. These two modules are always excluded, because Logger is not permitted to log itself.

Here are some examples:

```
0:001> !logm
Excluded modules:
  LOGEXTS.DLL      [mandatory]
  KERNEL32.DLL     [mandatory]
  USER32.DLL
  GDI32.DLL
  ADVAPI32.DLL

0:001> !logm x winmine.exe
Excluded modules:
  Logexts.dll      [mandatory]
  kernel32.dll     [mandatory]
  winmine.exe

0:001> !logm x user32.dll gdi32.dll
Excluded modules:
  Logexts.dll      [mandatory]
  kernel32.dll     [mandatory]
  user32.dll
  gdi32.dll

0:001> !logm i winmine.exe mymodule2.dll
Included modules:
  winmine.exe
  mymodule2.dll
```

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[debugger\debugger]:%20!logexts.logm%20%20RELEASE:%20%285/15/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")




