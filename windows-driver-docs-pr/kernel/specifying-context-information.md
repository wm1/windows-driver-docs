---
title: Specifying Context Information
author: windows-driver-content
description: Specifying Context Information
ms.assetid: 7133529f-5a6c-4df1-8d03-1c79c0d98fa9
keywords: ["filtering registry calls WDK kernel , context information", "registry filtering drivers WDK kernel , context information", "context information", "context information WDK filter registry call"]
ms.author: windowsdriverdev
ms.date: 06/16/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

# Specifying Context Information


The configuration manager provides several ways for registry filtering drivers to assign context information to registry operations. A registry filtering driver can:

-   Assign context information to the [*RegistryCallback*](https://msdn.microsoft.com/library/windows/hardware/ff560903) routine.

    When your driver calls [**CmRegisterCallback**](https://msdn.microsoft.com/library/windows/hardware/ff541918) or [**CmRegisterCallbackEx**](https://msdn.microsoft.com/library/windows/hardware/ff541921) to register for notification of a registry operation, the driver can specify a driver-defined context value. The configuration manager passes this context value to the driver's *RegistryCallback* routine each time that the configuration manager calls the routine.

    This context information is supported starting with Windows XP.

-   Assign context information to a registry operation.

    Drivers can store operation-specific context information in the **CallContext** member of each **REG\_*XXX*\_KEY\_INFORMATION** structure that the driver's *RegistryCallback* routine receives. If your driver receives both a pre-notification and a post-notification for a registry operation, the [**REG\_POST\_OPERATION\_INFORMATION**](https://msdn.microsoft.com/library/windows/hardware/ff560971) structure contains a pointer to the appropriate pre-notification structure. When a *RegistryCallback* routine receives a **REG\_POST\_OPERATION\_INFORMATION** structure, the **CallContext** member of that structure matches the **CallContext** member of the pre-notification structure.

    The **CallContext** member of these structures is available starting with Windows Vista.

-   Assign context information to a registry key object.

    A [*RegistryCallback*](https://msdn.microsoft.com/library/windows/hardware/ff560903) routine can assign context information to a particular registry key object. If the *RegistryCallback* routine calls [**CmSetCallbackObjectContext**](https://msdn.microsoft.com/library/windows/hardware/ff541924) to assign context information to a key object, subsequent pre-notifications and post-notifications for all operations on the object will include the context value in the **ObjectContext** member of each **REG\_*XXX*\_KEY\_INFORMATION** structure. If a driver provides multiple *RegistryCallback* routines, the driver can assign different context information for each routine, for a single registry key object.

    If a driver has called **CmSetCallbackObjectContext**, the driver's *RegistryCallback* routine will receive a **RegNtCallbackObjectContextCleanup** notification after the key object's handle has been closed. In response to this notification, the routine should release any resources that it allocated for the object's context. When the *Argument1* parameter to the *RegistryCallback* routine is **RegNtCallbackObjectContextCleanup**, the *Argument2* parameter is a pointer to a [**REG\_CALLBACK\_CONTEXT\_CLEANUP\_INFORMATION**](https://msdn.microsoft.com/library/windows/hardware/ff560919) structure that contains a pointer to the context.

    The **CmSetCallbackObjectContext** routine and **RegNtCallbackObjectContextCleanup** notification are available starting with Windows Vista.

 

 


--------------------
[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bkernel\kernel%5D:%20Specifying%20Context%20Information%20%20RELEASE:%20%286/14/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")


