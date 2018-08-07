---
title: Windows kernel opaque structures
author: windows-driver-content
description: Windows kernel opaque structures
ms.assetid: 4053d82e-78ae-4945-ad5b-44ba41229a5d
---

# Windows kernel opaque structures


The following table contains Windows kernel opaque structures:

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Opaque Structure</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>EPROCESS</strong></td>
<td><p>The <strong>EPROCESS</strong> structure is an opaque structure that serves as the process object for a process.</p>
<p>Some routines, such as [<strong>PsGetProcessCreateTimeQuadPart</strong>](https://msdn.microsoft.com/library/windows/hardware/ff559939), use <strong>EPROCESS</strong> to identify the process to operate on. Drivers can use the [<strong>PsGetCurrentProcess</strong>](https://msdn.microsoft.com/library/windows/hardware/ff559933) routine to obtain a pointer to the process object for the current process and can use the [<strong>ObReferenceObjectByHandle</strong>](https://msdn.microsoft.com/library/windows/hardware/ff558679) routine to obtain a pointer to the process object that is associated with the specified handle. The [<strong>PsInitialSystemProcess</strong>](https://msdn.microsoft.com/library/windows/hardware/ff559943) global variable points to the process object for the system process.</p>
<p>Note that a process object is an Object Manager object. Drivers should use Object Manager routines such as [<strong>ObReferenceObject</strong>](https://msdn.microsoft.com/library/windows/hardware/ff558678) and [<strong>ObDereferenceObject</strong>](https://msdn.microsoft.com/library/windows/hardware/ff557724) to maintain the object's reference count.</p>
<p>Header: Wdm.h. Include: Wdm.h, Ntddk.h, Ntifs.h.</p></td>
</tr>
<tr class="even">
<td><strong>ETHREAD</strong></td>
<td><p>The <strong>ETHREAD</strong> structure is an opaque structure that serves as the thread object for a thread.</p>
<p>Some routines, such as [<strong>PsIsSystemThread</strong>](https://msdn.microsoft.com/library/windows/hardware/ff559945), use <strong>ETHREAD</strong> to identify the thread to operate on. Drivers can use the [<strong>PsGetCurrentThread</strong>](https://msdn.microsoft.com/library/windows/hardware/ff559936) routine to obtain a pointer to the thread object for the current thread and can use the [<strong>ObReferenceObjectByHandle</strong>](https://msdn.microsoft.com/library/windows/hardware/ff558679) routine to obtain a pointer to the thread object that is associated with the specified handle.</p>
<p>Note that a thread object is an Object Manager object. Drivers should use Object Manager routines such as [<strong>ObReferenceObject</strong>](https://msdn.microsoft.com/library/windows/hardware/ff558678) and [<strong>ObDereferenceObject</strong>](https://msdn.microsoft.com/library/windows/hardware/ff557724) to maintain the object's reference count.</p>
<p>Header: Wdm.h. Include: Wdm.h, Ntddk.h, Ntifs.h.</p></td>
</tr>
<tr class="odd">
<td><strong>EX_RUNDOWN_REF</strong></td>
<td><p>The <strong>EX_RUNDOWN_REF</strong> structure is an opaque system structure that contains information about the status of run-down protection for an associated shared object.</p>
<pre class="syntax"><code>typedef struct _EX_RUNDOWN_REF {
  
  ...  // opaque
  
} EX_RUNDOWN_REF, *PEX_RUNDOWN_REF;</code></pre>
<p>The run-down protection routines all take a pointer to an <strong>EX_RUNDOWN_REF</strong> structure as their first parameter. These routines are listed at the bottom of this page.</p>
<p>For more information, see [Run-Down Protection](run-down-protection.md).</p>
<p>Header: Wdm.h. Include Wdm.h.</p></td>
</tr>
<tr class="even">
<td><strong>EX_TIMER</strong></td>
<td><p>The <strong>EX_TIMER</strong> structure is an opaque structure that is used by the operating system to represent an <strong>EX_TIMER</strong> timer object.</p>
<pre class="syntax"><code>typedef struct _EX_TIMER *PEX_TIMER;</code></pre>
<p>All members of this structure are opaque to drivers.</p>
<p>The following <strong>Ex<em>Xxx</em>Timer</strong> routines require a pointer to a system-allocated <strong>EX_TIMER</strong> structure as an input parameter:</p>
<ul>
<li>[<strong>ExSetTimer</strong>](https://msdn.microsoft.com/library/windows/hardware/dn265188)</li>
<li>[<strong>ExCancelTimer</strong>](https://msdn.microsoft.com/library/windows/hardware/dn265180)</li>
<li>[<strong>ExDeleteTimer</strong>](https://msdn.microsoft.com/library/windows/hardware/dn265181)</li>
</ul>
<p><strong>EX_TIMER</strong>-based timer objects are created by the operating system. To get such a timer object, your driver calls the [<strong>ExAllocateTimer</strong>](https://msdn.microsoft.com/library/windows/hardware/dn265179) routine. When this object is no longer needed, the driver is responsible for deleting the object by calling <strong>ExDeleteTimer</strong>.</p>
<p>For more information, see [Ex<em>Xxx</em>Timer Routines and EX_TIMER Objects](exxxxtimer-routines-and-ex-timer-objects.md).</p>
<p>Header: Wdm.h. Include: Wdm.h, Ntddk.h, Ntifs.h.</p></td>
</tr>
<tr class="odd">
<td><strong>FAST_MUTEX</strong></td>
<td><p>A <strong>FAST_MUTEX</strong> structure is an opaque data structure that represents a fast mutex.</p>
<p>A <strong>FAST_MUTEX</strong> structure is initialized by the [<strong>ExInitializeFastMutex</strong>](https://msdn.microsoft.com/library/windows/hardware/ff545293) routine.</p>
<p>For more information about fast mutexes, see [Fast Mutexes and Guarded Mutexes](fast-mutexes-and-guarded-mutexes.md).</p>
<p>Header: Wdm.h. Include: Wdm.h, Ntddk.h, Ntifs.h.</p></td>
</tr>
<tr class="even">
<td><strong>IO_CSQ</strong></td>
<td><p>The <strong>IO_CSQ</strong> structure is an opaque structure used to specify the driver's cancel-safe IRP queue routines. Do not set the members of this structure directly. Use [<strong>IoCsqInitialize</strong>](https://msdn.microsoft.com/library/windows/hardware/ff549054) or [<strong>IoCsqInitializeEx</strong>](https://msdn.microsoft.com/library/windows/hardware/ff549060) to initialize this structure.</p>
<p>For an overview of how to use cancel-safe IRP queues, see [Cancel-Safe IRP Queues](cancel-safe-irp-queues.md).</p>
<p>Available on Microsoft Windows XP and later versions of the Windows operating system.</p>
<p>Header: Wdm.h. Include: Wdm.h, Ntddk.h, Ntifs.h.</p></td>
</tr>
<tr class="odd">
<td><strong>IO_CSQ_IRP_CONTEXT</strong></td>
<td><p>The <strong>IO_CSQ_IRP_CONTEXT</strong> structure is an opaque data structure used to specify the IRP context for an IRP in the driver's cancel-safe IRP queue. It is used as a key by the [<strong>IoCsqInsertIrp</strong>](https://msdn.microsoft.com/library/windows/hardware/ff549066), [<strong>IoCsqInsertIrpEx</strong>](https://msdn.microsoft.com/library/windows/hardware/ff549067), and [<strong>IoCsqRemoveIrp</strong>](https://msdn.microsoft.com/library/windows/hardware/ff549070) routines to identify particular IRPs in the queue.</p>
<p>For an overview of how to use cancel-safe IRP queues, see [Cancel-Safe IRP Queues](cancel-safe-irp-queues.md).</p>
<p>Available on Microsoft Windows XP and later versions of the Windows operating system.</p>
<p>Header: Wdm.h. Include: Wdm.h, Ntddk.h, Ntifs.h.</p></td>
</tr>
<tr class="even">
<td><strong>IO_WORKITEM</strong></td>
<td><p>The <strong>IO_WORKITEM</strong> structure is an opaque structure that describes a work item for a system worker thread.</p>
<p>A driver can allocate a work item by calling [<strong>IoAllocateWorkItem</strong>](https://msdn.microsoft.com/library/windows/hardware/ff548276). Alternatively, a driver can allocate its own buffer, and then call [<strong>IoInitializeWorkItem</strong>](https://msdn.microsoft.com/library/windows/hardware/ff549349) to initialize that buffer as a work item.</p>
<p>Any work item that is allocated by <strong>IoAllocateWorkItem</strong> must be freed by [<strong>IoFreeWorkItem</strong>](https://msdn.microsoft.com/library/windows/hardware/ff549133). Any memory that is initialized by <strong>IoInitializeWorkItem</strong> must be uninitialized by [<strong>IoUninitializeWorkItem</strong>](https://msdn.microsoft.com/library/windows/hardware/ff550392) before it can be freed.</p>
<p>For more information about work items, see [System Worker Threads](system-worker-threads.md).</p>
<p>Header: Wdm.h. Include: Wdm.h, Ntddk.h, Ntifs.h.</p></td>
</tr>
<tr class="odd">
<td><strong>KBUGCHECK_CALLBACK_RECORD</strong></td>
<td><p>The <strong>KBUGCHECK_CALLBACK_RECORD</strong> structure is an opaque structure that is used by the [<strong>KeRegisterBugCheckCallback</strong>](https://msdn.microsoft.com/library/windows/hardware/ff553105) and [<strong>KeDeregisterBugCheckCallback</strong>](https://msdn.microsoft.com/library/windows/hardware/ff551992) routines.</p>
<p>The <strong>KBUGCHECK_CALLBACK_RECORD</strong> structure is used for bookkeeping by the [<strong>KeRegisterBugCheckReasonCallback</strong>](https://msdn.microsoft.com/library/windows/hardware/ff553110) and [<strong>KeDeregisterBugCheckReasonCallback</strong>](https://msdn.microsoft.com/library/windows/hardware/ff552003) routines.</p>
<p>The structure must be allocated in resident memory, such as nonpaged pool. Use the [<strong>KeInitializeCallbackRecord</strong>](https://msdn.microsoft.com/library/windows/hardware/ff552109) routine to initialize the structure before using it.</p>
<p>Header: Ntddk.h. Include: Ntddk.h.</p></td>
</tr>
<tr class="even">
<td><strong>KBUGCHECK_REASON_CALLBACK_RECORD</strong></td>
<td><p>The <strong>KBUGCHECK_REASON_CALLBACK_RECORD</strong> structure is an opaque structure that is used by the [<strong>KeRegisterBugCheckReasonCallback</strong>](https://msdn.microsoft.com/library/windows/hardware/ff553110) and [<strong>KeDeregisterBugCheckReasonCallback</strong>](https://msdn.microsoft.com/library/windows/hardware/ff552003) routines.</p>
<p>The <strong>KBUGCHECK_REASON_CALLBACK_RECORD</strong> structure is used for bookkeeping by the [<strong>KeRegisterBugCheckReasonCallback</strong>](https://msdn.microsoft.com/library/windows/hardware/ff553110) and [<strong>KeDeregisterBugCheckReasonCallback</strong>](https://msdn.microsoft.com/library/windows/hardware/ff552003) routines.</p>
<p>The structure must be allocated in resident memory, such as nonpaged pool. Use the [<strong>KeInitializeCallbackRecord</strong>](https://msdn.microsoft.com/library/windows/hardware/ff552109) routine to initialize the structure before using it.</p>
<p>Available on Microsoft Windows XP with Service Pack 1 (SP1), Windows Server 2003, and later versions of the Windows operating system.</p>
<p>Header: Ntddk.h. Include: Ntddk.h.</p></td>
</tr>
<tr class="odd">
<td><strong>KDPC</strong></td>
<td><p>The <strong>KDPC</strong> structure is an opaque structure that represents a DPC object. Do not set the members of this structure directly. See [DPC Objects and DPCs](dpc-objects-and-dpcs.md).</p>
<p>Header: Wdm.h. Include: Wdm.h, Ntddk.h, Ntifs.h.</p></td>
</tr>
<tr class="even">
<td><strong>KFLOATING_SAVE</strong></td>
<td><p>The <strong>KFLOATING_SAVE</strong> structure is an opaque structure that describes the floating-point state that the [<strong>KeSaveFloatingPointState</strong>](https://msdn.microsoft.com/library/windows/hardware/ff553243) routine saved.</p>
<p>Use [<strong>KeRestoreFloatingPointState</strong>](https://msdn.microsoft.com/library/windows/hardware/ff553185) to restore the floating-point state.</p>
<p>Header: Wdm.h. Include: Wdm.h, Ntddk.h, Ntifs.h.</p></td>
</tr>
<tr class="odd">
<td><strong>KGUARDED_MUTEX</strong></td>
<td><p>The <strong>KGUARDED_MUTEX</strong> structure is an opaque structure that represents a guarded mutex.</p>
<p>Use <strong>KeInitializeGuardedMutex</strong> to initialize a <strong>KGUARDED_MUTEX</strong> structure as a guarded mutex.</p>
<p>Guarded mutexes must be allocated from non-paged pool.</p>
<p>For more information about guarded mutexes, see [Fast Mutexes and Guarded Mutexes](fast-mutexes-and-guarded-mutexes.md).</p>
<p>Header: Wdm.h. Include: Wdm.h, Ntddk.h, Ntifs.h.</p></td>
</tr>
<tr class="even">
<td><strong>KINTERRUPT</strong></td>
<td><p>A <strong>KINTERRUPT</strong> structure is an opaque structure that represents an interrupt to the system.</p>
<p>[<strong>IoConnectInterruptEx</strong>](https://msdn.microsoft.com/library/windows/hardware/ff548378) provides a pointer to the <strong>KINTERRUPT</strong> structure for the interrupt when the driver registers an [<em>InterruptService</em>](https://msdn.microsoft.com/library/windows/hardware/ff547958) or [<em>InterruptMessageService</em>](https://msdn.microsoft.com/library/windows/hardware/ff547940) routine. The driver uses this pointer when acquiring or releasing the interrupt spin lock for the interrupt. The driver also uses this pointer when unregistering an <em>InterruptService</em> routine.</p>
<p>Header: Wdm.h. Include: Wdm.h, Ntddk.h, Ntifs.h.</p></td>
</tr>
<tr class="odd">
<td><strong>KLOCK_QUEUE_HANDLE</strong></td>
<td><p>The <strong>KLOCK_QUEUE_HANDLE</strong> structure is an opaque structure that describes a queued spin lock. The driver allocates the <strong>KLOCK_QUEUE_HANDLE</strong> structure, and passes it to [<strong>KeAcquireInStackQueuedSpinLock</strong>](https://msdn.microsoft.com/library/windows/hardware/ff551899) and [<strong>KeAcquireInStackQueuedSpinLockAtDpcLevel</strong>](https://msdn.microsoft.com/library/windows/hardware/ff551908) to acquire the queued spin lock. Those routines initialize the structure to represent the queued spin lock. The driver passes the structure to [<strong>KeReleaseInStackQueuedSpinLock</strong>](https://msdn.microsoft.com/library/windows/hardware/ff553130) and [<strong>KeReleaseInStackQueuedSpinLockFromDpcLevel</strong>](https://msdn.microsoft.com/library/windows/hardware/ff553137) when releasing the spin lock.</p>
<p>For more information, see [Queued Spin Locks](queued-spin-locks.md).</p>
<p>Header: Wdm.h. Include: Wdm.h, Ntddk.h, Ntifs.h.</p></td>
</tr>
<tr class="even">
<td><strong>KTIMER</strong></td>
<td><p>The <strong>KTIMER</strong> structure is an opaque structure that represents a timer object. Do not set the members of this structure directly. For more information, see [Timer Objects and DPCs](timer-objects-and-dpcs.md).</p>
<p>Header: Wdm.h. Include: Wdm.h, Ntddk.h, Ntifs.h.</p></td>
</tr>
<tr class="odd">
<td><strong>LOOKASIDE_LIST_EX</strong></td>
<td><p>The <strong>LOOKASIDE_LIST_EX</strong> structure describes a lookaside list.</p>
<pre class="syntax"><code>typedef struct _LOOKASIDE_LIST_EX {
  ...  // opaque
} LOOKASIDE_LIST_EX, *PLOOKASIDE_LIST_EX;</code></pre>
<p>A lookaside list is a pool of fixed-size buffers that the driver can manage locally to reduce the number of calls to system allocation routines and, thereby, to improve performance. The buffers are of uniform size and are stored as entries in the lookaside list.</p>
<p>Drivers should treat the <strong>LOOKASIDE_LIST_EX</strong> structure as opaque. Drivers that access structure members or that have dependencies on the locations of these members might not remain portable and interoperable with other drivers.</p>
<p>The following See Also section contains a list of the routines that use this structure.</p>
<p>For more information about lookaside lists, see [Using Lookaside Lists](using-lookaside-lists.md).</p>
<p>On 64-bit platforms, this structure must be 16-byte aligned.</p>
<p>Supported starting with Windows Vista.</p>
<p>Header: Wdm.h. Include: Wdm.h, Ntddk.h, Ntifs.h.</p></td>
</tr>
<tr class="even">
<td><strong>NPAGED_LOOKASIDE_LIST</strong></td>
<td><p>The <strong>NPAGED_LOOKASIDE_LIST</strong> structure is an opaque structure that describes a lookaside list of fixed-size buffers allocated from nonpaged pool. The system creates new entries and destroys unused entries on the list as necessary. For fixed-size buffers, using a lookaside list is quicker than allocating memory directly.</p>
<p>Use [<strong>ExInitializeNPagedLookasideList</strong>](https://msdn.microsoft.com/library/windows/hardware/ff545301) to initialize the lookaside list. Use [<strong>ExAllocateFromNPagedLookasideList</strong>](https://msdn.microsoft.com/library/windows/hardware/ff544388) to allocate a buffer from the list, and [<strong>ExFreeToNPagedLookasideList</strong>](https://msdn.microsoft.com/library/windows/hardware/ff544601) to return a buffer to the list.</p>
<p>Drivers must always explicitly free any lookaside lists they create before unloading. It is a serious programming error to do otherwise. Use [<strong>ExDeleteNPagedLookasideList</strong>](https://msdn.microsoft.com/library/windows/hardware/ff544566) to free the list.</p>
<p>Drivers can also use lookaside lists for paged pool. Starting with Windows 2000, a <strong>PAGED_LOOKASIDE_LIST</strong> structure describes a lookaside list that contains paged buffers. Starting with Windows Vista, a <strong>LOOKASIDE_LIST_EX</strong> structure can describe a lookaside list that contains either paged or nonpaged buffers. For more information, see [Using Lookaside Lists](using-lookaside-lists.md).</p>
<p>On 64-bit platforms, this structure must be 16-byte aligned.</p>
<p>Supported starting with Windows 2000.</p>
<p>Header: Wdm.h. Include: Wdm.h, Ntddk.h, Ntifs.h.</p></td>
</tr>
<tr class="odd">
<td><strong>OBJECT_TYPE</strong></td>
<td><p><strong>OBJECT_TYPE</strong> is an opaque structure that specifies the object type of a handle. For more information, see [<strong>ObReferenceObjectByHandle</strong>](https://msdn.microsoft.com/library/windows/hardware/ff558679).</p>
<p>Header: Wdm.h. Include: Wdm.h, Ntddk.h, Ntifs.h.</p></td>
</tr>
<tr class="even">
<td><strong>PAGED_LOOKASIDE_LIST</strong></td>
<td><p>The <strong>PAGED_LOOKASIDE_LIST</strong> structure is an opaque structure that describes a lookaside list of fixed-size buffers allocated from paged pool. The system creates new entries and destroys unused entries on the list as necessary. For fixed-size buffers, using a lookaside list is quicker than allocating memory directly.</p>
<p>Use [<strong>ExInitializePagedLookasideList</strong>](https://msdn.microsoft.com/library/windows/hardware/ff545309) to initialize the lookaside list. Use [<strong>ExAllocateFromPagedLookasideList</strong>](https://msdn.microsoft.com/library/windows/hardware/ff544393) to allocate a buffer from the list, and [<strong>ExFreeToPagedLookasideList</strong>](https://msdn.microsoft.com/library/windows/hardware/ff544605) to return a buffer to the list.</p>
<p>Drivers must always explicitly free any lookaside lists they create before unloading. It is a serious programming error to do otherwise. Use [<strong>ExDeletePagedLookasideList</strong>](https://msdn.microsoft.com/library/windows/hardware/ff544570) to free the list.</p>
<p>Drivers can also use lookaside lists for nonpaged pool. Starting with Windows 2000, an <strong>NPAGED_LOOKASIDE_LIST</strong> structure describes a lookaside list that contains nonpaged buffers. Starting with Windows Vista, a <strong>LOOKASIDE_LIST_EX</strong> structure can describe a lookaside list that contains either paged or nonpaged buffers. For more information, see [Using Lookaside Lists](using-lookaside-lists.md).</p>
<p>On 64-bit platforms, this structure must be 16-byte aligned.</p>
<p>Supported starting with Windows 2000.</p>
<p>Header: Wdm.h. Include: Wdm.h, Ntddk.h, Ntifs.h.</p></td>
</tr>
<tr class="odd">
<td><strong>RTL_BITMAP</strong></td>
<td><p>The <strong>RTL_BITMAP</strong> structure is an opaque structure that describes a bitmap.</p>
<pre class="syntax"><code>typedef struct _RTL_BITMAP {
  // opaque
} RTL_BITMAP, *PRTL_BITMAP;</code></pre>
<p>Do not directly access the members of this structure. Drivers that have dependencies on member locations or that access member values directly might not remain compatible with future versions of the Windows operating system.</p>
<p>The <strong>RTL_BITMAP</strong> structure serves as a header for a general-purpose, one-dimensional bitmap of arbitrary length. A driver can use such a bitmap as an economical way to keep track of a set of reusable items. For example, a file system can use bitmaps to track which clusters and sectors on a hard disk have already been allocated to hold file data.</p>
<p>For a list of the <strong>Rtl<em>Xxx</em></strong> routines that use <strong>RTL_BITMAP</strong> structures, see the following See Also section. The caller of these <strong>Rtl<em>Xxx</em></strong> routines is responsible for allocating the storage for the <strong>RTL_BITMAP</strong> structure and for the buffer that contains the bitmap. This buffer must begin on a four-byte boundary in memory and must be a multiple of four bytes in length. The bitmap begins at the start of the buffer but can contain any number of bits that will fit in the allocated buffer.</p>
<p>Before supplying an <strong>RTL_BITMAP</strong> structure as a parameter to an <strong>Rtl<em>Xxx</em></strong> routine, call the [<strong>RtlInitializeBitMap</strong>](https://msdn.microsoft.com/library/windows/hardware/ff561925) routine to initialize the structure. The input parameters to this routine are a pointer to a buffer that contains the bitmap, and the size, in bits, of the bitmap. <strong>RtlInitializeBitMap</strong> does not change the contents of this buffer.</p>
<p>If the caller allocates the storage for the <strong>RTL_BITMAP</strong> structure and bitmap in paged memory, the caller must be running at IRQL &lt;= APC_LEVEL when it passes a pointer to this structure as a parameter to any of the <strong>Rtl<em>Xxx</em></strong> routines that are listed in the See Also section. If the caller allocates the storage from nonpaged memory (or, equivalently, from paged memory that is locked), the caller can be running at any IRQL when it calls the <strong>Rtl<em>Xxx</em></strong> routine.</p>
<p>Supported in Windows 2000 and later versions of Windows.</p>
<p>Header: Wdm.h. Include: Wdm.h, Ntddk.h, Ntifs.h.</p></td>
</tr>
<tr class="even">
<td><strong>RTL_RUN_ONCE</strong></td>
<td><p>The <strong>RTL_RUN_ONCE</strong> structure is an opaque structure that stores the information for a one-time initialization.</p>
<p>Drivers must initialize this structure by calling the [<strong>RtlRunOnceInitialize</strong>](https://msdn.microsoft.com/library/windows/hardware/ff562767) routine before passing it to any other <strong>RtlRunOnce<em>Xxx</em></strong> routines.</p>
<p>Available only on Windows Vista and later versions of the Windows operating system.</p>
<p>Header: Ntddk.h. Include: Ntddk.h.</p></td>
</tr>
<tr class="odd">
<td><strong>SECURITY_SUBJECT_CONTEXT</strong></td>
<td><p>The <strong>SECURITY_SUBJECT_CONTEXT</strong> structure is an opaque structure that represents the security context within which a particular operation is taking place.</p>
<p>Header: Wdm.h. Include: Wdm.h, Ntddk.h, Ntifs.h.</p></td>
</tr>
<tr class="even">
<td><strong>SLIST_HEADER</strong></td>
<td><p>An <strong>SLIST_HEADER</strong> structure is an opaque structure that serves as the header for a sequenced singly linked list. For more information, see [Singly and Doubly Linked Lists](singly-and-doubly-linked-lists.md).</p>
<p>On 64-bit platforms, <strong>SLIST_HEADER</strong> structures must be 16-byte aligned.</p>
<p>Header: Wdm.h. Include: Wdm.h, Ntddk.h, Ntifs.h.</p></td>
</tr>
<tr class="odd">
<td><strong>XSTATE_SAVE</strong></td>
<td><p>The <strong>XSTATE_SAVE</strong> structure is an opaque structure that describes the extended processor state information that a kernel-mode driver saves and restores.</p>
<pre class="syntax"><code>typedef struct _XSTATE_SAVE {
  ...  // opaque
} XSTATE_SAVE, *PXSTATE_SAVE;</code></pre>
<p>All members are opaque.</p>
<p>This structure is used by the [<strong>KeSaveExtendedProcessorState</strong>](https://msdn.microsoft.com/library/windows/hardware/ff553238) and [<strong>KeRestoreExtendedProcessorState</strong>](https://msdn.microsoft.com/library/windows/hardware/ff553182) routines.</p>
<p>Supported in Windows 7 and later versions of the Windows operating system.</p>
<p>Header: Wdm.h. Include: Wdm.h, Ntddk.h, Ntifs.h.</p></td>
</tr>
</tbody>
</table>

 

## Related topics
[**BugCheckDumpIoCallback**](https://msdn.microsoft.com/library/windows/hardware/ff540677)  
[**BugCheckSecondaryDumpDataCallback**](https://msdn.microsoft.com/library/windows/hardware/ff540679)  
[**ExAcquireFastMutex**](https://msdn.microsoft.com/library/windows/hardware/ff544337)  
[**ExAcquireFastMutexUnsafe**](https://msdn.microsoft.com/library/windows/hardware/ff544340)  
[**ExAllocateFromLookasideListEx**](https://msdn.microsoft.com/library/windows/hardware/ff544381)  
[**ExAllocateFromNPagedLookasideList**](https://msdn.microsoft.com/library/windows/hardware/ff544388)  
[**ExAllocateFromPagedLookasideList**](https://msdn.microsoft.com/library/windows/hardware/ff544393)  
[**ExAllocateTimer**](https://msdn.microsoft.com/library/windows/hardware/dn265179)  
[**ExDeletePagedLookasideList**](https://msdn.microsoft.com/library/windows/hardware/ff544570)  
[**ExFreeToPagedLookasideList**](https://msdn.microsoft.com/library/windows/hardware/ff544605)  
[**ExInitializePagedLookasideList**](https://msdn.microsoft.com/library/windows/hardware/ff545309)  
[**ExCancelTimer**](https://msdn.microsoft.com/library/windows/hardware/dn265180)  
[**ExDeleteLookasideListEx**](https://msdn.microsoft.com/library/windows/hardware/ff544563)  
[**ExDeleteNPagedLookasideList**](https://msdn.microsoft.com/library/windows/hardware/ff544566)  
[**ExDeleteTimer**](https://msdn.microsoft.com/library/windows/hardware/dn265181)  
[**ExFlushLookasideListEx**](https://msdn.microsoft.com/library/windows/hardware/ff544587)  
[**ExFreeToLookasideListEx**](https://msdn.microsoft.com/library/windows/hardware/ff544597)  
[**ExFreeToNPagedLookasideList**](https://msdn.microsoft.com/library/windows/hardware/ff544601)  
[**ExInitializeLookasideListEx**](https://msdn.microsoft.com/library/windows/hardware/ff545298)  
[**ExInitializeNPagedLookasideList**](https://msdn.microsoft.com/library/windows/hardware/ff545301)  
[**ExInitializeSListHead**](https://msdn.microsoft.com/library/windows/hardware/ff545321)  
[**ExInterlockedFlushSList**](https://msdn.microsoft.com/library/windows/hardware/ff545379)  
[**ExInterlockedPopEntrySList**](https://msdn.microsoft.com/library/windows/hardware/ff545414)  
[**ExInterlockedPushEntrySList**](https://msdn.microsoft.com/library/windows/hardware/ff545422)  
[**ExQueryDepthSList**](https://msdn.microsoft.com/library/windows/hardware/ff545502)  
[**ExReleaseFastMutex**](https://msdn.microsoft.com/library/windows/hardware/ff545549)  
[**ExReleaseFastMutexUnsafe**](https://msdn.microsoft.com/library/windows/hardware/ff545567)  
[**ExSetTimer**](https://msdn.microsoft.com/library/windows/hardware/dn265188)  
[**ExTryToAcquireFastMutex**](https://msdn.microsoft.com/library/windows/hardware/ff545647)  
[*ExTimerCallback*](https://msdn.microsoft.com/library/windows/hardware/dn265190)  
[**IoAllocateWorkItem**](https://msdn.microsoft.com/library/windows/hardware/ff548276)  
[**IoConnectInterruptEx**](https://msdn.microsoft.com/library/windows/hardware/ff548378)  
[**IoCsqInitialize**](https://msdn.microsoft.com/library/windows/hardware/ff549054)  
[**IoCsqInitializeEx**](https://msdn.microsoft.com/library/windows/hardware/ff549060)  
[**IoCsqInsertIrp**](https://msdn.microsoft.com/library/windows/hardware/ff549066)  
[**IoCsqInsertIrpEx**](https://msdn.microsoft.com/library/windows/hardware/ff549067)  
[**IoCsqRemoveIrp**](https://msdn.microsoft.com/library/windows/hardware/ff549070)  
[**IoDisconnectInterruptEx**](https://msdn.microsoft.com/library/windows/hardware/ff549093)  
[**IoFreeWorkItem**](https://msdn.microsoft.com/library/windows/hardware/ff549133)  
[**IoInitializeWorkItem**](https://msdn.microsoft.com/library/windows/hardware/ff549349)  
[**IoRequestDpc**](https://msdn.microsoft.com/library/windows/hardware/ff549657)  
[**IoUninitializeWorkItem**](https://msdn.microsoft.com/library/windows/hardware/ff550392)  
[**KeAcquireGuardedMutex**](https://msdn.microsoft.com/library/windows/hardware/ff551892)  
[**KeAcquireGuardedMutexUnsafe**](https://msdn.microsoft.com/library/windows/hardware/ff551894)  
[**KeAcquireInStackQueuedSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff551899)  
[**KeAcquireInStackQueuedSpinLockAtDpcLevel**](https://msdn.microsoft.com/library/windows/hardware/ff551908)  
[**KeAcquireInterruptSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff551914)  
[**KeCancelTimer**](https://msdn.microsoft.com/library/windows/hardware/ff551970)  
[**KeInitializeCallbackRecord**](https://msdn.microsoft.com/library/windows/hardware/ff552109)  
[**KeInitializeGuardedMutex**](https://msdn.microsoft.com/library/windows/hardware/ff552144)  
[**KeInitializeTimer**](https://msdn.microsoft.com/library/windows/hardware/ff552168)  
[**KeInitializeTimerEx**](https://msdn.microsoft.com/library/windows/hardware/ff552173)  
[**KeReadStateTimer**](https://msdn.microsoft.com/library/windows/hardware/ff553099)  
[**KeRestoreExtendedProcessorState**](https://msdn.microsoft.com/library/windows/hardware/ff553182)  
[**KeSaveExtendedProcessorState**](https://msdn.microsoft.com/library/windows/hardware/ff553238)  
[**KeSetTimer**](https://msdn.microsoft.com/library/windows/hardware/ff553286)  
[**KeSetTimerEx**](https://msdn.microsoft.com/library/windows/hardware/ff553292)  
[**KeDeregisterBugCheckCallback**](https://msdn.microsoft.com/library/windows/hardware/ff551992)  
[**KeDeregisterBugCheckReasonCallback**](https://msdn.microsoft.com/library/windows/hardware/ff552003)  
[**KeInsertQueueDpc**](https://msdn.microsoft.com/library/windows/hardware/ff552185)  
[**KeRegisterBugCheckCallback**](https://msdn.microsoft.com/library/windows/hardware/ff553105)  
[**KeRegisterBugCheckReasonCallback**](https://msdn.microsoft.com/library/windows/hardware/ff553110)  
[**KeReleaseGuardedMutexUnsafe**](https://msdn.microsoft.com/library/windows/hardware/ff553125)  
[**KeReleaseInStackQueuedSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff553130)  
[**KeReleaseInStackQueuedSpinLockFromDpcLevel**](https://msdn.microsoft.com/library/windows/hardware/ff553137)  
[**KeReleaseInterruptSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff553139)  
[**KeRestoreFloatingPointState**](https://msdn.microsoft.com/library/windows/hardware/ff553185)  
[**KeSaveFloatingPointState**](https://msdn.microsoft.com/library/windows/hardware/ff553243)  
[**KeSynchronizeExecution**](https://msdn.microsoft.com/library/windows/hardware/ff553302)  
[*LookasideListAllocateEx*](https://msdn.microsoft.com/library/windows/hardware/ff554322)  
[*LookasideListFreeEx*](https://msdn.microsoft.com/library/windows/hardware/ff554324)  
[**ObReferenceObjectByHandle**](https://msdn.microsoft.com/library/windows/hardware/ff558679)  
[**PsGetCurrentProcess**](https://msdn.microsoft.com/library/windows/hardware/ff559933)  
[**PsGetProcessCreateTimeQuadPart**](https://msdn.microsoft.com/library/windows/hardware/ff559939)  
[**PsInitialSystemProcess**](https://msdn.microsoft.com/library/windows/hardware/ff559943)  
[**PsIsSystemThread**](https://msdn.microsoft.com/library/windows/hardware/ff559945)  
[**RtlRunOnceBeginInitialize**](https://msdn.microsoft.com/library/windows/hardware/ff562759)  
[**RtlRunOnceComplete**](https://msdn.microsoft.com/library/windows/hardware/ff562763)  
[**RtlRunOnceExecuteOnce**](https://msdn.microsoft.com/library/windows/hardware/ff562765)  
[**RtlRunOnceInitialize**](https://msdn.microsoft.com/library/windows/hardware/ff562767)  
[*RunOnceInitialization*](https://msdn.microsoft.com/library/windows/hardware/ff563635)  
[Run-Down Protection](run-down-protection.md)  
[**SeAccessCheck**](https://msdn.microsoft.com/library/windows/hardware/ff563674)  
[**SeAssignSecurity**](https://msdn.microsoft.com/library/windows/hardware/ff563676)  
[**SeAssignSecurityEx**](https://msdn.microsoft.com/library/windows/hardware/ff563679)  

--------------------
[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bkernel\kernel%5D:%20Windows%20kernel%20opaque%20structures%20%20RELEASE:%20%286/14/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")


