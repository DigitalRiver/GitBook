---
description: Learn how to configure Boleto for DigitalRiver.js with Elements.
---

# Configuring Boleto

If you're using[ DigitalRiver.js with Elements](../), you can create a [Boleto](../../../supported-payment-methods/boleto.md) payment method for your app or website in three easy steps:

* [Step 1: Build a Boleto Source Request and Details object](configuring-boleto.md#step-2-build-a-boleto-source-request-and-details-object)
* [Step 2: Create a Boleto source using DigitalRiver.js](configuring-boleto.md#step-3-create-a-boleto-source-using-digitalriver.js)
* [Step 3: Use the authorized source](configuring-boleto.md#step-4-use-the-authorized-source)

## Step 1: Build a Boleto Source Request and Details object

Build the Boleto Source Request and Details object.  The Boleto Source Request object requires the following fields:

| Field            | Value                                                                                  |
| ---------------- | -------------------------------------------------------------------------------------- |
| `type`           | `boletoBancario`                                                                       |
| `sessionId`      | The payment session identifier.                                                        |
| `owner`          | An [Owner object](common-payment-objects.md#owner-object).                             |
| `boletoBancario` | A [Boleto Source Details object](configuring-boleto.md#boleto-source-details-object).  |

### Boleto Source Details object

Use the Boleto Source Details object code sample.&#x20;

{% code overflow="wrap" %}
```javascript
{
    "returnUrl": "https://example.com",
    "nationalId": "16235836597"
}
```
{% endcode %}

The Boleto Source Details object requires the following fields:

| Field        | Required/Optional | Description                                                                                                                                                                                                                                                                                                                                                                    |
| ------------ | ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `returnUrl`  | Required          | If you choose to use the full redirect flow, this is where you will redirect your customer to after authorizing or canceling within the Boleto experience.                                                                                                                                                                                                                     |
| `nationalId` | Required          | If the shopper is an individual buyer, `nationalId` represents their CPF tax ID. If the shopper is a business shopper, `nationalId` represents their CNPJ tax ID. Use the [DigitalRiver.js Tax Identifier element](https://docs.digitalriver.com/digital-river-api/payment-integrations-1/digitalriver.js/reference/tax-identifier-element) to collect these from the shopper. |

## Step 2: Create a Boleto source using DigitalRiver.js

Use the DigitalRiver.js library to create and mount elements to the HTML container. ****&#x20;

{% hint style="info" %}
The `address` object must contain postal code and state/province data that **** [adheres to a standardized format](../../../../shopper-apis/cart/creating-or-updating-a-cart/providing-address-information.md) using the `state` attribute. Note that the `state` attribute listed below corresponds to the `countrySubdivision` attribute used when providing address information. The payment session manages the correct field name on the backend.
{% endhint %}

{% code overflow="wrap" %}
```javascript
var data = {
   "type":"boletoBancario",
   "sessionId":"ea03bf6f-84ef-4993-b1e7-b7d5ecf71d1f",
   "owner":{
      "firstName":"John",
      "lastName":"Doe",
      "email":"john.doe@gmail.com",
      "phoneNumber":"1555000000",
      "address":{
         "line1":"123 Main Street",
         "line2":"",
         "city":"Mossoró",
         "state":"SP",
         "postalCode":"59625-105",
         "country":"BR"
      }
   },
   "boletoBancario":{
      nationalId: "16704641000167"
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

### Boleto source response example

{% code overflow="wrap" %}
```javascript
{
   "clientId":"gc",
   "channelId":"drdod15",
   "liveMode":false,
   "id":"42eace34-cd2c-47ff-bcde-5bedbbbffce1",
   "sessionId":"0f97ee7c-4c62-4ec6-b2c6-f36bd744ebdd",
   "clientSecret":"42eace34-cd2c-47ff-bcde-5bedbbbffce1_3606ed97-37c0-47d2-af40-79d062993ac0",
   "type":"boletoBancario",
   "reusable":false,
   "owner":{
      "firstName":"John",
      "lastName":"Doe",
      "email":"john.doe@gmail.com",
      "phoneNumber":"1555000000",
      "address":{
         "line1":"123 Main Street",
         "city":"Mossoró",
         "state":"SP",
         "postalCode":"59625-105",
         "country":"BR"
      }
   },
   "amount":"100.00",
   "currency":"BRL",
   "state":"pending_funds",
   "creationIp":"209.87.180.27",
   "createdTime":"2021-10-18T18:28:36.191Z",
   "updatedTime":"2021-10-18T18:28:36.191Z",
   "flow":"receiver",
   "language":"en",
   "boletoBancario":{
      "documentCode":"23790001246004987209031123456704579990000010000",
      "document":"https://link/to/the/payment-slip.pdf"
   }
}
```
{% endcode %}

## Step 3: Use the authorized source

Once authorized, you can use the source by [attaching it to a cart](../../../sources/#attaching-a-payment-method-to-an-order-or-cart).

{% tabs %}
{% tab title="POST /v1/shoppers/me/carts/active/apply-payment-method" %}
```javascript
{
  "paymentMethod": {
    "sourceId": "e7ba0595-059c-460c-bad8-2812123b9313"
  }
}
```
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
Before you can use the Boleto payment method, you must attach a tax ID to the cart.  See [Submit a Boleto payment flow](../../../sources/using-the-source-identifier.md#submit-a-boleto-payment-flow) for instructions.
{% endhint %}

