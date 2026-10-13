---
title: Route Data Collection Through a CDN
description: Learn how to configure a content delivery network (CDN) to forward data collection requests to Adobe without affecting data quality.
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
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
    internal-label: Security
  - id: d3cdead0-685a-4489-9250-4bb709942f66
    internal-label: Data collection
---
# Route data collection through a CDN

Some organizations route data collection requests through their content delivery network (CDN) instead of sending them directly to Adobe. Common reasons include web application firewall (WAF) protection, corporate policies that require all website traffic to pass through a CDN, and the ability to inspect traffic sent to Adobe. The CDN receives requests on a hostname that your organization owns, then forwards them to an Adobe data collection hostname, called the origin.

>[!IMPORTANT]
>
>Adobe can't review or validate your CDN configuration. Your organization and your CDN provider are responsible for configuring the CDN correctly. For help configuring your CDN, contact your CDN provider. Incorrectly configured CDNs can result in data loss.

## Choose an origin type {#origin-type}

| | Third-party origin (recommended) | First-party origin |
| --- | --- | --- |
| **Origin hostname** | Your tenant ID subdomain of `data.adobedc.net`, such as `example.data.adobedc.net` | Your first-party hostname, such as `data.example.com` |
| **Certificate on Adobe servers** | Adobe's certificate | [Customer-managed certificate](customer-managed-cert.md) |
| **Certificate renewals** | None required | Your organization renews the certificate and provides it to Adobe before each expiration |
| **Region-locked [RDC](rdc.md)** | Not supported | Supported |
| **When to use** | All CDN implementations, unless your organization requires a first-party origin | Your security policy requires direct control of the origin certificate, or your organization requires a region-locked RDC type |

>[!NOTE]
>
>The [Adobe-managed certificate program](adobe-managed-cert.md) doesn't support CDN implementations. Adobe can't validate domain ownership or renew certificates for hostnames that point to your CDN. Use a third-party origin, or a first-party origin with a [customer-managed certificate](customer-managed-cert.md).

## Requirements for all CDN implementations {#requirements}

Adobe data collection libraries, such as AppMeasurement and the Web SDK, include everything that Adobe needs in each request. Configure your CDN to forward these requests to Adobe without changing them.

>[!IMPORTANT]
>
>Never change the endpoint or anything that determines where data goes, including the report suite ID (AppMeasurement) or the datastream ID (Web SDK). Changing these values causes data loss.

Your CDN configuration must:

* Forward the request method, URL path, query string, and body without changes.
* Leave the `Host` header unchanged.
* Leave the domain that Adobe cookies are set on unchanged.
* Keep all cookies listed in the [cookies section](cookies/overview.md) of this guide.
* Add the `X-Forwarded-For` header containing the visitor's IP address. Adobe uses this header for geolocation. Without it, geolocation data reflects the location of your CDN's servers instead of your visitors.
* Return Adobe's responses to the browser without changes.

Your CDN configuration can:

* Remove cookies that Adobe doesn't use, such as cookies from other systems on your site. Unrelated cookies add overhead to every request.
* Use WAF, bot filtering, or personal data removal services, as long as they don't change anything listed above. Test these services with a development report suite or datastream before applying them to production traffic. Overly aggressive filtering can remove enough data to make reports unusable.

Your CDN configuration must not:

* Cache data collection requests or responses. Every request must reach Adobe.
* Point to an origin hostname that doesn't exist.
* Accept expired certificates or pin a specific certificate from the origin. Adobe doesn't support serving expired certificates and can remove them at any time.

## Configure a CDN with a third-party origin {#third-party-origin}

A third-party origin uses Adobe's own certificate, so your organization doesn't need to maintain a certificate on Adobe servers.

