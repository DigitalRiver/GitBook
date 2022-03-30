---
description: >-
  Korea Bank is a payment method that represents 20% of the local market share.
  Recurring payments are supported.
---

# Korea–Bank Transfer

## Configuring Korea—Bank transfer for DigitalRiver.js

Create a Bank Transfer payment method for your app or website in four easy steps:

* [Step 1: Build the Bank Transfer source request object](korea-bank-transfer.md#step-1-build-the-bank-transfer-objects)
* [Step 2: Create the Bank Transfer source using DigitalRiver.js](korea-bank-transfer.md#step-2-create-the-bank-transfer-source-using-digitalriver-js)
* [Step 3: Authorize a Bank Transfer source](korea-bank-transfer.md#step-3-authorize-a-bank-transfer-source)
* [Step 4: Use the Authorized source](korea-bank-transfer.md#step-4-use-the-authorized-source)

### Step 1: Build the Bank Transfer objects

Build a Bank Transfer Source Request and Details objects.&#x20;

#### Bank Transfer source request object

The Bank Transfer Source Request object requires the following fields.

| Field        | Value                                                                                                 |
| ------------ | ----------------------------------------------------------------------------------------------------- |
| type         | bankTransfer                                                                                          |
| sessionId    | The payment session identifier.                                                                       |
| owner        |  An [Owner object](../common-payment-objects.md#owner-object).                                        |
| bankTransfer |  A [Bank Transfer Source Details object](korea-bank-transfer.md#bank-transfer-source-request-object). |

#### Bank Transfer source details object

The Bank Transfer Source Details object requires the following fields.

```javascript
{
    "returnUrl": "https://example.com"
}
```

| Field     | Required/Optional | Description                                                                                                                                                       |
| --------- | ----------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| returnUrl | Required          | If you choose to use the full redirect flow, this is where you will redirect your Customer to after authorizing or canceling within the Bank Transfer experience. |

### Step 2: Create the Bank Transfer source using DigitalRiver.js

Use the DigitalRiver.js library to create and mount elements to the HTML container.

```javascript
var data = {
    "type": "bankTransfer",
    "sessionId": "3c9473b0-630d-4f20-af61-63d3aa8acb35",
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
    "bankTransfer": {
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

#### Bank Transfer source example

```javascript
{
    "clientId": "gc",
    "channelId": "drdod15",
    "liveMode": false,
    "id": "bdcf5832-fc2c-4c79-92e0-85b261s18ae0",
    "clientSecret": "bdcf5832-fc2c-4c79-92e0-85b261s18ae0_bdcf5832-fc2c-4c79-92e0-85b261s18ae0",
    "sessionId": "3c9473b0-630d-4f20-af61-63d3aa8acb35",    
    "type": "bankTransfer",
    "reusable": false,
    "owner": {
        "firstName": "John",
        "lastName": "Doe",
        "email": "jdoe@digitalriver.com",
        "phoneNumber": "000-000-0000",
        "address": {
            "line1": "1-16-24 Minami-gyotoku",
            "line2": "Ichikawa-shi",
            "city": "Chiba",
            "state": "Kyongsangnamdo",
            "postalCode": "272-0138",
            "country": "JP"
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
    "bankTransfer": {}
}
```

### Step 3: Authorize a Bank Transfer source

When you create a Bank Transfer source, the customer is required to authorize the charge through their payment provider. You can accomplish this by redirecting the customer to their payment provider.

#### Redirecting the customer for Bank Transfer authorization

To redirect your customer to the payment provider for authorization, use the `redirectUrl` parameter in your `createSource` response.

```javascript
window.location.href = sourceResponse.redirect.redirectUrl;
```

The payment provider will present the customer with the transaction details where they can authorize, or cancel the transaction. A successful authorization redirects the customer to the Bank Transfer Return URL parameter you specified when you created the source.

Once authorized, the source state will change to `chargeable`.

```javascript
{
    "clientId": "gc",
    "channelId": "drdod15",
    "liveMode": false,
    "id": "bdcf5832-fc2c-4c79-92e0-85b261s18ae0",
    "clientSecret": "bdcf5832-fc2c-4c79-92e0-85b261s18ae0_bdcf5832-fc2c-4c79-92e0-85b261s18ae0",
    "type": "bankTransfer",
    "reusable": false,
    "owner": {
        "firstName": "John",
        "lastName": "Doe",
        "email": "jdoe@digitalriver.com",
        "phoneNumber": "000-000-0000",
        "address": {
            "line1": "1-16-24 Minami-gyotoku",
            "line2": "Ichikawa-shi",
            "city": "Chiba",
            "state": "Kyongsangnamdo",
            "postalCode": "272-0138",
            "country": "JP"
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
    "bankTransfer": {}
}
```

### Step 4: Use the Authorized source

Once authorized, you can use the source by [attaching it to a cart](../../../../cart/attaching-a-payment-method-to-a-cart-or-customer.md#attaching-a-payment-method-to-an-order-or-cart).

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

## Supported markets

For information on supported markets and currencies for Drop-in and DigitalRiver.js, go to:&#x20;

* **Payment Method Guide:** [digitalriver.com/payment-method-guide](https://www.digitalriver.com/payment-method-guide/)
* **Country Guide:** [digitalriver.com/country-guide/](https://www.digitalriver.com/country-guide/)
