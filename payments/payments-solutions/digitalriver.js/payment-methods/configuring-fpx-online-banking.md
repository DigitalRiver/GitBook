---
description: Learn how to configure FXP Online Banking for DigitalRiver.js with Elements.
---

# Configuring FPX Online Banking

If you're using[ DigitalRiver.js with Elements](../), you can create an [FPX Online Banking](../../../supported-payment-methods/fpx-online-banking.md) payment method for your app or website in four easy steps:

* [Step 1: Build an FPX Online Banking Source Request object](configuring-fpx-online-banking.md#step-1-build-an-fpx-online-banking-source-request-object)
* [Step 2: Create an FPX Online Banking source using DigitalRiver.js](configuring-fpx-online-banking.md#step-2-create-an-fpx-online-banking-source-using-digitalriver.js)
* [Step 3: Authorize an FPX Online Banking source](configuring-fpx-online-banking.md#step-3-authorize-the-fpx-online-banking-source)
* [Step 4: Use the authorized source](configuring-fpx-online-banking.md#step-4-use-the-authorized-source)

## Step 1: Build an FPX Online Banking Source Request object

Build an FPX Online Banking Source Request object. An FPX Online Banking Source Request object requires the following fields:

| Field              | Value                                                                                                                      |
| ------------------ | -------------------------------------------------------------------------------------------------------------------------- |
| `type`             | `fpxOnlineBanking`                                                                                                         |
| `sessionid`        | The payment session identifier.                                                                                            |
| `owner`            | An [Owner object](common-payment-objects.md#owner-object).                                                                 |
| `fpxOnlineBanking` | An [FPX Online Banking Source Details object](configuring-fpx-online-banking.md#fpx-online-banking-source-details-object). |

### **FPX Online Banking Source Details Object**

{% code overflow="wrap" %}
```json
{
    "returnUrl": "https://example.com",
}
```
{% endcode %}

| Field       | Required/Optional | Description                                                                                                                                                            |
| ----------- | ----------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `returnUrl` | Required          | If you choose to use the full redirect flow, this is where you will redirect your customer to after authorizing or canceling within the FPX Online Banking experience. |

## Step 2: Create an FPX Online Banking source using DigitalRiver.js

Build an FPX Online Baning source request object. Use the DigitalRiver.js library to create and mount elements to the HTML container.

{% hint style="info" %}
The `address` object must contain postal code and state/province data that [adheres to a standardized format](../../../../shopper-apis/cart/creating-or-updating-a-cart/providing-address-information.md) using the `state` attribute. Note that the `state` attribute listed below corresponds to the `countrySubdivision` attribute used when providing address information. The payment session manages the correct field name on the backend.
{% endhint %}

{% code overflow="wrap" %}
```json
var sourceData = {
    "type": "fpxOnlineBanking",
    "sessionId": "ea03bf6f-84ef-4993-b1e7-b7d5ecf71d1f",
    "owner":{
        "firstName":"John",
        "lastName":"Doe",
        "email":"jdoe@email.com",
        "phoneNumber":"077 1723 6984",
        "address":{
            "line1":"Prai Industrial Estate, Phase 4",
            "line2":"",
            "city":"Perai",
            "state":"Pulau Pinang",
            "postalCode":"13600",
            "country":"MY"
        }
    },
    "fpxOnlineBanking": {
        "returnUrl": "https://example.com"
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

### **FPX Online Banking Source response example**

{% code overflow="wrap" %}
```
{
   "clientId":"gc",
   "channelId":"paylive",
   "liveMode":false,
   "id":"42ff0014-3992-49b7-a3f0-12ec4c374229",
   "sessionId":"ddaef87a-57ee-4491-87b8-fc3e20390600",
   "clientSecret":"42ff0014-3992-49b7-a3f0-12ec4c374229_e3e5cfd7-5750-411d-bad7-94e74d5590e4",
   "type":"fpxOnlineBanking",
   "reusable":false,
   "owner":{
      "firstName":"John",
      "lastName":"Doe",
      "customerId":"502283345689",
      "email":"jdoe@digitalriver.com",
      "phoneNumber":"032692-1961",
      "upstreamId":"123456789",
      "organization":"Digital River",
      "address":{
         "line1":"Prai Industrial Estate, Phase 4,",
         "city":"Perai",
         "state":"Pulau Pinang",
         "country":"MY",
         "postalCode":"13600"
      }
   },
   "amount":"100.00",
   "currency":"MYR",
   "state":"pending_redirect",
   "creationIp":"209.87.180.27",
   "createdTime":"2022-03-29T19:48:27.109Z",
   "updatedTime":"2022-03-29T19:48:27.109Z",
   "flow":"redirect",
   "redirect":{
      "redirectUrl":"https://api.digitalriver.com:443/payments/redirects/b0b27385-dbda-468d-9e49-210147bda1ff?apiKey=pk_sys_c2608001bba7477eae22808e1eb138db",
      "returnUrl":"https://js-test.digitalriver.com/v1/1.20220329.1453/components/redirect-receiver/redirect-receiver.html?controllerId=controller-a4b5a4a4-0db4-43a5-8ba0-01786fd0c338&componentId=redirect-receiver-1757f835-c21b-4f4e-b208-92adc5c30573&action=return",
      "offline":false
   },
   "language":"en",
   "fpxOnlineBanking":{}
}
```
{% endcode %}

## Step 3: Authorize the FPX Online Banking source

When you create an FPX Online Banking source, the customer is redirected to a bank selector age and chooses their preferred bank. They are then redirected to their online bank, where they sign in and review their transaction. The shopper will complete the transaction by authorizing it with an SMS code. You can accomplish this by redirecting the customer to FPX Online Banking.

### **Redirecting the customer for FPX Online Banking authorization**

To redirect your customer use the `redirectUrl` parameter in your `createSource` response.

{% code overflow="wrap" %}
```html
window.location.href = sourceResponse.redirect.redirectUrl;
```
{% endcode %}

The shopper's online bank will present the shopper with the transaction details where they can authorize or cancel the transaction. The shopper will then complete the transaction by authorizing it with an SMS code to complete the order. A successful authorization redirects the customer to the FPX Online Banking Return URL parameter you specified when you created the source.

Once authorized, the source state will change to chargeable.

{% code overflow="wrap" %}
```json
{
   "clientId":"gc",
   "channelId":"paylive",
   "liveMode":false,
   "id":"42ff0014-3992-49b7-a3f0-12ec4c374229",
   "sessionId":"ddaef87a-57ee-4491-87b8-fc3e20390600",
   "clientSecret":"42ff0014-3992-49b7-a3f0-12ec4c374229_e3e5cfd7-5750-411d-bad7-94e74d5590e4",
   "type":"fpxOnlineBanking",
   "reusable":false,
   "owner":{
      "firstName":"John",
      "lastName":"Doe",
      "customerId":"502283345689",
      "email":"jdoe@digitalriver.com",
      "phoneNumber":"032692-1961",
      "upstreamId":"123456789",
      "organization":"Digital River",
      "address":{
         "line1":"Prai Industrial Estate, Phase 4,",
         "city":"Perai",
         "state":"Pulau Pinang",
         "country":"MY",
         "postalCode":"13600"
      }
   },
   "amount":"100.00",
   "currency":"MYR",
   "state":"chargeable",
   "creationIp":"209.87.180.27",
   "createdTime":"2022-03-29T19:48:27.109Z",
   "updatedTime":"2022-03-29T19:48:27.109Z",
   "flow":"redirect",
   "redirect":{
      "redirectUrl":"https://api.digitalriver.com:443/payments/redirects/b0b27385-dbda-468d-9e49-210147bda1ff?apiKey=pk_sys_c2608001bba7477eae22808e1eb138db",
      "returnUrl":"https://js-test.digitalriver.com/v1/1.20220329.1453/components/redirect-receiver/redirect-receiver.html?controllerId=controller-a4b5a4a4-0db4-43a5-8ba0-01786fd0c338&componentId=redirect-receiver-1757f835-c21b-4f4e-b208-92adc5c30573&action=return",
      "offline":false
   },
   "language":"en",
   "fpxOnlineBanking":{}
}
```
{% endcode %}

## Step 4: Use the authorized source

Once authorized, you can use the source by [attaching it to a cart](broken-reference).

{% code title="POST /v1/shoppers/me/carts/active/apply-payment-method" overflow="wrap" %}
```json
{
  "paymentMethod": {
    "sourceId": "f1e89f7a-4857-4e0a-9c31-bdb70401fea0"
  }
}
```
{% endcode %}

## Testing FPX Online Banking

See [Testing redirect payment methods](../../../../resources/testing-scenarios.md#testing-redirect-payment-methods) for testing instructions.
