---
description: >-
  Gain a better understanding of how to perform customized actions in a Prebuilt
  Checkout
---

# Performing actions

In [Prebuilt Checkout](../../../../integration-options/low-code-checkouts/drop-in-checkout.md), various callback functions can be assigned to properties in its[ configuration object](./). Some of these functions accept an optional `actions` parameter, which allows you to:

* [Display custom messages in the order summary section](performing-actions.md#display-custom-order-summary-messages)
* [Customize the thank you page](performing-actions.md#customize-the-order-confirmation)
* [Reject invalid address inputs](performing-actions.md#reject-address-inputs)

{% hint style="info" %}
Some callbacks in the [checkout button configuration object](../rendering-a-checkout-button/) also accept `actions`.  For details, refer to [Performing actions on the checkout button](../rendering-a-checkout-button/performing-actions-on-the-checkout-button.md).
{% endhint %}

## Display custom order summary messages

You can use [`orderSummary`](performing-actions.md#ordersummary) to render specific messages the Prebuilt Checkout window.

### `orderSummary`

The `orderSummary` property in [`actions`](performing-actions.md) allows you to specify whether you want a customized message to be displayed in the [`middle`](performing-actions.md#middle) and/or the [`bottom`](performing-actions.md#bottom) of this section in Prebuilt Checkout.&#x20;

You might find this useful if you'd like to, as an example, inform customers that the order summary amounts aren't final until they've selected a shipping option, provided applicable tax identification numbers, and applied payment.

#### `middle`

This property allows you to access the `middle` of the window's [`orderSummary`](performing-actions.md#ordersummary) section.

#### `bottom`

This property allows you to access the `bottom` of the window's [`orderSummary`](performing-actions.md#ordersummary) section.

#### `addCustomMessage(message, showInfoIcon)`

This function displays a customized message in the [`middle`](performing-actions.md#middle) or [`bottom`](performing-actions.md#bottom) of [`orderSummary`](performing-actions.md#ordersummary). It accepts an optional string, which represents the message you want displayed and an optional boolean, which determines whether Digital River displays an information icon next to your message.

The default value of `showInfoIcon` is `true`.

#### `deleteCustomMessage()`

This function deletes any customized messages that exists in the [`middle`](performing-actions.md#middle) or [`bottom`](performing-actions.md#bottom) of  [`orderSummary`](performing-actions.md#ordersummary).

{% tabs %}
{% tab title="Add and delete custom message" %}
When [`onInit`](./#oninit) executes, the following procedure loads your message in the middle of the order summary section.

<pre class="language-javascript"><code class="lang-javascript"><strong>config.onInit = (checkoutSession, actions) => {
</strong><strong>     actions.orderSummary.middle.addCustomMessage('A message in the middle');  
</strong>};
...
config.onAddressComplete = (address, actions) => {
     actions.orderSummary.middle.deleteCustomMessage();
     actions.orderSummary.bottom.addCustomMessage('A new message at the bottom');
};
</code></pre>

<figure><img src="../../../../.gitbook/assets/message in the middle.png" alt=""><figcaption></figcaption></figure>

After users successfully submit their address information and [`onAddressComplete`](./#onaddresscomplete) executes, the middle message is deleted and a different message is added to the bottom.

<figure><img src="../../../../.gitbook/assets/message at the bottom.png" alt=""><figcaption></figcaption></figure>
{% endtab %}

{% tab title="Add custom message without icon" %}
When [`onInit`](./#oninit) executes, the following procedure loads your message, without an information icon, in the middle of the order summary section.

```javascript
config.onInit = (checkoutSession, actions) => {
     actions.orderSummary.middle.addCustomMessage('A message in the middle', false);  
};
```

<figure><img src="../../../../.gitbook/assets/message in the middle w-o icon.png" alt=""><figcaption></figcaption></figure>
{% endtab %}
{% endtabs %}

## Customize the order confirmation

You can use [`thankYouPage`](performing-actions.md#thankyoupage) to customize the order confirmation stage.&#x20;

### `thankYouPage`

In [`actions`](performing-actions.md), the `thankYouPage` property, which defines the [order confirmation stage](../../../../integration-options/low-code-checkouts/drop-in-checkout.md#order-confirmation), exposes [`replaceDefaultMessage()`](performing-actions.md#replacedefaultmessage-message-showcheckcircleicon).

#### `replaceDefaultMessage(message, showCheckCircleIcon)`

If you omit [`options.thankYouPage`](./#customize-order-confirmation), then you can use `replaceDefaultMessage()` to modify the [default order confirmation](../../../../integration-options/low-code-checkouts/drop-in-checkout.md#order-confirmation).&#x20;

This function accepts a string, which represents the message you want displayed.

If you'd like the order's identifier to be injected into this message, then add `{{orderId}}` to the string. When the template renders, Digital River dynamically replaces this placeholder with the `id` of the [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) in our system or, in the event you passed [`upstreamId`](../../../digital-river-api-reference/checkout-sessions.md#upstream-identifier) in the [create checkout-session request](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions/operation/createDropInCheckoutSession), that value.

The function also accepts an optional boolean that determines whether Digital River displays a circle check icon (a visual cue that the purchase was successful) prior to your customized message.

The default value of `showCheckCircleIcon` is `true`.&#x20;

Invoke `replaceDefaultMessage()` inside [`onInit`](./#oninit) and make sure to pass `checkoutSession` to this callback function.

{% tabs %}
{% tab title="Custom message" %}
When `onInit` executes, the following procedure loads your replacement message in [`thankYouPage`](performing-actions.md#thankyoupage).

```javascript
config.onInit = (checkoutSession, actions) => {
     actions.thankYouPage.replaceDefaultMessage('<p>A customized thank you message. The order number is #{{orderId}}.</p>');  
};
```

<figure><img src="../../../../.gitbook/assets/message on the thank you page.png" alt=""><figcaption></figcaption></figure>
{% endtab %}

{% tab title="Custom message without icon" %}
When `onInit` executes, the following procedure loads your replacement message, without a check circle icon, in [`thankYouPage`](performing-actions.md#thankyoupage).

```javascript
config.onInit = (checkoutSession, actions) => {
     actions.thankYouPage.replaceDefaultMessage('<p>A customized thank you message without a circle check icon. The order number is #{{orderId}}.</p>', false);  
};
```

<figure><img src="../../../../.gitbook/assets/message w-o icon on the thank you page.png" alt=""><figcaption></figcaption></figure>
{% endtab %}
{% endtabs %}

## Reject address inputs

The [`reject()`](performing-actions.md#reject) function, exposed by [`actions`](performing-actions.md), allows you to refuse shipping and billing inputs that you deem to be invalid.&#x20;

### `reject()`

If invoked in [`onAddressComplete`](./#onaddresscomplete), then `reject()` (1) blocks customers from proceeding to the checkout's next stage and (2) displays an error message to them.&#x20;

It accepts an optional string that represents the error message you'd like displayed. If you don't define this parameter, then Digital River displays a default message.

{% tabs %}
{% tab title="Custom error message" %}
```javascript
config.onAddressComplete = (address, actions) => {
    ...
    return actions.reject('Your customized error message');
};
```

<figure><img src="../../../../.gitbook/assets/image (30).png" alt=""><figcaption></figcaption></figure>
{% endtab %}

{% tab title="Default error message" %}
```javascript
config.onAddressComplete = (address, actions) => {
    ...
    return actions.reject();
};
```

<figure><img src="../../../../.gitbook/assets/image (25).png" alt=""><figcaption></figcaption></figure>
{% endtab %}
{% endtabs %}

You can use `reject()` to screen out specific address categories. For example, with a regular expression and `reject()`, you can prevent customers from shipping products to P.O. boxes.

{% tabs %}
{% tab title="Event handler" %}
```javascript
config.onAddressComplete = (address, actions) => {
    if (address.address.shipping === null) {
        console.log("This is a checkout that only contains digital products. No shipping validation needed");
    }
    else {
        let line1 = address.address.shipping.address.line1;
        let line2 = address.address.shipping.address.line2;
        let combinedLines;
        if (line2 !== undefined) {
            combinedLines = line1 + line2;
        }
        else {
            combinedLines = line1;
        }
        const regexPostOfficeBox = /\b[P|p]*(OST|ost)*\.*\s*[O|o|0]*(ffice|FFICE)*\.*\s*[B|b][O|o|0][X|x]\b/;
        let isPostOfficeBox = regexPostOfficeBox.test(combinedLines);
        if (isPostOfficeBox) {
            return actions.reject('We cannot ship to a post office box.\nPlease provide a different shipping address.');
        }
    }
};
```
{% endtab %}

{% tab title="Prebuilt Checkout" %}
<figure><img src="../../../../.gitbook/assets/image (60).png" alt=""><figcaption></figcaption></figure>
{% endtab %}
{% endtabs %}







