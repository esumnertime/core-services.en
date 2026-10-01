---
description: Learn to create a [!DNL Customer Attributes] data source and upload it to CX Enterprise.
solution: Experience Cloud
title: Create and Upload a [!DNL Customer Attributes] Data Source File
uuid: 53dca789-9a91-4385-839d-c9d1aa36b9be
feature: Customer Attributes
topic: Administration
role: Admin
level: Experienced
exl-id: 21ed7c35-aac9-46f1-a50c-84e7c075209c
TQID: 'https://experienceleague.adobe.com/tnqjX4iY7OQx4XW9MjHNg8LaXB1Of6MrtLX-7efyz-E'
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
  - id: d3cdead0-685a-4489-9250-4bb709942f66
    internal-label: Data collection
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
    internal-label: Administration
---
# Create and upload customer attribute data

Create the customer attribute source (`.csv` and `.fin` files) and upload the data. You can activate the data source when you are ready. After the data source is active, share the attribute data to [!DNL Analytics] and [!DNL Target]. 

**[!DNL Customer Attributes] workflow**

![Customer Attributes workflow](assets/crs.png) 

## Prerequisites for using [!DNL Customer Attributes] {#prerequisites}

* **Group membership:** To upload the data, users must be members of the [!DNL Customer Attributes] group. You must also belong to either an Adobe Analytics group or an Adobe Target group.

  To know whether your company has access to Customer Attributes, your [!DNL CX Enterprise] administrator should log into the [CX Enterprise](https://experience.adobe.com). Navigate to **[!UICONTROL Admin Console]** > **[!UICONTROL Products]**. If *[!DNL Customer Attributes]* displays as one of the [!UICONTROL product profiles], you are ready to begin.

  Users that are added to [!DNL Customer Attributes] see the [!DNL Customer Attributes] menu item on the left side of the CX Enterprise interface.

* **Adobe Target** `at.js` (any version) or `mbox.js` version 58 or later is required for Customer Attributes.

  See [How to deploy at.js](https://experienceleague.adobe.com/en/docs/target-dev/developer/client-side/overview).

## Create a data file 

This data is enterprise customer data from your CRM. The data might include subscriber data for products, including member IDs, entitled products, most-launched products, and so on.

1. Create a `.csv` file.

   >[!NOTE]
   >
   >Later in this process, you drag and drop the `.csv` file to upload the file. However, if you [upload via FTP](t-upload-attributes-ftp.md#task_591C3B6733424718A62453D2F8ADF73B), you also need a `.fin` file with the same name as the `.csv`. 

   Sample enterprise customer data file: 

   ![Sample enterprise customer data file](assets/01_crs_usecase.png) 

1. Before continuing, review the important information in [Data File Requirements](crs-data-file.md), before you upload the file.
1. [Create a customer attribute source and upload the data](t-crs-usecase.md#create-source), described below.

## Create the attribute source and upload the data file 

Perform these steps on the _[!UICONTROL Create Customer Attribute Source]_ page in CX Enterprise.

>[!IMPORTANT]
>
>When creating, modifying, or deleting customer attribute sources, there is a delay of up to one hour before IDs begin synchronizing with the new data source. You must have administrative rights in Audience Manager to create or modify customer attribute sources. Contact Audience Manager customer Care or consulting to obtain administrative rights.

1. To open [!UICONTROL Customer Attributes], click **[!UICONTROL Apps]** ![menu](assets/menu-icon.png) > **[!DNL Customer Attributes]**.

   ![Customer Attributes page](assets/cust-attr.png)

1. Click **[!UICONTROL New]**.

   ![Step Result](assets/new-customer-attribute-source.png)
 
1. On the [!UICONTROL Create Customer Attribute Source] page, configure the following fields:

    * **[!UICONTROL Name:]** A friendly name for the data attribute source. For [!DNL Adobe Target], attribute names cannot include spaces. If an attribute with a space is passed, [!DNL Target] ignores it. Other characters not supported include: `< , >, ', "`. 
    
    * **[!UICONTROL Description:]** (Optional) A description of the data attribute source. 
    
    * **[!UICONTROL Alias ID:]** Represents a source of customer attribute data, such as a specific CRM system. [!UICONTROL Alias ID] is a unique ID that is used in your [!UICONTROL customer attribute Source] code. The ID should be unique, lowercase, with no spaces. The value that is entered in the [!UICONTROL Alias ID] field for a customer attribute source in CX Enterprise should match the values that are being passed in from the implementation (whether via Platform Data Collection or JavaScript of the Mobile SDK.) 

      >[!IMPORTANT]
      >
      >Deleting a data source associated with an Alias ID does not make the Alias ID available, as the Alias ID is saved in multiple services and used to map profiles between them.
            
      The Alias ID corresponds to certain areas where you set additional customer ID values. For example: 
    
        * **Tags:** The Alias ID corresponds to the *Integration Code* value under [!UICONTROL customer Settings], in the [[!UICONTROL Experience Cloud ID Service]](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html) tag extension. 

        * **Visitor ID Service:** The Alias ID corresponds to the additional [customer IDs](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html) that you can associate with each visitor. 
        
          For example, *"crm_id"* in: 
        
          ```
          "crm_id":"67312378756723456"
          ```
       
        * **iOS:** The Alias ID corresponds to *"idType"* in [visitorSyncIdentifiers:identifiers](https://experienceleague.adobe.com/docs/mobile-services/ios/overview.html). 
        
          For example: 
               
          `[ADBMobile visitorSyncIdentifiers:@{@<`**`"idType"`**`:@"idValue"}];` 
        
        * **Android&trade;:** The Alias ID corresponds to *"idType"* in [syncIdentifiers](https://experienceleague.adobe.com/docs/mobile-services/android/overview.html). 
        
          For example: 
        
          `identifiers.put(`**`"idType"`**`, "idValue");`
        
          See [Leveraging multiple data sources](crs-data-file.md#section_76DEB6001C614F4DB8BCC3E5D05088CB) for additional information about data processing regarding the Alias ID field and customer IDs. 

    * **[!UICONTROL Namespace Code:]** Use this value to identify the customer attribute source when using the [IdentityMap](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/identity/overview) as part of an AEP WebSDK Implementation.

1. Click **[!UICONTROL Save]**.

## Upload the file {#upload-customer-attributes}

The customer attribute record is created, and you can upload the file by editing the customer attribute.

1. On the [!DNL Customer Attributes] page, click the attribute source.

1. On the [!UICONTROL Edit Customer Data Source] page, click **[!UICONTROL File Upload]**.

   ![File Upload and Schema Validation](assets/file-upload-schema-validation.png) 

1. Drag and drop the `.csv` or `.zip` or `.gzip` data file into the drag-and-drop window.
    
   >[!IMPORTANT]
   >
   >Specific data file requirements exist. See [Data File Requirements](crs-data-file.md) for more information. 
    
   After uploading the file, table data is displayed under the [!UICONTROL File Upload] heading on this page. You can validate the schema, configure subscriptions, or set up the FTP. 
    
   ![attributes](assets/file_upload_attributes.png) 
  
* **[!UICONTROL Unique customer ID:]** Displays how many unique IDs you have uploaded to this attribute source. 
    
* **[!UICONTROL Customer-Provided IDs Aliased to Experience Cloud Visitor IDs:]** Displays how many IDs have been aliased to ECIDs. 
    
* **[!UICONTROL Customer-Provided IDs with High Alias Counts:]** Displays the count of customer-provided IDs with 500 or more aliased ECIDs. These customer-provided IDs most likely do not represent individuals but rather some sort of shared login. The system distributes the attributes associated with these IDs to the 500 most recent aliased ECIDs, until the alias count reaches 10,000. Then, the system invalidates the customer-provided ID and no longer distributes associated attributes.
    
## Validate the schema {#validate-schema}

The validation process lets you map display names and descriptions to uploaded attributes (strings, integers, numbers, and so on). You can also delete attributes by updating the schema.

See [Validate the schema](validate-schema.md). 

To delete attributes, see [(Optional) Update the schema (deletes attributes)](t-crs-usecase.md). 

## (Optional) Update the schema (delete attributes) 

How to delete attributes and replace attributes in the schema.

1. On the [!UICONTROL Edit Customer Attribute Source] page, remove the **[!UICONTROL Target]** or **[!UICONTROL Analytics]** subscription (under **[!UICONTROL Configure Subscriptions]**).

1. [Upload a new data file with updated fields](t-crs-usecase.md).

## Configure subscriptions and activate the attribute source 

Configuring a subscription sets up the data flow between CX Enterprise and applications. Activating the attribute source allows the data to flow to subscribed applications. The customer records you have uploaded are matched up with incoming ID signals from your web site or application.

See [Configure subscriptions and activate the data source](subscription.md). 

## Use [!DNL Customer Attributes] data in Adobe Analytics 

With the data now available in applications like Adobe Analytics, you can report on the data, analyze it, and take the appropriate action in your marketing campaigns.

The following example shows an [!DNL Analytics] segment based on the uploaded attributes. This segment shows [!DNL Photoshop Lightroom] subscribers whose most-launched product is Photoshop. 

![Analytics segment based on the uploaded attributes](assets/08_crs_usecase.png) 

When you publish a segment to CX Enterprise, it becomes available in CX Enterprise Audiences and Audience Manager. 

## Use [!DNL Customer Attributes] data in Adobe Target 

In [!DNL Target], you can select a customer attribute from the [!UICONTROL Visitor Profile] section when creating an audience. All customer attributes have the prefix `crs.` in the list. Combine these attributes as required with other data attributes to build audiences.

![Use Customer Attributes in Adobe Target](assets/crs-add-attribute-target.png) 

See [Create an Audience](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/audiences.html) in [!DNL Target] help.
