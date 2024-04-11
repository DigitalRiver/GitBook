---
description: Learn how to configure TreviPay for DigitialRiver.js with Elements.
---

# Configuring TreviPay

If you're using [DigitalRiver.js with Elements](../), you can create a [TreviPay](../../../supported-payment-methods/trevipay.md) payment method for your app or website in four easy steps:

* [Step 1: Build the TreviPay object](trevipay.md#step-1-build-the-trevipay-object)
* [Step 2: Create a TreviPay agreement source using DigitalRiver.js](trevipay.md#step-2-create-a-trevipay-agreement-source-using-digitalriver-js)
* [Step 3: Authorize a TreviPay source](trevipay.md#step-3-authorize-a-trevipay-source)
* [Step 4: Use the authorized source](trevipay.md#step-4-use-the-authorized-source)

## Step 1: Build the TreviPay object

A TreviPay source request object requires the following fields.

| Field       | Value                                                                          |
| ----------- | ------------------------------------------------------------------------------ |
| `type`      | `msts`                                                                         |
| `sessionId` | The payment session identifier.                                                |
| `msts`      | A TreviPay source details object that includes the details of the transaction. |

### TreviPay source details object

The TreviPay source details object requires the following fields.

{% code overflow="wrap" %}
```javascript
{
    "returnUrl": "https://mypage.com",
    "cancelUrl": "https://mypage.com/cancel",
}
```
{% endcode %}

| Field       | Required/Optional | Description                                                                                                                                                                              |
| ----------- | ----------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `returnUrl` | Required          | If you choose to use the full redirect flow, this is where you will redirect your customer after authorizing within the TreviPay experience. Note that the `returnUrl` must use `https`. |
| `cancelUrl` | Required          | If you choose to utilize the full redirect flow, this is where you will redirect your customer after canceling within the TreviPay experience.                                           |

## Step 2: Create a TreviPay agreement source using DigitalRiver.js

Use the DigitalRiver.js library to create and mount elements to the HTML container.

{% hint style="info" %}
The `address` object must contain [postal code](../../../../integration-options/checkouts/creating-checkouts/providing-address-information.md#postal-code-validations) and [state/province](../../../../integration-options/checkouts/creating-checkouts/providing-address-information.md#states-and-province-validations) data that [adheres to a standardized format](../../../../integration-options/checkouts/creating-checkouts/providing-address-information.md#postal-code-and-state-province-validations).
{% endhint %}

{% tabs %}
{% tab title="JavaScript" %}
{% code overflow="wrap" %}
```javascript
var data = {
    "type": "msts",
    "sessionId": "ea03bf6f-84ef-4993-b1e7-b7d5ecf71d1f",
    "msts": {
        "returnUrl": "http://mypage.com",
        "cancelUrl": "https://mypage.com/cancel"
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
{% endtab %}
{% endtabs %}

### TreviPay source response example

{% tabs %}
{% tab title="Source response" %}
{% code overflow="wrap" %}
```javascript
{
    "clientId": "gc",
    "channelId": "drdod15",
    "liveMode": false,
    "id": "d6a44e5d-1373-4013-847d-10deb4ded4df",
    "sessionId": "ea03bf6f-84ef-4993-b1e7-b7d5ecf71d1f",    
    "clientSecret": "d6a44e5d-1373-4013-847d-10deb4ded4df_ddd44e5d-1373-4013-847d-10deb4ded4df",
    "type": "msts",
    "reusable": false,
    "amount": "10.00",
    "currency": "USD",
    "state": "pending_redirect",
    "creationIp": "209.87.178.4",
    "createdTime": "2019-05-22T00:00:46.975Z",A 
    "updatedTime": "2019-05-22T00:00:46.975Z",
    "flow": "redirect",
    "redirect": {
        "redirectUrl": "https://api.digitalriver.com:443/payments/redirects/b8f2207b-8236-4608-b5a2-812790d42ed8?apiKey=pk_test_6cb0fe9ce3124093a9ad906f6c589e2ds",
        "returnUrl": "https://example.com?action=paymentSuccess",
        "cancelUrl": "https://example.com?action=paymentFailure"
    },
    "msts": {
        "shipping": {
            "recipient": "John Doe",
            "phoneNumber": "555-555-1212",
            "address": {
                "line1": "54321 Fake St.",
                "line2": "Apt. 3C",
                "city": "Minnetonka",
                "state": "MN",
                "country": "US",
                "postalCode": "55341"
            }
        },
        "token": "EC-1HD67063RG318840B"
    }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Step 3: Authorize a TreviPay source

When you create a TreviPay source, the customer is required to authorize the charge at TreviPay. You can accomplish this by redirecting the customer to TreviPay to authorize the charge as part of your experience.

### Redirecting the customer to TreviPay for authorization <a href="#redirecting-the-customer-to-paypal-for-authorization" id="redirecting-the-customer-to-paypal-for-authorization"></a>

To redirect your customer to TreviPay for authorization, use the `redirectUrl` parameter in your `createSource` response.

{% code overflow="wrap" %}
```
window.location.href = sourceResponse.redirect.redirectUrl;
```
{% endcode %}

At TreviPay, the customer can authorize or cancel the transaction when presented with the transaction details. If the authorization is successful, the customer will be redirected to the TreviPay Return URL parameter you specified when you created the source. If the customer cancels, they will be returned to the TreviPay Cancel URL parameter you specified.​

## Step 4: Use the authorized source

Once authorized, you can use the source by [attaching it to a checkout](../../../payment-sources/using-the-source-identifier.md#attaching-sources-to-checkouts).

{% tabs %}
{% tab title="POST /checkouts/{id}" %}
{% code overflow="wrap" %}
```javascript
{
  "sourceId": "src_a78cfeae-f7ae-4719-8e1c-d05ec04e4d37"
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Testing TreviPay

See [Testing redirect payment methods](../../../../developer-resources/testing-scenarios.md#testing-redirect-payment-methods) for testing instructions.
