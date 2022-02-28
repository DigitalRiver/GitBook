---
description: >-
  Klarna allows the consumer to purchase a product and then be billed for it
  afterward.
---

# Klarna

Klarna offers the following payment options:

* **Invoice**–Choose one of the following options to make shopping easier for customers by letting them try before they buy:
  * **Pay later in 30 days**–Once the order is shipped, you are paid upfront while the customer has 30 days to pay. Available in the US and UK.
  * **Pay later in 14 days**–Once the order is shipped, you are paid upfront while the customer has 14 days to pay. Available in Austria, Denmark, Finland, Germany, Norway, Netherlands, and Sweden.
* **Installments**–Allows a partial payment at approval and the balance to be collected later at specific times at 0%.
* **Financing**–Allows the shopper to finance the order at an interest-bearing installment plan.

Financing orders reduce cart abandonment and improve conversions at a higher average order value. There are unique display and entry requirements for each country. Please contact your Digital River Representative for more details.

## Configuring Klarna for DigitalRiver.js

Create a Klarna payment method for your app or website in five easy steps:

* [Step 1: Build a Klarna source request object](klarna.md#step-1-build-a-klarna-source-request-object)
* [Step 2: Create a Klarna source using DigitalRiver.js](klarna.md#step-2-create-a-klarna-source-using-digitalriver-js)
* [Step 3: Authorize the Klarna source](klarna.md#step-3-authorize-the-klarna-source)
* [Step 4: Use the Authorized source](klarna.md#step-4-use-the-authorized-source)
* [Step 5: Support recurring payments](klarna.md#step-5-support-recurring-payments)

### Step 1: Build a Klarna Source Request object

{% hint style="warning" %}
**Important**: The Klarna payment type does not support recurring payments. For recurring payments, you must use the `klarnaCreditRecurring` payment type.
{% endhint %}

Build a Klarna Source Request object. A Klarna Source Request object requires the following fields.

#### Klarna Source Request object

| Field        | Value                                                                                                                   |
| ------------ | ----------------------------------------------------------------------------------------------------------------------- |
| type         | klarnaCredit                                                                                                            |
| sessionId    | The payment session identifier.                                                                                         |
| owner        | An [Owner object](common-payment-objects.md#owner-object).                                                              |
| klarnaCredit |  A [Klarna Source Details object](klarna.md#klarna-source-details-object) that includes the details of the transaction. |

#### Klarna Source Details object

The Klarna Source Details object requires the following fields.

```javascript
{
    "returnUrl": "https://redirectUrl.com",
    "cancelUrl": "https://cancelurl.com",
}
```

| Field     | Required/Optional | Description                                                                                                                                        |
| --------- | ----------------- | -------------------------------------------------------------------------------------------------------------------------------------------------- |
| returnUrl | Required          | If you choose to utilize the full redirect flow, this is where your Customer will be redirected to after authorizing within the Klarna experience. |
| cancelUrl | Required          | If you choose to utilize the full redirect flow, this is where your Customer will be redirected to after cancelling within the Klarna experience.  |

### Step 2: Create a Klarna source using DigitalRiver.js

Use the DigitalRiver.js library to create and mount elements to the HTML container.

```javascript
 var data = {
  "type" : "klarnaCredit",
  "owner" : {
    "firstName" : "firstName",
    "lastName" : "lastName",
    "email" : "email@email.org",
    "phoneNumber" : "9522253720",
    "address" : {
      "line1" : "line1",
      "line2" : "line2",
      "city" : "Minnetonka",
      "state" : "MN",
      "country" : "US",
      "postalCode" : "55410"
    }
  },
  "sessionId" : "3aa75613-9596-438a-9604-67e20016aa96",
  "klarnaCredit" : {
    "returnUrl" : "http://example.org/return",
    "cancelUrl" : "http://example.org/cancel"
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

#### Klarna source example

```javascript
{
    "clientId": "gc",
    "channelId": "drdod15",
    "liveMode": false,
    "sessionId": "ea03bf6f-84ef-4993-b1e7-b7d5ecf71d1f",       
    "id": "231fa002-3831-4ded-9705-4a455df2697b",
    "clientSecret": "231fa002-3831-4ded-9705-4a455df2697b_3341d8c6-e66b-43a5-af4b-c623459b44af",
    "type": "klarnaCredit",
    "reusable": false,
    "owner": {
        "firstName": "John",
        "lastName": "Doe",
        "email": "jdoe@yahoo.com",
        "phoneNumber": "5559895326",
        "address": {
            "line1": "10380 Bren Road West",
            "line2": "",
            "city": "Minnetonka",
            "state": "MN",
            "country": "US",
            "postalCode": "55343"
        }
    },
    "amount": "210.50",
    "currency": "USD",
    "state": "pending_redirect",
    "creationIp": "10.81.3.92",
    "createdTime": "2020-02-27T01:10:57.513Z",
    "updatedTime": "2020-02-27T01:10:57.513Z",
    "flow": "redirect",
    "redirect": {
        "redirectUrl": "https://api.digitalriverws.com:443/payments/redirects/bca8a56b-7afb-4670-891c-313630ef748e?apiKey=pk_hc_e03ee62c0d964bb3ac75595b1203d13c",
        "returnUrl": "https://yourdomain.com?paymentAction=success",
        "cancelUrl": "https://yourdomain.com?paymentAction=failure"
    },
    "klarnaCredit": {
        "shipping": {
            "recipient": "John Doe",
            "phoneNumber": "5559895326",
            "address": {
                "line1": "10380 Bren Road West",
                "city": "Minnetonka",
                "state": "MN",
                "country": "US",
                "postalCode": "55343"
            },
            "email": "jdoe@yahoo.com"
        },
        "token": "63449012720000000000000534937705"
    }
}
```

### Step 3: Authorize the Klarna source

When you create a Klarna source, the customer is required to authorize the charge through Klarna. You can accomplish this by redirecting the customer to Klarna, where they will be presented with different payment options.

#### Redirecting the Customer to Klarna for authorization

To redirect your customer to Klarna for authorization, use the `redirectUrl` parameter in your `createSource` response.

{% tabs %}
{% tab title="HTML" %}
```markup
window.location.href = sourceResponse.redirect.redirectUrl;
```
{% endtab %}
{% endtabs %}

At Klarna, the customer will be presented with the transaction details where they can authorize or cancel the transaction. If the authorization is successful, the customer will be redirected to the `returnUrl` parameter you specified when creating the source. If the customer cancels, they will be returned to the `cancelURL` parameter you specified when creating the source.

### Step 4: Use the Authorized source

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

### Step 5: Support recurring payments

{% hint style="info" %}
**Note**: To support recurring payments, use a payment type of `klarnaCreditRecurring` in the [createSource request](klarna.md#klarna-source-request-object). Only use the Klarna Recurring payment type for recurring payments. Klarna Recurring uses a different type of agreement with the lender, Klarna, to facilitate the recurring payments.

For standard payments, you must use the Klarna payment type.
{% endhint %}

| Field                 | Value                                                                                                                  |
| --------------------- | ---------------------------------------------------------------------------------------------------------------------- |
| type                  | klarnaCreditRecurring                                                                                                  |
| amount                | klarnaCreditRecurring                                                                                                  |
| owner                 | An [Owner object](common-payment-objects.md#owner-object).                                                             |
| klarnaCreditRecurring | A [Klarna Source Details object](klarna.md#klarna-source-details-object) that includes the details of the transaction. |

#### Klarna Recurring source example

```javascript
var data = {
  "type" : "klarnaCreditRecurring",
  "owner" : {
    "firstName" : "firstName",
    "lastName" : "lastName",
    "email" : "email@email.org",
    "phoneNumber" : "9522253720",
    "address" : {
      "line1" : "line1",
      "line2" : "line2",
      "city" : "Minnetonka",
      "state" : "MN",
      "country" : "US",
      "postalCode" : "55410"
    }
  },
  "sessionId" : "3aa75613-9596-438a-9604-67e20016aa96",
  "klarnaCreditRecurring" : {
    "returnUrl" : "http://example.org/return",
    "cancelUrl" : "http://example.org/cancel"
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

{% hint style="warning" %}
**Additional setup required**: If you are interested in using Klarna, contact your Account Manager. The Account Manager will send set up instructions for Klarna Banners after you sign the client addendum.
{% endhint %}

## Supported markets

For information on supported markets and currencies for Drop-in and DigitalRiver.js, go to:&#x20;

* **Payment Method Guide:** [digitalriver.com/payment-method-guide](https://www.digitalriver.com/payment-method-guide/)
* **Country Guide:** [digitalriver.com/country-guide/](https://www.digitalriver.com/country-guide/)
