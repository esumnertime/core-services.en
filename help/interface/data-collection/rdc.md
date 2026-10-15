---
title: Regional Data Collection
description: Learn about regional data collection in CX Enterprise.
exl-id: 295e9736-2a58-48a8-9968-5dfa33b70d95
TQID: https://experienceleague.adobe.com/hjHQDRoNOP2e6pKhKHB9DZaII2o8eJVzL5wjRzaMFwM
product_v2:
  - id: e1971122-7081-4556-9222-8a31bd71800c
    internal-label: Experience Cloud Services
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
topic_v2:
  - id: c2be0313-b3ae-45e0-b454-d20bf54b23f2
    internal-label: Measurement
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
    internal-label: Optimization
  - id: d3cdead0-685a-4489-9250-4bb709942f66
    internal-label: Data collection
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
    internal-label: Administration
---
# Regional Data Collection

Adobe CX Enterprise uses regional data collection (RDC) so that interactions between your visitors and Adobe happen as close to your visitors as possible. Data collected locally at an edge site is securely forwarded to a core site for processing. Once processed, the data is available to Adobe CX Enterprise products and services.

The regional data collection workflow provides several benefits:

* **Performance**: With RDC, your visitors connect to the closest edge site. This optimization provides the fastest response time, resulting in more accurate tracking and faster loading times.
* **Redundancy**: If there is a disruption in communication between any edge site and core site, Adobe's infrastructure saves data locally, then forwards it to the core site when communications are restored. Adobe can also route traffic to other edge sites if a specific location experiences interruptions.

## First-party data collection

First-party data collection uses a CNAME implementation to route data to Adobe through your own domain. Your RDC type is selected as part of the [Adobe-Managed Certificate Program](adobe-managed-cert.md) setup process. To check or update your RDC type, contact your Adobe Account Team. The following RDC types and associated data centers are available:

| RDC Type | Data Collection Centers |
| --- | --- |
| Global (default) | Oregon, Virginia, Ireland, Paris, Mumbai, Singapore, Tokyo, Sydney |
| Global + China* | Beijing*, Oregon, Virginia, Ireland, Paris, Mumbai, Singapore, Tokyo, Sydney |
| Americas only | Oregon, Virginia |
| Europe only | Ireland, Paris |
| Asia Pacific only | Mumbai, Singapore, Tokyo, Sydney |
| China only* | Beijing |

_*China RDC requires the China Performance Optimization add-on package, and only applies to Adobe Analytics using AppMeasurement data collection. Other CX Enterprise services and Web SDK data collection are not supported. Contact your Adobe Account Team to learn more about the China Performance Optimization add-on package._

If you [route data collection through a CDN](cdn.md), region-locked RDC types require a first-party origin with a [customer-managed certificate](customer-managed-cert.md).

## Third-party data collection

Third-party data collection uses cookie domains that don't match your website domain. Examples include `adobedc.net`, `omtrdc.net`, and `2o7.net`.

| RDC Type | Data Collection Centers |
| --- | --- |
| Default | Oregon, Virginia, Ireland, Paris, Mumbai, Singapore, Tokyo, Sydney |
| Default + China* | Beijing*, Oregon, Virginia, Ireland, Paris, Mumbai, Singapore, Tokyo, Sydney |

_*Requires the China Performance Optimization add-on package. See the first-party data collection section above for details._

Data routed through a CDN to a [third-party origin](cdn.md#third-party-origin) always uses the default RDC type.
