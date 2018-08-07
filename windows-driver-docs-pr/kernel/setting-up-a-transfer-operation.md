---
title: Setting Up a Transfer Operation
author: windows-driver-content
description: Setting Up a Transfer Operation
ms.assetid: cabac16d-b946-4b96-af2c-5fd0a0d848da
keywords: ["bus-master DMA WDK kernel", "DMA transfers WDK kernel , bus-master DMA", "adapter objects WDK kernel , bus-master DMA", "logical address ranges WDK DMA", "addresses WDK DMA", "transfer operations WDK DMA"]
ms.author: windowsdriverdev
ms.date: 06/16/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

# Setting Up a Transfer Operation


## <a href="" id="ddk-setting-up-a-transfer-operation-kg"></a>


When [**AllocateAdapterChannel**](https://msdn.microsoft.com/library/windows/hardware/ff540573) transfers control to a driver's [*AdapterControl*](https://msdn.microsoft.com/library/windows/hardware/ff540504) routine, it has allocated a set of map registers. However, the driver must map system physical memory for the current IRP's transfer request to the bus-master adapter's logical address range, as follows:

1.  Call [**MmGetMdlVirtualAddress**](https://msdn.microsoft.com/library/windows/hardware/ff554539) with the MDL at **Irp-&gt;MdlAddress** to get an index for the system physical address where the transfer should start.

    The return value is a required parameter (*CurrentVa*) to [**MapTransfer**](https://msdn.microsoft.com/library/windows/hardware/ff554402).

2.  Call **MapTransfer** to map the system physical address ranges for the IRP's buffer to the bus-master adapter's logical address range.

The driver can then set up the adapter for the transfer operation. The following figure shows the steps involved in setting up the transfer.

![diagram illustrating setting up a transfer operation](images/3dmabus.png)

As the previous figure shows, a driver's *AdapterControl* routine sets up a bus-master DMA operation as follows:

1.  The *AdapterControl* routine gets the address at which to start the transfer. For the initial transfer required to satisfy an IRP, the *AdapterControl* routine calls [**MmGetMdlVirtualAddress**](https://msdn.microsoft.com/library/windows/hardware/ff554539), passing a pointer to the MDL at **Irp-&gt;MdlAddress**, which describes the buffer for this DMA transfer.

    **MmGetMdlVirtualAddress** returns a virtual address that the driver can use as an index for the system physical address where the transfer should start.

    If the IRP requires more than one transfer operation, the driver calculates an updated starting address, as described later in this section.

2.  The *AdapterControl* routine saves the address returned by **MmGetMdlVirtualAddress** or calculated in Step 1. This address is a required parameter (*CurrentVa*) to [**MapTransfer**](https://msdn.microsoft.com/library/windows/hardware/ff554402).

3.  The *AdapterControl* routine calls **MapTransfer**, which returns a logical address at which the driver can program the bus-master adapter to begin the transfer operation. In the call to **MapTransfer**, the driver supplies the following parameters:
    -   The adapter object pointer returned by [**IoGetDmaAdapter**](https://msdn.microsoft.com/library/windows/hardware/ff549220)

    -   A pointer to the MDL at **Irp-&gt;MdlAddress** for the current IRP

    -   The *MapRegisterBase* handle passed to the driver's *AdapterControl* routine by **AllocateAdapterChannel** (see [Allocating the Bus-Master Adapter Object](allocating-the-bus-master-adapter-object.md))

    -   The value returned by **MmGetMdlVirtualAddress** if this is the first call to **MapTransfer** for the current IRP

        Otherwise, the driver supplies an updated *CurrentVa* value, indicating the next physical-to-logical mapping to be done. (How to calculate an updated *CurrentVa* is described later in this section.)

    -   A pointer to a variable (*Length*), which indicates the number of bytes for this transfer

        If the driver has enough map registers to transfer all the requested data in a single DMA operation and has no device-specific constraints on its DMA operations, the *Length* can be set to the value of **Length** in the driver's I/O stack location of the IRP. At most, the input length in bytes can be (PAGE\_SIZE \* the *NumberOfMapRegisters* returned by **IoGetDmaAdapter**). Otherwise, the driver must split up the request, as explained in [Splitting Transfer Requests](splitting-dma-transfer-requests.md), and must update the value of *Length* in subsequent calls to **MapTransfer** for the current IRP.

    -   A Boolean value (*WriteToDevice*), indicating the direction of the transfer operation (TRUE to transfer data from memory to the device)

4.  The *AdapterControl* routine sets up the device for the DMA operation.

5.  The *AdapterControl* routine returns **DeallocateObjectKeepRegisters**.

If the driver must call **MapTransfer** more than once to satisfy the current IRP, it supplies the same adapter object pointer, *Mdl* pointer, *MapRegisterBase* handle, and transfer direction in every call to **MapTransfer**. However, the driver must supply updated *CurrentVa* and *Length* values in its second and subsequent calls to **MapTransfer**. Use the following formulas to calculate these values:

-   *CurrentVa* = *CurrentVa* + (*Length* requested in preceding call to **MapTransfer**)

-   *Length* = Minimum (remaining **Length** to be transferred, (PAGE\_SIZE \* *NumberOfMapRegisters* returned by **IoGetDmaAdapter**))

The context information each driver should maintain about its DMA transfers depends on the needs of its particular device. Typical context might include the current virtual address in the MDL (*CurrentVa*), the number of bytes transferred so far, the number of bytes remaining to transfer, and possibly a pointer to the current IRP.

For drivers of devices with scatter/gather capabilities, the *Length* parameter to **MapTransfer** is both an input and output parameter. On return from **MapTransfer**, it indicates how many bytes of data the system has mapped. That is, the return value of *Length*, in combination with the returned logical address, indicates the range of logical addresses the bus-master adapter can use for this piece of the transfer in this DMA operation.

**Note**   Since *Length* is overwritten by **MapTransfer**, follow this implementation guideline:
Never pass a pointer to the **Length** in the driver's I/O stack location of an IRP as the *Length* parameter to **MapTransfer** if your device supports scatter/gather.

Doing this could destroy the value in the current IRP, making it impossible to determine whether the driver has transferred all the requested data.

 

At the end of each DMA operation, the driver must call [**FlushAdapterBuffers**](https://msdn.microsoft.com/library/windows/hardware/ff545917) with a valid adapter object pointer and the *MapRegisterBase* handle to be sure that all the data has been transferred, and to release the physical-to-logical mappings for the current DMA operation. If the driver must set up additional DMA operations to satisfy the current IRP, it must call **FlushAdapterBuffers** after each transfer operation is complete.

When all the requested transfer is complete or the driver must return an error status for the IRP, the driver should call [**FreeMapRegisters**](https://msdn.microsoft.com/library/windows/hardware/ff546513) immediately after its last call to **FlushAdapterBuffers** in order to get the best possible throughput for the bus-master adapter. In its call to **FreeMapRegisters**, the driver must pass the adapter object pointer that it passed in the preceding call to **AllocateAdapterChannel**.

 

 


--------------------
[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bkernel\kernel%5D:%20Setting%20Up%20a%20Transfer%20Operation%20%20RELEASE:%20%286/14/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")


