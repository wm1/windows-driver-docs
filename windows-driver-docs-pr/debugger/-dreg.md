---
title: dreg
description: The dreg extension displays registry information.
ms.assetid: a54ed14e-eb9d-48fd-877d-d6d0fe4a8d3f
keywords: ["dreg Windows Debugging"]
ms.author: windowsdriverdev
ms.date: 05/23/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
topic_type:
- apiref
api_name:
- dreg
api_type:
- NA
---

# !dreg


The **!dreg** extension displays registry information.

```
!dreg [-d|-w] KeyPath[!Value] 
!dreg
```

## <span id="ddk__dreg_dbg"></span><span id="DDK__DREG_DBG"></span>Parameters


<span id="_______-d______"></span><span id="_______-D______"></span> **-d**   
Causes binary values to be displayed as DWORDs.

<span id="_______-w______"></span><span id="_______-W______"></span> **-w**   
Causes binary values to be displayed as WORDs.

<span id="_______KeyPath______"></span><span id="_______keypath______"></span><span id="_______KEYPATH______"></span> *KeyPath*   
Specifies the registry key path. It can begin with any of the following abbreviations:

<span id="hklm"></span><span id="HKLM"></span>**hklm**  
HKEY\_LOCAL\_MACHINE

<span id="hkcu"></span><span id="HKCU"></span>**hkcu**  
HKEY\_CURRENT\_USER

<span id="hkcr"></span><span id="HKCR"></span>**hkcr**  
HKEY\_CLASSES\_ROOT

<span id="hku"></span><span id="HKU"></span>**hku**  
HKEY\_USERS

If no abbreviation is used, HKEY\_LOCAL\_MACHINE is assumed.

<span id="_______Value______"></span><span id="_______value______"></span><span id="_______VALUE______"></span> *Value*   
Specifies the name of the registry value to be displayed. If an asterisk (\*) is used, all values are displayed. If *Value* is omitted, all subkeys are displayed.

### <span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Ntsdexts.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP and later</strong></p></td>
<td align="left"><p>Ntsdexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>Additional Information

For information about the registry, see the Windows Driver Kit (WDK) documentation and *Microsoft Windows Internals* by Mark Russinovich and David Solomon. (These resources may not be available in some languages and countries.)

Remarks
-------

The **!dreg** extension can be used to display the registry during user-mode debugging.

It is most useful during remote debugging, as it allows you to browse the registry of the remote machine. It is also useful when controlling the user-mode debugger from the kernel debugger, because you cannot run a standard registry editor on the target machine when it is frozen. (You can use the [**.sleep**](-sleep--pause-debugger-.md) command for this purpose as well. See [Controlling the User-Mode Debugger from the Kernel Debugger](controlling-the-user-mode-debugger-from-the-kernel-debugger.md) for details.)

It is also useful when debugging locally, as the information is presented in an easily readable format.

If **!dreg** is used during kernel-mode debugging, the results shown will be for the host computer, and not the target computer. To display raw registry information for the target computer, use the [**!reg**](-reg.md) extension instead.

Here are some examples. The following will display all subkeys of the specified registry key:

```
!dreg hkcu\Software\Microsoft
```

The following will display all values in the specified registry key:

```
!dreg System\CurrentControlSet\Services\Tcpip!*
```

The following will display the value Start in the specified registry key:

```
!dreg System\CurrentControlSet\Services\Tcpip!Start
```

Typing **!dreg** without any arguments will display some brief Help text for this extension in the Debugger Command window.

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[debugger\debugger]:%20!dreg%20%20RELEASE:%20%285/15/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")




