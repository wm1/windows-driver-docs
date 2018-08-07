---
title: Moving Through a Window
description: Moving Through a Window
ms.assetid: c164a446-1f6c-4d37-8ad6-aa254d3268bc
keywords: ["debugging information windows, navigating"]
ms.author: windowsdriverdev
ms.date: 05/23/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

# Moving Through a Window


## <span id="ddk_moving_through_a_window_dbg"></span><span id="DDK_MOVING_THROUGH_A_WINDOW_DBG"></span>


There are several ways of moving through a debugging information window.

If a scrollbar appears in the window, you can use it to display more of the window.

In addition, some windows support the **Find**, **Go to Address**, or **Go to Line** commands. These commands only change the WinDbg display. They do not affect the execution of the target or any other debugger operations.

### <span id="find_command"></span><span id="FIND_COMMAND"></span>Find Command

You can use the **Find** command in the [Debugger Command window](debugger-command-window.md) or in a [Source window](source-window.md).

When one of these windows is active, click **Find** on the **Edit** menu or press CTRL+F. The **Find** dialog box opens.

Enter the text that you want to find in the dialog box, and select **Up** or **Down** to determine the direction of your search. The search begins wherever the cursor is in the window. You can put the cursor at any point by using the mouse.

Select the **Match whole word only** check box if you want to search for a single whole word. (If you select this check box and you enter multiple words, this check box is ignored.) Select the **Match case** check box to perform a case-sensitive search.

If you close the **Find** dialog box, you can repeat the previous search in a forward direction by clicking **Find Next** on the **Edit** menu or pressing F3. You can repeat the search in a backward direction by pressing SHIFT+F3.

### <span id="go_to_address_command"></span><span id="GO_TO_ADDRESS_COMMAND"></span>Go to Address Command

The **Go to Address** command searches for an address in the application that you are debugging. To use this option, click **Go to Address** on the **Edit** menu or press CTRL+G.

When the **View Code Offset** dialog box appears, enter the address that you want to search for. You can enter this address as an expression, such as a function, symbol, or integer memory address. If the address is ambiguous, a list appears with all of the ambiguous items.

After you click **OK**, the debugger moves the cursor to the beginning of the function or address in the [Disassembly window](disassembly-window.md) or a [Source window](source-window.md).

You can use the **Go to Address** command regardless of which debugging information window is open. If the debugger is in disassembly mode, the debugger finds the address that you are searching for in the Disassembly window. If the debugger is in source mode, the debugger tries to find the address in a Source window. If the debugger cannot find the address in a Source window, the debugger finds the address in the Disassembly window. If the needed window is not open, the debugger opens it.

### <span id="moving_to_a_specific_line"></span><span id="MOVING_TO_A_SPECIFIC_LINE"></span>Moving to a Specific Line

The **Go to Line** command searches for a line number in the active Source window. If the active window is not a Source window, you cannot use the **Go to Line** command.

To activate this option, click **Go to Line** on the **Edit** menu or press CTRL+L.

When the **Go to Line** dialog box appears, enter the line number that you want to find and then click **OK**. The debugger moves the cursor to that line. If the line number is larger than the last line in the file, the cursor moves to the end of the file.

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[debugger\debugger]:%20Moving%20Through%20a%20Window%20%20RELEASE:%20%285/15/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")




