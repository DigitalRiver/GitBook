---
description: Learn how to use Google Pay elements.
---

# Google Pay elements

Use DigitalRiver.js to create a Google Pay element and interact with Google Pay.‌

## Creating a Google Pay element

To create a Google Pay element, you should use the `createElement` function exposed through the DigitalRiver object.

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

var googlepay = digitalriver.createElement('googlepay', paymentRequestData);
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Google Pay element styles and customization

All Google Payment buttons on your site must adhere to the Google Pay [Brand Guidelines](https://developers.google.com/pay/api/web/guides/brand-guidelines), which include, but aren't limited to, the following requirements. Digital River provides the following Google Pay button options for clients to add to the product page/checkout page (express checkout) or payment options page.

| Configure Button Type                               | HTML Code                                                                             |
| --------------------------------------------------- | ------------------------------------------------------------------------------------- |
| ![](<../../../.gitbook/assets/G Pay.png>)           | `buttonType: "plain"`                                                                 |
| ![](<../../../.gitbook/assets/Buy with G Pay.png>)  | <p><code>buttonType: "long"</code><br>The shopper hasn't logged in to Google Pay.</p> |
| ![](<../../../.gitbook/assets/G Pay long.png>)      | <p><code>buttonType: "long"</code><br>The shopper has logged in to Google Pay</p>     |
| Configure Button Color                              | HTML Code                                                                             |
| ![](<../../../.gitbook/assets/G Pay black.png>)     | `buttonColor: "dark"`                                                                 |
| ![](<../../../.gitbook/assets/G Pay white (1).png>) | `buttonColor: "light"`                                                                |

When configuring a button, note the following:

* The button color must contrast with the background color of the area that surrounds it.
* Always maintain the minimum clear space of 8 density-independent pixels (dp) on all sides of the payment button. Ensure the clear space is never broken with graphics or text. ![](<../../../.gitbook/assets/G-Pay button.png>)
* Observe the [Google Pay Dos and Don'ts](https://developers.google.com/pay/api/web/guides/brand-guidelines#dos-and-donts).

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

Call this function to remove the Google Pay element from your page as well as remove its functionality. You cannot re-add the destroyed element to your page via `mount()`.

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


googlepay.update(paymentRequest);
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Google Pay element events — googlepay.on('event', handler);

The Google Pay Element can receive the following events by creating an event listener. Use this function to listen to events that can be used to build and enhance your purchase flow.

| Event                 | Triggered When                                                                                                                                            |
| --------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ready                 | The created element is loaded and ready to accept an update request.                                                                                      |
| click                 | A shopper clicked the element's button.                                                                                                                   |
| cancel                | The customer has canceled the experience.                                                                                                                 |
| shippingoptionchange  | The customer has chosen a different shipping option than was previously selected. You should use this data to re-price your order totals (if applicable). |
| shippingaddresschange | The customer has chosen a different address than was previously selected. You should use this data to re-price your order totals (if applicable).         |
| source                | The customer has authorized the payment and a source, and DigitalRiver.js returned its associated data.                                                   |

### Source

The Source event emits when the Customer completes their interaction with the Payment Request interface, and creates a Payment Source. The emitted object will be a [Payment Request Response object](../digital-river-payment-objects.md#payment-request-response-object).

{% tabs %}
{% tab title="Example" %}
{% code overflow="wrap" %}
```javascript
googlepay.on('source', function(result) {
    var source = result.source;

    //pass the source to your back end for further processing
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Ready

The Ready event emits when the Google Pay Element has loaded and is available to take an `update()` call.

{% tabs %}
{% tab title="Example" %}
{% code overflow="wrap" %}
```javascript
googlepay.on('ready', function(event) {
    //google pay can accept an update call
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Example" %}
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
{% code overflow="wrap" %}
```javascript
googlepay.on('shippingoptionchange', function(event) {
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
{% tab title="Response ojbect" %}
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

### Shipping option change

The Shipping Option Change event emits when the Customer selects a different Shipping Option within the Payment Request interface. The event will emit the following object structure.

| Key            | Type                                                                                                                        | Description                                                                                                                                                                                                        |
| -------------- | --------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| updateWith     | Function                                                                                                                    | Calling this function with a [Payment Request Details Update object](../digital-river-payment-objects.md#payment-request-details-update-error-object) merges your updates into the current Payment Request object. |
| shippingOption | A [Payment Request Details Update object](../digital-river-payment-objects.md#payment-request-details-update-error-object)​ | A [Payment Request Shipping Option object](../digital-river-payment-objects.md#payment-request-shipping-option-object) contains the details of the customer's chosen Shipping Option.                              |

{% tabs %}
{% tab title="Example" %}
{% code overflow="wrap" %}
```javascript
googlepay.on('shippingaddresschange', function(event) {
    var shippingAddress = event.shippingAddress;


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

| Key             | Type                                                                                       | Description                                                                                                                                                                                                        |
| --------------- | ------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| updateWith      | Function                                                                                   | Calling this function with a [Payment Request Details Update object](../digital-river-payment-objects.md#payment-request-details-update-error-object) merges your updates into the current Payment Request object. |
| shippingAddress | A [Shipping Address object](../digital-river-payment-objects.md#shipping-address-object) ​ | A [Shipping Address object](../digital-river-payment-objects.md#shipping-address-object) contains the details of the customer's chosen Shipping Option.                                                            |

{% tabs %}
{% tab title="Example" %}
{% code overflow="wrap" %}
```javascript
googlepay.on('shippingaddresschange', function(event) {
    var shippingAddress = event.shippingAddress;


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
