---
title: Risks Entailed When Setting Breakpoints
description: Risks Entailed When Setting Breakpoints
ms.assetid: 92c1007b-f871-48e9-a215-4d36ed1371ea
keywords: ["breakpoints, risks"]
ms.author: windowsdriverdev
ms.date: 05/23/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

# Risks Entailed When Setting Breakpoints


When you are setting a [breakpoints](using-breakpoints.md) by specifying a memory address or a symbol plus an offset, you must not put this breakpoint in the middle of an instruction.

For example, consider the following disassembled code.

```
770000f1 5e               pop     esi
770000f2 5b               pop     ebx
770000f3 c9               leave
770000f4 c21000           ret     0x10
770000f7 837ddc00         cmp     dword ptr [ebp-0x24],0x0
```

The first three instructions are only one byte long. However, the fourth instruction is three bytes long. (It includes bytes 0x770000F4, 0x770000F5, and 0x770000F6.) If you want to put a breakpoint on this instruction by using the **bp**, **bu**, or **ba** command, you must specify the 0x770000F4 address.

If you put a breakpoint in the 0x770000F5 address by using the **ba** command, the processor puts a breakpoint at that location. But this breakpoint would never be triggered, because the processor considers 0x770000F4 to be the actual address of the instruction.

If you put a breakpoint in the 0x770000F5 address by using the **bp** or **bu** commands, the debugger writes a breakpoint at that location. However, this breakpoint might corrupt the target because of how the debugger creates breakpoints:

1.  The debugger saves the contents of 0x770000F5 and overwrites this memory with a breakpoint instruction.

2.  If you try to display this memory in the debugger, the debugger does not show the breakpoint instruction that it has written. Instead, the debugger shows the memory that "should" be there. That is, the debugger shows the original memory, or any modifications to that memory that you have made since inserting the breakpoint.

3.  If you use the **BC** command to remove the breakpoint, the debugger restores the original memory to its proper location.

When you put a breakpoint at 0x770000F5, the debugger saves this byte and a break instruction is written here. However, when the application runs, it reaches the 0x770000F4 address and recognizes this address as the first byte of a multibyte instruction. The processor then tries to combine 0x770000F4, 0x770000F5, and possibly some later bytes into a single instruction. This combination can create a variety of behaviors, none of which are desirable.

Therefore, when you put breakpoints by using a **bp**, **bu**, or **ba** command, make sure that you always put the breakpoints at the proper address. If you are using the WinDbg graphical interface to add breakpoints, you do not have to be concerned about this situation because the correct address is chosen automatically.

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[debugger\debugger]:%20Risks%20Entailed%20When%20Setting%20Breakpoints%20%20RELEASE:%20%285/15/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")




