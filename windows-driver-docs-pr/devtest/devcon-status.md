---
title: DevCon Status
description: Displays the status (running, stopped, or disabled) of the driver for devices on the computer. Valid on local and remote computers.
ms.assetid: 97da6df4-ad93-440a-9136-13f2b79cbe9c
keywords:
- DevCon Status Driver Development Tools
topic_type:
- apiref
api_name:
- DevCon Status
api_type:
- NA
ms.author: windowsdriverdev
ms.date: 04/20/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

# DevCon Status


Displays the status (running, stopped, or disabled) of the driver for devices on the computer. Valid on local and remote computers.

```
    devcon [/m:\\computer] status {* | ID [ID ...] | =class [ID [ID ...]]} 

   
```

## <span id="ddk_devcon_status_tools"></span><span id="DDK_DEVCON_STATUS_TOOLS"></span>Parameters


<span id="________m___computer______"></span><span id="________M___COMPUTER______"></span> **/m:\\\\***computer*   
Runs the command on the specified remote computer. The backslashes are required.

**Note**   To run DevCon commands on a remote computer, the Group Policy setting must allow the Plug and Play service to run on the remote computer. On computers that run Windows Vista and Windows 7, the Group Policy disables remote access to the service by default. On computers that run WDK 8.1 and WDK 8, the remote access is unavailable.

 

<span id="______________"></span> **\***   
Represents all devices on the computer.

<span id="_______ID______"></span><span id="_______id______"></span> *ID*   
Specifies all or part of a hardware ID, compatible ID, or device instance ID of a device. When specifying multiple IDs, type a space between each ID. IDs that include an ampersand character (**&**) must be enclosed in quotation marks.

The following special characters modify the ID parameter.

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Character</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>*</strong></p></td>
<td align="left"><p>Matches any character or no character. Use the wildcard character (*) to create an ID pattern, for example, *disk*.</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>@</strong></p></td>
<td align="left"><p>Indicates a device instance ID, for example, <strong>@ROOT\FTDISK\0000</strong>.</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>'</strong></p>
<p>(single quote)</p></td>
<td align="left"><p>Matches the string literally (exactly as it appears). Precede a string with a single quote to indicate that an asterisk is part of the ID name and is not a wildcard character, for example, <strong>'*PNP0600</strong>, where *PNP0600 (including the asterisk) is the hardware ID.</p></td>
</tr>
</tbody>
</table>

 

<span id="________class______"></span><span id="________CLASS______"></span> **=***class*   
Specifies the device setup class of the devices. The equal sign (**=**) identifies the string as a class name.

You can also specify hardware IDs, compatible IDs, device instance IDs, or ID patterns following the class name. Type a space between each ID or pattern. DevCon finds devices in the class that match the specified IDs.

### <span id="comments"></span><span id="COMMENTS"></span>Comments

The **/m** parameter must precede the operation name (**status**). Otherwise, DevCon ignores the **/m** parameter and displays the status of device drivers on the local computer without returning a syntax error.

If DevCon cannot determine the status of the device, such as when the device is no longer attached to the computer, DevCon omits the line describing the status from the status display.

The following example shows a successful status command. The text describing the device status appears in bold type.

```
STORAGE\VOLUME\1&30A96598&0&SIGNATURE80OFFSET7E0000LENGTH270987600
    Name: Generic volume
    Driver is running.
1 matching device(s) found.
```

In contrast, the following example shows how DevCon displays the status of a device that it cannot find. The status description is missing from the display.

```
STORAGE\VOLUME\1&30A96598&0&SIGNATURE80OFFSET7E0000LENGTH270987600
    Name: Generic volume
1 matching device(s) found.
```

### <span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>Sample Usage

```
devcon /m:\\Server01 status *
devcon status pci*
devcon status "PCI\VEN_115D&DEV_0003&SUBSYS_0181115D"
devcon status =printer
```

### <span id="examples"></span><span id="EXAMPLES"></span>Examples

[Example 17: Display the status of all devices on the local computer](devcon-examples.md#ddk_example_17_display_the_status_of_all_devices_on_the_local_computer)

[Example 18: Display the status of a device by device instance ID](devcon-examples.md#ddk_example_18_display_the_status_of_a_device_by_device_instance_id_to)

[Example 19: Display the status of related devices on a remote computer](devcon-examples.md#ddk_example_19_display_the_status_of_related_devices_on_a_remote_compu)

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[devtest\devtest]:%20DevCon%20Status%20%20RELEASE:%20%2811/17/2016%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")




