---
title: Grant controls in Conditional Access policy - Azure Active Directory
description: What are grant controls in an Azure AD Conditional Access policy

services: active-directory
ms.service: active-directory
ms.subservice: conditional-access
ms.topic: conceptual
ms.date: 06/29/2022

ms.author: joflore
author: MicrosoftGuyJFlo
manager: karenhoran
ms.reviewer: calebb, sandeo

ms.collection: M365-identity-device-management
---
# Conditional Access: Grant

Within a Conditional Access policy, an administrator can make use of access controls to either grant or block access to resources.

:::image type="content" source="media/concept-conditional-access-session/conditional-access-session.png" alt-text="Screenshot of Conditional Access policy with a grant control requiring multifactor authentication." lightbox="media/concept-conditional-access-session/conditional-access-session.png":::

## Block access

Block takes into account any assignments and prevents access based on the Conditional Access policy configuration.

Block is a powerful control that should be wielded with appropriate knowledge. Policies with block statements can have unintended side effects. Proper testing and validation are vital before enabling at scale. Administrators should utilize tools such as [Conditional Access report-only mode](concept-conditional-access-report-only.md) and [the What If tool in Conditional Access](what-if-tool.md) when making changes.

## Grant access

Administrators can choose to enforce one or more controls when granting access. These controls include the following options: 

