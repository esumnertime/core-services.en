---
title: Customer-Managed Certificates
description: Learn when to use a customer-managed certificate for first-party data collection, and your organization's responsibilities for renewing it.
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
# Customer-managed certificates

With a customer-managed certificate, your organization obtains the certificate for your first-party data collection hostname and provides it to Adobe. Adobe hosts the certificate on its data collection servers. Your organization is responsible for renewing the certificate and providing each renewed certificate to Adobe before the current certificate expires.

>[!TIP]
>
>Adobe recommends the [Adobe-managed certificate program](adobe-managed-cert.md) for most first-party implementations. It is more secure and renews certificates automatically. Use a customer-managed certificate only when your organization requires it.

## When to use a customer-managed certificate

* **You route data collection through a CDN with a first-party origin**: The [Adobe-managed certificate program](adobe-managed-cert.md) doesn't support CDN implementations. See [Configure a CDN with a first-party origin](cdn.md#first-party-origin).
* **Your security policy requires direct control of the certificate**: For example, your organization must be able to revoke the certificate through its own certificate authority, instead of requesting revocation through Adobe Customer Care.
* **Your organization requires a specific certificate authority or certificate type**: The Adobe-managed certificate program uses certificates issued by DigiCert.

## Compare certificate methods

| | Adobe-managed certificate | Customer-managed certificate |
| --- | --- | --- |
| **Who obtains the certificate** | Adobe, through DigiCert | Your organization, through a commercial certificate authority of your choice |
| **Renewals** | Adobe renews the certificate automatically | Your organization renews the certificate and provides it to Adobe before each expiration |
| **Certificate types** | Adobe provides both RSA and ECC certificates | RSA is required; ECC is recommended |
| **Supported with a CDN** | No | Yes, as a first-party origin |

## Set up a customer-managed certificate

1. Contact Adobe Customer Care to request first-party data collection with a customer-managed certificate. Include your first-party hostname, such as `data.example.com`. If your organization has data residency or compliance requirements, specify your desired [RDC type](rdc.md) in your request.
1. Adobe Customer Care provides a certificate signing request (CSR) for your hostname. Adobe generates and keeps the private key, so your organization never handles the private key. Adobe requires an RSA certificate and recommends an ECC certificate. Each certificate type requires its own CSR, so if you want an ECC certificate, ask Adobe Customer Care for an ECC CSR.
1. Submit each CSR to the desired commercial certificate authority to obtain a signed certificate. Free certificate services aren't supported. Provide the issued certificates to Adobe as instructed by Customer Care.
1. Once Adobe installs your certificate, direct traffic for your hostname to Adobe:
   * **Without a CDN**: Update your organization's DNS records as instructed by Adobe Customer Care.
   * **With a CDN**: Set your CDN origin to your first-party hostname. See [Configure a CDN with a first-party origin](cdn.md#first-party-origin).
1. If your implementation doesn't already send data to this hostname, [update your implementation](collection-domain.md#update-implementation).

## Renew your certificate {#renewals}

Your organization is responsible for renewing your certificate and providing the renewed certificate to Adobe Customer Care before the current certificate expires.

If the certificate on Adobe servers expires, browsers and CDNs reject connections to your hostname, and data from those requests is lost. A CDN can discard this data without notifying you.

Maximum certificate lifetimes are decreasing, which makes renewals more frequent. See [6.3.2 Certificate operational periods and key pair usage periods](https://cabforum.org/working-groups/server/baseline-requirements/requirements/#632-certificate-operational-periods-and-key-pair-usage-periods) in the CA/Browser Forum Server Certificate Baseline Requirements for more information. To avoid gaps in data collection:

* Track the expiration date of each certificate that you provide to Adobe.
* Assign an owner for renewals, and document the renewal process so that it continues through staff changes.

Adobe is currently exploring a self-service certificate renewal process.

## Stop using a customer-managed certificate

* **To move to the Adobe-managed certificate program**: Contact Adobe Customer Care. The Adobe-managed certificate program requires that your hostname points directly to Adobe, not to a CDN.
* **To stop using your first-party hostname**: Update all implementations that use the hostname, then contact Adobe Customer Care to remove the certificate from Adobe servers.
* **To move to a CDN with a third-party origin**: See [Move an existing first-party implementation to a CDN](cdn.md#migrate).
