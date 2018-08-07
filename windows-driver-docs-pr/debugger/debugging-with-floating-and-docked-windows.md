---
title: Debugging with Floating and Docked Windows
description: Debugging with Floating and Docked Windows
ms.assetid: 2b3e67de-576e-4cbb-bdf1-58a31cea733c
keywords: ["docking windows, debugging", "floating windows, debugging"]
ms.author: windowsdriverdev
ms.date: 05/23/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

# Debugging with Floating and Docked Windows


## <span id="ddk_debugging_with_floating_and_docked_windows_dbg"></span><span id="DDK_DEBUGGING_WITH_FLOATING_AND_DOCKED_WINDOWS_DBG"></span>


The features that are available in a debugging information window are not affected by whether the window is floating, docked, or docked in a tabbed collection.

### <span id="overview_of_the_window_configuration"></span><span id="OVERVIEW_OF_THE_WINDOW_CONFIGURATION"></span>Overview of the Window Configuration

A floating window is not connected to the WinDbg window or any other dock. Floating windows always appear directly in front of the WinDbg window.

A docked window occupies a fixed position within the WinDbg window or in a separate dock.

When two or more docked windows are tabbed together, they occupy the same position within the frame. You can see only one of these tabbed windows at one time. At the bottom of each tabbed window collection is a set of tabs. The selected tab indicates which window in the collection is visible.

### <span id="making_a_window_active"></span><span id="MAKING_A_WINDOW_ACTIVE"></span>Making a Window Active

You can make any window active, regardless of its position. When a floating window is active, it appears in the foreground. When a window that is inside an additional dock is active, that dock appears in the foreground. When a docked window within the WinDbg window is active, one or more floating windows might still obscure the docked window.

To make a floating window or a docked window active, click its title bar. To make a docked window in a tabbed collection active, click its tab.

You can also make a window active by using the WinDbg menu or toolbar. You can activate any window by clicking the window name at the bottom of the **Window** menu. You can also activate any window (other than a [Memory window](memory-window.md) or a [Source window](source-window.md)) by clicking its name on the **View** menu or clicking its toolbar button.

Press CTRL+TAB to switch between debugging information windows. By pressing these keys repeatedly, you can scan through all of the windows, regardless of whether they are floating, docked by themselves, or part of a tabbed collection of docked windows. When you release the CTRL key, the window that you are currently viewing becomes active.

The ALT+TAB shortcut keys are the standard Microsoft Windows shortcut keys to switch between the windows on the desktop. You can use these shortcut keys to switch between the WinDbg window and any additional docks that you have created. You can also make a dock active by clicking its button in the Windows taskbar.

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[debugger\debugger]:%20Debugging%20with%20Floating%20and%20Docked%20Windows%20%20RELEASE:%20%285/15/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")




