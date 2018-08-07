---
title: Debugging Performance-Optimized Code
description: Debugging Performance-Optimized Code
ms.assetid: 9dbae9e7-c181-491e-9566-6f5e8182aae0
keywords: ["performance-optimized code"]
ms.author: windowsdriverdev
ms.date: 05/23/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

# Debugging Performance-Optimized Code


## <span id="ddk_performance_optimized_code_dbg"></span><span id="DDK_PERFORMANCE_OPTIMIZED_CODE_DBG"></span>


Microsoft has certain techniques that it uses to re-arrange compiled and linked code so that it executes with more efficiency. These techniques optimize the component for memory hierarchies, and are based on training scenarios.

The resulting optimization reduces paging (and page faults), and increases spatial locality between code and data. It addresses a key performance bottleneck that would be introduced by poor positioning of the original code. A component that has gone through this optimization may have its code or data block within a function moved to different locations of the binary.

In modules that have been optimized by these techniques, the locations of code and data blocks will often be found at memory addresses different than the locations where they would reside after normal compilation and linking. Furthermore, functions may have been split into many non-contiguous blocks, in order that the most commonly-used code paths can be located close to each other on the same pages.

Therefore, a function (or any symbol) plus an offset will not necessarily have the same meaning it would have in non-optimized code.

### <span id="debugging_performance_optimized_code"></span><span id="DEBUGGING_PERFORMANCE_OPTIMIZED_CODE"></span>Debugging Performance-Optimized Code

When debugging, you can see if a module has been performance-optimized by using the [**!lmi**](-lmi.md) extension command on any module for which symbols have been loaded:

```
0:000> !lmi ntdll
Loaded Module Info: [ntdll]
         Module: ntdll
   Base Address: 77f80000
     Image Name: ntdll.dll
   Machine Type: 332 (I386)
     Time Stamp: 394193d2 Fri Jun 09 18:03:14 2000
       CheckSum: 861b1
Characteristics: 230e stripped perf
Debug Data Dirs: Type Size     VA  Pointer
                 MISC  110,     0,   76c00 [Data not mapped]
     Image Type: DBG      - Image read successfully from symbol server.
                 c:\symbols\dll\ntdll.dbg
    Symbol Type: DIA PDB  - Symbols loaded successfully from symbol server.
                 c:\symbols\dll\ntdll.pdb
```

In this output, notice the term **perf** on the "Characteristics" line. This indicates that this performance optimization has been applied to ntdll.dll.

The debugger is able to understand a function or other symbol without an offset; this allows you to set breakpoints on functions or other labels without any problem. However, the output of a dissassembly operation may be confusing, because this disassembly will reflect the changes made by the optimizer.

Since the debugger will try to stay close to the original code, you might see some amusing results. The rule of thumb when working with performance-optimized codes is simply that you cannot perform reliable address arithmetic on optimized code.

Here is an example:

```
kd> bl
 0 e f8640ca6     0001 (0001) tcpip!IPTransmit
 1 e f8672660     0001 (0001) tcpip!IPFragment

kd> u f864b4cb
tcpip!IPTransmit+e48:
f864b4cb f3a4             rep     movsb
f864b4cd 8b75cc           mov     esi,[ebp-0x34]
f864b4d0 8b4d10           mov     ecx,[ebp+0x10]
f864b4d3 8b7da4           mov     edi,[ebp-0x5c]
f864b4d6 8bc6             mov     eax,esi
f864b4d8 6a10             push    0x10
f864b4da 034114           add     eax,[ecx+0x14]
f864b4dd 57               push    edi
```

You can see from the breakpoint list that the address of **IPTransmit** is 0xF8640CA6.

When you unassemble a section of code within this function at 0xF864B4CB, the output indicates that this is 0xE48 bytes past the beginning of the function. However, if you subtract the base of the function from this address, the actual offset appears to be 0xA825.

What is happening is this: The debugger is indeed showing a disassembly of the binary instructions beginning at 0xF864B4CB. But instead of computing the offset by simple subtraction, the debugger displays -- as best it can -- the offset to the function entry as it existed in the original code before the optimizations were performed. That value is 0xE48.

On the other hand, if you try to look at **IPTransmit**+0xE48, you will see this:

```
kd> u tcpip!iptransmit+e48
tcpip!ARPTransmit+d8:
f8641aee 0856ff           or      [esi-0x1],dl
f8641af1 75fc             jnz     tcpip!ARPTransmit+0xd9 (f8641aef)
f8641af3 57               push    edi
f8641af4 e828eeffff       call    tcpip!ARPSendData (f8640921)
f8641af9 5f               pop     edi
f8641afa 5e               pop     esi
f8641afb 5b               pop     ebx
f8641afc c9               leave
```

What is happening here is that the debugger recognizes the symbol **IPTransmit** as equivalent to the address 0xF8640CA6, and the command parser performs a simple addition to find that 0xF8640CA6 + 0xE48 = 0xF8641AEE. This address is then used as the argument for the [**u (Unassemble)**](u--unassemble-.md) command. But once this location is analyzed, the debugger discovers that this is not **IPTransmit** plus an offset of 0xE48. Indeed, it is not part of this function at all. Rather, it corresponds to the function **ARPTransmit** plus an offset of 0xD8.

The reason this happens is that performance optimization is not reversible through address arithmetic. While the debugger can take an address and deduce its original symbol and offset, it does not have enough information to take a symbol and offset and translate it to the correct address. Consequently, disassembly is not useful in these cases.

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[debugger\debugger]:%20Debugging%20Performance-Optimized%20Code%20%20RELEASE:%20%285/15/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")




