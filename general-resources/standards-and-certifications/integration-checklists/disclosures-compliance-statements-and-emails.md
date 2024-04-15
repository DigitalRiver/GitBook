---
description: >-
  Learn more about the standards related to displaying Digital River policies,
  notices, and terms.
---

# Disclosures, compliance statements, and emails

The [checklist items](disclosures-compliance-statements-and-emails.md#integration-checklist) and [standards](disclosures-compliance-statements-and-emails.md#integration-standards) in this section cover how to display the Digital River policies, notices, and terms that necessary for maintaining [MOR/SOR](../../glossary.md#merchant-of-record-seller-of-record-mor-sor) compliance. This includes how to display the proper localized text and links on various pages in your integration and do the same in customer email notifications.

## Integration checklist

Click any checklist item to be provided more detail on how to meet the integration standard.

* [ ] [Do you use the DigitalRiver.js compliance element to retrieve all required disclosure elements?](disclosures-compliance-statements-and-emails.md#integrate-method-to-retrieve-disclosure-elements)
* [ ] [During the review step in the checkout process, do you display Digital River's reseller disclosure terms, provide a checkbox for the customer to accept the terms, and then acquire active acceptance?](disclosures-compliance-statements-and-emails.md#present-reseller-disclosure-terms-and-acquire-acceptance)
* [ ] [At certain stages of the order lifecycle, does your integration send event-driven email notifications to customers that contain the proper disclosures?](disclosures-compliance-statements-and-emails.md#send-customer-email-notifications-that-contain-the-necessary-disclosures)

#### Subscription specific

* [ ] [Does your integration send the required subscription notifications?](disclosures-compliance-statements-and-emails.md#send-subscription-notifications)
* [ ] [Do you display and acquire the customer's acceptance of the autorenewal subscription terms?](disclosures-compliance-statements-and-emails.md#disclose-the-autorenewal-terms)

## Integration standards

These integration standards relate to disclosures and compliance statements:

### Integrate method to retrieve disclosure elements

In the footer of all checkout pages, your integration must have a [compliance element](../../../developer-resources/reference/elements/compliance-elements.md) that automatically retrieves and renders the required links to Digital River's policies, notices, and terms.

When you pass this compliance element to the [`createElement()`](../../../payments/payment-integrations-1/digitalriver.js/reference/digitalriver-object.md#creating-elements) method, you can include two parameters: `locale` and `entity.` By specifying these parameters, the compliance element returns localized text and hyperlinks.

The optional `locale` sets the language of the disclosure information presented to the customer. The required `entity` should be the Digital River [selling entity](../../../integration-options/checkouts/creating-checkouts/selling-entities.md) that is facilitating the transaction. During the checkout process, retrieve the [`locale`](../../../integration-options/checkouts/creating-checkouts/designating-a-locale.md) and `sellingEntity.id` returned by the [Checkouts API](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) and then pass these values to the `createElement()` method.

### Present reseller disclosure terms and acquire acceptance

In the footer of all your checkout pages, you should use the [get compliance details method ](../../../payments/payment-integrations-1/digitalriver.js/reference/digitalriver-object.md#digitalriver-compliance-getdetails-businessentitycode-locale)to render the required links to Digital River's policies, notices, and terms. Each `url` returned by this method is contained within an easily identifiable hash table (such as `termsOfSale`, `privacyPolicy` or `legalNotice`) that simplifies placement.

{% hint style="warning" %}
In some regions and locales, additional disclosures may be required. For your convenience, they are also returned by the compliance method.
{% endhint %}

On the review order page of your checkout flow, use `resellerDisclosure.localizedText` and `resellerDisclosure.url` to both display and provide a link to Digital River's reseller disclosure.

On the same page, use `confirmDisclosure.localizedText` to provide Digital River's terms and display a checkbox control to acquire the customer's active acceptance of those terms.

### Send customer email notifications that contain the necessary disclosures

At certain stages in the order life cycle, your integration should respond to [Digital River emitted events](../../../order-management/events-and-webhooks-1/events-1/) by sending email notifications to the customer. At a minimum, you should email the customer when the order is confirmed, cancelled, shipped, and refunded. Either [programmatically](../../../order-management/events-and-webhooks-1/webhooks/creating-a-webhook.md#create-a-webhook-programmatically) or in [Digital River Dashboard](../../../order-management/events-and-webhooks-1/webhooks/creating-a-webhook.md#create-a-webhook-from-the-dashboard), you can configure webhooks to detect these events, and then your integration can respond by emailing the customer.

Customer emails must also contain the required disclosures, similar to those in the [footer of your checkout experience pages](disclosures-compliance-statements-and-emails.md#present-reseller-disclosure-terms-and-acquire-acceptance), that you retrieve with the [get compliance details method.](../../../payments/payment-integrations-1/digitalriver.js/reference/digitalriver-object.md#digitalriver-compliance-getdetails-businessentitycode-locale)

### Send subscription notifications

In the [Subscription Notifications](https://digitalriver.service-now.com/kb?id=kb\_article\_view\&sys\_kb\_id=785fc80adbd8341046e8d6aa48961907) article (_click_ [_here_](../compliance-requirements.md#accessing-the-learning-tools) _for access information_), you can find a complete list of the required and recommended subscription-related notifications and what should be included in each.

### Disclose the autorenewal terms

When customers purchase an auto-renewing subscription, you must disclose the terms and acquire the customer's active acceptance of them. For more information on the specific disclosures that are required, refer to the [Subscriptions and Auto-Renewal Considerations](https://digitalriver.service-now.com/kb?id=kb\_article\_view\&sys\_kb\_id=23d0d88adb5c341046e8d6aa489619ae) article (_click_ [_here_](../compliance-requirements.md#accessing-the-learning-tools) _for access information_).

## API interfaces

| Documentation                                                                                                                                                              | Direct API | PHP SDK |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- | ------- |
| [DigitalRiver.js](https://github.com/DigitalRiver/GitBook/blob/Digital-River-API-latest/payments/payment-integrations-1/digitalriver.js#getting-started)                   |            |         |
| [dr.js compliance](../../../payments/payment-integrations-1/digitalriver.js/reference/digitalriver-object.md#digitalriver-compliance-getdetails-businessentitycode-locale) |            |         |
