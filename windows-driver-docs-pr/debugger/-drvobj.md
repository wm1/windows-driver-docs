---
title: drvobj
description: The drvobj extension displays detailed information about a DRIVER_OBJECT.
ms.assetid: 98f3cacf-311c-4000-8336-4964cc2cb9b0
keywords: ["drvobj Windows Debugging"]
ms.author: windowsdriverdev
ms.date: 05/23/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
topic_type:
- apiref
api_name:
- drvobj
api_type:
- NA
---

# !drvobj


The **!drvobj** extension displays detailed information about a DRIVER\_OBJECT.

```
!drvobj DriverObject [Flags] 
```

## <span id="ddk__drvobj_dbg"></span><span id="DDK__DRVOBJ_DBG"></span>Parameters


<span id="_______DriverObject______"></span><span id="_______driverobject______"></span><span id="_______DRIVEROBJECT______"></span> *DriverObject*   
Specifies the driver object. This can be the hexadecimal address of the DRIVER\_OBJECT structure or the name of the driver.

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *Flags*   
Can be any combination of the following bits. (The default is 0x01.)

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>Bit 0 (0x1)  
Causes the display to include device objects owned by the driver.

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>Bit 1 (0x2)  
Causes the display to include entry points for the driver's dispatch routines.

<span id="Bit_2__0x4_"></span><span id="bit_2__0x4_"></span><span id="BIT_2__0X4_"></span>Bit 2 (0x4)  
Lists with detailed information the device objects owned by the driver (requires bit 0 (0x1)).

### <span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Kdextx86.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP and later</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>Additional Information

See [Plug and Play Debugging](plug-and-play-debugging.md) for examples and applications of this extension command. For information about driver objects, see the Windows Driver Kit (WDK) documentation and *Microsoft Windows Internals* by Mark Russinovich and David Solomon.

Remarks
-------

If *DriverObject* specifies the name of the device but supplies no prefix, the prefix "\\Driver\\" is assumed. Note that this command will check to see if *DriverObject* is a valid address or device name before using the expression evaluator.

If *DriverObject* is an address, it must be the address of the DRIVER\_OBJECT structure. This can be obtained by examining the arguments passed to the driver's **DriverEntry** routine.

This extension command will display a list of all device objects created by a specified driver. It will also display all fast I/O routines registered with this driver object.

The following is an example for the Symbios Logic 810 SCSI miniport driver:

```
kd> bp DriverEntry          //  breakpoint at DriverEntry

kd> g
symc810!DriverEntry+0x40:    
80006a20: b07e0050 stl     t2,50(sp)

kd> r a0  //address of DevObj (the first parameter)
a0=809d5550

kd> !drvobj 809d5550   //  display the driver object
Driver object is for:
\Driver\symc810
Device Object list:
809d50d0
```

You can also use [**!devobj 809d50d0**](-devobj.md) to get information about the device object.

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[debugger\debugger]:%20!drvobj%20%20RELEASE:%20%285/15/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")