1. Find your organization's tenant ID. See [Find your tenant ID](collection-domain.md#tenant-id).
1. In your CDN configuration, set the origin hostname to your tenant ID subdomain of `data.adobedc.net`. For example, `example.data.adobedc.net`.
1. Enable Server Name Indication (SNI) for the origin. Set the SNI hostname to the origin hostname (for example, `example.data.adobedc.net`), not your website's hostname.
1. Configure your CDN to meet the [requirements for all CDN implementations](#requirements) above.
1. If the hostname that your implementation sends data to changes, [update your implementation](collection-domain.md#update-implementation). If you keep the same hostname, no implementation changes are needed.

>[!WARNING]
>
>Do not set your origin to the hostname that Adobe provided as your CNAME target, such as `hiodsibxvip01.data.adobedc.net`. That hostname is tied to your first-party certificate and can stop working when the certificate is removed.

Third-party origins always use the default [RDC type](rdc.md), so data can be collected at any Adobe data collection location.

## Configure a CDN with a first-party origin {#first-party-origin}

Use a first-party origin only if your organization requires it. Common reasons include:

* Your security policy requires direct control of the origin certificate. For example, your organization must be able to revoke the certificate through its own certificate authority.
* Your organization requires a region-locked [RDC type](rdc.md).

1. Contact Adobe Customer Care to set up a [customer-managed certificate](customer-managed-cert.md) for your first-party hostname, such as `data.example.com`. If your organization requires a region-locked RDC type, specify it in your request.
1. In your CDN configuration, set the origin hostname to your first-party hostname.
1. Enable Server Name Indication (SNI) for the origin. Set the SNI hostname to your first-party hostname, and configure your CDN to expect your first-party certificate from the origin.
1. Configure your CDN to meet the [requirements for all CDN implementations](#requirements) above.
1. If the hostname that your implementation sends data to changes, [update your implementation](collection-domain.md#update-implementation). If you keep the same hostname, no implementation changes are needed.

>[!IMPORTANT]
>
>Your organization is responsible for renewing your customer-managed certificate and providing it to Adobe Customer Care before it expires. If the certificate on Adobe servers expires, your CDN can reject the connection and discard data without notifying you. See [Renew your certificate](customer-managed-cert.md#renewals).

## Move an existing first-party implementation to a CDN {#migrate}

If your organization currently sends data directly to a first-party hostname with a certificate hosted by Adobe, use the following steps to move to a CDN:

1. Identify every implementation that sends data to your first-party hostname, across all Adobe products. Other products, such as Adobe Target or Adobe Journey Optimizer, might use the same hostname, and a single certificate can cover many hostnames.
1. Choose an [origin type](#origin-type). If you choose a first-party origin, contact Adobe Customer Care to convert your certificate to a [customer-managed certificate](customer-managed-cert.md) before it expires.
1. Configure your CDN. Keep your existing hostname so that you don't need to update your implementations.
1. Before your certificate expires, point your hostname to your CDN and switch all implementations to use it.
1. [Check your data](#check).
1. If you chose a third-party origin, contact Adobe Customer Care to mark your first-party certificate for removal.

Once your hostname points to your CDN, Adobe can't renew your first-party certificate. If any implementation still relies on the certificate when it expires, data from that implementation is lost. Contacting Adobe Customer Care lets your organization control when the certificate is removed.

## Check your data {#check}

Adobe can't validate your CDN configuration. After you route data collection through your CDN, compare your data before and after the change:

* Data continues to arrive in the expected report suites, datastreams, or datasets at the usual volume.
* Geolocation reports show your visitors' locations, not a small number of cities where your CDN's servers are located.
* Unique visitor counts don't increase unexpectedly.
* In your browser's developer tools, data collection requests to your hostname succeed, and Adobe cookies are set on the same domain as before.

## Common misconfigurations

The following issues are known to cause data quality issues or data loss. This list is not exhaustive.

| Symptom | Likely cause |
| --- | --- |
| Data stops arriving in a report suite or datastream | The CDN changes the request URL, or the origin hostname doesn't exist |
| Data stops arriving after a certificate expires | The CDN expects a first-party certificate from the origin, and that certificate expired |
| Geolocation data shows only a few cities | The CDN doesn't add the `X-Forwarded-For` header |
| Unique visitor counts increase unexpectedly | The CDN removes Adobe cookies, changes the `Host` header, or changes the cookie domain |
| Reports are missing large amounts of data | Personal data removal or WAF rules remove too much of each request |

## Frequently asked questions

+++Does this page apply to products other than Adobe Analytics?

Yes. This page applies to all Adobe products that use Adobe data collection, including Customer Journey Analytics, Adobe Experience Platform, Adobe Target, and Adobe Journey Optimizer.

+++

+++Can Adobe reject data that doesn't come through my CDN?

No. Adobe doesn't currently offer a way to restrict data collection to requests from your CDN.

+++

+++Can Adobe provide or validate a configuration for my CDN?

No. CDN configuration options differ between providers and change over time. Contact your CDN provider for help configuring your CDN, and see [Check your data](#check) for ways to identify issues with your configuration.

+++