- [Require multifactor authentication (Azure AD Multi-Factor Authentication)](../authentication/concept-mfa-howitworks.md)
- [Require device to be marked as compliant (Microsoft Intune)](/intune/protect/device-compliance-get-started)
- [Require hybrid Azure AD joined device](../devices/concept-azure-ad-join-hybrid.md)
- [Require approved client app](app-based-conditional-access.md)
- [Require app protection policy](app-protection-based-conditional-access.md)
- [Require password change](#require-password-change)

When administrators choose to combine these options, they can choose the following methods:

- Require all the selected controls (control **AND** control)
- Require one of the selected controls (control **OR** control)

By default Conditional Access requires all selected controls.

### Require multifactor authentication

Selecting this checkbox will require users to perform Azure AD Multifactor Authentication. More information about deploying Azure AD Multifactor Authentication can be found in the article [Planning a cloud-based Azure AD Multifactor Authentication deployment](../authentication/howto-mfa-getstarted.md).

[Windows Hello for Business](/windows/security/identity-protection/hello-for-business/hello-overview) satisfies the requirement for multifactor authentication in Conditional Access policies. 

### Require device to be marked as compliant

Organizations who have deployed Microsoft Intune can use the information returned from their devices to identify devices that meet specific compliance requirements. Policy compliance information is sent from Intune to Azure AD so Conditional Access can decide to grant or block access to resources. For more information about compliance policies, see the article [Set rules on devices to allow access to resources in your organization using Intune](/intune/protect/device-compliance-get-started).

A device can be marked as compliant by Intune (for any device OS) or by third-party MDM system for Windows 10 devices. A list of supported third-party MDM systems can be found in the article [Support third-party device compliance partners in Intune](/mem/intune/protect/device-compliance-partners).

Devices must be registered in Azure AD before they can be marked as compliant. More information about device registration can be found in the article, [What is a device identity](../devices/overview.md).

**Remarks**

- The **Require device to be marked as compliant** requirement:
   - Only supports Windows 10+, iOS, Android, and macOS devices registered with Azure AD and enrolled with Intune.
   - For devices enrolled with third-party MDM systems, see [Support third-party device compliance partners in Intune](/mem/intune/protect/device-compliance-partners).
   - Conditional Access can’t consider Microsoft Edge in InPrivate mode as a compliant device.

> [!NOTE]
> On Windows 7, iOS, Android, macOS, and some third-party web browsers Azure AD identifies the device using a client certificate that is provisioned when the device is registered with Azure AD. When a user first signs in through the browser the user is prompted to select the certificate. The end user must select this certificate before they can continue to use the browser.

### Require hybrid Azure AD joined device

Organizations can choose to use the device identity as part of their Conditional Access policy. Organizations can require that devices are hybrid Azure AD joined using this checkbox. For more information about device identities, see the article [What is a device identity?](../devices/overview.md).

When using the [device-code OAuth flow](../develop/v2-oauth2-device-code.md), the require managed device grant control or a device state condition aren’t supported. This is because the device performing authentication can’t provide its device state to the device providing a code and the device state in the token is locked to the device performing authentication. Use the require multi-factor authentication grant control instead.

**Remarks**

- The **Require hybrid Azure AD joined device** requirement:
   - Only supports domain joined Windows down-level (pre Windows 10) and Windows current (Windows 10+) devices.
   - Conditional Access can’t consider Microsoft Edge in InPrivate mode as a hybrid Azure AD joined device.

### Require approved client app

Organizations can require that an access attempt to the selected cloud apps needs to be made from an approved client app. These approved client apps support [Intune app protection policies](/intune/app-protection-policy) independent of any mobile-device management (MDM) solution.

In order to apply this grant control, Conditional Access requires that the device is registered in Azure Active Directory, which requires the use of a broker app. The broker app can be the Microsoft Authenticator for iOS, or either the Microsoft Authenticator or Microsoft Company portal for Android devices. If a broker app isn’t installed on the device when the user attempts to authenticate, the user gets redirected to the appropriate app store to install the required broker app.

The following client apps have been confirmed to support this setting:

- Microsoft Azure Information Protection
- Microsoft Bookings
- Microsoft Cortana
- Microsoft Dynamics 365
- Microsoft Edge
- Microsoft Excel
- Microsoft Power Automate
- Microsoft Invoicing
- Microsoft Kaizala
- Microsoft Launcher
- Microsoft Lists
- Microsoft Office
- Microsoft OneDrive
- Microsoft OneNote
- Microsoft Outlook
- Microsoft Planner
- Microsoft Power Apps
- Microsoft Power BI
- Microsoft PowerPoint
- Microsoft SharePoint
- Microsoft Skype for Business
- Microsoft StaffHub
- Microsoft Stream
- Microsoft Teams
- Microsoft To-Do
- Microsoft Visio
- Microsoft Word
- Microsoft Yammer
- Microsoft Whiteboard
- Microsoft 365 Admin

**Remarks**

- The approved client apps support the Intune mobile application management feature.
- The **Require approved client app** requirement:
   - Only supports the iOS and Android for device platform condition.
   - A broker app is required to register the device. The broker app can be the Microsoft Authenticator for iOS, or either the Microsoft Authenticator or Microsoft Company portal for Android devices.
- Conditional Access can’t consider Microsoft Edge in InPrivate mode an approved client app.
- Using Azure AD Application Proxy to enable the Power BI mobile app to connect to on premises Power BI Report Server isn’t supported with Conditional Access policies that require the Microsoft Power BI app as an approved client app.

See the article, [How to: Require approved client apps for cloud app access with Conditional Access](app-based-conditional-access.md) for configuration examples.

### Require app protection policy

In your Conditional Access policy, you can require an [Intune app protection policy](/intune/app-protection-policy) be present on the client app before access is available to the selected cloud apps. 

In order to apply this grant control, Conditional Access requires that the device is registered in Azure Active Directory, which requires the use of a broker app. The broker app can be either the Microsoft Authenticator for iOS, or the Microsoft Company portal for Android devices. If a broker app isn’t installed on the device when the user attempts to authenticate, the user gets redirected to the app store to install the broker app.

Applications are required to have the **Intune SDK** with **Policy Assurance** implemented and meet certain other requirements to support this setting. Developers implementing applications with the Intune SDK can find more information in the SDK documentation on these requirements.

The following client apps have been confirmed to support this setting:

- Microsoft Cortana
- Microsoft Edge
- Microsoft Excel
- Microsoft Lists
- Microsoft Office
- Microsoft OneDrive
- Microsoft OneNote
- Microsoft Outlook
- Microsoft Planner
- Microsoft Power BI
- Microsoft PowerPoint
- Microsoft SharePoint
- Microsoft Teams
- Microsoft To Do
- Microsoft Word
- MultiLine for Intune
- Nine Mail - Email & Calendar

> [!NOTE]
> Microsoft Kaizala, Microsoft Skype for Business and Microsoft Visio do not support the **Require app protection policy** grant. If you require these apps to work, please use the **Require approved apps** grant exclusively. The use of the `or` clause between the two grants will not work for these three applications.

**Remarks**

- Apps for app protection policy support the Intune mobile application management feature with policy protection.
- The **Require app protection policy** requirements:
    - Only supports the iOS and Android for device platform condition.
    - A broker app is required to register the device. On iOS, the broker app is Microsoft Authenticator and on Android, it’s Intune Company Portal app.

See the article, [How to: Require app protection policy and an approved client app for cloud app access with Conditional Access](app-protection-based-conditional-access.md) for configuration examples.

### Require password change 

When user risk is detected, using the user risk policy conditions, administrators can choose to have the user securely change the password using Azure AD self-service password reset. If user risk is detected, users can perform a self-service password reset to self-remediate, this process will close the user risk event to prevent unnecessary noise for administrators. 

When a user is prompted to change their password, they’ll first be required to complete multi-factor authentication. You’ll want to make sure all of your users have registered for multi-factor authentication, so they’re prepared in case risk is detected for their account.  

> [!WARNING]
> Users must have previously registered for self-service password reset before triggering the user risk policy. 

Restrictions when you configure a policy using the password change control.  

1. The policy must be assigned to ‘all cloud apps’. This requirement prevents an attacker from using a different app to change the user’s password and reset account risk, by signing into a different app. 
1. Require password change can’t be used with other controls, like requiring a compliant device.  
1. The password change control can only be used with the user and group assignment condition, cloud app assignment condition (which must be set to all), and user risk conditions. 

### Terms of use

If your organization has created terms of use, other options may be visible under grant controls. These options allow administrators to require acknowledgment of terms of use as a condition of accessing the resources protected by the policy. More information about terms of use can be found in the article, [Azure Active Directory terms of use](terms-of-use.md).

## Next steps

- [Conditional Access: Session controls](concept-conditional-access-session.md)

- [Conditional Access common policies](concept-conditional-access-policy-common.md)

- [Report-only mode](concept-conditional-access-report-only.md)
