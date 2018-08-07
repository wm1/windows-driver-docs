---
title: NetTxQueueCreate method
topic_type:
- apiref
api_name:
- NetTxQueueCreate
api_location:
- nettxqueue.h
api_type:
- HeaderDef
---

# NetTxQueueCreate method


[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

Creates a net transmit queue object.

Syntax
------

```cpp
NTSTATUS NetTxQueueCreate(
  _Inout_ PNETTXQUEUE_INIT       NetTxQueueInit,
  _In_    PWDF_OBJECT_ATTRIBUTES TxQueueAttributes,
  _In_    PNET_TXQUEUE_CONFIG    Configuration,
  _Out_   NETTXQUEUE             *TxQueue
);
```

Parameters
----------

*NetTxQueueInit* [in, out]  
A pointer to the **NETTXQUEUE_INIT** structure that the client driver received in [*EVT_NET_ADAPTER_CREATE_TXQUEUE*](evt-net-adapter-create-txqueue.md).

*TxQueueAttributes* [in]  
A pointer to caller-allocated [**WDF_OBJECT_ATTRIBUTES**](https://msdn.microsoft.com/library/windows/hardware/ff552400) structure. The structure’s **ParentObject** must be NULL. The parameter is optional and can be WDF_NO_OBJECT_ATTRIBUTES.

*Configuration* [in]  
A pointer to a caller-allocated [**NET_TXQUEUE_CONFIG**](net-txqueue-config.md) structure.

*TxQueue* [out]  
A pointer to a location that receives a handle to the new net receive queue object.

Return value
------------

The method returns STATUS_SUCCESS if the operation succeeds. Otherwise, this method may return an appropriate NTSTATUS error code.

Remarks
-------

The client calls **NetTxQueueCreate** from within its [*EVT_NET_ADAPTER_CREATE_TXQUEUE*](evt-net-adapter-create-txqueue.md) event callback function. For info on assigning context space to the new object, see [Framework Object Context Space](https://msdn.microsoft.com/windows/hardware/drivers/wdf/framework-object-context-space).

The NETTXQUEUE object is a standard WDF object. The framework manages its deletion, which occurs when the parent WDFDEVICE is deleted.


Requirements
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Target platform</p></td>
<td align="left">Universal</td>
</tr>
<tr class="even">
<td align="left"><p>Minimum KMDF version</p></td>
<td align="left"><p>1.21</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Minimum NetAdapterCx version</p></td>
<td align="left"><p>1.0</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Nettxqueue.h (include Netadaptercx.h)</td>
</tr>
<tr class="odd">
<td align="left"><p>IRQL</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
</tr>
</tbody>
</table>

 

 





