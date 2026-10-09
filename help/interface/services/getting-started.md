---
description: Modernize your Adobe Analytics and Adobe Target applications for cross-application services. Learn how to start using CX Enterprise services.
solution: Experience Cloud
title: Get Started with CX Enterprise
index: true
feature: Central Interface Components
topic: Administration
role: Admin
level: Experienced
exl-id: 48e79e23-b339-4143-b3b1-969c370efeff
TQID: 'https://experienceleague.adobe.com/5SyRdqyQkymJJygKeQ9FXIYoVe70br51DY2VKmqSC0E'
product_v2:
  - id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87
    internal-label: CX Enterprise
feature_v2:
  - id: dab36b01-8bfa-48f3-8392-626455a058e6
    internal-label: Experience Cloud services
  - id: fdbb8fc9-ffa3-4b86-88fe-aa4c5a3e1bc6
    internal-label: Administration
subfeature_v2:
  - id: b75843fa-0a67-4a44-a6b1-cc627b0481dc
    internal-label: Support
  - id: bdea9bc8-5600-45db-b85e-d74bb59dfcff
    internal-label: Organizations
  - id: d27b1945-f442-4607-91bd-537a0b16e687
    internal-label: Assets
  - id: eb7e29b9-c5e9-4ed0-8e4b-6465dabb3cb1
    internal-label: Admin tools
  - id: ecb4a972-6786-444c-a014-abc528b9407a
    internal-label: Customer attributes
  - id: fef08361-6ac5-460c-93fe-d063e40b6a49
    internal-label: Getting started
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
level_v2:
  - id: d378ca77-2da1-4f39-ad92-1917fe974a38
    internal-label: Experienced
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
    internal-label: Reporting
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
  - id: c2be0313-b3ae-45e0-b454-d20bf54b23f2
    internal-label: Measurement
  - id: d3cdead0-685a-4489-9250-4bb709942f66
    internal-label: Data collection
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
    internal-label: Administration
  - id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
    internal-label: Privacy
---
# Get started with CX Enterprise

