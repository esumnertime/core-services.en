---
title: Choose a Data Collection Domain
description: Learn about the domains that you can use to send data to Adobe, and how to find your organization's tenant ID.
product_v2:
  - id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87
    internal-label: CX Enterprise
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
level_v2:
  - id: d378ca77-2da1-4f39-ad92-1917fe974a38
    internal-label: Experienced
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
  - id: d3cdead0-685a-4489-9250-4bb709942f66
    internal-label: Data collection
---
# Choose a data collection domain

Your data collection domain is the hostname that your implementation sends data to. All Adobe CX Enterprise products that use Adobe data collection (such as Adobe Analytics, Customer Journey Analytics, Adobe Experience Platform, Adobe Target, and Adobe Journey Optimizer) rely on this domain.

## Data collection domain options

| Option | Implementation domain | Region-locked [RDC](rdc.md) | Certificate maintenance |
| --- | --- | --- | --- |
| [Third-party domain](#third-party) | `example.data.adobedc.net` | Not supported | None |
| First-party domain with an [Adobe-managed certificate](adobe-managed-cert.md) | `data.example.com` | Supported | None (Adobe renews the certificate automatically) |
| First-party domain with a [customer-managed certificate](customer-managed-cert.md) | `data.example.com` | Supported | Your organization renews the certificate and provides it to Adobe |
| [Content delivery network (CDN) with a third-party origin](cdn.md#third-party-origin) | `data.example.com` | Not supported | None |
| [CDN with a first-party origin](cdn.md#first-party-origin) | `data.example.com` | Supported | Your organization renews the certificate and provides it to Adobe |

## Third-party data collection domain {#third-party}

If you don't use a first-party domain, send data to a subdomain of `data.adobedc.net`. Adobe recommends using your organization's [tenant ID](#tenant-id) as the subdomain. For example, `example.data.adobedc.net`. This domain is also the recommended origin when you [route data collection through a CDN](cdn.md).

* Third-party domains always use the default [RDC type](rdc.md#third-party-data-collection).
* Do not use any subdomains deeper than `example.data.adobedc.net`. For example, `custom.example.data.adobedc.net` is not a valid data collection domain.
* Older implementations might use domains such as `sc.omtrdc.net` or `2o7.net`. While these domains are still valid, Adobe recommends using `data.adobedc.net` where possible.

### Find your tenant ID {#tenant-id}

1. Log in to [Adobe CX Enterprise](https://experience.adobe.com) using your Adobe ID credentials.
1. Anywhere in the CX Enterprise interface, press `[Cmd]` + `[I]` (macOS) or `[Ctrl]` + `[I]` (Windows).
1. A **[!UICONTROL User data debugger]** appears. Select the **[!UICONTROL Assigned orgs]** tab.
1. Expand the desired IMS organization.
1. Locate the **[!UICONTROL Tenant]** field. This value is your tenant ID.

Your tenant ID is different from your IMS organization ID, which ends in `@AdobeOrg`. Each IMS organization has one tenant ID. If your company uses multiple IMS organizations, each organization has its own tenant ID.

## Update your implementation {#update-implementation}

When you change your data collection domain, update every implementation that sends data to Adobe:

* **Web SDK tag extension**: Update the [[!UICONTROL Edge domain]](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/client/web-sdk/configure/general) field when configuring the extension.
* **Web SDK (alloy)**: Update the [`edgeDomain`](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/commands/configure/edgedomain) property within the `configure` command.
* **Adobe Analytics extension**: Update the [[!UICONTROL SSL Tracking Server]](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/client/analytics/overview) field when configuring the extension. Make sure that you also have the [Visitor ID Service tag extension](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/client/id-service/overview) installed. See [Visitor identification using the Analytics tag extension](https://experienceleague.adobe.com/en/docs/analytics/implementation/id/analytics-extension) for more information.
* **AppMeasurement**: Update the [`trackingServerSecure`](https://experienceleague.adobe.com/en/docs/analytics/implementation/vars/config-vars/trackingserversecure) configuration variable. Make sure that you also have the [Visitor ID Service](https://experienceleague.adobe.com/en/docs/id-service/using/home) implemented using `VisitorAPI.js`. See [Visitor identification using AppMeasurement](https://experienceleague.adobe.com/en/docs/analytics/implementation/id/appmeasurement) for more information.
* **Other implementations**: Update the data collection domain in any other implementation that sends data to Adobe, such as mobile apps or server-side implementations.

If your implementation doesn't use the Visitor ID Service or the Web SDK, changing your data collection domain changes the domain of visitor cookies, and returning visitors can be counted as new visitors.

If your site uses multiple implementation methods and you cannot update all of them simultaneously, consider configuring a grace period. See [Visitor ID Service migration considerations](https://experienceleague.adobe.com/en/docs/analytics/implementation/id/migration) for additional steps on how to prevent visitors from being counted as new visitors across your site.
