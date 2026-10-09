---
description: Learn about Adobe Advertising cookies for mapping ad engagement events to conversion events and, potentially, use that information to optimize ad bids.
title: Adobe Advertising Cookies
uuid: 2eec48a3-3e81-488e-8e30-5fd62885de0b
feature: Cookies
topic: Administration
role: Admin
level: Experienced
exl-id: 6818edea-31b1-49fc-bca2-32828c7ca78d
TQID: 'https://experienceleague.adobe.com/jr9RwaF63elDUN-XewIdrPNsGb6T5wo98vktP5U6jIM'
product_v2:
  - id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87
    internal-label: CX Enterprise
feature_v2:
  - id: dab36b01-8bfa-48f3-8392-626455a058e6
    internal-label: Experience Cloud services
  - id: fdbb8fc9-ffa3-4b86-88fe-aa4c5a3e1bc6
    internal-label: Administration
subfeature_v2:
  - id: eb7e29b9-c5e9-4ed0-8e4b-6465dabb3cb1
    internal-label: Admin tools
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
level_v2:
  - id: d378ca77-2da1-4f39-ad92-1917fe974a38
    internal-label: Experienced
topic_v2:
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
    internal-label: Customer experience
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
    internal-label: Administration
---
# Adobe Advertising cookies

Adobe Advertising (formerly Adobe Advertising Cloud) uses cookies to map ad engagement events to conversion events and, potentially, to use that information to optimize ad bids.

>[!NOTE]
>
>The beta Adobe Advertising Javascript tag that uses the [Adobe CX Enterprise ID (ECID) Service](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html) creates first-party [CX Enterprise](experience-cloud.md) `s_ecid` cookies, not Adobe Advertising cookies.

| Cookie name | Expiration | Size | Location | Description |
| --- | --- | --- | --- | --- |
| **`_lcc`** | 15 minutes | 52 bytes | `everesttech.net` | Stores IDs and timestamps of display clicks. Determines if a click event on a display ad applies to an Adobe Analytics hit. |
| **`_tmae`** | 1 year | 1 KB | `everesttech.net` | Stores encoded IDs and timestamps for ad engagements using DSP tracking. Includes user engagement with ads, such as ad last seen |
| **`_tmid`** | 1 year | ~20 bytes | `everesttech.net` | Stores the Adobe Advertising Demand Side Platform (DSP) ID. Corresponds to the visitor ID in the `everest_g_v2` cookie. |
| **`adcloud`** | 1 year | 50-150 bytes | First-party | The timestamps of the visitor's last visit to your website and the visitor's last search click. Also stores the `ef_id` that was created when the visitor clicked an ad. Ties the visitor ID with relevant audience segments and conversions. Helps optimize page load times by avoiding unnecessary requests to Adobe. |
| **`ev_sync_*`** |  | 8 bytes | `everesttech.net` | The date when synchronization is performed in `yyymmdd` format. Syncs the Adobe Advertising visitor ID with the partner ad exchange. It is created for new visitors and sends a synchronization request when expired. Includes the cookies `ev_sync_ax`, `ev_sync_bk`, `ev_sync_dd`, `ev_sync_fs`, `ev_sync_ix`, `ev_sync_nx`, `ev_sync_ox`, `ev_sync_pm`, `ev_sync_rc`, `ev_sync_tm`, and `ev_sync_yh`. |
| **`everest_g_v2`** | 1 year | ~27 bytes | `everesttech.net` | Stores the browser and visitor ID. Created after a user initially clicks an ad. Used to map the current and subsequent clicsk with other events on your website. |
| **`everest_session_v2`** | Session | ~16 bytes | `everesttech.net` | Stores the current session ID. |
| **`id_adcloud`** | 91 days | 16 bytes | First-party | Stores the visitor ID. |

{style="table-layout:auto"}

