---
description: Learn how to trigger connector events for the customer credit feature.
---

# Publishing connector events

To implement the customer credit feature, in addition to calling the methods described above, you must publish the events that interact with the components included in the connector.  This section describes those events.

## Reloading Drop-In

You should publish the event to reload Drop-in after applying or removing a partial amount from customer credit. &#x20;

### Publishing an event to reload the Drop-in component

{% hint style="info" %}
**Prerequisite**: Publish this event after calling [`addCustomerCreditSourceToCheckout` ](addcustomercreditsourcetocheckout.md)or [`deattachPaymentToCheckout` ](deattachpaymenttocheckout.md)methods.
{% endhint %}

To publish the event to reload the Drop-in (drb2b\_dropin) component, import the `DigitalRiverMessageChannel__c` **message channel** and **message service** into the customer credit javascript file.

{% code title="Import example" %}
```javascript
import {publish, MessageContext } from 'lightning/messageService';
import dr_lms from '@salesforce/messageChannel/ digitalriverv3__ DigitalRiverMessageChannel__c';
```
{% endcode %}

Declare the `messageContext` variable as shown in below.

{% code title="messageContext example" %}
```javascript
@wire(MessageContext) messageContext; 
```
{% endcode %}

Publish the event. When publishing the event, use the `reloadDropin` value for the `purpose` parameter as shown in the following example:

{% code title="Publish example" %}
```javascript
publish(this.messageContext, dr_lms, {
  purpose: 'reloadDropin' 
  });
```
{% endcode %}

### Reloading the checkout summary component

{% hint style="info" %}
**Prerequisite**: Publish this event after calling [`addCustomerCreditSourceToCheckout` ](addcustomercreditsourcetocheckout.md)or [`deattachPaymentToCheckout` ](deattachpaymenttocheckout.md)methods.
{% endhint %}

Reload the checkout summary component to reflect the latest values whenever a shopper adds or removes a source from the checkout. This will update the UI with the latest values, including the amount contributed and the amount remaining to be contributed.

To publish an event to reload the checkout summary (`drb2b_checkoutSummary`) component, import the `DigitalRiverMessageChannel__c` **message channel** and **message service** into the customer credit javascript file.

{% hint style="info" %}
If you already imported the `DigitalRiverMessageChannel__c` **message channel** and **message service** into the customer credit JavaScript file, you can skip this step.
{% endhint %}

{% code title="Import example" %}
```javascript
import {publish, MessageContext } from 'lightning/messageService';
import dr_lms from '@salesforce/messageChannel/ digitalriverv3__ DigitalRiverMessageChannel__c';
```
{% endcode %}

Declare the `messageContext` variable as shown below.

{% code title="messageContext example" %}
```javascript
 @wire(MessageContext) messageContext;
```
{% endcode %}



{% hint style="info" %}
If you already declared the `messageContext` variable, you can skip this step.
{% endhint %}

Publish the event. When publishing the event, use the `reloadCheckoutSummary` value for the `purpose` parameter as shown in the following example:

{% code title="Publish example" %}
```javascript
publish(this.messageContext, dr_lms, {
            purpose: 'reloadCheckoutSummary' 
        });
```
{% endcode %}

###
