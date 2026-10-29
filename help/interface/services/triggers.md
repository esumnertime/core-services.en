---
description: Learn how to configure CX Enterprise Triggers.
solution: Experience Cloud
title: Overview of Triggers
uuid: dab536e3-1969-4661-919e-5b15f423fecd
feature: Admin Console
topic: Administration
role: Admin
level: Experienced
exl-id: 9dc26e2f-479b-49a5-93ce-b877559fea43
TQID: 'https://experienceleague.adobe.com/1R70ZEmKiP9VhhSRVCXHjGoJbOb7Mh8spKRm4FgNRPc'
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
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
    internal-label: Reporting
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
  - id: d3cdead0-685a-4489-9250-4bb709942f66
    internal-label: Data collection
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
    internal-label: Administration
---
# CX Enterprise Triggers

[!UICONTROL Triggers] in CX Enterprise enables you to identify, define, and monitor key consumer behaviors, then generate cross-application communication to re-engage visitors. You can use triggers in real-time decisions and personalization. For more information about using [!UICONTROL Triggers] with Adobe Campaign, see [Campaign Standard](https://experienceleague.adobe.com/docs/campaign-standard/using/integrating-with-adobe-cloud/working-with-campaign-and-triggers/using-triggers-in-campaign.html).

For example:

* Configure fast re-marketing for cart abandons or cart abandons with products removed
* Incomplete forms and applications
* Any actions or sequence of actions on site

![Trigger example](../assets/trigger-abandonment-2.png)

>[!NOTE]
>
>Triggers are not deterministic in nature. When multiple users share a browser or device, such as a shared or public device, it might not be possible to map a trigger to the correct visitor ID.

## Types of triggers

Generally, a trigger can take 15-90 minutes to launch a marketing campaign. This delay varies depending on the implementation of data collection, load on the pipeline, custom configuration of the defined trigger, and the workflow in Adobe Campaign.

* **Abandonment:** You can create a trigger to fire when a visitor views a product but does not add anything to the cart.
* **Action:** You can create triggers, for example, to fire after newsletter sign-ups, email subscriptions, or applications for credit cards (confirmations). If you are a retailer, you can create a trigger for a visitor who signs up for a loyalty program. In media and entertainment, create triggers for visitors who watch a certain show, and perhaps you want to respond with a survey.
* **Session Start and Session End:** Create a trigger for session start and session end events.

## Hold period for abandonment triggers

Abandonment triggers have a fixed hold period of one hour after a trigger session ends, whether or not the trigger fires. During this period, a new session for the same abandonment trigger does not start for that visitor, even if the visitor returns and meets the trigger conditions again. The hold period is not configurable.

## Create a CX Enterprise trigger 

Create a trigger and configure the conditions for the trigger. For example, you can specify the criteria for a trigger's rules during a visit, such as metrics like Cart Abandon, or dimensions like the product name. When the rules are met, the trigger runs.

>[!NOTE]
>
>A technical limit of 100 triggers currently exists.

1. In CX Enterprise, click ![menu](../assets/menu-icon.png), then click **[!UICONTROL Data Collection/Launch]**.
1. On the [!UICONTROL Triggers] card, click **[!UICONTROL Manage Triggers]**.
1. Click **[!UICONTROL New Trigger]**, then specify the type of trigger:

   ![Step Result](../assets/add-trigger.png)

1. Configure the trigger by completing the following fields and dragging metrics and dimension items to the rule's containers:

    | Element | Description |
    | --- | --- |
    |[!UICONTROL Name]|The friendly name for this trigger.|
    |[!UICONTROL Description]|The description of this trigger, how you use it, and so on.|
    |[!UICONTROL Report Suite]|The Analytics [report suite](https://experienceleague.adobe.com/docs/analytics/admin/manage-report-suites/report-suites-admin.html) used for this trigger. This setting identifies the reporting data to use.|
    |Visit must include<br>Visit must not include<br>Trigger after no action<br>Include meta data|You can define criteria or visitor behaviors that you want to occur, and behaviors that you do not want to occur. For example, rules for a simple cart abandonment trigger can be:<ul><li>Visit must include: [!UICONTROL Cart Addition] (metric) and  [!UICONTROL Exists]. (You can further refine the rule with a specific product view or with dimensions like Browser Types.)</li><li>Visit must not include:  [!UICONTROL Checkout].</li><li>Trigger after no action for:  10 minutes.</li><li>[!UICONTROL Include Meta Data]: Lets you add a particular [!DNL Campaign] dimension or variables that are relevant to a visitor's behavior. This field can be useful for Adobe Campaign to build the correct re-marketing email.</li></ul><br>You can specify  [!UICONTROL Any],  [!UICONTROL And] or  [!UICONTROL Or] logic within or between containers, depending on the criteria you determine are important for the rule.|
    |[!UICONTROL Container]|[!UICONTROL Containers] are where you set and store rules, conditions, or filters that define a trigger. If you want events to occur at the same time, put them in the same container. Meaning, each container processes independently at the hit level. For example, if you have two containers joined by the  And operator, you can expect the rules to qualify when two hits meet the requirements.|
    |Start new session after|Create a trigger for session start and session end events.|

    {style="table-layout:auto"}

1. Click **[!UICONTROL Save]**.
1. Use triggers for [real-time remarketing](https://experienceleague.adobe.com/docs/campaign-standard/using/integrating-with-adobe-cloud/working-with-campaign-and-triggers/about-adobe-experience-cloud-triggers.html) in [!DNL Adobe Campaign].

## Example triggers

Examples of CX Enterprise Triggers:

### Cart Abandonment trigger

For example, the following page shows rules that you might use for a [!UICONTROL Cart Abandonment] trigger, based on products viewed during a visit.

![Cart Abandonment trigger](../assets/abandonment-trigger.png)

### Referrer trigger

The following trigger fires when a hit comes in with the product of Men's Boots and referrer of Facebook. For the two criteria (*products* and *referrer*) to be evaluated in the same hit, they should be added to the same container.

![Referrer trigger](../assets/fb-boots-promo.png)

## Verifying trigger activity

To verify that a trigger has fired, use the [!UICONTROL Triggers] interface to review recent activity for the trigger. The interface displays a limited number of recent trigger events, so for implementations with high data volumes it might not show all trigger activity. Programmatic verification through an API is not currently supported.
