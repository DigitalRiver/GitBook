---
description: Learn how to configure BNP Paribas for DigitalRiver.js with Elements.
---

# Configuring BNP Paribas

Integrating BNP Paribas as a payment method into your application or website can enhance your customers' payment options significantly, catering to those who prefer this specific bank for transactions. This guide outlines setting up BNP Paribas payments using DigitalRiver.js with Elements. By following the straightforward steps laid out below, you will be able to build and authorize a BNP Paribas payment source effortlessly. Whether you want to expand your payment methods or provide a more localized payment experience, this setup will ensure a smooth integration process.

If you're using [DigitalRiver.js with Elements](../), you can create a payment method for your app or website in four easy steps:

* [Step 1: Build a BNP Paribas Source Request object](configuring-bnp-paribas.md#step-1-build-a-bnp-paribas-source-request-and-details-object)
* [Step 2: Create a BNP Paribas source using DigitalRiver.js](configuring-bnp-paribas.md#step-2-create-a-bnp-paribas-source-using-digitalriver.js)
* [Step 3: Authorize the BNP Paribas source](configuring-bnp-paribas.md#step-3-authorize-the-bnp-paribas-source)
* [Step 4: Use the authorized source](configuring-bnp-paribas.md#step-4-use-the-authorized-source)

See the [Elements integration guide](../quick-start.md) for additional information.

## Step 1: Build a BNP Paribas Source Request and Details object

To build the BNP Paribas Source Request and Details object, follow these steps:

1. **Create the BNP Paribas Source Request object** with the necessary fields:

<table><thead><tr><th width="388.8501872659176">Field</th><th>Value</th></tr></thead><tbody><tr><td><code>type</code></td><td>Specify this as <code>bnpParibas</code> to indicate the payment method type</td></tr><tr><td><code>sessionId</code></td><td>Include the payment session identifier, which is crucial for transaction tracking.</td></tr><tr><td><code>owner</code></td><td>Incorporate an <a href="broken-reference">Owner object</a> that contains the details about the payment source's owner.</td></tr><tr><td><code>bnpParibas</code></td><td>Embed a <a href="configuring-bnp-paribas.md#bnp-paribas-source-details-object">BNP Paribas Source Details object</a> with specific information about the BNP Pariba payment.</td></tr></tbody></table>

2. **Define the BNP Paribas Source Details object** with additional parameters as needed for the transaction. This object structure and required fields will depend on BNP Paribas's specifications and any additional payment processing requirements.

### BNP Paribas Source Details object

The BNP Paribas Source Details object is crucial for processing payments with BNP Paribas. It includes several key parameters:

* **`returnUrl`**: This is the URL to which customers are redirected after they authorize the payment within the BNP Paribas payment interface. It's essential for the redirect flow.
* **`cancelUrl`**: This is the URL where customers are redirected if they decide to cancel the payment within the BNP Paribas system. It's also necessary for the redirect flow.
* **`termCodeId`**: Represents a unique identifier for the payment terms, such as duration, interest rate, and other conditions. It's important to use the correct termCodeId as specified by BNP Paribas.

Example JSON structure:

```json
{
  "returnUrl": "https://redirectUrl.com",
  "cancelUrl": "https://cancelurl.com",
  "termCodeId": "{specificTermCodeId}"
}
```

This object ensures that payments are processed correctly and provides a smooth experience for users by facilitating seamless redirection after transactions.

## Step 2: Create a BNP Paribas source using DigitalRiver.js

A BNP Paribas source is a structured data object that specifies the necessary parameters for processing payments through BNP Paribas. It contains crucial URLs for redirection (`returnUrl` and `cancelUrl`) upon authorizing or canceling the payment within the BNP Paribas payment experience, as well as `termCodeId`, which represents the terms under which the payment is made. This setup is necessary to initiate a payment process with BNP Paribas, ensuring transactions are processed under the correct terms and providing a seamless user experience.

Use the DigitalRiver.js library to create and mount elements to the HTML container.

{% hint style="info" %}
The `address` object must contain [postal code](../../../../integration-options/checkouts/creating-checkouts/providing-address-information.md#postal-code-validations) and [state/province](../../../../integration-options/checkouts/creating-checkouts/providing-address-information.md#states-and-province-validations) data that [adhere to a standardized format](../../../../integration-options/checkouts/creating-checkouts/providing-address-information.md#postal-code-and-state-province-validations).
{% endhint %}

{% code overflow="wrap" %}
```javascript
var data = {
  "type" : "bnpParibas",
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
      "termCodeId": "{specificTermCodeId}"
    }
  },
  "sessionId" : "3aa75613-9596-438a-9604-67e20016aa96",
  "bnpParibas" : {
    "returnUrl" : "http://example.org/return",
    "cancelUrl" : "http://example.org/cancel"
    "termCodeId": "{specificTermCodeId}"
    
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

### BNP Paribas source example

{% code overflow="wrap" %}
```javascript
{
    "clientId": "gc",
    "channelId": "drdod15",
    "liveMode": false,
    "sessionId": "ea03bf6f-84ef-4993-b1e7-b7d5ecf71d1f",    
    "id": "231fa002-3831-4ded-9705-4a455df2697b",
    "clientSecret": "231fa002-3831-4ded-9705-4a455df2697b_3341d8c6-e66b-43a5-af4b-c623459b44af",
    "type": "bnpParibas",
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
    "bnpParibas": {
        "token": "63449012720000000000000534937705"
    }
}
```
{% endcode %}

## Step 3: Authorize the BNP Paribas source

To authorize the BNP Paribas source, you must redirect the customer to their payment provider using the `redirectUrl` obtained from the `createSource` response. Here's how you can direct the customer for authorization:

```javascript
window.location.href = sourceResponse.redirect.redirectUrl;
```

The customer can then authorize or cancel the transaction at the BNP Paribas payment page. If authorization is successful, the customer will be redirected back to your website using the `returnUrl` you specified. If the transaction is canceled, they will be redirected back using the `cancelUrl`.

## Step 4: Use the authorized source

Once the customer has authorized the transaction at BNP Paribas, you can proceed with the payment process. Here's how you attach the authorized source to a checkout for finalizing the payment:

1. Retrieve the authorized source ID from the return URL parameters.
2. [Attach the source to a checkout](../../../payment-sources/using-the-source-identifier.md#attaching-sources-to-checkouts) for a customer by using the following payload in your charge request:

{% code title="POST /checkouts/{id}" overflow="wrap" %}
```javascript
{
  "customerId": "{customer_id}",
  "sourceId": "{authorized_source_id}"
}
```
{% endcode %}

3. Replace `{customer_id}` with your actual customer's ID and `{authorized_source_id}` with the source ID you've received upon successful authorization.

Following these steps, you finalize the payment transaction, leveraging the authorized source.

## Testing BNP Paribas

To test BNP Paribas payment transactions, follow the guidelines outlined in the [Testing redirect payment methods](../../../../developer-resources/testing-scenarios.md#testing-redirect-payment-methods) section. This includes simulating various scenarios to ensure the payment process works smoothly under different conditions. It's crucial to replace placeholders in your request with actual values:

* Replace `your_customer_id` with your test customer's ID.
* Replace `authorized_source_id` with the source ID you've received upon successful authorization.
