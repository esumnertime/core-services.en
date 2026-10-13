---
description: Learn how to set up secure certificates for use with Adobe CX Enterprise first-party cookies.
solution: Experience Cloud,Analytics
title: Adobe-Managed Certificate Program
index: true
snippet: 'y'
feature: Cookies
topic: Administration
role: Admin
level: Experienced
exl-id: e15abde5-8027-4aed-a0c1-8a6fc248db5e
autotag-review: '2026-09-09T20:12:24.943Z'
TQID: 'https://experienceleague.adobe.com/8CSBLQaw3KOByyxxCYr1By4gyAQsDIhiofOdAzn38dg'
product_v2:
  - id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87
    internal-label: CX Enterprise
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
    internal-label: Metrics
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
    internal-label: Implementations
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
    internal-label: API
  - id: fdbb8fc9-ffa3-4b86-88fe-aa4c5a3e1bc6
    internal-label: Administration
subfeature_v2:
  - id: b75843fa-0a67-4a44-a6b1-cc627b0481dc
    internal-label: Support
  - id: c8add8f2-4250-4fd9-9cde-9707036c567d
    internal-label: Methods
  - id: d2311670-43bd-4c2e-bc98-1da2aaba9cef
    internal-label: Appmeasurement implementation
  - id: e992d880-33bc-4949-a648-aa7d410276cd
    internal-label: Validation
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
level_v2:
  - id: d378ca77-2da1-4f39-ad92-1917fe974a38
    internal-label: Experienced
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
    internal-label: Customer experience
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
    internal-label: Troubleshooting
  - id: c2be0313-b3ae-45e0-b454-d20bf54b23f2
    internal-label: Measurement
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
    internal-label: Security
  - id: d3cdead0-685a-4489-9250-4bb709942f66
    internal-label: Data collection
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
    internal-label: Administration
---
# Adobe-managed certificate program

The Adobe-managed certificate program is the recommended process for setting up first-party certificates needed for a CNAME implementation. The program is fully automated once configured. It renews certificates in a timely manner so that there is no impact to data collection due to expired certificates. The program is free for your first 100 CNAMEs.

The Adobe-managed certificate program doesn't support routing data collection through a content delivery network (CDN). If you use a CDN, see [Route data collection through a CDN](cdn.md). Organizations that need to manage their own certificates can use [customer-managed certificates](customer-managed-cert.md) instead. If you currently manage your own certificates and want to move to the Adobe-managed certificate program, contact Adobe Customer Care.

## Implementation

To implement a new certificate for first-party data collection, follow these steps:

1. Download and fill out the [First-party domain request form](cookies/assets/First_Party_Domain_Request_Form.xlsx)
1. Open a ticket with Adobe Customer Care requesting to set up first-party data collection on the Adobe-managed certificate program. If your organization has data residency or compliance requirements, specify your desired [RDC type](rdc.md) in your request.
1. Upon receiving the ticket, the Adobe representative provides you with a CNAME record. This record must be configured on your company's DNS server before Adobe can purchase the certificate on your behalf. For example, the hostname `data.example.com` points to `hiodsibxvip01.data.adobedc.net`.
1. When the CNAME record is in place on your organization's servers, Adobe works with DigiCert to purchase and install a certificate on Adobe data collection servers.
1. If you need an update to your `robots.txt` file when hosted by Adobe CNAME for first-party purposes, reach out to Customer Care with a request. Such a request is relevant when you want to update the `robots.txt` file to prevent Google from crawling your subdomains.

## Validate hostname forwarding

Once Adobe has installed the certificate, you can use one of the following methods to validate that it is working.

+++**Browser validation**

You can use any browser to validate that a certificate is installed correctly. Type your CNAME with `_check` as the path into the address bar. For example:

`data.example.com/_check`

If everything works, the browser shows `SUCCESS`. If the certificate is not installed correctly, you are issued a security warning.

+++

+++**Command line (`curl`)**

