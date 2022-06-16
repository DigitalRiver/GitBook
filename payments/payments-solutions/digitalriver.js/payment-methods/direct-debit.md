---
description: >-
  SEPA Direct Debit allows users to authorize transactions directly from their
  bank account, which is a popular international payment method.
---

# SEPA Direct Debit

You can find an example of integration [here](https://drh.img.digitalriver.com/DRHM/Storefront/Site/drdod15/pb/multimedia/directdebit.html).

## Configuring SEPA Direct Debit for DigitalRiver.js

Create a SEPA (Single European Payment Area) Direct Debit payment method for your app or website in four easy steps:

* [Step 1: Build a SEPA Direct Debit Source Request object](direct-debit.md#step-1-build-a-direct-debit-source-request-and-details-objects)
* [Step 2: Create a SEPA Direct Debit source using DigitalRiver.js](direct-debit.md#step-2-create-a-direct-debit-source-using-digitalriver-js)
* [Step 3: Authorize a SEPA Direct Debit source](direct-debit.md#step-3-authorize-a-direct-debit-source)
* [Step 4: Use the authorized source](direct-debit.md#step-4-use-the-authorized-source)

### Step 1: Build a SEPA Direct Debit source request and details objects

Build the SEPA Direct Debit Source Request and Details objects.&#x20;

#### SEPA Direct Debit source request object

A SEPA Direct Debit Source Request object requires the following fields.

| Field         | Value                                                                                                                                              |
| ------------- | -------------------------------------------------------------------------------------------------------------------------------------------------- |
| type          | `directDebit`                                                                                                                                      |
| sessionId     | The payment session identifier.                                                                                                                    |
| `owner`       | An [Owner object](common-payment-objects.md#owner-object).                                                                                         |
| `directDebit` | A [SEPA Direct Debit Source Details object](direct-debit.md#sepa-direct-debit-source-details-object) that includes the details of the transaction. |

#### SEPA Direct Debit source details object

The SEPA Direct Debit Source Details object requires the following fields.

```javascript
{
    "returnUrl": "https://example.com"
}
```

| Field       | Required/Optional | Description                                                                                                                                                           |
| ----------- | ----------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `returnUrl` | Required          | If you choose to use the full redirect flow, this is where you will redirect your customer to after authorizing or canceling within the SEPA Direct Debit experience. |

### Step 2: Create a SEPA Direct Debit source using DigitalRiver.js

Use the DigitalRiver.js library to create and mount elements to the HTML container.

```javascript
var data = {
    "type": "directDebit",
    "sessionId": "ea03bf6f-84ef-4993-b1e7-b7d5ecf71d1f",
    "owner": {
        firstName: "John",
        lastName: "Doe",
        email: "test@digitalriver.com",
        phoneNumber: "000-000-0000",
        address: {
            line1: "123 Main Street",
            line2: "",
            city: "Paris",
            postalCode: "14390",
            country: "FR"
        }
    },
    "directDebit": {
        "returnUrl": "https://mypage.com"
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

#### SEPA Direct Debit source example

```javascript
{
    "clientId": "gc",
    "channelId": "drdod15",
    "liveMode": false,
    "id": "bddccfc7-4fa8-401b-b661-421cd5047792",
    "clientSecret": "bddccfc7-4fa8-401b-b661-421cd5047792_bdddssccfc7-4fa8-401b-b661-421cd5047792",
    "type": "directDebit",
    "reusable": false,
    "owner": {
        "firstName": "John",
        "lastName": "Doe",
        "email": "john.doe@digitalriver.com",
        "phoneNumber": "000-000-0000",
        "address": {
            "line1": "98 Boulevard Saint-Germain",
            "city": "Paris",
            "state": "Île-de-France",
            "country": "FR",
            "postalCode": "75005"
        }
    },
    "amount": "778.39",
    "currency": "EUR",
    "state": "pending_redirect",
    "creationIp": "209.87.178.4",
    "createdTime": "2019-05-22T01:48:42.168Z",
    "updatedTime": "2019-05-22T01:48:42.168Z",
    "flow": "redirect",
    "redirect": {
        "redirectUrl": "https://api.digitalriver.com:443/payments/redirects/4e478578-843a-48a5-beef-66c0dae99f5d?apiKey=pk_test_6cb0fe9ce3124093a9ad906f6c589e2d",
        "returnUrl": "https://example.com?action=paymentSuccess"
    },
    "directDebit": {}
}
```

### Step 3: Authorize a SEPA Direct Debit source

When you create a SEPA Direct Debit source, the customer is required to authorize the charge through their payment provider. You can accomplish this by redirecting the customer to their payment provider.

#### Redirecting the customer for SEPA Direct Debit authorization

To redirect your customer for authorization, use the `redirectUrl` parameter in your `createSource` response.

{% tabs %}
{% tab title="HTML" %}
```markup
window.location.href = sourceResponse.redirect.redirectUrl;
```
{% endtab %}
{% endtabs %}

The payment provider will present the customer with the transaction details where they can authorize or cancel the transaction. A successful authorization redirects the customer to the SEPA Direct Debit Return URL parameter you specified when you created the source.

### Step 4: Use the authorized source

Once authorized, you can use the source by [attaching it to a cart](../../../sources/#attaching-a-payment-method-to-an-order-or-cart) or [attaching it to a shopper](../../../sources/#attaching-a-payment-method-to-an-order-or-cart).

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

#### Option 2: Attach the source to a shopper

{% tabs %}
{% tab title="POST /v1/shoppers/me/payment-options" %}
```javascript
{
  "paymentOption": {
    "nickName": "My Token",
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
