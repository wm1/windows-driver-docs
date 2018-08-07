---
title: wudfext.umirps
description: The wudfext.umirps extension displays the list of pending user-mode I/O request packets (UM IRPs) in the host process.
ms.assetid: bba78784-f4f5-432c-ad5e-837770de79d9
keywords: ["wudfext.umirps Windows Debugging"]
ms.author: windowsdriverdev
ms.date: 05/23/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
topic_type:
- apiref
api_name:
- wudfext.umirps
api_type:
- NA
---

# !wudfext.umirps


The **!wudfext.umirps** extension displays the list of pending user-mode I/O request packets (UM IRPs) in the host process.

```
!wudfext.umirps NumberOfIrps Flags
```

## <span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______NumberOfIrps______"></span><span id="_______numberofirps______"></span><span id="_______NUMBEROFIRPS______"></span> *NumberOfIrps*   
Optional. Specifies the number of pending UM IRPs to display information about. If *NumberOfIrps* is an asterisk (\*) or is omitted, all UM all UM IRPs will be displayed.

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *Flags*   
Optional. Specifies the type of information to be displayed. *Flags* can be any combination of the following bits. The default value is 0x01.

<span id="Bit_0__0x01_"></span><span id="bit_0__0x01_"></span><span id="BIT_0__0X01_"></span>Bit 0 (0x01)  
Displays details about the pending IRPs.

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
<td align="left"><p>Wudfext.dll</p></td>
</tr>
</tbody>
</table>

 

### <span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>Additional Information

For more information, see [User-Mode Driver Framework Debugging](user-mode-driver-framework-debugging.md).

Remarks
-------

The list of pending UM IRPs that are displayed have either been presented to the driver or are waiting to be presented to the driver.

By default, **!wudfext.umirps** shows all UM IRPs. However, you can use the *NumberOfIrps* parameter to limit this display.

The following is an example of the **!wudfext.umirps** display:

```
kd> !umirps 0xa 
Number of pending IRPS: 0xc8
####  CWudfIrp          Type        UniqueId          KernelIrp
----  ----------------  ----------  ----------------  ---------
0000            3dd280        READ                dc  856f02f0
0001            3dd380       WRITE                dd  85b869e0
0002            3dd480        READ                de  85377850
0003            3dd580        READ                df  93bba4e8
0004            3dd680       WRITE                e0  84cb9d70
0005            3dd780        READ                e1  85bec150
0006            3dd880       WRITE                e2  86651db0
0007            3dd980        READ                e3  85c22818
0008            3dda80        READ                e4  9961d150
0009            3ddb80       WRITE                e5  85c15148
```

To determine the corresponding kernel-mode IRP, use the [**!wudfext.wudfdownkmirp**](-wudfext-wudfdownkmirp.md) extension. Alternatively, you can use the values in the **UniqueId** and **KernelIrp** columns to match a UMDF IRP (or UM IRP) to a corresponding kernel IRP. You can pass the values in the **CWudfIrp** column to the [**!wudfext.umirp**](-wudfext-umirp.md) extension to determine the framework **IWDFRequest** objects that each layer in the device stack can access.

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[debugger\debugger]:%20!wudfext.umirps%20%20RELEASE:%20%285/15/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")




