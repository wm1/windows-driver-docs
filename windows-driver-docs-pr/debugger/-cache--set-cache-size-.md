---
title: .cache (Set Cache Size)
description: The .cache command sets the size of the cache used to hold data obtained from the target. Also sets a number of cache and memory options.
ms.assetid: 638cb2e6-b333-4311-967c-d86c2e93b4ec
keywords: [".cache (Set Cache Size) Windows Debugging"]
ms.author: windowsdriverdev
ms.date: 05/23/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
topic_type:
- apiref
api_name:
- .cache (Set Cache Size)
api_type:
- NA
---

# .cache (Set Cache Size)


The **.cache** command sets the size of the cache used to hold data obtained from the target. Also sets a number of cache and memory options.

```
.cache Size 
.cache Option 
.cache 
```

## <span id="ddk_meta_set_cache_size_dbg"></span><span id="DDK_META_SET_CACHE_SIZE_DBG"></span>Parameters


<span id="_______Size______"></span><span id="_______size______"></span><span id="_______SIZE______"></span> *Size*   
The size of the kernel debugging cache, in kilobytes. If *Size* is zero, the cache is disabled. The command output displays the cache size in bytes. (The default size is 1000 KB.)

<span id="_______Option______"></span><span id="_______option______"></span><span id="_______OPTION______"></span> *Option*   
Can be any one of the following options:

<span id="hold"></span><span id="HOLD"></span>**hold**  
Automatic cache flushing is disabled.

<span id="unhold"></span><span id="UNHOLD"></span>**unhold**  
Turns off the **hold** option. (This is the default setting.)

<span id="decodeptes"></span><span id="DECODEPTES"></span>**decodeptes**  
All transition page table entries (PTEs) will be implicitly decoded. (This is the default setting.)

<span id="nodecodeptes"></span><span id="NODECODEPTES"></span>**nodecodeptes**  
Turns off the **decodeptes** option.

<span id="forcedecodeptes"></span><span id="FORCEDECODEPTES"></span>**forcedecodeptes**  
All virtual addresses will be translated into physical addresses before access. This option also causes the cache to be disabled. Unless you are concerned with kernel-mode memory, it is more efficient to use **forcedecodeuser** instead.

<span id="forcedecodeuser"></span><span id="FORCEDECODEUSER"></span>**forcedecodeuser**  
All user-mode virtual addresses will be translated into physical addresses before access. This option also causes the cache to be disabled.

**Note**   You must activate **forcedecodeuser** (or **forcedecodeptes**) before using [**.thread (Set Register Context)**](-thread--set-register-context-.md), [**.context (Set User-Mode Address Context)**](-context--set-user-mode-address-context-.md), [**.process (Set Process Context)**](-process--set-process-context-.md), or [**!session**](-session.md) during live debugging. If you use the **/p** option with **.thread** and **.process**, the **forcedecodeuser** option is automatically set. In any other case, you will need to use the **.cache forcedecodeuser** command explicitly.

 

<span id="noforcedecodeptes"></span><span id="NOFORCEDECODEPTES"></span>**noforcedecodeptes**  
Turns off the **forcedecodeptes** and **forcedecodeuser** options. (This is the default setting.)

<span id="flushall"></span><span id="FLUSHALL"></span>**flushall**  
Deletes the entire virtual memory cache.

<span id="flushu"></span><span id="FLUSHU"></span>**flushu**  
Deletes all entries of ranges with errors from the cache, as well as all user-mode entries.

<span id="flush_Address"></span><span id="flush_address"></span><span id="FLUSH_ADDRESS"></span>**flush** *Address*  
Deletes a 4096-byte block of the cache, beginning at *Address*.

### <span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>Environment

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Modes</strong></p></td>
<td align="left"><p>kernel mode only</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Targets</strong></p></td>
<td align="left"><p>live debugging only</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>Platforms</strong></p></td>
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

Remarks
-------

If **.cache** is used with no arguments, the current cache size, status, and options are displayed.

The **.cache forcedecodeuser** or **.cache forcedecodeptes** option will only last as long as the debugger remains broken into the target computer. If any stepping or execution of the target takes place, the **noforcedecodeptes** state will again take effect. This prevents the debugger from interfering with execution or a reboot in an unproductive manner.

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[debugger\debugger]:%20.cache%20%28Set%20Cache%20Size%29%20%20RELEASE:%20%285/15/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")




