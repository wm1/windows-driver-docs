---
title: Application Verifier
description: Application Verifier
ms.assetid: d3040254-aa9b-4aae-b850-966078df7988
keywords: ["verifying drivers (Application Verifier)", "driver verification (Application Verifier)", "Application Verifier", "AppVerif.exe", "user-mode application testing"]
ms.author: windowsdriverdev
ms.date: 05/23/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

# Application Verifier


Application Verifier (AppVerif.exe) is a *dynamic verification* tool for user-mode applications. This tool monitors application actions while the application runs, subjects the application to a variety of stresses and tests, and generates a report about potential errors in application execution or design.

Application Verifier can detect errors in any user-mode applications that are not based on managed code, including user-mode drivers. It finds subtle programming errors that might be difficult to detect during standard application testing or driver testing.

You can use Application Verifier alone or in conjunction with a user-mode debugger. This tool runs on Microsoft Windows XP and later versions of Windows. The current user must be a member of the Administrators group on the computer.

Application Verifier is not included in Debugging Tools for Windows. Application Verifier is included in the Windows Software Development Kit (SDK). You can find information about downloading and installing the Windows SDK [here](http://go.microsoft.com/fwlink/p?LinkID=271979). After you install the Windows SDK, Appverif.exe and Appverif.chm will be in Windows\\System32. To start Application Verifier, open a Command Prompt window and enter **appverif**.

The Application Verifier tool comes with its own documentation. To read the documentation, start Application Verifier, and from the **Help** menu, click **Help**, or press **F1**.

## <span id="related_topics"></span>Related topics


[Tools Related to Debugging Tools for Windows](tools-related-to-debugging-tools-for-windows.md)

[Tools Included in Debugging Tools for Windows](extra-tools.md)

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[debugger\debugger]:%20Application%20Verifier%20%20RELEASE:%20%285/15/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")





