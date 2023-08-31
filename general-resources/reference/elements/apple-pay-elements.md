---
description: Learn how to use Apple Pay elements.
---

# Apple Pay elements

‌With DigitalRiver.js, you can create an Apple Pay element and interact with Apple Pay.‌

## Creating an Apple Pay element

To create an Apple Pay element, you should use the `createElement` function exposed through the DigitalRiver object.

{% tabs %}
{% tab title="Example" %}
{% code overflow="wrap" %}
```javascript
var paymentRequestData = digitalriver.paymentRequest({
        country: "US",
        currency: "USD",
        total: {
            label: "Order Total",
            amount: 100
        },
        displayItems: lineItems,
        shippingOptions: shippingOptions,
        style: {
            buttonType: "plain",
            buttonColor: "dark",
            buttonLanguage: "en"
        }
    });
 
 
var applepay = digitalriver.createElement('applepay', paymentRequestData);
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Apple Pay element styles and customization

Use the following styles and types to create an Apple Pay button that you can more closely integrate into your experience.‌

### **Button type**‌

* Choose one of the following button types:
* `plain`: <img src="../../../.gitbook/assets/applepay-button-black.png" alt="" data-size="original">&#x20;
* `buy`: <img src="../../../.gitbook/assets/buywithapplepay-button-black.png" alt="" data-size="original">

### **Button color**‌

Choose one of the following button colors:

* ​`light`: <img src="../../../.gitbook/assets/applepay-button-white.png" alt="" data-size="original">&#x20;
* `light-outline`: <img src="../../../.gitbook/assets/applepay-button-white-outline.png" alt="" data-size="original">&#x20;
* `dark`: <img src="../../../.gitbook/assets/applepay-button-black.png" alt="" data-size="original">&#x20;

## Apple Pay element functions

### applepay.canMakePayment();

Call this function to determine whether or not the Customer's browser supports Apple Pay.

{% tabs %}
{% tab title="Example" %}
{% code overflow="wrap" %}
```javascript
if(applepay.canMakePayment()) {
    //can make payment with this element
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

### applepay.mount();

Call this function to place the created Apple Pay element on your page.

{% tabs %}
{% tab title="Example" %}
{% code overflow="wrap" %}
```javascript
<div id="apple-pay"></div>
 
if(applepay.canMakePayment()) {
    //can make payment with this element
    applepay.mount('apple-pay');
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

### applepay.show();

Call this function to show the Apple Pay Payment Request interface. This will automatically happen when using the element. If you'd like to trigger via another mechanism, call it part of the user interaction (click handler).

{% tabs %}
{% tab title="Example" %}
```javascript
applepay.show();
```
{% endtab %}
{% endtabs %}

### applepay.unmount();

Call this function to remove the Apple Pay element from your page. The element may be re-added to your page by calling `mount()`.

{% tabs %}
{% tab title="Example" %}
```javascript
applepay.unmount();
```
{% endtab %}
{% endtabs %}

### applepay.destroy();

Call this function to remove the Apple Pay element from your page and its functionality. You cannot re-add the element to your page via `mount()`.

{% tabs %}
{% tab title="JavaScript" %}
```javascript
applepay.destroy();
```
{% endtab %}
{% endtabs %}

### applepay.update();

Call this function to update the Apple Pay element's data. Calling this will merge your changes into the already existing Payment Request object.

{% tabs %}
{% tab title="Example" %}
{% code overflow="wrap" %}
```javascript
var paymentRequest = digitalriver.paymentRequest({
        country: "US",
        currency: "USD",
        total: {
            label: "Order Total",
            amount: 100
        },
        displayItems: lineItems,
        shippingOptions: shippingOptions,
        style: {
            buttonType: "plain",
            buttonColor: "dark",
            buttonLanguage: "en"
        }
    });
 
 
applepay.update(paymentRequest);
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Apple Pay element events — applepay.on('event', handler);

The Apple Pay element can receive the following events by creating an event listener. Use this function to listen to events that can be used to build and enhance your purchase flow.

| Event                                                                    | Triggered When                                                                                                                                            |
| ------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [​ready​](apple-pay-elements.md#ready)                                   | The created element is loaded and ready to accept an update request.                                                                                      |
| [​click​](apple-pay-elements.md#click)                                   | A shopper clicked the element's button.                                                                                                                   |
| ​[cancel​](apple-pay-elements.md#cancel)                                 | The customer has canceled the experience.                                                                                                                 |
| [​shippingoptionchange​](apple-pay-elements.md#shipping-option-change)   | The customer has chosen a different shipping option than was previously selected. You should use this data to re-price your order totals (if applicable). |
| [​shippingaddresschange​](apple-pay-elements.md#shipping-address-change) | The customer has chosen a different address than was previously selected. You should use this data to re-price your order totals (if applicable).         |
| ​[source​](apple-pay-elements.md#source)                                 | The customer has authorized the payment and a source, and DigitalRiver.js returned associated data.                                                       |

### Source

The Source event emits when the customer completes their interaction with the Payment Request interface, and creates a Payment Source. The emitted object will be a [Payment Request Response object](../digital-river-payment-objects.md#payment-request-response-object).

{% tabs %}
{% tab title="Example" %}
{% code overflow="wrap" %}
```javascript
applepay.on('source', function(event) {
    var source = result.source;
 
 
    //pass the source to your back end for further processing.  
});
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Ready

The Ready event emits when the Apple Pay Element has loaded and is available to take an `update()` call.

{% tabs %}
{% tab title="Example" %}
{% code overflow="wrap" %}
```javascript
applepay.on('ready', function(event) {
    //apple pay element is ready and can accept an update call
});
```
{% endcode %}
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Repsonse object" %}
```javascript
{
    elementType: "applepay"
}
```
{% endtab %}
{% endtabs %}

### Click

The Click event emits when the customer clicks an Apple Pay Element.

{% tabs %}
{% tab title="Example" %}
```javascript
applepay.on('click', function(event) {
    //do stuff
}
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Response object" %}
```
{
    elementType: "applepay"
}
```
{% endtab %}
{% endtabs %}

### Cancel

The Cancel event emits when the customer closes the Apple Pay Element Payment Request interface.

{% tabs %}
{% tab title="Example" %}
```javascript
applepay.on('cancel', function(event) {
    //do stuff
}
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Response object" %}
```
{
    elementType: "applepay"
}
```
{% endtab %}
{% endtabs %}

### Shipping option change

The Shipping Option Change event emits when the Customer selects a different Shipping Option within the Payment Request interface. The event will emit the following object structure.

<table><thead><tr><th width="214.33333333333331">Key</th><th>Type</th><th>Description</th></tr></thead><tbody><tr><td>updateWith</td><td>Function</td><td>Calling this function with a <a href="../digital-river-payment-objects.md#payment-request-details-update-error-object">Payment Request Details Update object</a> merges your updates into the current Payment Request object.</td></tr><tr><td>shippingAddress</td><td>A <a href="../digital-river-payment-objects.md#payment-request-details-update-error-object">Payment Request Details Update object</a></td><td>A <a href="../digital-river-payment-objects.md#payment-request-shipping-option-object">Payment Request Shipping Option object</a> contains the details of the customer's chosen Shipping Option.</td></tr></tbody></table>

{% tabs %}
{% tab title="Example" %}
{% code overflow="wrap" %}
```javascript
applepay.on('shippingoptionchange', function(event) {
    var shippingOption = event.shippingOption;
  
  
    //create a Payment Request Details Update Object
    var newDetails = createPaymentRequestDetailsUpdateObject();
    event.updateWith(newDetails);
});
```
{% endcode %}
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Response object" %}
{% code overflow="wrap" %}
```javascript
{
    "shippingOption": {
        "id": "overnight-shipping",
        "label": "Overnight Shipping",
        "amount": 100,
        "detail": "Get this in 1 business day."
    },
    "updateWith": function(data) {
        callback(data);
    }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Shipping address change

The Shipping Address Change emits when the Customer selects a different Shipping Address within the Payment Request interface. The event will emit the following object structure.

<table><thead><tr><th width="214.33333333333331">Key</th><th>Type</th><th>Description</th></tr></thead><tbody><tr><td>updateWith</td><td>Function</td><td>Calling this function with a <a href="../digital-river-payment-objects.md#payment-request-details-update-error-object">Payment Request Details Update object</a> merges your updates into the current Payment Request object.</td></tr><tr><td>shippingAddress</td><td>A <a href="../digital-river-payment-objects.md#payment-request-details-update-error-object">Payment Request Details Update object</a></td><td>A <a href="../digital-river-payment-objects.md#payment-request-shipping-option-object">Payment Request Shipping Option object</a> contains the details of the customer's chosen Shipping Option.</td></tr></tbody></table>

{% tabs %}
{% tab title="Example" %}
{% code overflow="wrap" %}
```javascript
applepay.on('shippingoptionchange', function(event) {
    var shippingOption = event.shippingOption;
  
  
    //create a Payment Request Details Update Object
    var newDetails = createPaymentRequestDetailsUpdateObject();
    event.updateWith(newDetails);
});
```
{% endcode %}
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Response object" %}
{% code overflow="wrap" %}
```
{
    "shippingOption": {
        "id": "overnight-shipping",
        "label": "Overnight Shipping",
        "amount": 100,
        "detail": "Get this in 1 business day."
    },
    "updateWith": function(data) {
        callback(data);
    }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

####
