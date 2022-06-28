---
description: >-
  Learn how to create a Delayed Payment Instructions element that will generate
  a template containing instructions for delayed payment.
---

# Delayed payment instructions element

You can use the Delayed Payment Instructions element to generate a template that contains the instructions that explain how to complete payment for delayed payment types such as: &#x20;

* ****[**Boleto**](../../payment-methods/boleto.md)–where the shopper can go to a variety of locations with cash or via bank transfer to make a payment.
* ****[**bPay**](../../payment-methods/bpay.md)–where the shopper can transfer funds from their bank account to make a payment.
* ****[**Konbini**](../../payment-methods/konbini.md)–where the shopper has to go to a convenience store to make their payment.
* ****[**Wire Transfer**](../../payment-methods/wire-transfer.md)–where the shopper has to go to their bank to wire money to the payment partner's bank.

You can style and arrange this content using custom CSS. Click [here ](https://tools.drapi.io/cm/delayed-payments/delayed-payment-instructions-builder)to see an example of the output.

## Creating a Delayed Payment Instructions element

To create a Delayed Payment Instructions element, use the `createElement` function exposed through the DigitalRiver Object. You can localize the content by using the localization functionality of DigitalRiver.js.

The Delayed Payment Instructions element also requires an `options` object. The `options` object requires the following attributes:

| Attribute          | Description                       |
| ------------------ | --------------------------------- |
| sourceId           | The source ID.                    |
| sourceClientSecret | The client secret for the source. |

{% tabs %}
{% tab title="Example" %}
```javascript
let options = {
    "sourceId": "fc8b2df1-2a57-4b2d-82bb-dc62081d76c4",
    "sourceClientSecret": "fc8b2df1-2a57-4b2d-82bb-dc62081d76c4_deb0d81e-0666-4189-a1c3-ed677b1a5b2a"
}
 
let delayedPaymentInstructions = digitalriver.createElement('delayedpaymentinstructions', options);
```
{% endtab %}
{% endtabs %}

## Delayed Payment Instructions element functions

### delayedPaymentInstructions.mount();

Call this function to place the created Delayed Payment Instructions element on your page.

{% tabs %}
{% tab title="Explain" %}
```javascript
<div id="delayed-payment-container"></div>
 
delayedPaymentInstructions.mount("delayed-payment-container");
```
{% endtab %}
{% endtabs %}

## Delayed Payment Instructions element events

### delayedPaymentInstructions.on('event', handler);



| Event                                                  | Triggered When                 |
| ------------------------------------------------------ | ------------------------------ |
| [ready](delayed-payment-instructions-element.md#ready) | The created element is loaded. |

### Ready

A Ready event triggers when the Delayed Payment Instructions element has loaded.

{% tabs %}
{% tab title="Example" %}
```javascript
delayedPaymentInstructions.on('ready', function(event) {
    //delayed payment instructions element is ready
});
```
{% endtab %}
{% endtabs %}

| Key         | Value                      |
| ----------- | -------------------------- |
| elementType | delayedPaymentInstructions |
