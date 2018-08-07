---
title: DevCon Update
description: Forcibly replaces the current device drivers for a specified device with drivers listed in the specified INF file. Valid only on the local computer.
ms.assetid: c07d7abe-31d8-4a8d-87da-8db649710c15
keywords:
- DevCon Update Driver Development Tools
topic_type:
- apiref
api_name:
- DevCon Update
api_type:
- NA
ms.author: windowsdriverdev
ms.date: 04/20/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

# DevCon Update


Forcibly replaces the current device drivers for a specified device with drivers listed in the specified INF file. Valid only on the local computer.

```
    devcon [/r] update INFfile HardwareID 

   
```

## <span id="ddk_devcon_update_tools"></span><span id="DDK_DEVCON_UPDATE_TOOLS"></span>Parameters


<span id="________r______"></span><span id="________R______"></span> **/r**   
Conditional reboot. Reboots the system after completing an operation only if a reboot is required to make a change effective.

<span id="_______INFfile______"></span><span id="_______inffile______"></span><span id="_______INFFILE______"></span> *INFfile*   
Specifies the full path and file name of the INF (information) file used in the update. If you omit the path, DevCon assumes that the file is in the current directory.

<span id="_______HardwareID______"></span><span id="_______hardwareid______"></span><span id="_______HARDWAREID______"></span> *HardwareID*   
Updates the drivers for devices with the specified hardware ID. The hardware ID specified in this command must exactly match the hardware ID of the device. Patterns are not valid. Do not type a single quote character (**'**) to indicate a literal value.

### <span id="comments"></span><span id="COMMENTS"></span>Comments

The **DevCon Update** operation forces an update to the most appropriate drivers in the specified INF file, even if those drivers are older or less appropriate than the current drivers or the drivers in a different INF file. For more information, see [How Setup Selects Drivers](https://msdn.microsoft.com/library/windows/hardware/ff546228).

You cannot use a **DevCon Update** command to update drivers for nonpresent devices.

Before updating the driver for any device, determine which devices will be affected by the update command. To do so, use the hardware ID in a display command, such as [**DevCon HwIDs**](devcon-hwids.md) or [**DevCon DriverFiles**](devcon-driverfiles.md). This is especially important in a **DevCon Update** operation because DevCon does not list the device drivers that it updates.

DevCon prompts the user if the INF file specifies an unsigned driver or if it cannot find a required file, such as a driver file on removable media. To suppress prompts that require a response, use the noninteractive update operation, [**DevCon UpdateNI**](devcon-updateni.md).

The system might need to be rebooted to make this change effective. To have DevCon reboot the system, add the conditional reboot parameter (/r) to the command.

### <span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>Sample Usage

```
devcon update c:\windows\inf\newdvc.inf ISAPNP\CSC4324\0
devcon /r update c:\windows\inf\newdvc.inf *PNP030b
```

### <span id="example"></span><span id="EXAMPLE"></span>Example

[Example 32: Update the driver for communication ports](devcon-examples.md#ddk_example_32_update_the_driver_for_communication_ports_tools)

[Example 44: Forcibly update the HAL](devcon-examples.md#ddk_example_44_forcibly_update_the_hal_tools)

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[devtest\devtest]:%20DevCon%20Update%20%20RELEASE:%20%2811/17/2016%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")




