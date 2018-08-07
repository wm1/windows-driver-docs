---
title: HTTP Sites and UNC Shares
description: HTTP Sites and UNC Shares
ms.assetid: a1b79242-41ba-4c95-89fd-dbb7f70b24eb
---

# HTTP Sites and UNC Shares


It is possible to set up a Web site that provides version-specific source to WinDbg using SrcSrv. Such a mechanism does not provide dynamic extraction of the source files from version control, but it is a valuable feature because it allows you to set the source path of WinDbg to a single unified path that provides source from many versions of many modules, instead of having to set separate paths for each debugging scenario. This is not of interest to debugging clients that have direct access to the actual version control systems but can be of assistance to those wanting to provide secure HTTP-based access to source from remote locations. The Web sites in question can be secured through HTTPS and smart cards, if desired. This same technique can be used to provide source files through a simple UNC share.

This section includes:

[Setting Up the Web Site](setting-up-the-web-site.md)

[Extracting Source Files](extracting-source-files.md)

[Modifying the Source Indexing Streams in a .pdb File](modifying-the-source-indexing-streams-in-a--pdb-file.md)

[Using UNC Shares](using-unc-shares.md)

[Using HTTP Sites and UNC Shares in Conjuction with Regular Version Control](using-http-sites-and-unc-shares-in-conjuction-with-regular-version-con.md)

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[debugger\debugger]:%20HTTP%20Sites%20and%20UNC%20Shares%20%20RELEASE:%20%285/15/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")




