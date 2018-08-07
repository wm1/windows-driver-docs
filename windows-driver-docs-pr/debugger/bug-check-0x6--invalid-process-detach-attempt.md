---
title: Bug Check 0x6 INVALID_PROCESS_DETACH_ATTEMPT
description: The INVALID_PROCESS_DETACH_ATTEMPT bug check has a value of 0x00000006. This bug check appears very infrequently.
ms.assetid: f468b348-6576-4430-aa8f-b6100a689fee
keywords: ["Bug Check 0x6 INVALID_PROCESS_DETACH_ATTEMPT", "INVALID_PROCESS_DETACH_ATTEMPT"]
ms.author: windowsdriverdev
ms.date: 05/23/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
topic_type:
- apiref
api_name:
- INVALID_PROCESS_DETACH_ATTEMPT
api_type:
- NA
---

# Bug Check 0x6: INVALID\_PROCESS\_DETACH\_ATTEMPT


The INVALID\_PROCESS\_DETACH\_ATTEMPT bug check has a value of 0x00000006.

This bug check appears very infrequently. This bug check can be caused by calling [**KeStackAttachProcess**](https://msdn.microsoft.com/library/windows/hardware/ff549659) routine and subsequently calling [**KeUnstackDetachProcess**](https://msdn.microsoft.com/en-us/library/windows/hardware/ff549677) in the driver's implementation of the [**PLOAD_IMAGE_NOTIFY_ROUTINE**](https://msdn.microsoft.com/en-us/library/windows/hardware/mt764088(v=vs.85).aspx) callback function. The callback runs in a thread of the process in which the image loaded.

**Important** This topic is for programmers. If you are a customer who has received a blue screen error code while using your computer, see [Troubleshoot blue screen errors](http://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors).

 

 




