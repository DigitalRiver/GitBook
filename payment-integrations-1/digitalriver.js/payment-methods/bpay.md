---
description: >-
  bPay is a wire transfer payment method used in Australia, where users can make
  payments online and over the phone for online purchases or utility bills.
---

# bPay

bPay is Australia's most widely used bill pay service, which allows shoppers to make easy and secure online purchases by transferring funds from their bank account.

Fulfillment occurs after authorization and settlement. The customer provides either the transfer information to their bank or completes a payment using bPay.

## Configuring bPay for DigitalRiver.js

Create a bPay payment method for your app or website in three easy steps:‌

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

{% tabs %}
{% tab title="JavaScript" %}
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
{% endtab %}
{% endtabs %}

#### bPay source example

The source event will surface a Source plus other details provided by bPay, like the billing address and the information required to send money to bPay.

{% tabs %}
{% tab title="Plain Text" %}
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
{% endtab %}
{% endtabs %}

### Step 3: Use the authorized source

Once authorized, you can use the source by [attaching it to a cart](../../../cart/attaching-a-payment-method-to-a-cart-or-customer.md#attaching-a-payment-method-to-an-order-or-cart).

{% tabs %}
{% tab title="POST /v1/shoppers/me/carts/active/apply-payment-method" %}
```javascript
{
  "paymentMethod": {
    "sourceId": "e7ba0595-059c-460c-bad8-2812123b9313"
  }
}
```
{% endtab %}
{% endtabs %}

#### Pushing funds

At this point, you should complete your order, and provide the instructions inside the bPay object to the shopper to wire payment.

When you push the funds, the source transitions to the `chargeable` state. The order will then be ready for fulfillment.

## Supported markets

For information on supported markets and currencies for Drop-in and DigitalRiver.js, go to:&#x20;

* **Payment Method Guide:** [digitalriver.com/payment-method-guide](https://www.digitalriver.com/payment-method-guide/)
* **Country Guide:** [digitalriver.com/country-guide/](https://www.digitalriver.com/country-guide/)
