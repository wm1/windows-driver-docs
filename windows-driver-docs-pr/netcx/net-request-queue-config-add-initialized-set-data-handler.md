---
title: NET_REQUEST_QUEUE_CONFIG_ADD_INITIALIZED_SET_DATA_HANDLER method
topic_type:
- apiref
api_name:
- NET_REQUEST_QUEUE_CONFIG_ADD_INITIALIZED_METHOD_HANDLER
api_location:
- netrequestqueue.h
api_type:
- HeaderDef
---

# NET_REQUEST_QUEUE_CONFIG_ADD_INITIALIZED_SET_DATA_HANDLER method


[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

Adds a caller-provided, pre-initialized custom request handler to a [**NET_REQUEST_QUEUE_CONFIG**](net-request-queue-config.md) structure.

Syntax
------

```cpp
FORCEINLINE VOID NET_REQUEST_QUEUE_CONFIG_ADD_INITIALIZED_METHOD_HANDLER(
  _In_ PNET_REQUEST_QUEUE_CONFIG           NetRequestQueueConfig,
  _In_ PNET_REQUEST_QUEUE_SET_DATA_HANDLER SetDataHandler
);
```

Parameters
----------

*NetRequestQueueConfig* [in]  
A pointer to a driver-allocated [**NET_REQUEST_QUEUE_CONFIG**](net-request-queue-config.md) structure to which the custom handler is being added.

*SetDataHandler* [in]  
A pointer to a driver-allocated and initialized [**NET_REQUEST_QUEUE_SET_DATA_HANDLER**](net-request-queue-set-data-handler.md) structure.  The client driver must call [**NET_REQUEST_QUEUE_SET_DATA_HANDLER_INIT**](net-request-queue-set-data-handler-init.md) method to initialize the custom handler before calling this function.

Return value
------------

This method does not return a value.

Remarks
-------

If the memory allocation for this method fails, the subsequent call to [**NetRequestQueueCreate**](netrequestqueuecreate.md) returns a failure code.

Requirements
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Minimum supported client</p></td>
<td align="left"><p>Windows 10</p></td>
</tr>
<tr class="even">
<td align="left"><p>Minimum supported server</p></td>
<td align="left"><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Netrequestqueue.h</td>
</tr>
<tr class="even">
<td align="left"><p>IRQL</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
</tr>
</tbody>
</table>

 

 





