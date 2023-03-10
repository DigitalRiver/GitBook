---
description: Learn how to configure Klarna for DigitalRiver.js with Elements.
---

# Configuring Klarna

If you're using[ DigitalRiver.js with Elements](../), you can create a [Klarna](../../../supported-payment-methods/klarna.md) payment method for your app or website in five easy steps:

* [Step 1: Build a Klarna source request object](klarna.md#step-1-build-a-klarna-source-request-object)
* [Step 2: Create a Klarna source using DigitalRiver.js](klarna.md#step-2-create-a-klarna-source-using-digitalriver-js)
* [Step 3: Authorize the Klarna source](klarna.md#step-3-authorize-the-klarna-source)
* [Step 4: Use the Authorized source](klarna.md#step-4-use-the-authorized-source)
* [Step 5: Support recurring payments](klarna.md#step-5-support-recurring-payments)

## Step 1: Build a Klarna Source Request object

{% hint style="warning" %}
**Important**: The Klarna payment type does not support recurring payments. For recurring payments, you must use the `klarnaCreditRecurring` payment type.
{% endhint %}

Build a Klarna Source Request object. A Klarna Source Request object requires the following fields.

### Klarna Source Request object

| Field          | Value                                                                                                                   |
| -------------- | ----------------------------------------------------------------------------------------------------------------------- |
| `type`         | `klarnaCredit`                                                                                                          |
| `sessionId`    | The payment session identifier.                                                                                         |
| `owner`        | An [Owner object](common-payment-objects.md#owner-object).                                                              |
| `klarnaCredit` |  A [Klarna Source Details object](klarna.md#klarna-source-details-object) that includes the details of the transaction. |

### Klarna Source Details object

The Klarna Source Details object requires the following fields.

{% code overflow="wrap" %}
```javascript
{
    "returnUrl": "https://redirectUrl.com",
    "cancelUrl": "https://cancelurl.com",
}
```
{% endcode %}

| Field       | Required/Optional | Description                                                                                                                                        |
| ----------- | ----------------- | -------------------------------------------------------------------------------------------------------------------------------------------------- |
| `returnUrl` | Required          | If you choose to utilize the full redirect flow, this is where your Customer will be redirected to after authorizing within the Klarna experience. |
| `cancelUrl` | Required          | If you choose to utilize the full redirect flow, this is where your Customer will be redirected to after cancelling within the Klarna experience.  |

## Step 2: Create a Klarna source using DigitalRiver.js

Use the DigitalRiver.js library to create and mount elements to the HTML container.

{% hint style="info" %}
The `address` object must contain postal code and state/province data that **** [adheres to a standardized format](../../../../shopper-apis/cart/creating-or-updating-a-cart/providing-address-information.md) using the `state` attribute. Note that the `state` attribute listed below corresponds to the `countrySubdivision` attribute used when providing address information. The payment session manages the correct field name on the backend.
{% endhint %}

{% code overflow="wrap" %}
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
{% endcode %}

### Klarna source example

{% code overflow="wrap" %}
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
{% endcode %}

## Step 3: Authorize the Klarna source

When you create a Klarna source, the customer is required to authorize the charge through Klarna. You can accomplish this by redirecting the customer to Klarna, where they will be presented with different payment options.

### Redirecting the Customer to Klarna for authorization

To redirect your customer to Klarna for authorization, use the `redirectUrl` parameter in your `createSource` response.

{% tabs %}
{% tab title="HTML" %}
{% code overflow="wrap" %}
```markup
window.location.href = sourceResponse.redirect.redirectUrl;
```
{% endcode %}
{% endtab %}
{% endtabs %}

At Klarna, the customer will be presented with the transaction details where they can authorize or cancel the transaction. If the authorization is successful, the customer will be redirected to the `returnUrl` parameter you specified when creating the source. If the customer cancels, they will be returned to the `cancelURL` parameter you specified when creating the source.

## Step 4: Use the Authorized source

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

When applying Klarna to a cart, use the [redirect and submit payment flow](../../../sources/using-the-source-identifier.md#redirect-then-submit-payment-flow).

## Step 5: Support recurring payments

{% hint style="info" %}
**Note**: To support recurring payments, use a payment type of `klarnaCreditRecurring` in the [createSource request](klarna.md#klarna-source-request-object). Only use the Klarna Recurring payment type for recurring payments. Klarna Recurring uses a different type of agreement with the lender, Klarna, to facilitate the recurring payments.

For standard payments, you must use the Klarna payment type.
{% endhint %}

| Field                   | Value                                                                                                                  |
| ----------------------- | ---------------------------------------------------------------------------------------------------------------------- |
| `type`                  | `klarnaCreditRecurring`                                                                                                |
| `amount`                | `klarnaCreditRecurring`                                                                                                |
| `owner`                 | An [Owner object](common-payment-objects.md#owner-object).                                                             |
| `klarnaCreditRecurring` | A [Klarna Source Details object](klarna.md#klarna-source-details-object) that includes the details of the transaction. |

### Klarna Recurring source example

{% code overflow="wrap" %}
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
{% endcode %}

{% hint style="warning" %}
**Additional setup required**: If you are interested in using Klarna, contact your Account Manager. The Account Manager will send setup instructions for Klarna Banners after you sign the client addendum.
{% endhint %}
