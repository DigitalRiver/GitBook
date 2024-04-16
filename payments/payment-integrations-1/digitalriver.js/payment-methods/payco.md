---
description: Learn how to configure PayCo for DigitalRiver.js with Elements.
---

# Configuring PayCo

If you're using [DigitalRiver.js with Elements](../), you can create a [PayCo](../../../supported-payment-methods/payco.md) payment method for your app or website in four easy steps:

* [Step 1: Build a PayCo Source Request object](payco.md#step-1-build-a-payco-source-request-and-details-object)
* [Step 2: Create a PayCo source using DigitalRiver.js](payco.md#step-2-create-a-payco-source-using-digitalriver-js)
* [Step 3: Authorize the PayCo source](payco.md#step-3-authorize-the-payco-source)
* [Step 4: Use the authorized source](payco.md#step-4-use-the-authorized-source)

## Step 1: Build a PayCo Source Request and Details object

Build the PayCo Source Request and Details objects. The PayCo Source Request object requires the following fields.

| Field       | Value                                                                  |
| ----------- | ---------------------------------------------------------------------- |
| `type`      | `payco`                                                                |
| `sessionId` | The payment session identifier.                                        |
| `owner`     | An [Owner object](common-payment-objects.md#owner-object).             |
| `payco`     | A [PayCo Source Details object](payco.md#payco-source-details-object). |

### PayCo Source Details object

The PayCo Source Details object requires the following fields.

{% code overflow="wrap" %}
```javascript
{
    "returnUrl": "https://example.com"
}
```
{% endcode %}

| Field       | Required/Optional | Description                                                                                                                                               |
| ----------- | ----------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `returnUrl` | Required          | If you choose to use the full redirect flow, this is where you will redirect your customer to after authorizing or canceling within the PayCo experience. |

## Step 2: Create a PayCo source using DigitalRiver.js

Use the DigitalRiver.js library to create and mount elements to the HTML container.

{% hint style="info" %}
The `address` object must contain [postal code](../../../../integration-options/checkouts/creating-checkouts/providing-address-information.md#postal-code-validations) and [state/province](../../../../integration-options/checkouts/creating-checkouts/providing-address-information.md#states-and-province-validations) data that [adheres to a standardized format](../../../../integration-options/checkouts/creating-checkouts/providing-address-information.md#postal-code-and-state-province-validations).
{% endhint %}

{% code overflow="wrap" %}
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
{% endcode %}

### PayCo source example

{% code overflow="wrap" %}
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
{% endcode %}

## Step 3: Authorize the PayCo source

When you create a Direct Debit source, the customer is required to authorize the charge through their payment provider. You can accomplish this by redirecting the customer to their payment provider.

### Redirecting the customer for PayCo authorization

To redirect your customer to the payment provider for authorization, use the `redirectUrl` parameter in your `createSource` response.

{% code overflow="wrap" %}
```javascript
window.location.href = sourceResponse.redirect.redirectUrl;
```
{% endcode %}

The payment provider will present the customer with the transaction details where they can authorize, or cancel the transaction. A successful authorization redirects the customer to the Payco Return URL parameter you specified when you created the source.

Once authorized, the source state will change to `chargeable`.

{% code overflow="wrap" %}
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
{% endcode %}

## Step 4: Use the authorized source

Once authorized, you can use the source by either [attaching it to a checkout](../../../payment-sources/using-the-source-identifier.md#attaching-sources-to-checkouts) or [attaching it to a customer for multiple uses.](../../../payment-sources/using-the-source-identifier.md#attaching-sources-to-customers)

### Option 1: Attach the source to a checkout

{% code title="POST /checkouts/{id}" overflow="wrap" %}
```javascript
{
  "customerId": "5774321008",
  "sourceId": "src_a78cfeae-f7ae-4719-8e1c-d05ec04e4d37"
}
```
{% endcode %}

### Option 2: Attach the source to a customer

{% code title="POST /customers/{id}/sources/{sourcesId}" overflow="wrap" %}
```javascript
{
  "id": "5774321008",
  "sourceId": "src_a78cfeae-f7ae-4719-8e1c-d05ec04e4d37"
}
```
{% endcode %}

## Testing PayCo

See [Testing standard payment methods](../../../../developer-resources/testing-scenarios.md#testing-standard-payment-methods) for testing instructions.