---
title: Requesting Special Pool by Pool Tag
description: Requesting Special Pool by Pool Tag
ms.assetid: 201eb8a5-b38b-4625-853d-448488214e52
---

# Requesting Special Pool by Pool Tag


## <span id="ddk_requesting_special_pool_for_allocations_with_a_specified_pool_tag_"></span><span id="DDK_REQUESTING_SPECIAL_POOL_FOR_ALLOCATIONS_WITH_A_SPECIFIED_POOL_TAG_"></span>


You can request special pool for all allocations that use a specified pool tag. Only one pool tag on the system can be associated with kernel special pool requests at one time.

In Windows Vista and later versions of Windows, you can also use the command line to request special pool by pool tag. For information, see [**GFlags Commands**](gflags-commands.md).

**To request special pool by pool tag**

1.  Select the **System Registry** tab or the **Kernel Flags** tab.

    On Windows Vista and later versions of Windows, this option is available on both tabs. On earlier versions of Windows, it is available only on the **System Registry** tab.

2.  In the **Kernel Special Pool Tag** section, click **Text**, and then type a four-character pattern for the tag.

    The tag can include the **?** (single character) and **\*** (multiple characters) wildcard characters. For example, Fat\* or Av?4.

3.  The following screen shot shows a tag entered as text on the System Registry tab.

    ![screen shot of a tag entered as text on the system registry tab](images/gflags-specialpool-text.png)

4.  Click **Apply**.

    When you click **Apply**, GFlags changes the selection from **Text** to **Hex** and displays the ASCII characters as hexadecimal values in reverse (lower endian) order. For example, if you type **Tag1**, GFlags displays the tag as **0x31676154** (1gaT). This is the way that it is stored in the registry and displayed by the debugger and other tools.

    The following illustration shows the effect of clicking **Apply**.

    ![screen shot that shows the effect of clicking apply](images/gflags-specialpool-hex.png)

### <span id="comments"></span><span id="COMMENTS"></span>Remarks

To use this feature effectively, make sure that your driver or other kernel-mode program uses a unique pool tag. If you suspect that your driver is consuming all of the special pool, consider using multiple pool tags in your code. You can then test your driver several times, assigning special pool to one pool tag in each test.

Also, select a pool tag with a hexadecimal value that is greater than the page size of the system. For kernel mode code, if you enter a pool tag that has a value less than PAGE\_SIZE, Gflags requests special pool for all allocations whose size is within the corresponding range and requests special pool for allocations with an equivalent pool tag. For example, if you select a size of **30**, special pool will be used for all allocations between 17 and 32 bytes in size, and for allocations with the pool tag 0x0030.

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[debugger\debugger]:%20Requesting%20Special%20Pool%20by%20Pool%20Tag%20%20RELEASE:%20%285/15/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")




