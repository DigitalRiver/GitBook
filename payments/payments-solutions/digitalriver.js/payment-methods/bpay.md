---
description: Learn how to configure bPay for DigitalRiver.js with Elements.
---

# Configuring bPay

If you're using[ DigitalRiver.js with Elements](../), you can create a[ bPay](../../../supported-payment-methods/bpay.md) payment method for your app or website in three easy steps:

* [Step 1: Build a bPay Source Request object](bpay.md#step-1-build-a-bpay-source-request-object)
* [Step 2: Create a bPay source using DigitalRiver.js](bpay.md#step-2-create-a-bpay-source-using-digitalriver-js)
* [Step 3: Use the Authorized source](bpay.md#step-3-use-the-authorized-source)

### Step 1: Build a bPay source request object

Build a bPay Source Request object. A bPay Source Request object requires the following fields.

| Field     | Value                                                      |
| --------- | ---------------------------------------------------------- |
| type      | bPay                                                       |
| sessionId | The payment session identifier.                            |
| owner     | An [Owner object](common-payment-objects.md#owner-object). |
| bPay      | A bPay Object. (This is currently empty)                   |

### Step 2: Create a bPay source using DigitalRiver.js

Use the DigitalRiver.js library to create and mount elements to the HTML container.

{% hint style="info" %}
The `address` object must contain postal code and state/province data that **** [adheres to a standardized format](../../../../cart/creating-or-updating-a-cart/providing-address-information.md) using the `state` attribute. Note that the `state` attribute listed below corresponds to the `countrySubdivision` attribute used when providing address information. The payment session manages the correct field name on the backend.
{% endhint %}

{% tabs %}
{% tab title="JavaScript" %}
{% code overflow="wrap" %}
```javascript
var data = {
    "type": "bPay",
    "sessionId": "ea03bf6f-84ef-4993-b1e7-b7d5ecf71d1f",
    "owner": {
        "firstName": "John",
        "lastName": "Doe",
        "email": "john.doe@digitalriver.com",
        "phoneNumber": "000-000-0000",
        "address": {
            "line1": "3 Bridge Lane",
            "line2": "",
            "city": "Sydney",
            "state": "NSW",
            "postalCode": "2000",
            "country": "AU"
        }
    },
    "bPay": {}
}
 
  
digitalriver.createSource(data).then(function(result) {
    if (result.error) {
        //handle errors
    } else {
        var source = result.source;
        //send source to back end
        sendToBackend(source);
    }
});
```
{% endcode %}
{% endtab %}
{% endtabs %}

#### bPay source example

The source event will surface a Source plus other details provided by bPay, like the billing address and the information required to send money to bPay.

{% tabs %}
{% tab title="Plain Text" %}
{% code overflow="wrap" %}
```javascript
{
    "clientId": "gc",
    "channelId": "drdod15",
    "liveMode": false,
    "id": "710e07b5-4ac5-4ce7-8257-aa9b4095573d",
    "clientSecret": "710e07b5-4ac5-4ce7-8257-aa9b4095573d_23f5c33d-1a54-412d-9e4f-cd37dc424c8a",
    "type": "bPay",
    "reusable": false,
    "owner": {
        "firstName": "John",
        "lastName": "Doe",
        "email": "john.doe@digitalriver.com",
        "phoneNumber": "192-976-1833",
        "address": {
            "line1": "3 Bridge Lane",
            "line2": "",
            "city": "Sydney",
            "state": "NSW",
            "country": "AU",
            "postalCode": "2000"
        }
    },
    "amount": "0.15",
    "currency": "AUD",
    "state": "pending_funds",
    "creationIp": "209.87.180.5",
    "createdTime": "2019-11-06T22:11:40.698Z",
    "updatedTime": "2019-11-06T22:11:40.753Z",
    "flow": "receiver",
    "bPay": {
        "accountHolder": "Global Collect BV",
        "bankName": "Commonwealth Bank",
        "city": "Sydney",
        "country": "Australia",
        "referenceId": "890701397589",
        "accountNumber": "062000-11002112",
        "billerId": "141606",
        "customerPaymentReference": "008907013975899",
        "swiftCode": "CTBAAU2S"
    }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Step 3: Use the authorized source

Once authorized, you can use the source by [attaching it to a cart](../../../sources/#attaching-a-payment-method-to-an-order-or-cart).

{% tabs %}
{% tab title="POST /v1/shoppers/me/carts/active/apply-payment-method" %}
{% code overflow="wrap" %}
```javascript
{
  "paymentMethod": {
    "sourceId": "e7ba0595-059c-460c-bad8-2812123b9313"
  }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

#### Pushing funds

At this point, you should complete your order, and provide the instructions inside the bPay object to the shopper to wire payment.

When you push the funds, the source transitions to the `chargeable` state. The order will then be ready for fulfillment.
