---
title: DevCon Classes
description: Lists all device setup classes, including classes that devices on the system do not use. Valid on local and remote computers.
ms.assetid: 05b9339c-30d1-45df-8f43-20a07e520a42
keywords:
- DevCon Classes Driver Development Tools
topic_type:
- apiref
api_name:
- DevCon Classes
api_type:
- NA
ms.author: windowsdriverdev
ms.date: 04/20/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

# DevCon Classes


Lists all [device setup classes](https://msdn.microsoft.com/library/windows/hardware/ff541509), including classes that devices on the system do not use. Valid on local and remote computers.

```
    devcon [/m:\\computer] classes 

   
```

## <span id="ddk_devcon_classes_tools"></span><span id="DDK_DEVCON_CLASSES_TOOLS"></span>Parameters


<span id="________m___computer______"></span><span id="________M___COMPUTER______"></span> **/m:\\\\computer**   
Runs the command on the specified remote computer. The backslashes are required.

**Note**   To run DevCon commands on a remote computer, the Group Policy setting must allow the Plug and Play service to run on the remote computer. On computers that run Windows Vista and Windows 7, the Group Policy disables remote access to the service by default. On computers that run WDK 8.1 and WDK 8, the remote access is unavailable.

 

### <span id="comments"></span><span id="COMMENTS"></span>Comments

The **/m** parameter must precede the operation name (**classes**). Otherwise, DevCon ignores the **/m** parameter and displays the classes on the local computer without returning a syntax error.

In the DevCon display, classes are listed in the order that they appear in the registry (alphanumeric order by GUID).

To find the devices in a setup class, use the [**DevCon ListClass**](devcon-listclass.md) operation. To find the setup class of a particular device, use the [**DevCon Stack**](devcon-stack.md) operation.

### <span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>Sample Usage

```
devcon classes
devcon classes > setupclasses.txt
devcon /m:\\Server01 classes
```

### <span id="examples"></span><span id="EXAMPLES"></span>Examples

[Example 4: List classes on the local computer](devcon-examples.md#ddk_example_4_list_classes_on_the_local_computer_tools)

[Example 5: List classes on the remote computer](devcon-examples.md#ddk_example_5_list_classes_on_the_remote_computer_tools)

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[devtest\devtest]:%20DevCon%20Classes%20%20RELEASE:%20%2811/17/2016%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")




