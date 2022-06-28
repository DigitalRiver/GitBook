---
description: >-
  Alipay is a delayed fulfillment payment method, meaning fulfillment occurs
  after authorization and settlement.
---

# Alipay

Alipay works much like PayPal, where the consumer chooses to make a payment and is directed to the external Alipay site, where they enter (or choose existing) payment information.

## Configuring Alipay for DigitalRiver.js

Create an Alipay payment method for your app or website in four easy steps:

* [Step 1: Alipay Source Details object](alipay.md#step-1-build-an-alipay-source-request-object)
* [Step 2: Create the Alipay source using DigitalRiver.js](alipay.md#step-2-create-the-alipay-source-using-digitalriver-js)
* [Step 3: Authorize an Alipay source](alipay.md#step-3-authorize-an-alipay-source)
* [Step 4: Use the Authorized source](alipay.md#step-4-use-the-authorized-source)

### Step 1: Build an Alipay source request object

Build an Alipay Source Request object. The Alipay Source Request object requires the following fields.

| Field     | Value                                                                                                                   |
| --------- | ----------------------------------------------------------------------------------------------------------------------- |
| type      | alipay                                                                                                                  |
| sessionId | The payment session identifier.                                                                                         |
| owner     | An [Owner object](common-payment-objects.md#owner-object).                                                              |
| alipay    | An [Alipay Source Details object](alipay.md#alipay-source-details-object) that includes the details of the transaction. |

#### Alipay source details object

```javascript
{
    "returnUrl": "https://example.com"
}
```

| Field     | Required/Optional | Description                                                                                                  |
| --------- | ----------------- | ------------------------------------------------------------------------------------------------------------ |
| returnUrl | Required          | Where you will redirect your customer after the customer authorizes or cancels within the Alipay experience. |

### Step 2: Create the Alipay source using DigitalRiver.js

Use the DigitalRiver.js library to create and mount elements to the HTML container.

```javascript
let alipaySourceData = {
                "type": "alipay",
                "sessionId": "3c9473b0-630d-4f20-af61-63d3aa8acb35",
                "owner": {
                    "firstName": "Donglei",
                    "lastName": "Ye",
                    "email": "j2r23ux28qj@temporary-mail.net",
                    "phoneNumber": "13063725095",
                    "address": {
                        "line1": "Wei Bai Chang",
                        "city": "ShunDe District)",
                        "state": "Guangdong",
                        "country": "CN",
                        "postalCode": "528322"
                    }
                },
                "alipay": {
                    "returnUrl": redirectUrl
                }
            }
 
digitalriver.createSource(alipaySourceData ).then(function(result) {
    if (result.error) {
        //handle errors as something went wrong
    } else {
        var source = result.source;
     
        //do something with the created source
    }
});
```

#### Alipay source example

```javascript
{
    "clientId": "gc",
    "channelId": "drdod15",
    "liveMode": false,
    "id": "5ce08114-143b-4bf6-ae0e-6fc501ee0c24",
    "clientSecret": "5ce08114-143b-4bf6-ae0e-6fc501ee0c24_a468b08e-2c47-4531-82af-d48d80ff6dcc",
    "type": "alipay",
    "reusable": false,
    "owner": {
        "firstName": "Donglei",
        "lastName": "Ye",
        "email": "j2r23ux28qj@temporary-mail.net",
        "phoneNumber": "13063725095",
        "address": {
            "line1": "Wei Bai Chang",
            "city": "ShunDe District)",
            "state": "Guangdong",
            "country": "CN",
            "postalCode": "528322"    
        }
    },
    "amount": "10.00",
    "currency": "CNY",
    "state": "pending_redirect",
    "creationIp": "10.81.3.92",
    "createdTime": "2020-02-26T02:48:11.508Z",
    "updatedTime": "2020-02-26T02:48:11.508Z",
    "flow": "redirect",
    "redirect": {
        "redirectUrl": "https://api.digitalriverws.com:443/payments/redirects/51314834-9bf9-483f-b3a7-4b36a14d3f5c?apiKey=pk_hc_e03ee62c0d964bb3ac75595b1203d13c",
        "returnUrl": "returnUrl.com"
    },
    "alipay": {}
}
```

### Step 3: Authorize an Alipay source

When you create an Alipay source, the customer is required to authorize the charge through their payment provider. You can accomplish this by redirecting the customer to their payment provider.

#### Redirecting the customer for authorization

To redirect your customer to the payment provider for authorization, use the `redirectUrl` parameter in your `createSource` response.

```javascript
window.location.href = sourceResponse.redirect.redirectUrl;
```

The payment provider will present the customer with the transaction details to authorize, or cancel the transaction. A successful authorization redirects the customer to the Alipay Return URL parameter you specified when you created the source.

### Step 4: Use the authorized source

Once authorized, you can use the source by [attaching it to a cart](../../../sources/#attaching-a-payment-method-to-an-order-or-cart).

{% tabs %}
{% tab title="POST /v1/shoppers/me/carts/active/apply-payment-method" %}
```javascript
{
  "paymentMethod": {
    "sourceId": "e7ba0595-059c-460c-bad8-2812123b9313"
  }

```
{% endtab %}
{% endtabs %}

## Supported markets

For information on supported markets and currencies for Drop-in and DigitalRiver.js, go to:&#x20;

* **Payment Method Guide:** [digitalriver.com/payment-method-guide](https://www.digitalriver.com/payment-method-guide/)
* **Country Guide:** [digitalriver.com/country-guide/](https://www.digitalriver.com/country-guide/)