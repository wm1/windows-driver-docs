---
title: .kframes (Set Stack Length)
description: The .kframes command sets the default length of a stack trace display.
ms.assetid: 4f11a197-add1-4957-8345-dfbdb2037605
keywords: ["Set Stack Length (.kframes) command", ".kframes (Set Stack Length) Windows Debugging"]
ms.author: windowsdriverdev
ms.date: 05/23/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
topic_type:
- apiref
api_name:
- .kframes (Set Stack Length)
api_type:
- NA
---

# .kframes (Set Stack Length)


The **.kframes** command sets the default length of a stack trace display.

```
.kframes FrameCountDefault 
```

## <span id="ddk_meta_set_stack_length_dbg"></span><span id="DDK_META_SET_STACK_LENGTH_DBG"></span>Parameters


<span id="_______FrameCountDefault______"></span><span id="_______framecountdefault______"></span><span id="_______FRAMECOUNTDEFAULT______"></span> *FrameCountDefault*   
Specifies the number of stack frames to display when a stack trace command is used.

### <span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>Environment

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Modes</strong></p></td>
<td align="left"><p>User mode, kernel mode</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Targets</strong></p></td>
<td align="left"><p>Live, crash dump</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>Platforms</strong></p></td>
<td align="left"><p>All</p></td>
</tr>
</tbody>
</table>

 

Remarks
-------

You can use the **.kframes** command to set the default length of a stack trace display. This length controls the number of frames that the [**k, kb, kp, kP, and kv**](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md) commands display and the number of DWORD\_PTRs that the **kd** command displays.

You can override this default length by using the *FrameCount* or *WordCount* parameters for these commands.

If you never issue the **.kframes** command, the default count is 20 (0x14).

## <span id="see_also"></span>See also


[**k, kb, kc, kd, kp, kP, kv (Display Stack Backtrace)**](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[debugger\debugger]:%20.kframes%20%28Set%20Stack%20Length%29%20%20RELEASE:%20%285/15/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")





