---
description: Learn how to use the Buyer Info component.
---

# Buyer info component

Use this `drb2b_buyerInfo` component with the `drb2b_taxCertificateCheckout` component.  The `drb2b_buyerInfo` publishes an event and the [`drb2b_taxCertificateCheckout` ](tax-certificate-component.md)listens for the event triggered by the `drb2b_buyerInfo` component. The `drb2b_taxCertificateCheckout` is dependent on `drb2b_buyerInfo` component.&#x20;

If you use a custom component instead of the `drb2b_buyerinfo` component, you must:

* Populate the following fields in the `WebCart` object:
  * `Buyer_Name__c`&#x20;
  * `Buyer_Email__c`
  * `Buyer_Phone__c`
  * `BillingAddress`
  * `DR_Customer_Type__c`
* Provide the selected ship-to contact point address ID to the OOTB flow which populates the ship-to address on the Cart Delivery Group object.
* [Publish an event](buyer-info-component.md#publishing-an-event) from the custom component using LMS (Lightning Message Service) as `drb2b_taxCertificateCheckout` is dependent on this component.

## Publishing an event

Import the `TaxCertificateMessageChannel__c` **message channel** and **message service** into a custom javascript file.

Declare the message context variable as shown below.

```javascript
import { publish, MessageContext } from 'lightning/messageService';
import toggleShowTC from '@salesforce/messageChannel/TaxCertificateMessageChannel__c';
```

Declare the `messageContext` variable as shown below.

{% code title="messageContext example" %}
```javascript
 @wire(MessageContext) messageContext;
```
{% endcode %}

To enable the `drb2b_taxCertificateCheckout` component, set the `showLink` value to `true` when publishing the event.

{% code title="Publish example" %}
```javascript
publish(this.messageContext, toggleShowTC, {
             showLink: true;
        }};
```
{% endcode %}

{% hint style="info" %}
Set the `showLink` value to `true` only when the shopper indicates that the purchase `type` is `business` and the country is the `United States`.  For digital purchases, check the country of the Billing Address. For physical and mixed cart purchases, check the country of the Shipping Address. In all other cases, set the `showLink` value to `false`.  Send the event any time the shopper updates these values.
{% endhint %}