If you recently implemented CX Enterprise using [Experience Platform tags](https://experienceleague.adobe.com/en/docs/experience-platform/tags/home), you are already set up for [Customer Attributes](../services/overview.md) and CX Enterprise [Audiences](../services/audiences/overview.md). You can also manage users and products in [Admin Console](../administration/admin-console.md).

Existing customers can modernize their application implementations and implement CX Enterprise. Doing so enables you to use Customer Attributes and Audience features across Adobe Analytics, Audience Manager, and Adobe Target.

## Sign in as an administrator {#admin-sign-in}

After you are an administrator, you can log in at [experience.adobe.com](https://experience.adobe.com).

The **[!UICONTROL Admin Console]** link is available in CX Enterprise menu navigation for managing users and product licenses. 

### Optional: Link existing user accounts {#link-accounts}

Most likely, you have users who are already members of application groups, such an Analytics group that you previously managed in [!UICONTROL Analytics] > [!UICONTROL Admin Tools].

When you map these groups to CX Enterprise enterprise groups, those users must manually link their application account credentials to their Adobe ID.

See [Link accounts in CX Enterprise](https://experienceleague.adobe.com/en/docs/core-services/interface/administration/organizations)

>[!NOTE]
>
>After enterprise and application groups are mapped, new users are automatically linked. (Solution credentials are automatically created and linked to their Adobe ID.) 

The following sections describe how to modernize your implementation. Modernizing your implementation enables core services in CX Enterprise. 

## Sign-in as a user {#user-sign-in}

To log in to CX Enterprise, your users must:

* Have an Adobe ID (or Enterprise ID for your company).
* Sign in at [experience.adobe.com](https://experience.adobe.com).
* Belong to an application group that is mapped to an enterprise group.
* If necessary, link their application accounts to their Adobe ID (described below).

## Adobe Analytics and Adobe Target requirements for CX Enterprise {#experience-cloud-requirements}

[!DNL Analytics] and [!DNL Adobe Target] requirements for using CX Enterprise: 

1. Ensure that you have the appropriate Adobe Analytics or Adobe Target SKUs. 

   * **Adobe Analytics:** Standard or Premium (not the legacy [!DNL SiteCatalyst] SKU).
   * **Adobe Target:** Standard or Premium.

     >[!NOTE]
     >
     >For [!DNL Target], migrate to at.js from `mbox.js`. See [Upgrading from at.js 1. x to at.js 2. x](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/upgrading-from-atjs-1x-to-atjs-20.html).

1. [Manage users and products](../administration/admin-console.md) in the [!UICONTROL Admin Console]. 

**Related:** [Analytics and Target - Synchronize customer IDs](#sync-ids) (on this page)

## Implement the Visitor ID Service

The Visitor ID Service provides a common ID for cross-application integration. It provides cross-domain visitor identification and a path for cross-device/browser targeting and personalization based on CRM data uploaded via [!DNL Customer Attributes].

The simplest method for enabling CX Enterprise core services is to activate it automatically for Analytics and Adobe Target via the [[!UICONTROL Experience Cloud ID Service] tag extension](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/id-service/overview.html), which implements the Visitor ID Service.  

For complete Visitor ID Service help, see [Visitor ID Service overview](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html#intro).


**Not Using [!UICONTROL Experience Platform tags]?**

If you are not using [!UICONTROL Experience Platform tags], manually implement the Visitor ID Service via the JavaScript Deployment (`VisitorAPI.js`), as follows:

| Task  | Description  |
| --- | --- |
| [Implement the Visitor ID Service (`VisitorAPI.js`) for Analytics](https://experienceleague.adobe.com/en/docs/analytics/implementation/id/overview)  | Adobe also recommends setting additional [customer IDs](https://experienceleague.adobe.com/en/docs/id-service/using/reference/authenticated-state). These IDs are associated with each visitor and enable current and future functionality in CX Enterprise. |
| Update your existing `s_code` to version H.27.3 or later, or your existing `AppMeasurement.js` to version 1.4 or later.  | These files are available for download in the [Code Manager](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/code-manager-admin.html) in Analytics Admin Tools. (The [JavaScript Implementation](https://experienceleague.adobe.com/en/docs/analytics/implementation/js/overview#js) guide is available if you need more information about `AppMeasurement.js`.) |

### Analytics & Adobe Target - Synchronize customer IDs {#sync-ids} 

As a part of setting up the Visitor ID Service, Adobe recommends for Analytics and [!DNL Target] that you synchronize your [customer IDs](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html) with the CX Enterprise. 

In Adobe Target, the `mbox3rdpartyid` must get the customer ID and send it to [!DNL Target]. (See [Working with Customer Attributes](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/working-with-customer-attributes.html) in [!DNL Target].) 

When a visitor authenticates on your website, or otherwise identifies themselves, your implementation must expose that person's CRM customer ID to the page or app. Then you can use the appropriate function call to synchronize your customer ID to CX Enterprise. This synchronization stores the visitor's CRM customer ID in CX Enterprise, and activates that customer's attributes for use in CX Enterprise. 

For example, assume that Bob has Customer ID `52mc210tr42` in your CRM system. When Bob authenticates on your site, you must expose this ID on the page, and use the ID to synchronize it by one of two means: 

* Call `visitor.setCustomerIDs({"crm_id":"52mc210tr42"})` using the Visitor ID Service. Or, 
* Populate the *`Customer ID (52mc210tr42)`* in a prop or eVar.

The Customer ID must be set on each [!DNL Analytics] server call where the Customer ID is known. 

#### Analytics: synching the customer ID with the Data Warehouse backfill method

When Customer Attributes first became available, some customers had not yet implemented the Visitor ID Service and could not easily utilize Customer Attributes. To help alleviate this problem, Adobe created a means to do a backfill of ID syncs using the Adobe Analytics Data Warehouse. This feature is known as the Data Warehouse backfill. The Data Warehouse backfill is now generally not necessary and as a result will no longer be available starting in October 2022.

### Mobile SDKs

See the *Visitor ID Service* section for syntax examples about how to set additional customer IDs in [Android&trade;](https://experienceleague.adobe.com/docs/mobile-services/android/overview.html) and [iOS](https://experienceleague.adobe.com/docs/mobile-services/ios/overview.html) Mobile applications.

### Enable attributes for Historical Data

Customer attribute data is made available after visitors log in. If you have not yet implemented the Visitor ID Service, and if you have historically been tracking customer IDs in a prop or eVar, you can request a process that sends historical logins to CX Enterprise. This process lets you begin using Customer Attributes immediately.

Contact Support to enable historical data.

## Update your Analytics AppMeasurement code 

If you are using first-party cookies, see the [Adobe-managed certificate program](/help/interface/data-collection/adobe-managed-cert.md) for information about data collection CNAMEs and cross-domain tracking. 

It is recommended that you modernize your Analytics implementation by updating your JavaScript libraries, including the Visitor API. The simple way to accomplish is to add an [Adobe Analytics extension](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/analytics/overview.html) in Experience Platform Data Collection.

## Update your Adobe Target implementation 

* It is recommended that you add an [Adobe Target extension](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/target-v2/overview.html) in [!UICONTROL Experience Platform] tags, so that your library retrieval is automatic. You can also set up the [[!UICONTROL Experience Cloud ID Service] tag extension](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/id-service/overview.html), which implements the Visitor ID Service for Adobe Target (and other applications) using tags. This tag extension is **required** for Adobe Target to use the People services.
* If you are not using [!UICONTROL Experience Platform] tags, [update your mbox library](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/implement-target-for-client-side-web.html) manually.
* Request access to use Adobe Analytics as the reporting source for [!DNL Adobe Target]. [!DNL Target] and [!DNL Analytics] data are combined on the same server call during processing so that visitors are connected between the two applications. See [Analytics for Target Implementation](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html).
 
  >[!IMPORTANT]
  >
  >All Analytics customers are already provisioned for core services like Customer Attributes. If you are not an Analytics customer, contact Customer Care to request to be provisioned.

## Verify the implementation 

Use the following process to ensure that the Visitor ID Service is implemented correctly on your site.

1. Clear cookies for your site so you can see the request to the Visitor ID Service (the request happens on the first visit, then once per visitor per week).
1. Using a packet analyzer or the network panel in a web browser debugger, look for a request going to [!DNL dpm.demdex.net].
1. Verify that the response contains `d_mid` and a value, for example: `_setMarketingCloudFields({"d_mid":"4235...`
1. Verify that the Analytics request contains the `mid` parameter (the ECID). During the grace period (if it is enabled), you should also see an `aid` parameter (the Analytics visitor ID).

Expected response containing the ECID:

![Expected response containing the ECID](../assets/mac_id_response.png)

Analytics image request containing the ECID (also known as `mid` or _visitor ID_):

![Analytics image request containing the ECID](../assets/mid.png)

ECID in the mbox request:

![ECID in the mbox request](../assets/mbox_request.png)

### What Is the Grace Period?

After you deploy the Visitor ID Service, new visitors no longer receive an Analytics ID (`aid`). If sections of your site have not yet implemented the Visitor ID Service, when visitors browse to these sections, the ECID (`mid`) is not recognized and visitors are assigned a legacy Analytics ID (`aid`). This setup can cause potential problems, including duplicate visits and incorrect attribution.

For example, if the support section of your site is managed in a separate CMS, you might have a different Analytics JavaScript file for this section. If you deploy the ECID on your main site before you deploy the Visitor ID Service to the support site, new visitors receive a legacy Analytics ID when they visit the support section. Visits that span both site sections are reported as different visits.

Deploying the Visitor ID Service on sites that are using multiple JavaScript files or other technologies (such as Flash) can cause coordination issues. These issues occur because you must enable the Visitor ID Service on all portions of your site at the same time. By configuring a grace period, new visitors to continue to receive an Analytics visitor ID from the Visitor ID Service. Visitors can be consistently identified on sections of your site that have not been upgraded to use the Visitor ID Service. 

## Manage users and products 

Once you are up and running, navigate to the [Admin Console](https://adminconsole.adobe.com/), where you can manage users and product profiles. 

![Access Admin Console](../assets/menu-administration-shell.png)

### Customer Attributes

Users that are added to the [!DNL Customer Attributes] group can see the [!DNL Customer Attributes] menu item on the left side of CX Enterprise.

## Begin sharing attribute and audience data 

Take advantage of the following features. 

### [!UICONTROL Customer Attributes]

If you capture enterprise customer data in a customer relationship management (CRM) database, you can upload the data into a customer attribute data source in CX Enterprise. Once uploaded, use the data in [!DNL Adobe Analytics] and [!DNL Adobe Target].

See [Customer Attributes](https://experienceleague.adobe.com/en/docs/core-services/interface/services/customer-attributes/attributes) for more information.

### [!UICONTROL People] > [!UICONTROL Audience Library] 

CX Enterprise [!UICONTROL Audiences] is the interface that lets you create audiences, combine existing audiences to create composite audiences, and view all shared audiences. 

See [Audiences](https://experienceleague.adobe.com/en/docs/core-services/interface/services/audiences/overview) for more information.

## Data storage and privacy disclosure 

If you use real-time audience profiling and other core services within the Adobe [!DNL CX Enterprise], use of these services might impact which data center (and country) your data resides. Specifically, because [!DNL CX Enterprise] uses Audience Manager, data used within the [!UICONTROL People] service must reside within Audience Manager servers in the United States. 

When using services made available via the [!UICONTROL People] service, the types of data sent from other Adobe products to audience management are: 

* [!DNL Analytics] key/value pairs (props, eVars, list vars, and so on). By default, the log lines include IP address, including the last octet of the IP (assuming that the IP address was not modified by IP obfuscation settings within Adobe [!DNL Analytics]).
* Traits and segments that visitors qualify for based on rules set up in Audience Manager.
* (Optional) One or more of your IDs. Depending on your implementation of the Visitor ID Service, you might also send in one or more of your IDs, such as CRM IDs or hashed email addresses. If this data is sent into Adobe Analytics, it is transferred to Adobe Audience Manager. Adobe recommends against providing personal data to Adobe Analytics. Rather, use a one-way hash to mask the data before it is sent to Adobe.
* Segments originating in [!DNL Analytics] via the back-end segment sharing capability
* The `demdex.net` cookie is set if third-party cookies are not blocked. The `AMCV_###@AdobeOrg` first-party cookie is always set with the Visitor ID Service.

All these data elements are delivered to Adobe Audience Manager in the form of log files. Audience Manager processes and stores this data within the United States. Audience Manager does not provide an option to store or process this data outside of the United States.
