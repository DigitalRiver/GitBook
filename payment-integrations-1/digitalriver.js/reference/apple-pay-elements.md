---
description: Learn how to use Apple Pay elements.
---

# Apple Pay elements

‌With DigitalRiver.js, you can create an Apple Pay element and interact with Apple Pay.‌

## Creating an Apple Pay element

{% tabs %}
{% tab title="Example" %}
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
{% endtab %}
{% endtabs %}

### Apple Pay element styles and customization

Use the following styles and types to create an Apple Pay button that you can more closely integrate into your experience.‌

### **Button type**‌

* `plain`: ![](../../../.gitbook/assets/ApplePay-Button-Black.png)&#x20;
* `buy`: ![](../../../.gitbook/assets/BuyWithApplePay-Button-Black.png)

Choose one of the following button types:

### **Button color**‌

Choose one of the following button colors:

* ​`light`: ![](../../../.gitbook/assets/ApplePay-Button-White.png)&#x20;
* `light-outline`: ![](../../../.gitbook/assets/ApplePay-Button-White-Outline.png)&#x20;
* `dark`: ![](../../../.gitbook/assets/ApplePay-Button-Black.png)&#x20;

## Apple Pay element functions

### applepay.canMakePayment();

Call this function to determine whether or not the Customer's browser supports Apple Pay.

{% tabs %}
{% tab title="Example" %}
```javascript
if(applepay.canMakePayment()) {
    //can make payment with this element
}
```
{% endtab %}
{% endtabs %}

### applepay.mount();

Call this function to place the created Apple Pay element on your page.

{% tabs %}
{% tab title="Example" %}
```javascript
<div id="apple-pay"></div>
 
if(applepay.canMakePayment()) {
    //can make payment with this element
    applepay.mount('apple-pay');
}
```
{% endtab %}
{% endtabs %}

### applepay.show();

Call this function to show the Apple Pay Payment Request interface. This will automatically happen when using the element. If you'd like to trigger via another mechanism, you must call it as part of the user interaction (click handler).

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

Call this function to remove the Apple Pay element from your page as well as remove its functionality. You cannot re-add the element to your page via `mount()`.

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
{% endtab %}
{% endtabs %}

## Apple Pay element events — applepay.on('event', handler);

Call this function to listen to events that can be used to build and enhance your purchase flow.

| Event                                                                    | Triggered When                                                                                                                                            |
| ------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [​ready​](apple-pay-elements.md#ready)                                   | The created element is loaded and ready to accept an update request.                                                                                      |
| [​click​](apple-pay-elements.md#click)                                   | A shopper clicked the element's button.                                                                                                                   |
| ​[cancel​](apple-pay-elements.md#cancel)                                 | The customer has canceled the experience.                                                                                                                 |
| [​shippingoptionchange​](apple-pay-elements.md#shipping-option-change)   | The customer has chosen a different shipping option than was previously selected. You should use this data to re-price your order totals (if applicable). |
| [​shippingaddresschange​](apple-pay-elements.md#shipping-address-change) | The customer has chosen a different address than was previously selected. You should use this data to re-price your order totals (if applicable).         |
| ​[source​](apple-pay-elements.md#source)                                 | The customer has authorized the payment and a source, and DigitalRiver.js returned associated data.                                                       |

### Source

The Source event emits when the Customer completes their interaction with the Payment Request interface, and they create a Payment Source. The emitted object will be a [Payment Request Response object](digital-river-payment-objects.md#payment-request-response-object).

{% tabs %}
{% tab title="Example" %}
```javascript
applepay.on('source', function(event) {
    var source = result.source;
 
 
    //pass the source to your back end for further processing.  
});
```
{% endtab %}
{% endtabs %}

### Ready

The Ready event emits when the Apple Pay Element has loaded and is available to take an `update()` call.

{% tabs %}
{% tab title="Example" %}
```javascript
applepay.on('ready', function(event) {
    //apple pay element is ready and can accept an update call
});
```
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

| Key            | Type                                                                                                                    | Description                                                                                                                                                                                                |
| -------------- | ----------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| updateWith     | Function                                                                                                                |  Calling this function with a [Payment Request Details Update object](digital-river-payment-objects.md#payment-request-details-update-object) merges your updates into the current Payment Request object. |
| shippingOption | A [Payment Request Details Update object](digital-river-payment-objects.md#payment-request-details-update-error-object) | A [Payment Request Shipping Option object](digital-river-payment-objects.md#payment-request-shipping-option-object) contains the details of the customer's chosen Shipping Option.                         |

{% tabs %}
{% tab title="Example" %}
```javascript
applepay.on('shippingoptionchange', function(event) {
    var shippingOption = event.shippingOption;
  
  
    //create a Payment Request Details Update Object
    var newDetails = createPaymentRequestDetailsUpdateObject();
    event.updateWith(newDetails);
});
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Response object" %}
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
{% endtab %}
{% endtabs %}

### Shipping address change

The Shipping Address Change emits when the Customer selects a different Shipping Address within the Payment Request interface. The event will emit the following object structure.

| Key             | Type                                                                                                                    | Description                                                                                                                                                                                                      |
| --------------- | ----------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| updateWith      | Function                                                                                                                |  Calling this function with a [Payment Request Details Update object](digital-river-payment-objects.md#payment-request-details-update-error-object) merges your updates into the current Payment Request object. |
| shippingAddress | A [Payment Request Details Update object](digital-river-payment-objects.md#payment-request-details-update-error-object) | A [Payment Request Shipping Option object](digital-river-payment-objects.md#payment-request-shipping-option-object) contains the details of the customer's chosen Shipping Option.                               |

{% tabs %}
{% tab title="Example" %}
```javascript
applepay.on('shippingoptionchange', function(event) {
    var shippingOption = event.shippingOption;
  
  
    //create a Payment Request Details Update Object
    var newDetails = createPaymentRequestDetailsUpdateObject();
    event.updateWith(newDetails);
});
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Response object" %}
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
{% endtab %}
{% endtabs %}

####
