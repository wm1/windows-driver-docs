---
title: obtrace
description: The obtrace extension displays object reference tracing data for the specified object.
ms.assetid: 6a124f9f-1c2f-4303-b84f-0032fb912cc1
keywords: ["obtrace Windows Debugging"]
ms.author: windowsdriverdev
ms.date: 05/23/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
topic_type:
- apiref
api_name:
- obtrace
api_type:
- NA
---

# !obtrace


The **!obtrace** extension displays object reference tracing data for the specified object.

```
!obtrace Object
```

## <span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Object______"></span><span id="_______object______"></span><span id="_______OBJECT______"></span> *Object*   
A pointer to the object or a path.

### <span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Unavailable</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP and later</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>Additional Information

For more information about the Global Flags utility (GFlags), see the Windows Driver Kit (WDK) documentation and *Microsoft Windows Internals* by Mark Russinovich and David Solomon.

Remarks
-------

The object reference tracing feature of Windows records sequential stack traces whenever an object reference counter is incremented or decremented.

Before using this extension to display object reference tracing data, you must use [GFlags](gflags.md) to enable [object reference tracing](object-reference-tracing.md) for the specified object. You can enable object reference tracing as a kernel flag (run-time) setting, in which the change is effective immediately, but disappears if you shut down or restart; or as a registry setting, which requires a restart, but remains effective until you change it.

Here is an example of the output from the **!obtrace** extension:

```
kd> !obtrace 0xfa96f700
Object: fa96f700        Image: cmd.exe
Sequence  (+/-)  Stack
--------  -----  ---------------------------------------------------
   2421d    +1  nt!ObCreateObject+180
                nt!NtCreateEvent+92
                nt!KiFastCallEntry+104
                nt!ZwCreateEvent+11
                win32k!UserThreadCallout+6f
                win32k!W32pThreadCallout+38
                nt!PsConvertToGuiThread+174
                nt!KiBBTUnexpectedRange+c

   2421e    -1  nt!ObfDereferenceObject+19
                nt!NtCreateEvent+d4
                nt!KiFastCallEntry+104
                nt!ZwCreateEvent+11
                win32k!UserThreadCallout+6f
                win32k!W32pThreadCallout+38
                nt!PsConvertToGuiThread+174
                nt!KiBBTUnexpectedRange+c

   2421f    +1  nt!ObReferenceObjectByHandle+1c3
                win32k!xxxCreateThreadInfo+37d
                win32k!UserThreadCallout+6f
                win32k!W32pThreadCallout+38
                nt!PsConvertToGuiThread+174
                nt!KiBBTUnexpectedRange+c

   24220    +1  nt!ObReferenceObjectByHandle+1c3
                win32k!ProtectHandle+22
                win32k!xxxCreateThreadInfo+3a0
                win32k!UserThreadCallout+6f
                win32k!W32pThreadCallout+38
                nt!PsConvertToGuiThread+174
                nt!KiBBTUnexpectedRange+c

   24221    -1  nt!ObfDereferenceObject+19
                win32k!xxxCreateThreadInfo+3a0
                win32k!UserThreadCallout+6f
                win32k!W32pThreadCallout+38
                nt!PsConvertToGuiThread+174
                nt!KiBBTUnexpectedRange+c

----  ----------------------------------------------------------
References: 3, Dereferences 2
```

The primary indicators in the **!obtrace 0xfa96f700** display are listed in the following table.

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Parameter</th>
<th align="left">Meaning</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Sequence</strong></p></td>
<td align="left"><p>Represents the order of operations.</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>+/-</strong></p></td>
<td align="left"><p>Indicates a reference or a dereference operation.</p>
<p>+1 indicates a reference operation.</p>
<p>-1 indicates a dereference operation.</p>
<p>+/- n indicates multiple reference/dereference operations.</p></td>
</tr>
</tbody>
</table>

 

The object reference traces on x64-based target computers might be incomplete because it is not always possible to acquire stack traces at IRQL levels higher than PASSIVE\_LEVEL.

You can stop execution at any time by pressing CTRL+BREAK (in WinDbg) or CTRL+C (in KD).

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[debugger\debugger]:%20!obtrace%20%20RELEASE:%20%285/15/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")




