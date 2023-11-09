---

title: Manage tenant registration 
description: Learn how to manage which tenants have permissions to register an on-premises data gateway.
ms.reviewer: dougklo
ms.topic: conceptual
ms.date: 11/6/2023
---

# Manage tenants allowed to register an on-premises data gateway

You can use the new tenant restriction settings to control which tenants are allowed to register the on-premises data gateway application. For example, an organization can choose to allow only tenants within the organization to prevent data exfiltration. By default there's no restriction on tenants.

> [!IMPORTANT]
> Although these steps are a good security measure to take, it doesn't guarantee total data exfiltration protection.

After you define a list of allowed tenants, use the following steps to add them to the registry for both personal and enterprise gateway versions.

## Restrict the enterprise and personal on-premises data gateway

1. [Find your tenant ID](/azure/active-directory/fundamentals/how-to-find-tenant).
2. Run the Registry Editor through the Windows start menu (regedit.exe).
3. Navigate to **\\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft**.
4. Select and hold (or right-click) on the Microsoft folder and select **New** > **Key**. Create a key named either **On-premises data gateway** for the enterprise gateway, or **On-premises data gateway (personal mode)** for the personal gateway.
5. Select and hold (or right-click) on the "on-premises data gateway" folder you just created and select **New** > **Key** again. Name this key **Registration**.
6. Select and hold (or right-click) on the window to the right and select **New** > **String Value**. Name the value **AllowedRegistrationTenants** (make sure it's plural and everything is spelled correctly). Select and hold (or right-click) on the **AllowedRegistrationTenants** value and select **Modify**. Set its data to a comma separated list of the tenant IDs that the machine should allow. Tenants are identified by their TenantID, which is a GUID. The results should appear as in the following screenshots.

   :::image type="content" source="media/service-gateway-tenant-registration/enterprise-tenant-registration.png" alt-text="Screenshot of the registry editor with required keys added for the enterprise gateway." lightbox="media/service-gateway-tenant-registration/enterprise-tenant-registration.png":::

   :::image type="content" source="media/service-gateway-tenant-registration/personal-tenant-registration.png" alt-text="Screenshot of the registry editor with required keys added for the personal gateway." lightbox="media/service-gateway-tenant-registration/personal-tenant-registration.png":::

## On-premises data gateway registration tenant settings

When you register the enterprise gateway, the tenant used to register is written to **\\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\On-premises data gateway\Registration\RegistrationTenant**.

When you register the personal gateway, the tenant used to register is written to **\\HKEY_CURRENT_USER\SOFTWARE\Microsoft\On-premises data gateway (personal mode)\Registration\RegistrationTenant**.

:::image type="content" source="media/service-gateway-tenant-registration/tenant-registration-tenant-used.png" alt-text="Screenshot of the registry editor with key of tenant used to register the gateway." lightbox="media/service-gateway-tenant-registration/tenant-registration-tenant-used.png":::

## Error associated with using a tenant not in the allow list

If the registry key is set to limit allowed tenants and a user attempts to register the gateway with a credential from a tenant that isn't specifically allowed, this action generates an error, and the gateway fails to register or launch.

In this case, an error is written to the gateway logs stating `[DM.GatewayServiceHost] Not starting transfer service because 'onmicrosoft.com' is not in tenant allow list`. The user receives a `You cannot login with this email address. Please contact your tenant administrator for help with allowed registration tenants.` This message indicates the user attempted to register or sign in using a tenant that isn't in the tenant registration allow list.

:::image type="content" source="media/service-gateway-tenant-registration/tenant-registration-error.png" alt-text="Screenshot of the error shown when using a tenant not in the registry to register the gateway.":::
