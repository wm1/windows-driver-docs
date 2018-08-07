---
title: gpiokd.pinisrvec
description: The gpiokd.pinisrvec command displays Interrupt Service Routine (ISR) vector information for a specified pin.
ms.assetid: 83D4C072-92B2-4F61-A099-0BA4F8255BE8
keywords: ["gpiokd.pinisrvec Windows Debugging"]
ms.author: windowsdriverdev
ms.date: 05/23/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
topic_type:
- apiref
api_name:
- gpiokd.pinisrvec
api_type:
- NA
---

# !gpiokd.pinisrvec


The **!gpiokd.pinisrvec** command displays Interrupt Service Routine (ISR) vector information for a specified pin.

```
!gpiokd.bankinfo PinAddress
```

## <span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>Parameters


<span id="_______PinAddress______"></span><span id="_______pinaddress______"></span><span id="_______PINADDRESS______"></span> *PinAddress*   
Address of the [\_GPIO\_PIN\_INFORMATION\_ENTRY](gpio-extensions.md#data-structures-used-by-the-gpio-commands) data structure that represents the pin.

## <span id="DLL"></span><span id="dll"></span>DLL


Gpiokd.dll

## <span id="see_also"></span>See also


[GPIO Extensions](gpio-extensions.md)

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[debugger\debugger]:%20!gpiokd.pinisrvec%20%20RELEASE:%20%285/15/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")





