---
description: Learn how to configure Afterpay for DigitalRiver.js with Elements.
---

# Configuring Afterpay

If you're using[ DigitalRiver.js with Elements](../), you can create an [Afterpay ](../../../supported-payment-methods/afterpay.md)payment method for your app or website in four easy steps:

* [Step 1: Build an Afterpay Source Request and Source Details objects](configuring-afterpay.md#step-1-build-an-afterpay-source-request-and-source-details-objects)
* [Step 2: Create an Afterpay source using DigitalRiver.js](configuring-afterpay.md#step-2-create-an-afterpay-source-using-digitalriver.js)
* [Step 3: Authorize the Afterpay source](configuring-afterpay.md#step-3-authorize-the-afterpay-source)
* [Step 4: Use the authorized source](configuring-afterpay.md#step-4-use-the-authorized-source)

## Step 1: Build an Afterpay Source Request and Source Details objects

Build the Afterpay Source Request and Source Details objects.&#x20;

### Afterpay Source Request object

The Afterpay Source Request object requires the following fields.

| Field       | Value                                                                                          |
| ----------- | ---------------------------------------------------------------------------------------------- |
| `type`      | `afterPay`                                                                                     |
| `sessionId` | The payment session identifier.                                                                |
| `owner`     | An [Owner object](common-payment-objects.md#owner-object).                                     |
| `afterPay`  | An [Afterpay Source Details object](configuring-afterpay.md#bancontact-source-details-object). |

### Afterpay Source Details object

The Afterpay Source Details object requires the following fields.

{% code overflow="wrap" %}
```json
{
  "returnUrl":"https://js-test.digitalriver.com/v1/1.20220329.1453/components/redirect-receiver/redirect-receiver.html?controllerId=controller-76ef3046-888c-4073-90ad-1b5d61a8af08&componentId=redirect-receiver-1757f835-c21b-4f4e-b208-92adc5c30573&action=return",
  "cancelUrl":"https://js-test.digitalriver.com/v1/1.20220329.1453/components/redirect-receiver/redirect-receiver.html?controllerId=controller-76ef3046-888c-4073-90ad-1b5d61a8af08&componentId=redirect-receiver-1757f835-c21b-4f4e-b208-92adc5c30573&action=cancel",
  "shipping":{
    "address":{
      "line1":"10380 Bren Rd W",
      "line2":"Suite 180",
      "city":"Minnetonka",
      "state":"MN",
      "postalCode":"55344",
      "country":"US"
    },
    "email":"example@example.com",
    "phoneNumber":"9525551212",
    "recipient":"Jane Doe"
  }
}
```
{% endcode %}

| Field       | Required/Optional | Description                                                                                                                                     |
| ----------- | ----------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| `cancelUrl` | Required          | If you choose to use the full redirect flow, this is where you will redirect your customer to after cancelling within the Afterpay experience.  |
| `returnUrl` | Required          | If you choose to use the full redirect flow, this is where you will redirect your customer to after authorizing within the Afterpay experience. |
| `shipping`  | Optional          | if the order contains a physical product that requires a shipping address, include it here.JSON                                                 |

## Step 2: Create an Afterpay source using DigitalRiver.js

Use the DigitalRiver.js library to create and mount elements to the HTML container.

{% hint style="info" %}
The `address` object must contain postal code and state/province data that [adheres to a standardized format](../../../../shopper-apis/cart/creating-or-updating-a-cart/providing-address-information.md) using the `state` attribute. Note that the `state` attribute listed below corresponds to the `countrySubdivision` attribute used when providing address information. The payment session manages the correct field name on the backend.
{% endhint %}

{% code overflow="wrap" %}
```javascript
var sourceData = {
  "type":"afterPay",
  "sessionId":"ea03bf6f-84ef-4993-b1e7-b7d5ecf71d1f",
  "owner":{
    "firstName":"Jane",
    "lastName":"Doe",
    "email":"example@example.com",
    "phoneNumber":"9525551212",
    "address":{
      "line1":"10380 Bren Rd W",
      "line2":"Suite 180",
      "city":"Minnetonka",
      "state":"MN",
      "postalCode":"55344",
      "country":"US"
    }
  },
  "afterPay":{
    "returnUrl":"https://js-test.digitalriver.com/v1/1.20220329.1453/components/redirect-receiver/redirect-receiver.html?controllerId=controller-76ef3046-888c-4073-90ad-1b5d61a8af08&componentId=redirect-receiver-1757f835-c21b-4f4e-b208-92adc5c30573&action=return",
    "cancelUrl":"https://js-test.digitalriver.com/v1/1.20220329.1453/components/redirect-receiver/redirect-receiver.html?controllerId=controller-76ef3046-888c-4073-90ad-1b5d61a8af08&componentId=redirect-receiver-1757f835-c21b-4f4e-b208-92adc5c30573&action=cancel",
    "shipping":{
      "address":{
        "line1":"10380 Bren Rd W",
        "line2":"Suite 180",
        "city":"Minnetonka",
        "state":"MN",
        "country":"US",
        "postalCode":"55344"
      },
      "email":"example@example.com",
      "recipient":"Jane Doe",
      "phoneNumber":"9525551212"
    }
  }
}
 
 
digitalriver.createSource(sourceData).then(function(result) {
    if(result.error) {
        //handle error message
        var errorMessage = result.error.errors[0].message;
    } else {
        //send the source to the back end for processing
        var source = result.source;
    }
});
```
{% endcode %}

### Afterpay source response example

{% code overflow="wrap" %}
```json
{
  "clientId":"gc",
  "channelId":"drdod15",
  "liveMode":false,
  "id":"cd53c5da-cc8a-4bbe-a51b-89fba9e82503",
  "sessionId":"ea03bf6f-84ef-4993-b1e7-b7d5ecf71d1f",
  "clientSecret":"cd53c5da-cc8a-4bbe-a51b-89fba9e82503_9e6cbc1e-41bc-4018-8ed8-f35b39c0c0b6",
  "type":"afterPay",
  "reusable":false,
  "owner":{
    "firstName":"Jane",
    "lastName":"Doe",
    "email":"example@example.com",
    "phoneNumber":"9525551212",
    "address":{
      "line1":"10380 Bren Rd W",
      "line2":"Suite 180",
      "city":"Minnetonka",
      "state":"MN",
      "postalCode":"55344",
      "country":"US"
    }
  },
  "amount":"100.00",
  "currency":"USD",
  "state":"pending_redirect",
  "creationIp":"209.87.180.27",
  "createdTime":"2022-03-29T20:09:25.752Z",
  "updatedTime":"2022-03-29T20:09:25.752Z",
  "flow":"redirect",
  "redirect":{
    "redirectUrl":"https://api.digitalriver.com:443/payments/redirects/954cf456-aad3-4957-87ed-743ea4c9c102?apiKey=pk_sys_c2608001bba7477eae22808e1eb138db",
    "returnUrl":"https://js-test.digitalriver.com/v1/1.20220329.1453/components/redirect-receiver/redirect-receiver.html?controllerId=controller-76ef3046-888c-4073-90ad-1b5d61a8af08&componentId=redirect-receiver-1757f835-c21b-4f4e-b208-92adc5c30573&action=return",
    "cancelUrl":"https://js-test.digitalriver.com/v1/1.20220329.1453/components/redirect-receiver/redirect-receiver.html?controllerId=controller-76ef3046-888c-4073-90ad-1b5d61a8af08&componentId=redirect-receiver-1757f835-c21b-4f4e-b208-92adc5c30573&action=cancel",
    "offline":false
  },
  "language":"en",
  "afterPay":{
    "returnUrl":"https://js-test.digitalriver.com/v1/1.20220329.1453/components/redirect-receiver/redirect-receiver.html?controllerId=controller-76ef3046-888c-4073-90ad-1b5d61a8af08&componentId=redirect-receiver-1757f835-c21b-4f4e-b208-92adc5c30573&action=return",
    "cancelUrl":"https://js-test.digitalriver.com/v1/1.20220329.1453/components/redirect-receiver/redirect-receiver.html?controllerId=controller-76ef3046-888c-4073-90ad-1b5d61a8af08&componentId=redirect-receiver-1757f835-c21b-4f4e-b208-92adc5c30573&action=cancel",
    "shipping":{
      "address":{
        "line1":"10380 Bren Rd W",
        "line2":"Suite 180",
        "city":"Minnetonka",
        "state":"MN",
        "postalCode":"55344",
        "country":"US"
      },
      "email":"example@example.com",
      "phoneNumber":"9525551212",
      "recipient":"Jane Doe"
    }
  }
}
```
{% endcode %}

## Step 3: Authorize the Afterpay source

When you create an Afterpay source, the customer is required to authorize the charge through their payment provider. You can accomplish this by redirecting the customer to their payment provider.

### Redirecting the customer for Afterpay authorization

Use the `redirectUrl` parameter in your `createSource` response to redirect your customer to the payment provider for authorization.

```javascript
window.location.href = sourceResponse.redirect.redirectUrl;
```

The payment provider will present the customer with the transaction details, and the customer can authorize or cancel the transaction. A successful authorization redirects the customer to the Afterpay Return URL parameter you specified when you created the source.

Once authorized, the source state will change to `chargeable`.

{% code overflow="wrap" %}
```json
{
  "clientId":"gc",
  "channelId":"drdod15",
  "liveMode":false,
  "id":"cd53c5da-cc8a-4bbe-a51b-89fba9e82503",
  "sessionId":"ea03bf6f-84ef-4993-b1e7-b7d5ecf71d1f",
  "clientSecret":"cd53c5da-cc8a-4bbe-a51b-89fba9e82503_9e6cbc1e-41bc-4018-8ed8-f35b39c0c0b6",
  "type":"afterPay",
  "reusable":false,
  "owner":{
    "firstName":"Jane",
    "lastName":"Doe",
    "email":"example@example.com",
    "phoneNumber":"9525551212",
    "address":{
      "line1":"10380 Bren Rd W",
      "line2":"Suite 180",
      "city":"Minnetonka",
      "state":"MN",
      "postalCode":"55344",
      "country":"US"
    }
  },
  "amount":"100.00",
  "currency":"USD",
  "state":"chargeable",
  "creationIp":"209.87.180.27",
  "createdTime":"2022-03-29T20:09:25.752Z",
  "updatedTime":"2022-03-29T20:09:25.752Z",
  "flow":"redirect",
  "redirect":{
    "redirectUrl":"https://api.digitalriver.com:443/payments/redirects/954cf456-aad3-4957-87ed-743ea4c9c102?apiKey=pk_sys_c2608001bba7477eae22808e1eb138db",
    "returnUrl":"https://js-test.digitalriver.com/v1/1.20220329.1453/components/redirect-receiver/redirect-receiver.html?controllerId=controller-76ef3046-888c-4073-90ad-1b5d61a8af08&componentId=redirect-receiver-1757f835-c21b-4f4e-b208-92adc5c30573&action=return",
    "cancelUrl":"https://js-test.digitalriver.com/v1/1.20220329.1453/components/redirect-receiver/redirect-receiver.html?controllerId=controller-76ef3046-888c-4073-90ad-1b5d61a8af08&componentId=redirect-receiver-1757f835-c21b-4f4e-b208-92adc5c30573&action=cancel",
    "offline":false
  },
  "language":"en",
  "afterPay":{
    "returnUrl":"https://js-test.digitalriver.com/v1/1.20220329.1453/components/redirect-receiver/redirect-receiver.html?controllerId=controller-76ef3046-888c-4073-90ad-1b5d61a8af08&componentId=redirect-receiver-1757f835-c21b-4f4e-b208-92adc5c30573&action=return",
    "cancelUrl":"https://js-test.digitalriver.com/v1/1.20220329.1453/components/redirect-receiver/redirect-receiver.html?controllerId=controller-76ef3046-888c-4073-90ad-1b5d61a8af08&componentId=redirect-receiver-1757f835-c21b-4f4e-b208-92adc5c30573&action=cancel",
    "accountToken":"33904584300000000000000600300905"
  }
}
```
{% endcode %}

## Step 4: Use the authorized source

Once authorized, you can use the source by [attaching it to a cart](../../../sources/#attaching-a-payment-method-to-an-order-or-cart).

{% code title="POST /v1/shoppers/me/carts/active/apply-payment-method" overflow="wrap" %}
```json
{
  "paymentMethod": {
    "sourceId": "f1e89f7a-4857-4e0a-9c31-bdb70401fea0"
  }
}
```
{% endcode %}
