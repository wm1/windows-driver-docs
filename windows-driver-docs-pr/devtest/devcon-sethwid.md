---
title: DevCon SetHwID
description: Adds, deletes, and changes the order of hardware IDs of root-enumerated devices on a local or remote computer.
ms.assetid: 79948ff0-8b30-4a64-beea-e3f08aef7170
keywords:
- DevCon SetHwID Driver Development Tools
topic_type:
- apiref
api_name:
- DevCon SetHwID
api_type:
- NA
ms.author: windowsdriverdev
ms.date: 04/20/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

# DevCon SetHwID


Adds, deletes, and changes the order of hardware IDs of root-enumerated devices on a local or remote computer.

```
    devcon [/m:\\computer] sethwid {* | ID [ID ...] | =class [ID [ID ...]]} := [ = | + | - | ! ]HardwareIDs ...

   
```

## <span id="ddk_devcon_sethwid_tools"></span><span id="DDK_DEVCON_SETHWID_TOOLS"></span>Parameters


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
Specifies the device setup class of the root-enumerated devices. The equal sign (**=**) identifies the string as a class name.

You can also specify hardware IDs, compatible IDs, device instance IDs, or ID patterns following the class name. Type a space between each ID or pattern. DevCon finds devices in the class that match the specified IDs.

<span id="_______HardwareIDs______"></span><span id="_______hardwareids______"></span><span id="_______HARDWAREIDS______"></span> *HardwareIDs*   
Specifies one or more hardware IDs.

If the hardware IDs are not preceded by a symbol parameter (**+**, **-**, **=**, **!**), DevCon adds or moves the specified hardware IDs to the end of the list of hardware IDs for the device in the specified order. This is equivalent to the - parameter.

<span id="_"></span>=  
Replaces the list of hardware IDs for the device with the specified hardware IDs in the specified order.

<span id="______________"></span> **+**   
Adds or moves the specified hardware IDs to the beginning of the list of hardware IDs for the device.

<span id="_______-______"></span> **-**   
Adds or moves the specified hardware IDs to the end of the list of hardware IDs for the device.

<span id="______________"></span> **!**   
Deletes the specified hardware IDs from the list of hardware IDs for the device.

### <span id="comments"></span><span id="COMMENTS"></span>Comments

A *root-enumerated* device is a device that appears in the ROOT registry subkey (HKEY\_LOCAL\_MACHINE\\System\\*ControlSet*\\Enum\\ROOT).

You can specify multiple hardware IDs in each command. The **!** (delete) parameter applies only to the hardware ID that it prefixes. The other symbol parameters apply to all hardware IDs that follow until the next symbol parameter in the command.

DevCon moves, rather than adds, a hardware ID if the specified hardware ID already exists in the list of hardware IDs for the device.

The success message for a **DevCon SetHwIDs** command reports the number of devices (or device lists) in which it has modified hardware IDs, not the number of modified hardware IDs .

### <span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>Sample Usage

```
devcon sethwid @ROOT\LEGACY* := legacy
devcon sethwid @ROOT\LEGACY_AFD\0000 := =afd1 afd2 afd3
devcon sethwid legacy := devtype3 -devtype4
devcon sethwid legacy afd1 := +devtype3
devcon sethwid @ROOT\LEGACY_BEEP\0000 := !beep legacy
```

### <span id="examples"></span><span id="EXAMPLES"></span>Examples

[Example 40: Assign a hardware ID to a legacy device](devcon-examples.md#ddk_example_40_assign_a_hardware_id_to_a_legacy_device_tools)

[Example 41: Add a hardware ID to all legacy devices on a remote computer](devcon-examples.md#ddk_example_41_add_a_hardware_id_to_all_legacy_devices_on_a_remote_com)

[Example 42: Delete a hardware ID from all legacy devices on a remote computer](devcon-examples.md#ddk_example_42_delete_a_hardware_id_from_all_legacy_devices_on_a_remot)

[Example 43: Add, delete, and replace hardware IDs](devcon-examples.md#ddk_example_43_add_delete_and_replace_hardwareids_tools)

[Example 44: Forcibly update the HAL](devcon-examples.md#ddk_example_44_forcibly_update_the_hal_tools)

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[devtest\devtest]:%20DevCon%20SetHwID%20%20RELEASE:%20%2811/17/2016%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")




