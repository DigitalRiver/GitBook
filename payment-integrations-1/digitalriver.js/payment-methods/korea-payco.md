---
description: >-
  Accept PayCo in Korea, a digital wallet that currently represents 10% market
  share and is expected to grow. Recurring payments are supported.
---

# PayCo

## Configuring PayCo for DigitalRiver.js

Create a PayCo payment method for your app or website in three easy steps:

* [Step 1: Build a PayCo Source Request object](korea-payco.md#step-1-build-a-payco-source-request-and-details-object)
* [Step 2: Create a PayCo source using DigitalRiver.js](korea-payco.md#step-2-create-a-payco-source-using-digitalriver-js)
* [Step 3: Authorize the PayCo source](korea-payco.md#step-3-authorize-the-payco-source)
* [Step 4: Use the authorized source](korea-payco.md#step-4-use-the-authorized-source)

### Step 1: Build a PayCo Source Request and Details object

Build the PayCo Source Request and Details objects.&#x20;

#### PayCo Source Request object

The PayCo Source Request object requires the following fields.

| Field     | Value                                                                        |
| --------- | ---------------------------------------------------------------------------- |
| type      | payco                                                                        |
| sessionId | The payment session identifier.The total value of the transaction.           |
| owner     | An [Owner object](common-payment-objects.md#owner-object).                   |
| payco     | A [PayCo Source Details object](korea-payco.md#payco-source-details-object). |

#### PayCo Source Details object

The PayCo Source Details object requires the following fields.

```javascript
{
    "returnUrl": "https://example.com"
}
```

| Field     | Required/Optional | Description                                                                                                                                               |
| --------- | ----------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| returnUrl | Required          | If you choose to use the full redirect flow, this is where you will redirect your customer to after authorizing or canceling within the PayCo experience. |

### Step 2: Create a PayCo source using DigitalRiver.js

Use the DigitalRiver.js library to create and mount elements to the HTML container.

```javascript
var data = {
    "type": "payco",
    "sessionId": "ea03bf6f-84ef-4993-b1e7-b7d5ecf71d1f",
    "owner": {
        firstName: "John",
        lastName: "Doe",
        email: "test@digitalriver.com",
        address: {
            line1: "1234 Fake Street",
            line2: "Yaum-dong",
            city: "Ulsan-si",
            state: "Kyongsangnamdo",
            postalCode: "100-011",
            country: "KR"
        }
    },
    "payco": {
        "returnUrl": "https://yourReturnUrl.com"
    }
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

#### PayCo source example

```javascript
{
    "clientId": "gc",
    "channelId": "drdod15",
    "liveMode": false,
    "id": "bdcf5832-fc2c-4c79-92e0-85b261s18ae0",
    "sessionId": "ea03bf6f-84ef-4993-b1e7-b7d5ecf71d1f",    
    "clientSecret": "bdcf5832-fc2c-4c79-92e0-85b261s18ae0_adcf5832-fc2c-4c79-92e0-85b261s18ae0",
    "type": "payco",
    "reusable": false,
    "owner": {
        "firstName": "John",
        "lastName": "Doe",
        "email": "john.doe@gmail.com",
        "phoneNumber": "000-000-0000",
        "address": {
            "line1": "1234 Fake Street",
            "line2": "Yaum-dong",
            "city": "Ulsan-si",
            "state": "Kyongsangnamdo",
            "postalCode": "100-011",
            "country": "KR"
        }
    },
    "amount": "100.00",
    "currency": "KRW",
    "state": "pending_redirect",
    "creationIp": "209.87.178.4",
    "createdTime": "2019-05-22T02:40:53.631Z",
    "updatedTime": "2019-05-22T02:40:53.631Z",
    "flow": "redirect",
    "redirect": {
        "redirectUrl": "https://api.digitalriver.com:443/payments/redirects/06e428cf-e23e-4ee9-b64f-ce17de062fd1?apiKey=pk_test_6cb0fe9ce312d093a9ad906f6c589e2d",
        "returnUrl": "https://example.com"
    },
    "payco": {}
}
```

### Step 3: Authorize the PayCo source

When you create a SEPA Direct Debit source, the customer is required to authorize the charge through their payment provider. You can accomplish this by redirecting the customer to their payment provider.

#### Redirecting the customer for PayCo authorization

To redirect your customer to the payment provider for authorization, use the `redirectUrl` parameter in your `createSource` response.

```javascript
window.location.href = sourceResponse.redirect.redirectUrl;
```

The payment provider will present the customer with the transaction details where they can authorize, or cancel the transaction. A successful authorization redirects the customer to the Payco Return URL parameter you specified when you created the source.

Once authorized, the source state will change to `chargeable`.

```javascript
{
    "clientId": "gc",
    "channelId": "drdod15",
    "liveMode": false,
    "id": "bdcf5832-fc2c-4c79-92e0-85b261s18ae0",
    "sessionId": "ea03bf6f-84ef-4993-b1e7-b7d5ecf71d1f",    
    "clientSecret": "bdcf5832-fc2c-4c79-92e0-85b261s18ae0_adcf5832-fc2c-4c79-92e0-85b261s18ae0",
    "type": "payco",
    "reusable": false,
    "owner": {
        "firstName": "John",
        "lastName": "Doe",
        "email": "john.doe@gmail.com",
        "phoneNumber": "000-000-0000",
        "address": {
            "line1": "1234 Fake Street",
            "line2": "Yaum-dong",
            "city": "Ulsan-si",
            "state": "Kyongsangnamdo",
            "postalCode": "100-011",
            "country": "KR"
        }
    },
    "amount": "100.00",
    "currency": "KRW",
    "state": "chargeable",
    "creationIp": "209.87.178.4",
    "createdTime": "2019-05-22T02:40:53.631Z",
    "updatedTime": "2019-05-22T02:40:53.631Z",
    "flow": "redirect",
    "redirect": {
        "redirectUrl": "https://api.digitalriver.com:443/payments/redirects/06e428cf-e23e-4ee9-b64f-ce17de062fd1?apiKey=pk_test_6cb0fe9ce312d093a9ad906f6c589e2d",
        "returnUrl": "https://example.com"
    },
    "payco": {}
}
```

### Step 4: Use the authorized source

Once authorized, you can use the source by either [attaching it to a checkout](../../../cart/attaching-a-payment-method-to-a-cart-or-customer.md#attaching-a-payment-method-to-an-order-or-cart) or [attaching it to a customer](../../../cart/attaching-a-payment-method-to-a-cart-or-customer.md#attaching-a-payment-method-to-a-customer) for multiple uses.

#### Option 1: Attach the source to a cart

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

#### Option 1: Attach the source to a shopper

{% tabs %}
{% tab title="POST /v1/shoppers/me/payment-options" %}
```javascript
{
  "paymentOption": {
    "nickName": "My Visa Card",
    "isDefault": "true",
    "sourceId": "61033d62-c0f4-4a7e-b844-07daf26ba84e"
  }
}
```
{% endtab %}
{% endtabs %}

## Supported markets

For information on supported markets and currencies for Drop-in and DigitalRiver.js, go to:&#x20;

* **Payment Method Guide:** [digitalriver.com/payment-method-guide](https://www.digitalriver.com/payment-method-guide/)
* **Country Guide:** [digitalriver.com/country-guide/](https://www.digitalriver.com/country-guide/)
