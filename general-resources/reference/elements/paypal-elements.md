---
description: Learn how to use the PayPal elements.
---

# PayPal elements

With DigitalRiver.js, you can create a PayPal element that will wrap the PayPal Checkout.js library and automatically handle payment authorization. The element follows the same creation and event structure as other DigitalRiver.js elements.

### Creating a PayPal element

To create a PayPal element, use the `createElement` function exposed through the DigitalRiver Object. This object follows the same pattern and allows for the same [custom classes](./#custom-classes) and [styles ](./#custom-styles)as other elements.

{% tabs %}
{% tab title="Example" %}
{% code overflow="wrap" %}
```javascript
var paypal = digitalriverpayments.createElement('paypal', {
    style: {
        label: 'checkout',
        size: 'responsive',
        color: 'gold',
        shape: 'pill',
        layout: 'horizontal',
        fundingicons: 'false',
        tagline: 'false'
    },
    sourceData: {
        "type": "payPal",
        "sessionId": "ea03bf6f-84ef-4993-b1e7-b7d5ecf71d1f",
        "payPal": {
            "returnUrl": "https://returnUrl.com",
            "cancelUrl": "https://cancelUrl.com"
        }
    }
});
 
paypalElement.mount('drjs-paypal');
```
{% endcode %}
{% endtab %}
{% endtabs %}

#### PayPal element data object

| Key        | Required | Description                                                                                                                                                                                       |
| ---------- | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| style      | Optional | A [PayPal element style option objec](paypal-elements.md#paypal-element-style-options)t.                                                                                                          |
| sourceData | Required | A [PayPal Source Details object](../../../payments/payments-solutions/digitalriver.js/payment-methods/paypal.md#paypal-source-details-object). See the PayPal documentation for more information. |

#### PayPal element style options

| Option       | Required | Description                                                                        |
| ------------ | -------- | ---------------------------------------------------------------------------------- |
| label        | Optional | The label that appears on the PayPal button. The default is `blank`.               |
| color        | Optional | The color of the PayPal button. The default is `gold`.                             |
| shape        | Optional | The shape of the PayPal button. The default is `pill`.                             |
| layout       | Optional | The layout of the PayPal button. The default is `horizontal`.                      |
| fundingicons | Optional | Indicates whether the funding icons appear on the button. The default is `false`.  |
| tagline      | Optional | Indicates whether the tagline appears on the PayPal button. The default is `none`. |

### PayPal element functions

#### paypal.mount();

Use this function to place the created PayPal element on your page.&#x20;

{% tabs %}
{% tab title="Example" %}
```javascript
<div id="paypal-container"></div>
 
paypal.mount('paypal-container');
```
{% endtab %}
{% endtabs %}

#### paypal.unmount();

Use this function to remove the PayPal element from your page. You can re-add the element to your page by calling `mount()`.

{% tabs %}
{% tab title="Example" %}
```javascript
<div id="paypal-container"></div>
 
paypal.mount('paypal-container');
```
{% endtab %}
{% endtabs %}

#### paypal.destroy();

Use this function to remove the PayPal element from your page as well as remove its functionality. You cannot re-add the element to your page via `mount()`.

{% tabs %}
{% tab title="Example" %}
```javascript
paypal.destroy();
```
{% endtab %}
{% endtabs %}

#### paypal.update();

Call this function to update the PayPal element's data.&#x20;

{% tabs %}
{% tab title="Example" %}
{% code overflow="wrap" %}
```javascript
let paypalData = {
    style: {
        label: 'checkout',
        size: 'responsive',
        color: 'gold',
        shape: 'pill',
        layout: 'horizontal',
        fundingicons: 'false',
        tagline: 'false'
    },
    sourceData: {
        "type": "payPal",
        "sessionId": "ea03bf6f-84ef-4993-b1e7-b7d5ecf71d1f",
        "payPal": {
            "returnUrl": "https://returnUrl.com",
            "cancelUrl": "https://cancelUrl.com"
        }
    }
}
 
paypal.update(paypalData);
```
{% endcode %}
{% endtab %}
{% endtabs %}

### PayPal element events–paypal.on('event', handler);

&#x20;Call this function to listen to events that can be used to build and enhance your purchase flows.

| Event                               | Triggered When                                                                              |
| ----------------------------------- | ------------------------------------------------------------------------------------------- |
| [ready](paypal-elements.md#ready)   | The created element is loaded and ready to accept an update request.                        |
| [click](paypal-elements.md#click)   | A shopper clicked the element's button.                                                     |
| [cancel](paypal-elements.md#cancel) | The customer has canceled the experience.                                                   |
| [source](paypal-elements.md#source) | The customer has authorized the payment and a source, and Drop-In returned associated data. |

#### Ready

The Ready event triggers when the PayPal Element has loaded and is available to take an `update()` call.

{% tabs %}
{% tab title="Example" %}
{% code overflow="wrap" %}
```javascript
paypal.on('ready', function(event) {
    //paypal element is ready and can accept an update call
});
```
{% endcode %}
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Response object" %}
```javascript
{
    elementType: "paypal"
}
```
{% endtab %}
{% endtabs %}

#### Click

The Click event triggers when the customer clicks a PayPal Element.

{% tabs %}
{% tab title="Example" %}
```javascript
paypal.on('click', function(event) {
    //receive the event
}
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Response object" %}
```javascript
{
    elementType: "paypal"
}
```
{% endtab %}
{% endtabs %}

#### Cancel

The Cancel event triggers when the customer closes the PayPal Element Payment Request interface.

{% tabs %}
{% tab title="Example" %}
```javascript
paypal.on('cancel', function(event) {
    //receive the event
}
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Response object" %}
```javascript
{
    elementType: "paypal"
}
```
{% endtab %}
{% endtabs %}

#### Source

The Source event triggers when the Customer completes their interaction with the Payment Request interface, and creates a Payment Source. The emitted object will be a [Payment Request Response object](../digital-river-payment-objects.md#payment-request-response-object).

{% tabs %}
{% tab title="Example" %}
```javascript
paypal.on('source', function(event) {
    var source = event.source;
  
    //pass the source to your back end for further processing.
});
```
{% endtab %}
{% endtabs %}

## Pay in 4

{% hint style="info" %}
**Additional setup required**: If you are interested in promoting Pay in 4, contact your Account Manager. The Account Manager will send setup instructions for PayPal in 4 banners.
{% endhint %}

Pay in 4 is a credit card installment product automatically provided by PayPal when a customer signs in to PayPal Express or PayPal Checkout. This option appears by default when a customer purchases a physical product, and the order value is between $30 and $600. When they complete their purchase, they make a down payment. They pay the rest in 3 payments–one every two weeks. This option is only available in the US.

When a customer selects this payment method, a "soft hit" shows up in their credit report.
