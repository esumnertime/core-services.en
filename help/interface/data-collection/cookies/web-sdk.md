---
title: Adobe Experience Platform Web SDK Cookies
description: Learn how the Web SDK uses cookies applicable to your implementation.
solution: Experience Cloud
feature: Cookies
topic: Administration
role: Admin
level: Experienced
exl-id: 14f06dc9-255e-4a6c-adec-471107cf202e
TQID: 'https://experienceleague.adobe.com/jysQ5m7o0cI3ECKz2RWZB4Kt3own7XAPm04pr4yLh-k'
product_v2:
  - id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87
    internal-label: CX Enterprise
feature_v2:
  - id: fdbb8fc9-ffa3-4b86-88fe-aa4c5a3e1bc6
    internal-label: Administration
subfeature_v2:
  - id: b75843fa-0a67-4a44-a6b1-cc627b0481dc
    internal-label: Support
  - id: fef08361-6ac5-460c-93fe-d063e40b6a49
    internal-label: Getting started
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
level_v2:
  - id: d378ca77-2da1-4f39-ad92-1917fe974a38
    internal-label: Experienced
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
    internal-label: Administration
---
# Adobe Experience Platform Web SDK cookies

The Adobe Experience Platform Web SDK uses cookies to store values specific to your implementation.

| Name | Max age | Size | Description |
| --- | --- | --- | --- |
| **`AMCV_###@AdobeOrg`** | 33696000 (390 days) when written by the Web SDK | 44 bytes when written by the Web SDK (`MCMID\|<ECID>`); larger when written by `VisitorAPI.js` | Present when [`idMigrationEnabled`](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/commands/configure/idmigrationenabled) is enabled, which is the default. It helps when transitioning to the Web SDK while some parts of the site still use `VisitorAPI.js`. The Web SDK reads this cookie to reuse an existing ECID. After the Edge Network returns an ECID, the Web SDK writes it to this cookie if the cookie is missing or contains a different ECID. |
| **`com.adobe.alloy.getTld`** | None (session cookie, immediately deleted) | 22 bytes | Temporary helper cookie used internally by the Web SDK to determine the top-level domain of the current site. The Web SDK writes and deletes this cookie when the library loads, before the `configure` command runs and before consent is evaluated, so cookie scanners can report it as set before consent. The cookie contains only its own name and does not store behavioral or profile data. |
| **`demdex`** | 15552000 (180 days) | varies | Third-party cookie on the `demdex.net` domain. Present when [`thirdPartyCookiesEnabled`](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/commands/configure/thirdpartycookiesenabled) is enabled (the default) and the browser allows third-party cookies by default, such as Chrome or Edge. In that case, the Web SDK sends identity requests to `adobedc.demdex.net`, which sets this cookie. Audience Manager uses this cookie to assign a unique ID and support ID sync, segmentation, modeling, and reporting. See `demdex` in [Audience Manager cookies](audience-manager.md). |
| **`kndctr_<orgId>_identity`** | 34128000 (395 days) | 100-120 bytes (variable) | Stores the ECID and other related information for that device. |
| **`kndctr_<orgId>_cluster`** | 1800 (30 minutes) | 3-5 bytes | Stores the Edge Network region (location hint) that serves the current user's requests. The region is used in the URL path so that the Edge Network can route the request to the correct region. If a user connects with a different IP address within the cookie lifetime, the request is again routed to the closest region. |
| **`kndctr_<orgId>_consent`** | 15552000 (180 days) | 10-11 bytes | Stores the visitor's consent preferences. Always set regardless of consent because it stores the consent preferences itself. |
| **`kndctr_<orgId>_consent_check`** | 7200 (2 hours) | | Session-scoped helper that signals the Edge Network to re-check consent server-side after the TTL expires. It enforces a TTL on cached consent. |
| **`kndctr_<orgId>_personalization`** | 34128000 (395 days) | | Stores session information that Adobe Target uses to personalize content. |
| **`kndctr_<orgId>_advertising`** | 31622400 (366 days), renewed each time the cookie is updated | 80 bytes to 1 KB (variable) | Present when the Adobe Advertising component (beta) is included in your Web SDK build and the visitor's consent is `in`. The Web SDK writes this cookie when the page URL contains Adobe Advertising click parameters (`s_kwcid` or `ef_id`), or when [Adobe Advertising DSP](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/client/web-sdk/configure/advertising) advertisers are configured. It stores URL-encoded JSON that can include search click data (`_les_lsc`), a hashed IP address, a LiveRamp RampID envelope (when a RampID JavaScript path is configured), and conversion timestamps used to throttle duplicate conversions. In browsers that allow third-party cookies by default, it also stores the Adobe Advertising surfer ID and display click data (`ev_lcc`). This cookie is set on the current hostname only. The component also loads resources from `pixel.everesttech.net`, `www.everestjs.net` (when an ID5 partner ID is configured), and your RampID `ats.js` path. These resources can set their own cookies, which are not listed on this page. |
| **`kndctr_<orgId>_bc_session_id`** | None (session cookie) | | Present when the Brand Concierge component (beta) is used. Stores the Brand Concierge chat session ID. The Web SDK reads this cookie only when [`stickyConversationSession`](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/commands/configure/conversation) is enabled, so that chat sessions persist across page loads. |
| **`mbox`** | 63072000 (2 years) | | Present when [`targetMigrationEnabled`](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/commands/configure/targetmigrationenabled) is enabled. It allows the Target [mbox cookie](https://developer.adobe.com/target/implement/client-side/atjs/atjs-cookies/) to be set by the Web SDK. |
| **`mboxEdgeCluster`** | 1800 (30 minutes) | | Present when [`targetMigrationEnabled`](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/commands/configure/targetmigrationenabled) is enabled. It allows the Web SDK to communicate the correct edge cluster to `at.js` so that Target profiles can stay in sync as users navigate across a site. When the `kndctr_<orgId>_cluster` cookie is not present, the Web SDK also reads this cookie to route requests to the matching Edge Network region. |
| **`s_ecid`** | 63115200 (2 years) | ~45 bytes | Contains a copy of the CX Enterprise ID (ECID/MID) in the format `s_ecid=MCMID\|<ECID>`. Acts as a first-party backup of the ECID, primarily for CNAME (first-party) scenarios. When [`idMigrationEnabled`](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/commands/configure/idmigrationenabled) is enabled, the Web SDK reads this cookie to reuse an existing ECID. |
| **Audience Manager cookie destinations** (name varies) | 864000 (10 days), unless the destination specifies a different lifetime | varies | Present when the Edge Network returns an Audience Manager [cookie destination](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-cookie-destination) for the visitor. The Web SDK writes a first-party cookie using the cookie name, value, and domain defined in the destination. Values are URL-encoded, consistent with the Audience Manager Data Integration Library (DIL). |

The Edge Network sets all of its cookies with the `secure` and `sameSite="none"` attributes. If you currently have both secure and non-secure sections on your website, user identification can be inaccurate. When a user navigates from a secure section of the site to a non-secure section, the Edge Network generates a new `ECID` with the request.

Cookies that the Web SDK creates on its own, rather than at the direction of the Edge Network, use different attributes. The `AMCV_###@AdobeOrg` cookie and Audience Manager cookie destinations include the `secure` and `sameSite="none"` attributes only on HTTPS pages. The `com.adobe.alloy.getTld` and `kndctr_<orgId>_advertising` cookies use the browser's default attributes.
