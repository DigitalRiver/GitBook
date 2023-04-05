---
description: Learn how to configure Trustly for DigitialRiver.js with Elements.
---

# Configuring Trustly

If you're using [DigitalRiver.js with Elements](../), you can create a [Trustly ](../../../supported-payment-methods/trustly.md)payment method for your app or website in four easy steps:

Create a Trustly payment method for your app or website in four easy steps:

* [Step 1: Build a Trustly Source Request object](configuring-trustly.md#step-1-build-a-trustly-source-request-object)&#x20;
* [Step 2: Create a Trustly source using DigitalRiver.js](configuring-trustly.md#step-2-create-a-trustly-source-using-digitalriver.js)&#x20;
* [Step 3: Authorize a Trustly source](configuring-trustly.md#step-3-authorize-the-trustly-source)&#x20;
* [Step 4: Use the authorized source](configuring-trustly.md#step-4-use-the-authorized-source)

### Step 1: Build a Trustly Source Request object

Build a Trustly Source Request object. A Trustly Source Request object requires the following fields:

| Field       | Value                                                                                    |
| ----------- | ---------------------------------------------------------------------------------------- |
| `type`      | `trustly`                                                                                |
| `sessionId` | The payment session identifier.                                                          |
| `owner`     | An [Owner Object](common-payment-objects.md#owner-object).                               |
| `trustly`   | A [Trustly Source Details object](configuring-trustly.md#trustly-source-details-object). |

#### **Trustly Source Details Object**

Create a Trustly source details object.

{% code overflow="wrap" %}
```javascript
{
    "returnUrl": "https://example.com",
}
```
{% endcode %}

| Field       | Required/Optional | Description                                                                                                                                                             |
| ----------- | ----------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `returnUrl` | Required          | If you choose the full redirect flow, this is where you will redirect your customer after the customer authorizes or cancels the payment within the Trustly experience. |

### Step 2: Create a Trustly source using DigitalRiver.js

Use the DigitalRiver.js library to create and mount elements to the HTML container.&#x20;

{% hint style="info" %}
The `address` object must contain postal code and state/province data that [adheres to a standardized format](../../../../shopper-apis/cart/creating-or-updating-a-cart/providing-address-information.md) using the `state` attribute. Note that the `state` attribute listed below corresponds to the `countrySubdivision` attribute used when providing address information. The payment session manages the correct field name on the backend.
{% endhint %}

{% code overflow="wrap" %}
```javascript
var sourceData = {
    "type": "trustly",
    "sessionId": "ea03bf6f-84ef-4993-b1e7-b7d5ecf71d1f",
    "owner":{
        "firstName":"John",
        "lastName":"Doe",
        "email":"jdoe@email.com",
        "phoneNumber":"077 1723 6984",
        "address":{
            "line1":"110  Uxbridge Road",
            "line2":"",
            "city":"SLAUGHDEN",
            "postalCode":"IP15 9RA",
            "country":"GB"
        }
    },
    "trustly": {
        "returnUrl": "https://example.com"
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

#### **Trustly Source response example**

{% code title="Source response" overflow="wrap" %}
```javascript
{
   "clientId":"gc",
   "channelId":"drdod15",
   "liveMode":false,
   "id":"f1e89f7a-4857-4e0a-9c31-bdb70401fea0",
   "sessionId":"ea03bf6f-84ef-4993-b1e7-b7d5ecf71d1f",
   "clientSecret":"f1e89f7a-4857-4e0a-9c31-bdb70401fea0_afe71fe9-f4fd-4a70-b6d9-edd808ed2190",
   "type":"trustly",
   "reusable":false,
   "owner":{
      "firstName":"John",
      "lastName":"Doe",
      "email":"jdoe@email.com",
      "phoneNumber":"077 1723 6984",
      "address":{
            "line1":"110  Uxbridge Road",
            "line2":"",
            "city":"SLAUGHDEN",
            "postalCode":"IP15 9RA",
            "country":"GB"
        }
   },
   "amount":"100.00",
   "currency":"GBP",
   "state":"pending_redirect",
   "creationIp":"209.87.180.27",
   "createdTime":"2022-01-24T16:23:12.823Z",
   "updatedTime":"2022-01-24T16:23:12.823Z",
   "flow":"redirect",
   "redirect":{
      "redirectUrl":"https://api.digitalriver.com:443/payments/redirects/6fccf5be-7c6f-4135-9a96-f5e943fc3bad?apiKey=pk_sys_c2608001bba7477eae22808e1eb138db",
      "returnUrl":"https://example.com",
      "offline":false
   },
   "language":"en",
   "trustly":{}
}
```
{% endcode %}

### Step 3: Authorize the Trustly source

When you create a Trustly source, the customer is required to authorize the charge through their payment provider. You can accomplish this by redirecting the customer to their payment provider.

#### **Redirecting the customer for Trustly authorization**

To redirect your customer to the payment provider for authorization, use the redirectUrl parameter in your [`createSource` response](../../../../general-resources/reference/digitalriver-object.md#createsource-sourcedata).

```javascript
window.location.href = sourceResponse.redirect.redirectUrl;
```

The payment provider will present the customer with the transaction details where they can authorize or cancel the transaction. A successful authorization redirects the customer to the Trustly Return URL parameter you specified when you created the source.

Once authorized, the source state will change to chargeable.

{% code overflow="wrap" %}
```javascript
{
   "clientId":"gc",
   "channelId":"drdod15",
   "liveMode":false,
   "id":"f1e89f7a-4857-4e0a-9c31-bdb70401fea0",
   "sessionId":"ea03bf6f-84ef-4993-b1e7-b7d5ecf71d1f",
   "clientSecret":"f1e89f7a-4857-4e0a-9c31-bdb70401fea0_afe71fe9-f4fd-4a70-b6d9-edd808ed2190",
   "type":"trustly",
   "reusable":false,
   "owner":{
      "firstName":"John",
      "lastName":"Doe",
      "email":"jdoe@email.com",
      "phoneNumber":"077 1723 6984",
      "address":{
            "line1":"110  Uxbridge Road",
            "line2":"",
            "city":"SLAUGHDEN",
            "postalCode":"IP15 9RA",
            "country":"GB"
        }
   },
   "amount":"100.00",
   "currency":"GBP",
   "state":"chargeable",
   "creationIp":"209.87.180.27",
   "createdTime":"2022-01-24T16:23:12.823Z",
   "updatedTime":"2022-01-24T16:23:12.823Z",
   "flow":"redirect",
   "redirect":{
      "redirectUrl":"https://api.digitalriver.com:443/payments/redirects/6fccf5be-7c6f-4135-9a96-f5e943fc3bad?apiKey=pk_sys_c2608001bba7477eae22808e1eb138db",
      "returnUrl":"https://example.com",
      "offline":false
   },
   "language":"en",
   "trustly":{}
}
```
{% endcode %}

### Step 4: Use the authorized source

Once authorized, you can use the source by [attaching it to a cart](wire-transfer.md#attach-the-source-to-a-cart).

{% code title="POST /v1/shoppers/me/carts/active/apply-payment-method" overflow="wrap" %}
```javascript
{
  "paymentMethod": {
    "sourceId": "f1e89f7a-4857-4e0a-9c31-bdb70401fea0"
  }
}
```
{% endcode %}
