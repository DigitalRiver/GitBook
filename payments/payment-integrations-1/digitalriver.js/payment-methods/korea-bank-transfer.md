---
description: Learn how to configure Korea Bank Transfer for DigitalRiver.js with Elements.
---

# Configuring Online Banking (Korea Bank Transfer)

If you're using [DigitalRiver.js with Elements](../), you can create a [Bank Transfer](../../../supported-payment-methods/korea-bank-transfer-online-banking.md) payment method for your app or website in four easy steps:

* [Step 1: Build the Bank Transfer source request object](korea-bank-transfer.md#step-1-build-the-bank-transfer-object)
* [Step 2: Create the Bank Transfer source using DigitalRiver.js](korea-bank-transfer.md#step-2-create-the-bank-transfer-source-using-digitalriver-js)
* [Step 3: Authorize a Bank Transfer source](korea-bank-transfer.md#step-3-authorize-a-bank-transfer-source)
* [Step 4: Use the Authorized source](korea-bank-transfer.md#step-4-use-the-authorized-source)

## Step 1: Build the Bank Transfer object

Build a Bank Transfer source request and details object

### Bank Transfer source request object

The Bank Transfer source request object requires the following fields.

| Field          | Value                                                                                                |
| -------------- | ---------------------------------------------------------------------------------------------------- |
| `type`         | `bankTransfer`                                                                                       |
| `sessionId`    | The payment session identifier.                                                                      |
| `owner`        | An [Owner object](common-payment-objects.md#owner-object).                                           |
| `bankTransfer` | A [Bank Transfer Source Details object](korea-bank-transfer.md#bank-transfer-source-request-object). |

### Bank Transfer source details object

The Bank Transfer source details object requires the following fields.

{% code overflow="wrap" %}
```javascript
{
    "returnUrl": "https://example.com"
}
```
{% endcode %}

| Field       | Required/Optional | Description                                                                                                                                                       |
| ----------- | ----------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `returnUrl` | Required          | If you choose to use the full redirect flow, this is where you will redirect your Customer to after authorizing or canceling within the Bank Transfer experience. |

## Step 2: Create the Bank Transfer source using DigitalRiver.js

Use the DigitalRiver.js library to create and mount elements to the HTML container.

{% hint style="info" %}
The `address` object must contain [postal code](../../../../integration-options/checkouts/creating-checkouts/providing-address-information.md#postal-code-validations) and [state/province](../../../../integration-options/checkouts/creating-checkouts/providing-address-information.md#states-and-province-validations) data that [adheres to a standardized format](../../../../integration-options/checkouts/creating-checkouts/providing-address-information.md#postal-code-and-state-province-validations).
{% endhint %}

{% code overflow="wrap" %}
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
{% endcode %}

### Bank Transfer source example

{% code overflow="wrap" %}
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
{% endcode %}

## Step 3: Authorize a Bank Transfer source

When you create a Bank Transfer source, the customer is required to authorize the charge through their payment provider. You can accomplish this by redirecting the customer to their payment provider.

### Redirecting the customer for Bank Transfer authorization

To redirect your customer to the payment provider for authorization, use the `redirectUrl` parameter in your `createSource` response.

{% code overflow="wrap" %}
```javascript
window.location.href = sourceResponse.redirect.redirectUrl;
```
{% endcode %}

The payment provider will present the customer with the transaction details where they can authorize, or cancel the transaction. A successful authorization redirects the customer to the Bank Transfer Return URL parameter you specified when you created the source.

Once authorized, the source state will change to `chargeable`.

{% code overflow="wrap" %}
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
{% endcode %}

## Step 4: Use the Authorized source

Once authorized, you can use the source by [attaching it to a checkout](../../../payment-sources/using-the-source-identifier.md#attaching-sources-to-checkouts).

{% tabs %}
{% tab title="POST /checkouts/{id}" %}
{% code overflow="wrap" %}
```javascript
{
  "customerId": "5774321008",
  "sourceId": "src_a78cfeae-f7ae-4719-8e1c-d05ec04e4d37"
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Testing Korea Bank Transfer

See [Testing redirect payment methods](../../../../developer-resources/testing-scenarios.md#testing-redirect-payment-methods) for testing instructions.