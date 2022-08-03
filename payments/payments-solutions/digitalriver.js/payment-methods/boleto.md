---
description: >-
  Boleto (meaning 'ticket') Bancário is an official Brazilian payment method,
  which is regulated by the Central Bank of Brazil.
---

# Boleto

Digital River has partnered with PPRO, a payment aggregator, to provide Boleto Bancário. In Brazil, two-thirds of the 200 million population do not have a credit card, Boleto Bancário is highly popular, generating over 50 million transactions a month. Local and regional merchants often offer discounts for Boleto Bancário payments as there is no chargeback risk, and payments are made upfront. After the shopper selects products or services, they go to the client’s Checkout page to select Boleto Bancário. The client site generates the billing details as a print-optimized voucher. The shopper can then pay at a variety of locations with cash or via bank transfer. Once the payment is received, the client ships the purchase order. Boleto Bancário also facilitates online payments via bank transfer or payment card.&#x20;

Boleto Bancário provides the following benefits:&#x20;

* Accounting for around 25% of all online payment transactions, offering Boleto Bancário is a must for doing business in Brazil.&#x20;
* There are literally thousands of ways a shopper can complete their Boleto payment in Brazil: ATMs, bank branches, and online banking, post office, lottery agent, convenience store, or supermarket.&#x20;
* When it comes to online purchases, Boleto Bancário is especially popular for high-ticket items because many consumers still do not feel secure providing their payment details online.&#x20;

For [refunds](../../../../returns-and-refunds-1/refunds/managing-a-refund-for-a-delayed-payment-method.md), the shopper who paid for the original transaction will receive the refund amount. The bank account details for the refund must match the shopper's CPF/CNPJ tax ID. The bank account owner must be identical to the bank account owner of the original request.

{% hint style="warning" %}
Before you can use the Boleto payment method, you must attach a tax ID to the cart.  See [Best practices](boleto.md#best-practices) for instructions.
{% endhint %}

## Configuring Boleto for DigitalRiver.js

Create a Boleto payment method for your app or website in four easy steps:

* [Step 1: Build a Boleto Source Request and Details object](boleto.md#step-2-build-a-boleto-source-request-and-details-object)
* [Step 2: Create a Boleto source using DigitalRiver.js](boleto.md#step-3-create-a-boleto-source-using-digitalriver.js)
* [Step 3: Use the authorized source](boleto.md#step-4-use-the-authorized-source)

### Step 1: Build a Boleto Source Request and Details object

Build the Boleto Source Request and Details object.  The Boleto Source Request object requires the following fields:

| Field            | Value                                                      |
| ---------------- | ---------------------------------------------------------- |
| `type`           | `boletoBancario`                                           |
| `sessionId`      | The payment session identifier.                            |
| `owner`          | An [Owner object](common-payment-objects.md#owner-object). |
| `boletoBancario` | A Boleto Source Details object.                            |

#### Boleto Source Details object

Use the Boleto Source Details object code sample.&#x20;

```javascript
{
    "returnUrl": "https://example.com",
    "nationalId": "16235836597"
}
```

The Boleto Source Details object requires the following fields:

| Field        | Required/Optional | Description                                                                                                                                                                                                                                                                                                                                                                    |
| ------------ | ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `returnUrl`  | Required          | If you choose to use the full redirect flow, this is where you will redirect your customer to after authorizing or canceling within the Boleto experience.                                                                                                                                                                                                                     |
| `nationalId` | Required          | If the shopper is an individual buyer, `nationalId` represents their CPF tax ID. If the shopper is a business shopper, `nationalId` represents their CNPJ tax ID. Use the [DigitalRiver.js Tax Identifier element](https://docs.digitalriver.com/digital-river-api/payment-integrations-1/digitalriver.js/reference/tax-identifier-element) to collect these from the shopper. |

### Step 2: Create a Boleto source using DigitalRiver.js

Use the DigitalRiver.js library to create and mount elements to the HTML container. ****&#x20;

{% hint style="info" %}
The `address` object must contain postal code and state/province data that **** [adheres to a standardized format](../../../../cart/creating-or-updating-a-cart/providing-address-information.md) using the `state` attribute. Note that the `state` attribute listed below corresponds to the `countrySubdivision` attribute used when providing address information. The payment session manages the correct field name on the backend.
{% endhint %}

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

#### Boleto source response example

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

### Step 3: Use the authorized source

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

## Best practices

To use Boleto as a payment method:

1. [Create a cart](https://docs.digitalriver.com/commerce-api/cart/creating-or-updating-a-cart#creating-a-cart).
2. Optional. Set the locale and currency.\
   `curl --location --request GET 'https://{host}/v1/shoppers/me.json?locale=pt_BR&currency=BRL' \`\
   `--header 'Content-Type: application/json'`\
   `--header 'authorization: bearer ***\`
3. Optional. Set cart address to the BR address.
4. [Attach the tax ID to the cart](https://docs.digitalriver.com/commerce-api/cart/managing-tax-identifiers#attaching-a-tax-identifier-to-a-cart). This action inserts the tax ID into the payment session.
5. [Create a Boleto source with a payment session ID](boleto.md#step-2-create-a-boleto-source-using-digitalriver.js). Note that the tax ID is required when creating the Boleto source. The payment session ID provides the tax ID.
6. [Apply the source to the cart](https://docs.digitalriver.com/commerce-api/cart/attaching-a-payment-method-to-a-cart-or-customer#attaching-a-payment-method-to-an-order-or-cart).
7. [Submit the cart](https://docs.digitalriver.com/commerce-api/cart/submitting-a-cart).

## Supported markets

For information on supported markets and currencies for Drop-in and DigitalRiver.js, go to:&#x20;

* **Payment Method Guide:** [digitalriver.com/payment-method-guide](https://www.digitalriver.com/payment-method-guide/)
* **Country Guide:** [digitalriver.com/country-guide/](https://www.digitalriver.com/country-guide/)
