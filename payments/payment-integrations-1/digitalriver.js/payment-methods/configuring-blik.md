---
description: Learn how to configure BLIK for DigitalRiver.js with Elements.
---

# Configuring BLIK

If you're using [DigitalRiver.js with Elements](../), you can create a [BLIK ](../../../supported-payment-methods/blik.md)payment method for your app or website in four easy steps:

* [Step 1: Build a BLIK Source Request object](configuring-blik.md#step-1-build-a-blik-source-request-details-object)
* [Step 2: Create a BLIK source using DigitalRiver.js](configuring-blik.md#step-2-create-a-blik-source-using-digitalriver.js)
* [Step 3: Authorize the BLIK source](configuring-blik.md#step-3-authorize-the-bancontact-source)
* [Step 4: Use the authorized source](configuring-blik.md#step-4-use-the-authorized-source)

## Step 1: Build a BLIK Source Request object

Build the BLIK Source Request and Details objects. The BLIK Source Request object requires the following fields.

| Field       | Value                                                                           |
| ----------- | ------------------------------------------------------------------------------- |
| `type`      | `blik`                                                                          |
| `sessionId` | The payment session identifier.                                                 |
| `owner`     | An [Owner object](common-payment-objects.md#owner-object).                      |
| `blik`      | A [BLIK Source Details object](configuring-blik.md#blik-source-details-object). |

### BLIK Source Details object

The BLIK Details object requires the following fields.

{% code overflow="wrap" %}
```javascript
{
    "cancelUrl": "https://example1.com",
    "returnUrl": "https://example2.com",
    "shipping": {
        "email": "jdoe@email.com",
        "phoneNumber": "077 1723 6984",
        "recipient": "John Doe"
        "address": {
            "line1": "ul. Fajansowa 98",
            "city": "Warszawa",
            "country": "PL",
            "postalCode": "02-217"
        }
    }
}
```
{% endcode %}

| Field       | Required/Optional | Description                                                                                                                                 |
| ----------- | ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| `cancelUrl` | Required          | If you choose to use the full redirect flow, this is where your Custcmer will be redirected to after cancelling within the BLIK experience. |
| `returnUrl` | Required          | If you choose to use the full redirect, this is where you will redirect your customer to after authorization within the BLIK experience.    |
| `shipping`  | Optonal           | If the order contains a physical product that requires a shipping address, include it here.                                                 |

## Step 2: Create a BLIK source using DigitalRiver.js

To create a BLIK payment source, use the DigitalRiver.js library to create and mount elements to the HTML container, or you can assemble the information and then send it using the standard calls in DigitalRiver.js.

{% hint style="info" %}
The `address` object must contain [postal code](../../../../integration-options/checkouts/creating-checkouts/providing-address-information.md#postal-code-validations) and [state/province](../../../../integration-options/checkouts/creating-checkouts/providing-address-information.md#states-and-province-validations) data that [adheres to a standardized format](../../../../integration-options/checkouts/creating-checkouts/providing-address-information.md#postal-code-and-state-province-validations).
{% endhint %}

{% code overflow="wrap" %}
```javascript
var sourceData = {
    "type": "blik",
    "sessionId": "ea03bf6f-84ef-4993-b1e7-b7d5ecf71d1f",
    "owner":{
        "firstName":"John",
        "lastName":"Doe",
        "email":"jdoe@email.com",
        "phoneNumber":"077 1723 6984",
        "address": {
            "line1": "ul. Fajansowa 98",
            "city": "Warszawa",
            "country": "PL",
            "postalCode": "02-217"
        },
    },
    "blik": {
        "returnUrl": "https://example1.com"
        "cancelUrl": "https://example2.com",
        "shipping": {
            "recipient": "John Doe",
            "phoneNumber": "077 1723 6984",
            "address": {
                "line1": "ul. Fajansowa 98",
                "city": "Warszawa",
                "country": "PL",
                "postalCode": "02-217"
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

### BLIK source response example

{% tabs %}
{% tab title="JSON" %}
{% code overflow="wrap" %}
```javascript
{
    "clientId":"gc",
    "channelId":"drdod15",
    "liveMode":false,
    "id":"cd53c5da-cc8a-4bbe-a51b-89fba9e82503",
    "sessionId":"f068e2aa-022a-4aa7-a098-deea82ead250",
    "clientSecret":"cd53c5da-cc8a-4bbe-a51b-89fba9e82503_9e6cbc1e-41bc-4018-8ed8-f35b39c0c0b6",
    "type":"blik",
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
            "line1":"ul. Fajansowa 98",
            "city":"Warszawa",
            "country":"PL",
            "postalCode":"02-217"
        }
    },
    "amount":"100.00",
    "currency":"PLN",
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
    "blik": {
        "cancelUrl": "https://example1.com",
        "returnUrl": "https://example2.com",
        "accountToken": "33904584300000000000000600300905"
    }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Step 3: Authorize the BLIK source

When you create a BLIK source, the customer is required to authorize the charge through their payment provider. You can accomplish this by redirecting the customer to their payment provider.

### Redirecting the customer for BLIK authorization

To redirect your customer to the payment provider for authorization, use the `redirectUrl` parameter in your `createSource` response.

```javascript
window.location.href = sourceResponse.redirect.redirectUrl;
```

The payment provider will present the customer with the transaction details and the customer can authorize, or cancel the transaction. A successful authorization redirects the customer to the BLIK Return URL parameter you specified when you created the source.

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
    "type":"blik",
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
            "line1": "ul. Fajansowa 98",
            "city": "Warszawa",
            "country": "PL",
            "postalCode": "02-217"
        },
    },
    "amount":"100.00",
    "currency":"PLN",
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
    "blik":{
        "cancelUrl": "https://example1.com",
        "returnUrl": "https://example2.com",
    }
}
```
{% endcode %}

## Step 4: Use the authorized source

Once authorized, you can use the source by [attaching it to a checkout](../../../payment-sources/using-the-source-identifier.md#attaching-sources-to-checkouts).

{% code title="POST /checkouts/{id}" overflow="wrap" %}
```javascript
{
  "customerId": "502283345689",
  "sourceId": "cd53c5da-cc8a-4bbe-a51b-89fba9e82503"
}
```
{% endcode %}

## Testing BLIK

See [Testing redirect payment methods](../../../../developer-resources/testing-scenarios.md#testing-redirect-payment-methods) for testing instructions.