Most modern operating systems already have [`curl`](https://curl.se) installed.

Type the following into the command line:

```sh
curl data.example.com/_check
```

If everything works correctly, the console returns `SUCCESS`.

>[!TIP]
>
>You can use the `-k` flag to disable the security warning to help with troubleshooting.

+++

+++**Command line (`nslookup`)**

Type the following into the command line:

```sh
nslookup data.example.com
```

If everything works correctly, Adobe's data collection servers are returned:

```text
Server: hiodsibxvip01.corp.adobe.com
Address: 10.50.112.247

Name: example.com.ssl.d1.sc.omtrdc.net
Addresses: 63.140.37.126
    63.140.37.206
    63.140.36.51
    63.140.36.145
Aliases: data.example.com
```

+++

## Update implementation code

To use your new CNAME hostname, update your Adobe implementation once you have validated that your certificate works correctly. See [Update your implementation](collection-domain.md#update-implementation).

## Maintenance and renewals

Thirty days before your first-party certificate expires, Adobe validates whether the CNAME is still valid and in use. If so, Adobe assumes that you want to continue using the service, and automatically renews the certificate on your behalf. 

>[!IMPORTANT]
>
>If your organization's CNAME record is removed or no longer maps to the provided Adobe secure hostname, Adobe cannot renew the certificate. The entry in Adobe's system is marked for removal without further communication. This condition includes pointing your CNAME record to a content delivery network (CDN). If you plan to route data collection through a CDN, see [Move an existing first-party implementation to a CDN](cdn.md#migrate) before you change your DNS records.

## Frequently asked questions

+++Is this process secure?

Yes. The Adobe-managed certificate program is more secure than [customer-managed certificates](customer-managed-cert.md). No certificate or private key is transferred outside of Adobe and the issuing certificate authority.

+++

+++How can Adobe purchase a certificate for our domain?

The certificate can only be purchased when you have pointed the specified hostname to an Adobe-owned hostname. You delegate this hostname to Adobe and allow Adobe to purchase the certificate on your behalf.

+++

+++Can I request that the certificate be revoked?

Yes. As the owner of the domain, you are entitled to request that the certificate be revoked. Contact Adobe Customer Care to start this process.

+++

+++What encryption type is used?

Adobe works with DigiCert to issue an SHA-2 certificate.

+++

+++Does this program incur any additional cost?

Adobe offers this program to all Adobe CX Enterprise customers at no additional cost for the first 100 CNAMEs.

+++

+++What cipher security levels does Adobe offer?

Adobe offers two cipher security levels to meet varying customer needs for security on first-party data collection. These levels determine which encryption algorithms are supported for HTTPS connections with Adobe servers. Adobe regularly reviews and updates the set of supported algorithms based on current security practices. To change your cipher security settings, contact Customer Care.

* **Standard** requires TLS 1.2 or newer and at least 128-bit encryption. It is designed to provide the widest device compatibility while maintaining secure encryption.
* **High** requires TLS 1.2 or newer and removes support for weaker ciphers. It is designed for customers who desire the strongest encryption and are not concerned about support for older devices.

The following clients are known to be unable to connect with cipher security set to **High**:

* Windows 8.1 and earlier (last updated in 2018)
* Windows Phone 8.1 and earlier (last updated in 2016)
* OS X 10.10 and earlier (last updated in 2017)
* iOS 8.4 and earlier (last updated in 2015)

+++

+++What HTTPS certificate types are supported?

Adobe supports both RSA and ECC certificate types to meet varying customer needs. RSA certificates are more widely supported for clients, but ECC certificates use less processing on both the server and client side. For Adobe-managed certificates, both RSA and ECC are provided. For [customer-managed certificates](customer-managed-cert.md), RSA is required and ECC is recommended. Modern clients support both RSA and ECC. The following clients support only RSA certificates:

* Windows Vista and earlier (last updated in 2012)
* Windows Phone 8.0 and earlier (last updated in 2014)
* OS X 10.8 and earlier (last updated in 2013)
* iOS 5.1 and earlier (last updated in 2012)
* Android 4.3 and earlier (last updated in 2013)

+++

