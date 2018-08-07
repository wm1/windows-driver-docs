---
title: NET_TXQUEUE_CONFIG structure
topic_type:
- apiref
api_name:
- NET_TXQUEUE_CONFIG
api_location:
- nettxqueue.h
api_type:
- HeaderDef
---

# NET_TXQUEUE_CONFIG structure


[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

Call [NET_TXQUEUE_CONFIG_INIT](net-txqueue-config-init.md) to initialize this structure.

Syntax
------

```cpp
typedef struct _NET_TXQUEUE_CONFIG {
  ULONG                                Size;
  PFN_TXQUEUE_CANCEL                   EvtTxQueueCancel;
  PFN_TXQUEUE_SET_NOTIFICATION_ENABLED EvtTxQueueSetNotificationEnabled;
  PFN_TXQUEUE_ADVANCE                  EvtTxQueueAdvance;
  PCNET_CONTEXT_TYPE_INFO              ContextTypeInfo;
} NET_TXQUEUE_CONFIG, *PNET_TXQUEUE_CONFIG;
```

Members
-------

**Size**  
The size, in bytes, of this structure.

**EvtTxQueueCancel**  
A pointer to the client driver's [*EVT_TXQUEUE_CANCEL*](evt-txqueue-cancel.md) event callback function. This callback function is required.

**EvtTxQueueSetNotificationEnabled**  
A pointer to the client driver's [*EVT_TXQUEUE_SET_NOTIFICATION_ENABLED*](evt-txqueue-set-notification-enabled.md) event callback function. This callback function is required.

**EvtTxQueueAdvance**  
A pointer to the client driver's [*EVT_TXQUEUE_ADVANCE*](evt-txqueue-advance.md) event callback function. This callback function is required.

**ContextTypeInfo**  
A pointer to a [**WDF_OBJECT_CONTEXT_TYPE_INFO**](https://msdn.microsoft.com/library/windows/hardware/ff552407) structure.

Remarks
-------

Call [**NET_TXQUEUE_CONFIG_INIT**](net-txqueue-config-init.md) to initialize this structure.

The **NET_TXQUEUE_CONFIG** structure is an input parameter to [**NetTxQueueCreate**](nettxqueuecreate.md). The client must use [**NET_TXQUEUE_CONFIG_INIT**](net-txqueue-config-init.md) to initialize this structure.

Requirements
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Minimum KMDF version</p></td>
<td align="left"><p>1.21</p></td>
</tr>
<tr class="even">
<td align="left"><p>Minimum NetAdapterCx version</p></td>
<td align="left"><p>1.0</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Nettxqueue.h</td>
</tr>
</tbody>
</table>

 

 





