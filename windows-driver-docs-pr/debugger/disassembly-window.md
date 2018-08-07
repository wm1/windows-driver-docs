---
title: Assembly Code Debugging in WinDbg
description: In WinDbg, you can view assembly code by entering commands or by using the Disassembly window.
ms.assetid: e00ea29e-4153-4588-8353-de69910bfc65
keywords: ["debugging information windows, Disassembly window", "Disassembly window", "assembly debugging, Disassembly window"]
ms.author: windowsdriverdev
ms.date: 05/23/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

# Assembly Code Debugging in WinDbg


In WinDbg, you can view assembly code by entering commands or by using the Disassembly window.

## <span id="Debugger_Command_Window"></span><span id="debugger_command_window"></span><span id="DEBUGGER_COMMAND_WINDOW"></span>Debugger Command Window


You can view assembly code by entering the one of the [**u, ub, uu (Unassemble)**](u--unassemble-.md) commands in the Debugger Command window.

## <span id="ddk_disassembly_window_dbg"></span><span id="DDK_DISASSEMBLY_WINDOW_DBG"></span>Dissasembly Window


To open or switch to the Disassembly window, choose **Dissasembly** from the **View** menu. (You can also press ALT+7 or click the **Disassembly** button (![screen shot of the disassembly button](images/tbdisasm2.png)) on the toolbar. ALT+SHIFT+7 will close the Disassembly Window.)

The following screen shot shows an example of a Disassembly window.

![screen shot of the disassembly window](images/window-disassembly.png)

The debugger takes a section of memory, interprets it as binary machine instructions, and then disassembles it to produce an assembly-language version of the machine instructions. The resulting code is displayed in the Disassembly window.

In the Disassembly window, you can do the following:

-   To disassemble a different section of memory, in the **Offset** box, type the address of the memory you want to disassemble. (You can press ENTER after typing the address, but you do not have to.) The Disassembly window displays code before you have completed the address; you can disregard this code.

-   To see other sections of memory, click the **Previous** or **Next** buttons or press the PAGE UP or PAGE DOWN keys. These commands display disassembled code from the preceding or following sections of memory, respectively. By pressing the RIGHT ARROW, LEFT ARROW, UP ARROW, and DOWN ARROW keys, you can navigate within the window. If you use these keys to move off of the page, a new page will appear.

The Disassembly window has a toolbar that contains two buttons and a shortcut menu with additional commands. To access the menu, right-click the title bar or click the icon that appears near the upper-right corner of the window (![screen shot of the button that displays the disassembly window toolbar shortcut menu](images/tbdisasm2.png)). The following list describes some of the menu commands:

-   **Go to current address** opens the Source window with the source file that corresponds to the selected line in the Disassembly window and highlights this line.

-   **Disassemble before current instruction** causes the current line to be placed in the middle of the Disassembly window. This command is the default option. If this command is cleared, the current line will appear at the top of the Disassembly window, which saves time because reverse-direction disassembly can be time-consuming.

-   **Highlight instructions from the current source line** causes all of the instructions that correspond to the current source line to be highlighted. Often, a single source line will correspond to multiple assembly instructions. If code has been optimized, these assembly instructions might not be consecutive. This command enables you to find all of the instructions that were assembled from the current source line.

-   **Show source line for each instruction** displays the source line number that corresponds to each assembly instruction.

-   **Show source file for each instruction** displays the source file name that corresponds to each assembly instruction.

### <span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>Additional Information

For more information about assembly debugging and related commands and a full explanation of the assembly display, see [Debugging in Assembly Mode](debugging-in-assembly-mode.md).

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[debugger\debugger]:%20Assembly%20Code%20Debugging%20in%20WinDbg%20%20RELEASE:%20%285/15/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")




