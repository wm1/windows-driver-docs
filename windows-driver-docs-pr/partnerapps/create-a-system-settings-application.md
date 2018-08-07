---
title: Create a partner settings app
description: Create a partner settings app
ms.assetid: 3b549c11-f8b2-46e8-9d22-4edc787743ee
ms.author: windowsdriverdev
ms.date: 04/20/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

# Create a partner settings app

OEMs and mobile operators can expose custom settings for hardware components that they add to a device to differentiate it from other devices, such as speakers, sensors, or microphones. Up to five of these settings appear as additional links in one of the Settings app's level two pages. 

For example, in the **Devices** tab of the **Settings** app, the following pages can have up to five additional links to custom settings apps: 
* Printers & scanners 
* Connected devices 
* Bluetooth 
* Mouse
* Touchpad
* Typing
* Pen and Windows Ink
* AutoPlay
* USB 

![Devices list in Settings app](images/devices-list-in-settings.png)

You can find a list of all level two pages in the [Launch the Windows Settings app](https://msdn.microsoft.com/en-us/windows/uwp/launch-resume/launch-settings-app) topic. It is important to note that all links must relevant to the page they are placed on.

In addition to the five links, you are able to add up to five search terms on each page. Search terms must be relevant to the content on the page. For the best experience, use specific phrases for your terms, as general and one-word terms may cause your links to not be displayed in relevant searchs. For example, if you have a “Fabricam multipen” device, create a search phrase like “set up fabricam mulitipen” instead of a generic search term such as “pen”.

## <span id="Characteristics_of_partner_settings_app"></span><span id="characteristics_of_partner_settings_app"></span><span id="CHARACTERISTICS_OF_PARTNER_SETTINGS_APP"></span>Characteristics of partner settings app


Partner settings apps have the following characteristics:

-   They are Universal Windows Platform (UWP) apps, or, in the case of Windows Phone, can also be Windows Phone Silverlight apps.

-   Users can uninstall them directly just like any other application. They can be upgraded by updating the settings application in the Store like any other Windows app.

-   They are preinstalled applications. Like any other preinstalled application, partners must submit a system settings application to Windows Dev Center in order to certify the application and obtain the signed .appx file and license file needed to include the application in a device image. They are installed at first boot.

-   They are published to a hidden location in the Store that users cannot browse to or find by using search.

## <span id="Creating_system_settings_applications"></span><span id="creating_system_settings_applications"></span><span id="CREATING_SYSTEM_SETTINGS_APPLICATIONS"></span>Creating system settings applications


Settings applications are Windows Universal apps and should therefore conform to all programming guidelines for Windows Universal apps (see [Guidelines for Universal Windows Platform (UWP) apps](https://msdn.microsoft.com/en-us/library/windows/apps/hh465424.aspx) for more information):

1.  Use the Windows Software Development Kit (SDK) to create a Windows Universal app. For more information on creating a Windows Universal app, see [Build UWP apps with Visual Studio](https://msdn.microsoft.com/en-us/library/windows/apps/xaml/dn609832.aspx). This application will be a system settings application. If you're writing a settings app targeting Windows Phone, you can also create a Windows Phone Silverlight app. 
2.  Declare the settings app capability and the SettingPageUri to describe the page that your application link is listed. Also add the AppActivationMode setting to point to the link. Do this in the application manifest: `xmlns:rescap=http://schemas.microsoft.com/appx/manifest/foundation/windows10/restrictedcapabilities`

    ```
    <Extensions>
      <rescap:Extension Category="windows.settingsApp">
        <rescap:SettingsApp SettingsPageUri="ms-settings:l2pageuri">
          <rescap:AppLinks>
            <rescap:Link AppActivationMode ="uri://yourapp#deeplink" DisplayName="Link 1 Title" />
	          <rescap:Link AppActivationMode ="uri://yourapp#deeplink" DisplayName="Link 2 Title" />
	          <rescap:SearchTerms>
	            <rescap:Term>setup foo</rescap:Term>
	            <rescap:Term>disable foo</rescap:Term>
	          </rescap:SearchTerms>
	        </rescap:AppLinks>
	      </rescap:SettingsApp>
	    </rescap:Extension>
    </Extensions>
    ```

3.  Configure the system settings application as a preinstalled application by submitting the application to Windows Dev Center to sign the .appx and obtain a license file, and then include the application in the device image.

## <span id="Updated_system_settings_applications"></span><span id="updated_system_settings_applications"></span><span id="UPDATED_SYSTEM_SETTINGS_APPLICATIONS"></span>Updated system settings applications


Settings applications follow the typical process for any Windows app. Partners can submit updates to system settings applications to the Store. After an update is submitted, customers who have the system settings application installed are notified of the update and can install the update through the Store.

Because system settings applications don't appear in devices' application list, users might be confused when they are notified of an update for the application on the Store. To help avoid confusion, Microsoft recommends providing some context for users by specifying in the Store description for the application that it provides system-level settings that appear in **Settings** on the device.

## <span id="What_happens_to_legacy_Control_Panel_or_system_settings_apps_when_the_OS_upgrades_to_Windows_10_"></span><span id="what_happens_to_legacy_control_panel_or_system_settings_apps_when_the_os_upgrades_to_windows_10_"></span><span id="WHAT_HAPPENS_TO_LEGACY_CONTROL_PANEL_OR_SYSTEM_SETTINGS_APPS_WHEN_THE_OS_UPGRADES_TO_WINDOWS_10_"></span>What happens to legacy Control Panel or system settings apps when the OS upgrades to Windows 10?


If your Control Panel application was written for Windows 7, Windows 8, or Windows 8.1, it will continue to work in the legacy Control Panel, but it will not support any of the features of the Windows 10 system settings app. Likewise, if your legacy system settings app was written for Windows 8 or Windows 8.1, it will continue to work but it will not support any of the features of the Windows 10 system settings app. Legacy apps cannot display in the Windows 10 system settings app. All UWP apps in the Windows 10 settings app must be preinstalled on the machine. Control Panel is deprecated and will be removed in an upcoming release.

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bp_phPartAppDev\p_phPartAppDev%5D:%20Create%20a%20partner%20settings%20app%20%20RELEASE:%20%281/18/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")




