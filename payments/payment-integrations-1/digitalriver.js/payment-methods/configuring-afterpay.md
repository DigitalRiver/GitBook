---
description: Learn how to configure Afterpay for DigitalRiver.js with Elements.
---

# Configuring Afterpay

If you're using [DigitalRiver.js with Elements](../), you can create an [Afterpay ](../../../supported-payment-methods/afterpay.md)payment method for your app or website in four easy steps:

* [Step 1: Build an Afterpay Source Request and Detail objects](configuring-afterpay.md#step-1-build-an-afterpay-source-request-and-details-objects)
* [Step 2: Create an Afterpay source using DigitalRiver.js](configuring-afterpay.md#step-2-create-an-afterpay-source-using-digitalriver.js)
* [Step 3: Authorize the Afterpay source](configuring-afterpay.md#step-3-authorize-the-afterpay-source)
* [Step 4: Use the authorized source](configuring-afterpay.md#step-4-use-the-authorized-source)

## Step 1: Build an Afterpay Source Request and Details objects

Build the Afterpay Source Request and Source Details objects.&#x20;

### Afterpay Source Request object

The Afterpay Source Request object requires the following fields.

| Field       | Value                                                                                        |
| ----------- | -------------------------------------------------------------------------------------------- |
| `type`      | `afterPay`                                                                                   |
| `sessionId` | The payment session identifier.                                                              |
| `owner`     | An [Owner object](common-payment-objects.md#owner-object).                                   |
| `afterPay`  | An [Afterpay Source Details object.](configuring-afterpay.md#afterpay-source-details-object) |

### Afterpay Source Details object

The Afterpay Source Details object requires the following fields.

{% code overflow="wrap" %}
```json
{
    "cancelUrl": "https://example1.com",
    "returnUrl": "https://example2.com",
    "shipping": {
        "email": "jdoe@email.com",
        "phoneNumber": "077 1723 6984",
        "recipient": "John Doe"
        "address": {
            "line1": "200 Broadway Ave",
            "city": "West Beach",
            "country": "AU",
            "state": "South Australia",
            "postalCode": "5024"
        }
    }
}
```
{% endcode %}

| Field       | Required/Optional | Description                                                                                                                                     |
| ----------- | ----------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| `cancelUrl` | Required          | If you choose to use the full redirect flow, this is where you will redirect your customer to after cancelling within the Afterpay experience.  |
| `returnUrl` | Required          | If you choose to use the full redirect flow, this is where you will redirect your customer to after authorizing within the Afterpay experience. |
| `shipping`  | Optional          | if the order contains a physical product that requires a shipping address, include it here.                                                     |

## Step 2: Create an Afterpay source using DigitalRiver.js

Use the DigitalRiver.js library to create and mount elements to the HTML container.

{% hint style="info" %}
The `address` object must contain [postal code](../../../../integration-options/checkouts/creating-checkouts/providing-address-information.md#postal-code-validations) and [state/province](../../../../integration-options/checkouts/creating-checkouts/providing-address-information.md#states-and-province-validations) data that [adheres to a standardized format](../../../../integration-options/checkouts/creating-checkouts/providing-address-information.md#postal-code-and-state-province-validations).
{% endhint %}

{% code overflow="wrap" %}
```javascript
var sourceData = {
    "type": "afterPay",
    "sessionId": "ea03bf6f-84ef-4993-b1e7-b7d5ecf71d1f",
    "owner":{
        "firstName":"John",
        "lastName":"Doe",
        "email":"jdoe@email.com",
        "phoneNumber":"077 1723 6984",
        "address": {
            "line1": "200 Broadway Ave",
            "city": "West Beach",
            "country": "AU",
            "state": "South Australia",
            "postalCode": "5024"
        },
    },
    "afterPay": {
        "returnUrl": "https://example1.com"
        "cancelUrl": "https://example2.com",
        "shipping": {
            "recipient": "John Doe",
            "phoneNumber": "077 1723 6984",
            "address": {
                "line1": "200 Broadway Ave",
                "city": "West Beach",
                "country": "AU",
                "state": "South Australia",
                "postalCode": "5024"
            },
            "email": "jdoe@email.com"
        }
    }
}
 
 
digitalriver.createSource(sourceData).then(function(result) {
    if(result.error) {
        //handle error message
        var errorMessage = result.error.errors[0].message;
    } else {
        //send source to back end for processing
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
    "sessionId":"f068e2aa-022a-4aa7-a098-deea82ead250",
    "clientSecret":"cd53c5da-cc8a-4bbe-a51b-89fba9e82503_9e6cbc1e-41bc-4018-8ed8-f35b39c0c0b6",
    "type":"afterPay",
    "reusable":false,
    "owner":{
        "firstName":"John",
        "lastName":"Doe",
        "customerId":"502283345689",
        "email":"jdoe@email.com",
        "phoneNumber":"077 1723 6984",
        "upstreamId":"123456789",
        "organization":"Digital River",
        "address":{
            "line1":"200 Broadway Ave",
            "city":"West Beach",
            "state":"South Australia",
            "country":"AU",
            "postalCode":"5024"
        }
    },
    "amount":"100.00",
    "currency":"AUD",
    "state":"pending_redirect",
    "creationIp":"209.87.180.27",
    "createdTime":"2022-03-29T20:09:25.752Z",
    "updatedTime":"2022-03-29T20:09:25.752Z",
    "flow":"redirect",
    "redirect":{
        "cancelUrl":"https://example1.com",
        "returnUrl":"https://example2.com",
        "offline":false
    },
    "language":"en",
    "afterPay": {
        "cancelUrl": "https://example1.com",
        "returnUrl": "https://example2.com",
        "accountToken": "33904584300000000000000600300905"
    }
}
```
{% endcode %}

## Step 3: Authorize the Afterpay source

When you create an Afterpay source, the customer is required to authorize the charge through their payment provider. You can accomplish this by redirecting the customer to their payment provider.

### Redirecting the customer for Afterpay authorization

To redirect your customer to the payment provider for authorization, use the `redirectUrl` parameter in your `createSource` response.

{% code overflow="wrap" %}
```javascript
window.location.href = sourceResponse.redirect.redirectUrl;
```
{% endcode %}

The payment provider will present the customer with the transaction details and the customer can authorize, or cancel the transaction. A successful authorization redirects the customer to the Afterpay Return URL parameter you specified when you created the source.

Once authorized, the source state will change to `chargeable`.

{% code overflow="wrap" %}
```javascript
{
    "clientId":"gc",
    "channelId":"drdod15",
    "liveMode":false,
    "id":"cd53c5da-cc8a-4bbe-a51b-89fba9e82503",
    "sessionId":"f068e2aa-022a-4aa7-a098-deea82ead250",
    "clientSecret":"cd53c5da-cc8a-4bbe-a51b-89fba9e82503_9e6cbc1e-41bc-4018-8ed8-f35b39c0c0b6",
    "type":"afterPay",
    "reusable":false,
    "owner":{
        "firstName":"John",
        "lastName":"Doe",
        "customerId":"502283345689",
        "email":"jdoe@email.com",
        "phoneNumber":"077 1723 6984",
        "upstreamId":"123456789",
        "organization":"",
            "address": {
            "line1": "200 Broadway Ave",
            "city": "West Beach",
            "country": "AU",
            "state": "South Australia",
            "postalCode": "5024"
        },
    },
    "amount":"100.00",
    "currency":"AUD",
    "state":"chargeable",
    "creationIp":"209.87.180.27",
    "createdTime":"2022-03-29T20:09:25.752Z",
    "updatedTime":"2022-03-29T20:09:25.752Z",
    "flow":"redirect",
    "redirect":{
        "redirectUrl":"https://example3.com",
        "returnUrl":"https://example2.com",
        "offline":false
    },
    "language":"en",
    "afterPay":{
        "cancelUrl": "https://example1.com",
        "returnUrl": "https://example2.com",
    }
}
```
{% endcode %}

## Step 4: Use the authorized source

Once authorized, you can use the source by [attaching it to a checkout](../../../payment-sources/using-the-source-identifier.md#attaching-sources-to-checkouts).

{% code title="POST /checkouts/{id}" overflow="wrap" %}
```json
{
  "customerId": "5774321008",
  "sourceId": "src_a78cfeae-f7ae-4719-8e1c-d05ec04e4d37"
}
```
{% endcode %}

## Testing Afterpay

See [Testing redirect payment methods](../../../../developer-resources/testing-scenarios.md#testing-redirect-payment-methods) for testing instructions.