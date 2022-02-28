---
description: Learn how to use Google Pay elements.
---

# Google Pay elements

Use DigitalRiver.js to create a Google Pay element and interact with Google Pay.‌

## Creating a Google Pay element

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
 
 
 
var googlepay = digitalriver.createElement('googlepay', paymentRequestData);
```
{% endtab %}
{% endtabs %}

### Google Pay element styles and customization

#### **Button type**‌

Choose one of the following button types:

![](../../../.gitbook/assets/Google-Pay-elements-buttons.png)

#### **Button color**‌

Choose one of the following button colors:

![](../../../.gitbook/assets/Google-Pay-elements-colors.png)

## Google Pay element functions

### googlepay.canMakePayment();

{% tabs %}
{% tab title="Example" %}
```javascript
if(googlepay.canMakePayment()) {
 
 
}
```
{% endtab %}
{% endtabs %}

### googlepay.mount();

Call this function to place the created Google Pay element on your page.

{% tabs %}
{% tab title="Example" %}
```javascript
<div id="google-pay"></div>
 
 
if(googlepay.canMakePayment()) {
    googlepay.mount('google-pay');
}
```
{% endtab %}
{% endtabs %}

### **googlepay.show();**

Call this function to show the Google Pay Payment Request interface. This will automatically happen when using the element. If you'd like to trigger using another mechanism, you must call it as part of the user interaction (click handler).

{% tabs %}
{% tab title="Example" %}
```javascript
googlepay.show();
```
{% endtab %}
{% endtabs %}

### googlepay.unmount();

Call this function to remove the Google Pay element from your page. The element may be re-added to your page by calling `mount()`.

{% tabs %}
{% tab title="Example" %}
```javascript
googlepay.unmount();
```
{% endtab %}
{% endtabs %}

### googlepay.destroy();

Call this function to remove the Google Pay element from your page as well as remove its functionality. You cannot re-add the destroyed element to your page via mount().

{% tabs %}
{% tab title="Example" %}
```javascript
googlepay.destroy();
```
{% endtab %}
{% endtabs %}

### googlepay.update();

Call this function to update the Google Pay element's data.

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
 
 
googlepay.update(paymentRequest);
```
{% endtab %}
{% endtabs %}

## Google Pay element events — googlepay.on('event', handler);

The Google Pay Element can receive the following events by creating an event listener. Use this function to listen to events that can be used to build and enhance your purchase flow.

| Event                  | Triggered When                                                                                                                                            |
| ---------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
|  ready                 | The created element is loaded and ready to accept an update request.                                                                                      |
|  click                 | A shopper clicked the element's button.                                                                                                                   |
|  cancel                | The customer has canceled the experience.                                                                                                                 |
|  shippingoptionchange  | The customer has chosen a different shipping option than was previously selected. You should use this data to re-price your order totals (if applicable). |
|  shippingaddresschange | The customer has chosen a different address than was previously selected. You should use this data to re-price your order totals (if applicable).         |
|  source                | The customer has authorized the payment and a source, and DigitalRiver.js returned its associated data.                                                   |

### Source

The Source event emits when the Customer completes their interaction with the Payment Request interface, and they create a Payment Source. The emitted object will be a [Payment Request Response object](digital-river-payment-objects.md#payment-request-response-object).

{% tabs %}
{% tab title="Example" %}
```javascript
googlepay.on('source', function(result) {
    var source = result.source;
     
    //pass the source to your back end for further processing
}
```
{% endtab %}
{% endtabs %}

### Ready

The Ready event emits when the Google Pay Element has loaded and is available to take an `update()` call.

{% tabs %}
{% tab title="Example" %}
```javascript
googlepay.on('ready', function(event) {
    //google pay can accept an update call
}
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Response object" %}
```javascript
{
    elementType: "googlepay"
}
```
{% endtab %}
{% endtabs %}

### Click

The Click event emits when the customer clicks a Google Pay Element.

{% tabs %}
{% tab title="Example" %}
```javascript
googlepay.on('click', function(event) {
    //do stuff
}
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Response object" %}
```javascript
{
    elementType: "googlepay"
}
```
{% endtab %}
{% endtabs %}

### Cancel

The Cancel event emits when the customer closes the Google Pay Element Payment Request interface.

{% tabs %}
{% tab title="Example" %}
```javascript
googlepay.on('shippingoptionchange', function(event) {
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

### Shipping option change

The Shipping Option Change event emits when the Customer selects a different Shipping Option within the Payment Request interface. The event will emit the following object structure.

| Key            | Type                                                                                                                     | Description                                                                                                                                                                                                      |
| -------------- | ------------------------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| updateWith     | Function                                                                                                                 |  Calling this function with a [Payment Request Details Update object](digital-river-payment-objects.md#payment-request-details-update-error-object) merges your updates into the current Payment Request object. |
| shippingOption | A [Payment Request Details Update object​](digital-river-payment-objects.md#payment-request-details-update-error-object) | A [Payment Request Shipping Option object](digital-river-payment-objects.md#payment-request-shipping-option-object) contains the details of the customer's chosen Shipping Option.                               |

{% tabs %}
{% tab title="Example" %}
```javascript
googlepay.on('shippingaddresschange', function(event) {
    var shippingAddress = event.shippingAddress;
 
 
    //create a Payment Request Details Update Object
    var newDetails = createPaymentRequestDetailsUpdateObject();
     
    event.updateWith(newDetails);
});
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Response oject" %}
{% code title="Response object" %}
```javascript
{
    shippingAddress: {
        "name": "John Smith",
        "firstName": "John",
        "lastName": "Smith",
        "phone": "952-111-1111",
        "email": "jsmith@digitalriver.com",
        "address": {
            "line1": "10380 Bren Rd W",
            "line2": "string",
            "city": "Minnetonka",
            "postalCode": "55129",
            "state": "MN",
            "country": "US"
        }
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

| Key             | Type                                                                                    | Description                                                                                                                                                                                                      |
| --------------- | --------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| updateWith      | Function                                                                                |  Calling this function with a [Payment Request Details Update object](digital-river-payment-objects.md#payment-request-details-update-error-object) merges your updates into the current Payment Request object. |
| shippingAddress | A [Shipping Address object ](digital-river-payment-objects.md#shipping-address-object)​ | A [Shipping Address object](digital-river-payment-objects.md#shipping-address-object) contains the details of the customer's chosen Shipping Option.                                                             |

{% tabs %}
{% tab title="Example" %}
```javascript
googlepay.on('shippingaddresschange', function(event) {
    var shippingAddress = event.shippingAddress;
 
 
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
    shippingAddress: {
        "name": "John Smith",
        "firstName": "John",
        "lastName": "Smith",
        "phone": "952-111-1111",
        "email": "jsmith@digitalriver.com",
        "address": {
            "line1": "10380 Bren Rd W",
            "line2": "string",
            "city": "Minnetonka",
            "postalCode": "55129",
            "state": "MN",
            "country": "US"
        }
    }, 
    "updateWith": function(data) {
        callback(data);
    }
}
```
{% endtab %}
{% endtabs %}
