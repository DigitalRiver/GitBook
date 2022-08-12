---
description: Learn how to configure iDEAL for DigitalRiver.js with Elements.
---

# Configuring iDEAL

If you're using[ DigitalRiver.js with Elements](../), you can create an [iDEAL ](../../../supported-payment-methods/ideal.md)payment method for your app or website in four easy steps:

* [Step 1: Build an iDEAL Source Request object](configuring-ideal.md#step-1-build-an-ideal-source-request-object)
* [Step 2: Create an iDEAL source using DigitalRiver.js](configuring-ideal.md#step-2-create-an-ideal-source-using-digitalriver.js)
* [Step 3: Authorize an iDEAL source](configuring-ideal.md#step-3-authorize-an-ideal-source)
* [Step 4: Use the authorized source](configuring-ideal.md#step-4-use-the-authorized-source)

### Step 1: Build an iDEAL source request object

Build an iDEAL Source Request object. An iDEAL Source Request object requires the following fields:

| Field       | Value                                                                                                          |
| ----------- | -------------------------------------------------------------------------------------------------------------- |
| `type`      | `ideal`                                                                                                        |
| `sessionID` | The payment session identifier.                                                                                |
| `owner`     | An [Owner object](common-payment-objects.md#owner-object).                                                     |
| `ideal`     | An [iDEAL source details object](configuring-ideal.md#ideal-source-details-object). (This is currently empty.) |

#### iDEAL source details object

Create an iDEAL source details object.

{% code overflow="wrap" %}
```javascript
{
    "returnUrl": "https://example.com",
}
```
{% endcode %}

| Field       | Required/Optional | Description                                                                                                                                                           |
| ----------- | ----------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `returnUrl` | Required          | If you choose the full redirect flow, this is where you will redirect your customer after the customer authorizes or cancels the payment within the iDEAL experience. |

### Step 2: Create an iDEAL source using DigitalRiver.js

Use the DigitalRiver.js library to create and mount elements to the HTML container.

{% hint style="info" %}
The `address` object must contain postal code and state/province data that **** [adheres to a standardized format](../../../../cart/creating-or-updating-a-cart/providing-address-information.md) using the `state` attribute. Note that the `state` attribute listed below corresponds to the `countrySubdivision` attribute used when providing address information. The payment session manages the correct field name on the backend.
{% endhint %}

{% code overflow="wrap" %}
```javascript
var sourceData = {
    "type": "ideal",
    "sessionId": "ea03bf6f-84ef-4993-b1e7-b7d5ecf71d1f",
    "owner":{
        "firstName":"John",
        "lastName":"Doe",
        "email":"jdoe@email.com",
        "phoneNumber":"0614811096",
        "address":{
            "line1":"Hans Vonkstraat 26",
            "line2":"",
            "city":"Hengelo",
            "postalCode":"7558 BN",
            "country":"NL"
        }
    },
    "ideal": {
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

#### iDEAL source response example

{% tabs %}
{% tab title="Source response" %}
{% code overflow="wrap" %}
```javascript
{
   "clientId":"gc",
   "channelId":"drdod15",
   "liveMode":false,
   "id":"f1e89f7a-4857-4e0a-9c31-bdb70401fea0",
   "sessionId":"ea03bf6f-84ef-4993-b1e7-b7d5ecf71d1f",
   "clientSecret":"f1e89f7a-4857-4e0a-9c31-bdb70401fea0_afe71fe9-f4fd-4a70-b6d9-edd808ed2190",
   "type":"ideal",
   "reusable":false,
   "owner":{
      "firstName":"John",
      "lastName":"Doe",
      "email":"jdoe@email.com",
      "phoneNumber":"0614811096",
      "address":{
         "line1":"Hans Vonkstraat 26",
         "city":"Hengelo",
         "country":"NL",
         "postalCode":"7558 BN"
      }
   },
   "amount":"100.00",
   "currency":"EUR",
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
   "ideal":{}
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Step 3: Authorize an iDEAL source

When you create an iDEAL source, the customer must authorize the charge through their payment provider. You can accomplish this by redirecting the customer to their payment provider.&#x20;

#### Redirecting the customer for iDEAL authorization

To redirect the customer to the payment provider for authorization, use the `redirectUrl` parameter in your [`createSource` response](../../../../general-resources/reference/digitalriver-object.md#createsource-sourcedata).

{% code overflow="wrap" %}
```javascript
window.location.href = sourceResponse.redirect.redirectUrl;
```
{% endcode %}

The payment provider will present the customer with the transaction details where they can authorize or cancel the transaction. A successful authorization redirects the customer to the iDEAL Return URL parameter you specified when you created the source.&#x20;

Once authorized, the source `state` will change to `chargeable`.

{% code title="Source response" overflow="wrap" %}
```javascript
{
   "clientId":"gc",
   "channelId":"drdod15",
   "liveMode":false,
   "id":"f1e89f7a-4857-4e0a-9c31-bdb70401fea0",
   "sessionId":"ea03bf6f-84ef-4993-b1e7-b7d5ecf71d1f",
   "clientSecret":"f1e89f7a-4857-4e0a-9c31-bdb70401fea0_afe71fe9-f4fd-4a70-b6d9-edd808ed2190",
   "type":"ideal",
   "reusable":false,
   "owner":{
      "firstName":"John",
      "lastName":"Doe",
      "email":"jdoe@email.com",
      "phoneNumber":"0614811096",
      "address":{
         "line1":"Hans Vonkstraat 26",
         "city":"Hengelo",
         "country":"NL",
         "postalCode":"7558 BN"
      }
   },
   "amount":"100.00",
   "currency":"EUR",
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
   "ideal":{}
}
```
{% endcode %}

### Step 4: Use the authorized source

Once authorized, you can use the source by [attaching it to a cart](../../../sources/#attaching-a-payment-method-to-an-order-or-cart).

{% tabs %}
{% tab title="POST /v1/shoppers/me/carts/active/apply-payment-method" %}
{% code overflow="wrap" %}
```javascript
{
  "paymentMethod": {
    "sourceId": "f1e89f7a-4857-4e0a-9c31-bdb70401fea0"
  }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}
