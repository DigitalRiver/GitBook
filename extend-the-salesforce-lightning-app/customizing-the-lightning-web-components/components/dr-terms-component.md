---
description: Learn how to use the DR terms component.
---

# DR terms component

Use the `drb2b_drTermsElement` component to display the Digital River terms and conditions. The shopper must select the check box in this component to accept the Digital River terms and conditions. You can configure this component in the flow.

You can use the `drb2b_drTermsElement` component with the [Bypass Validation designer attribute](../designer-attributes.md). If the **Bypass Validation** value is **true**, the system bypasses validation for the `drb2b_drTermsElement` component.

{% hint style="info" %}
If you choose to bypass the validation, you must add a custom validation using the event triggered by the `drb2b_drTermsElement` component to ensure the shopper agrees to the terms and conditions.
{% endhint %}

This component uses a visual force page where DigitalRiver.js and DR.CSS are loaded.

The Lightning Messaging service triggers an event every time a shopper selects or clears the check box next to the Digital River terms and conditions. The event data includes `isSelected` with a value of `true` or `false`. The `true` value indicates the shopper selected the check box and the `false` value indicates the shopper cleared the check box. The event data also contains the `termsString` variable which contains the text for the terms the shopper agrees to. The text includes any raw HTML tags returned by Digital River. This allows you to save the terms the shopper agreed to if needed.

You can subscribe to this event. This event is triggered when the shopper selects the check box to agree to the Digital River terms and conditions or a custom validation.

## Subscribing to an event

Import the `digitalriverv3__DRTermsMessageChannel__c` **message channel** and **message service** into a custom javascript file as shown in below.

{% code title="Import example" %}
```javascript
import { subscribe, MessageContext } from 'lightning/messageService';
import toggleCheckboxMS from '@salesforce/messageChannel/digitalriverv3__DRTermsMessageChannel__c';
```
{% endcode %}

Declare the `messageContext` variable as shown below.

{% code title="messageContext example" %}
```javascript
 @wire(MessageContext) messageContext;
```
{% endcode %}

Subscribe to an event as shown below.

{% code title="Subscribe example" %}
```json
 subscribeToMessageChannel() {
        if (!this.subscription) {
            this.subscription = subscribe(
                this.messageContext,
                toggleCheckboxMS,
                (message) => this.handleMessage(message),
            );
        }
    }
 
   
 
    handleMessage(message){
       // implement logic here
    }

```
{% endcode %}

The message contains the following parameters.

| Parameter    | Description                                                                                                                           |
| ------------ | ------------------------------------------------------------------------------------------------------------------------------------- |
| `isSelected` | The value is `true` or `false` depending on whether or not the shopper agreed to the terms and conditions by selecting the check box. |
| `termString` | The value contains the HTML encoded text for the terms and conditions displayed to the shopper.                                       |

{% hint style="warning" %}
If you want to add the `drb2b_drTermsElement`component to the Place Order page, you can only use one `drb2b_orderSummary`component in the flow or template.
{% endhint %}
