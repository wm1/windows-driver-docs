---
title: DevCon Install
description: Creates a new, root-enumerated devnode for a non-Plug and Play device and installs its supporting software. Valid only on the local computer.
ms.assetid: d31007dd-6f20-460d-8561-d1639c69aa09
keywords:
- DevCon Install Driver Development Tools
topic_type:
- apiref
api_name:
- DevCon Install
api_type:
- NA
ms.author: windowsdriverdev
ms.date: 04/20/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

# DevCon Install


Creates a new, root-enumerated devnode for a non-Plug and Play device and installs its supporting software. Valid only on the local computer.

```
    devcon [/r] install INFfile HardwareID 

   
```

## <span id="ddk_devcon_install_tools"></span><span id="DDK_DEVCON_INSTALL_TOOLS"></span>Parameters


<span id="________r______"></span><span id="________R______"></span> **/r**   
Conditional reboot. Reboots the system after completing an operation when a reboot is required to make the change effective. By default, DevCon does not reboot the system.

<span id="_______INFfile______"></span><span id="_______inffile______"></span><span id="_______INFFILE______"></span> *INFfile*   
Specifies the full path and file name of the INF file for the device. If you omit the path, DevCon assumes that the file is in the current directory.

<span id="_______HardwareID______"></span><span id="_______hardwareid______"></span><span id="_______HARDWAREID______"></span> *HardwareID*   
Specifies a hardware ID for the device.

The specified hardware ID must exactly match the hardware ID of the device. Patterns are not valid. Do not type a single quote character (**'**) to indicate a literal value. For more information, see [Hardware IDs](https://msdn.microsoft.com/library/windows/hardware/ff546152) and [Device Identification Strings](https://msdn.microsoft.com/library/windows/hardware/ff541224).

### <span id="comments"></span><span id="COMMENTS"></span>Comments

The system might need to be rebooted to make this change effective. To have DevCon reboot the system, add the conditional reboot parameter (**/r**) to the command.

You cannot use the **DevCon Install** operation for Plug and Play devices.

The **DevCon Install** operation creates a new non-Plug and Play device node. Then, it uses the [**DevCon Update**](devcon-update.md) operation to install drivers for the newly added device. As a result, the success message for the **DevCon Install** operation reports that DevCon has created the device node and that it has updated the drivers for the device.

If any step of the **DevCon Install** operation fails, DevCon displays a failure message and does not proceed with the driver installation.

The **DevCon Install** command creates a new non-Plug and Play device node each time you run it. To update or reinstall drivers, use the [**DevCon Update**](devcon-update.md) command.

### <span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>Sample Usage

```
devcon install c:\windows\inf\newdvc.inf ISAPNP\CSC4324\0
devcon /r install c:\windows\inf\newdvc.inf ISAPNP\CSC4324\0
```

### <span id="examples"></span><span id="EXAMPLES"></span>Examples

[Example 33: Install a device](devcon-examples.md#ddk_example_33_install_a_device_tools)

[Example 34: Install a device using unattended setup](devcon-examples.md#ddk_example_34_install_a_device_using_unattended_setup_tools)

## <span id="see_also"></span>See also


[Hardware IDs](https://msdn.microsoft.com/library/windows/hardware/ff546152)

[Device Identification Strings](https://msdn.microsoft.com/library/windows/hardware/ff541224)

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[devtest\devtest]:%20DevCon%20Install%20%20RELEASE:%20%2811/17/2016%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")





