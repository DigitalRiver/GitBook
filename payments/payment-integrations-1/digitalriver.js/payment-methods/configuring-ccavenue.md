---
description: Learn how to configure CCAvenue for DigitalRiver.js with Elements.
---

# Configuring CCAvenue

CCAvenue is an auto-settle payment method offering locale India payment options such as Credit Card, Wallet, Net Banking, and UPI.&#x20;

## Configuring CCAvenue for DigitalRiver.js

Create a method for your app or website in four easy steps:

* [Step 1: Build a CCAvenue Source Request and Details object](configuring-ccavenue.md#step-1-build-a-ccavenue-source-request-and-details-object)
* [Step 2: Create a CCAvenue source using DigitalRiver.js](configuring-ccavenue.md#step-2-create-a-ccavenue-source-using-digitalriver.js)
* [Step 3: Authorize the CCAvenue source](configuring-ccavenue.md#step-3-authorize-the-ccavenue-source)
* [Step 4: Use the authorized source](configuring-ccavenue.md#step-4-use-the-authorized-source)

### Step 1: Build a CCAvenue Source Request and Details object

Build the CCAvenue Source Request and Details objects.&#x20;

#### CCAvenue Source Request object

The CCAvenue Source Request object requires the following fields.

| Field       | Value                                                                                        |
| ----------- | -------------------------------------------------------------------------------------------- |
| `type`      | `ccavenue`                                                                                   |
| `sessionId` | The payment session identifier.                                                              |
| `owner`     | An [Owner object](common-payment-objects.md#owner-object).                                   |
| `ccavenue`  | A [CCAvenue Source Details object](configuring-ccavenue.md#ccavenue-source-details-object).  |

#### CCAvenue Source Details object

The CCAvenue Source Details object requires the following fields.

{% code overflow="wrap" %}
```javascript
{
    "returnUrl": "https://example.com/return",
    "cancelUrl": "https://example.com/cancel"
}
```
{% endcode %}

The CCAvenue Source Details object requires the following field.

| Field       | Required/Optional | Description                                                                                         |
| ----------- | ----------------- | --------------------------------------------------------------------------------------------------- |
| `returnUrl` | Required          | Where you will redirect your customer after the customer authorizes within the CCAvenue experience. |
| `cancelUrl` | Required          | Where you will redirect your customer after the customer cancels within the CCAvenue experience.    |

### Step 2: Create a CCAvenue source using DigitalRiver.js

Use the DigitalRiver.js library to create and mount elements to the HTML container.

{% hint style="info" %}
Note the following requirements when configuring CCAvenue:

* The `address` object must contain [postal code](../../../../integration-options/checkouts/creating-checkouts/providing-address-information.md#postal-code-validations) and [state/province](../../../../integration-options/checkouts/creating-checkouts/providing-address-information.md#states-and-province-validations) data that [adhere to a standardized format](../../../../integration-options/checkouts/creating-checkouts/providing-address-information.md#postal-code-and-state-province-validations).
* CCAvenue's risk policy requires the shopper's phone number (a ten-digit numeric value) in the address object, which cannot be empty. However, Digital River does not validate the phone number.
{% endhint %}

{% code overflow="wrap" %}
```javascript
let ccavenueSourceData = {
    "type": "ccavenue",
    "sessionId": "3c9473b0-630d-4f20-af61-63d3aa8acb35",
    "owner": {
        "firstName": "John",
        "lastName": "Doe",
        "email": "john.doe@digitalriver.com",
        "phoneNumber": "1306372509",
        "address":{
            "line1":"34th Floor, Promod Industrial Estate, Western X-highway, B/h Kohinoor Ind Est, Goregaon (e)",
            "line2":"",
            "city":"Mumbai",
            "state":"Maharashtra",
            "postalCode":"400063",
            "country":"IN"
        }
    },
    "ccavenue": {
        "returnUrl": "https://example.com/return",
        "cancelUrl": "https://example.com/cancel"
    }
}
 
digitalriver.createSource(ccavenueSourceData).then(function(result) {
    if (result.error) {
        //handle errors as something went wrong
    } else {
        var source = result.source;
     
        //do something with the created source
    }
});
```
{% endcode %}

#### **CCAvenue** source example

{% code overflow="wrap" %}
```javascript
{
    "clientId": "gc",
    "channelId": "drdod15",
    "liveMode": false,
    "id": "5ce08114-143b-4bf6-ae0e-6fc501ee0c24",
    "clientSecret": "5ce08114-143b-4bf6-ae0e-6fc501ee0c24_a468b08e-2c47-4531-82af-d48d80ff6dcc",
    "type": "ccavenue",
    "reusable": false,
    "owner": {
        "firstName": "John",
        "lastName": "Doe",
        "email": "john.doe@digitalriver.com",
        "phoneNumber": "13063725095",
        "address":{
            "line1":"34th Floor, Promod Industrial Estate, Western X-highway, B/h Kohinoor Ind Est, Goregaon (e)",
            "line2":"",
            "city":"Mumbai",
            "state":"Maharashtra",
            "postalCode":"400063",
            "country":"IN"
        }
    },
    "amount": "10.00",
    "currency": "INR",
    "state": "pending_redirect",
    "creationIp": "10.81.3.92",
    "createdTime": "2020-02-26T02:48:11.508Z",
    "updatedTime": "2020-02-26T02:48:11.508Z",
    "flow": "redirect",
    "redirect": {
        "redirectUrl": "https://api.digitalriverws.com:443/payments/redirects/51314834-9bf9-483f-b3a7-4b36a14d3f5c?apiKey=pk_hc_e03ee62c0d964bb3ac75595b1203d13c",
        "returnUrl": "https://example.com/return",
        "cancelUrl": "https://example.com/cancel"
    },
    "ccavenue": {}
}
```
{% endcode %}

#### Payment options

CCAvenue offers multiple payment options. The `bankCode` identifies the payment options and determines the value of the `subType` field.

The `bankCode` value will be used as the subType value unless the `bankCode` is `"Credit Card"`, then the `bankName` will be used as the `subType`.&#x20;

{% code title="Credit Card" overflow="wrap" %}
```json
"ccavenue": {

    "bankReferenceNumber": "1634229024157",
    "accountToken": "71826934100000000000000575766005",
    "trackingId": "310007639563",
    "subType": "Visa",
    "bankName": "Visa",
    "bankCode": "Credit Card",
    "orderStatus": "Success"
}
```
{% endcode %}

{% code title="Net Banking" overflow="wrap" %}
```json
"ccavenue": {
    "bankReferenceNumber": "1634229110338",
    "accountToken": "71826934100000000000000575766005",
    "trackingId": "310007639565",
    "subType": "Net Banking",
    "bankName": "AvenuesTest",
    "bankCode": "Net Banking",
    "orderStatus": "Success"
}
```
{% endcode %}

{% code title="Wallet" overflow="wrap" %}
```json
"ccavenue": {
    "bankReferenceNumber": "1634229189578",
    "accountToken": "71826934100000000000000575766005",
    "trackingId": "310007639569",
    "subType": "Wallet",
    "bankName": "AvenuesTest",
    "bankCode": "Wallet",
    "orderStatus": "Success"

```
{% endcode %}

{% code title="UPI" overflow="wrap" %}
```json
"ccavenue": {
    "bankReferenceNumber": "377494",
    "accountToken": "71826934100000000000000575766005",
    "trackingId": "310007639571",
    "subType": "Unified Payments",
    "bankName": "UPI",
    "bankCode": "Unified Payments",
    "orderStatus": "Success"
}

```
{% endcode %}

| Field                 | Optional/Required | Description                                          |
| --------------------- | ----------------- | ---------------------------------------------------- |
| `bankReferenceNumber` | Required          | The bank reference nubmer for the shopper's account. |
| `accountToken`        | Required          | The shopper's account token.                         |
| `trackingId`          | Required          | The tracking identifier for the order.               |

### Step 3: Authorize the CCAvenue source

When you create a CCAvenue source, the customer must authorize the charge through their payment provider. You can accomplish this by redirecting the customer to their payment provider.

#### Redirecting the customer for CCAvenue authorization

Use the `redirectUrl` parameter in your `createSource` response to redirect your customer to the payment provider for authorization.

{% code overflow="wrap" %}
```javascript
window.location.href = sourceResponse.redirect.redirectUrl;
```
{% endcode %}

The payment provider will present the customer with the transaction details, and the customer can authorize or cancel the transaction. A successful authorization redirects the customer to the CCAvenue Return URL parameter specified when you created the source.

Once authorized, the source state will change to `chargeable`.

### Step 4: Use the authorized source

Once authorized, you can use the source by attaching it to a [checkout ](configuring-ccavenue.md#option-1-attach-the-source-to-a-checkout)or a [customer](configuring-ccavenue.md#option-2-attach-the-source-to-a-customer).

#### Option 1: Attach the source to a checkout

{% code title="POST /checkouts/{id}" overflow="wrap" %}
```javascript
{
  "customerId": "5774321008",
  "sourceId": "src_5ce08114-143b-4bf6-ae0e-6fc501ee0c24"
}
```
{% endcode %}

### Option 2: Attach the source to a customer

{% code title="POST /customers/{id}/sources/{sourcesId}" overflow="wrap" %}
```javascript
{
  "id": "5774321008",
  "sourceId": "src_5ce08114-143b-4bf6-ae0e-6fc501ee0c24"
}
```
{% endcode %}

## Testing CCAvenue

See [Testing the CCAvenue payment method](../../../../developer-resources/testing-scenarios.md#testing-the-ccavenue-payment-method) for testing instructions.
