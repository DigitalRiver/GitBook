---
description: Learn how to use the offline refund element.
---

# Offline refund element

With certain payment flows such as [Boleto](../../../payments/payments-solutions/digitalriver.js/payment-methods/configuring-boleto.md), [Konbini](../../../payments/payments-solutions/digitalriver.js/payment-methods/konbini.md), [Online Banking](../../../payments/payments-solutions/digitalriver.js/payment-methods/online-banking.md), or [Wire Transfer](../../../payments/payments-solutions/digitalriver.js/payment-methods/wire-transfer.md), it may be necessary to collect details from your customer to facilitate a refund.&#x20;

## Creating an offline refund element

To create an offline refund element, you should use the createElement function exposed through the DigitalRiver Object. This object follows the same pattern and allows for the same [custom classes](./#custom-classes) and [styles](./#custom-styles) as other elements.

With this element, you must provide a `refundToken`, which is provided in the refund response from our APIs.

{% tabs %}
{% tab title="Example" %}
```javascript
var offlineOptions = {
    classes: {
        base: "DRElement",
        complete: "offline-refund-complete",
        invalid: "offline-refund-invalid"
    },
    style: {
        base: {
            color: '#495057',
            height: '35px',
            fontSize: '1rem',
            fontFamily: 'apple-system,BlinkMacSystemFont,Segoe UI,Roboto,Helvetica Neue,Arial,sans-serif',
            fontWeight: 'lighter',
            ':hover': {
                color: '#ccc',
            },
            '::placeholder': {
                color: '#495057'
            }
        },
        focus: {
            ':hover': {
                color: '#495057',
            },
        },
        empty: {
            ':hover': {
                color: '#495057',
            },
        },
        complete: {
            ':hover': {
                color: '#495057',
            },
        }
    },
    refundToken: 'fb19fceb-a5e7-454d-af1a-017b7bd73d5b'
};
 
 
let offlineRefund = digitalriverpayments.createElement('offlinerefund', offlineOptions);
```
{% endtab %}
{% endtabs %}

## Offline refund element functions

### offlineRefund.mount();

Call this function to place the created offline refund element on your page.

{% tabs %}
{% tab title="Example" %}
```markup
<div id="offline-refund"></div>
 
offlineRefund.mount('offline-refund')
```
{% endtab %}
{% endtabs %}

### offlineRefund.unmount();

Call this function to remove the offline refund element from your page. The element may be re-added to your page by calling `mount()`.

{% tabs %}
{% tab title="Example" %}
```markup
offlineRefund.unmount();
```
{% endtab %}
{% endtabs %}

### offlineRefund.destroy();

Call this function to remove the offline refund element from your page as well as remove its functionality. You cannot re-add an element that has been destroyed to your page via `mount()`.

{% tabs %}
{% tab title="Example" %}
```javascript
offlineRefund.destroy();
```
{% endtab %}
{% endtabs %}

## Offline refund element events - offlineRefund.on('event', handler);

Use this function to listen to events that can be used to build and enhance your purchase flow.

| Event                                      | Triggered When                                           |
| ------------------------------------------ | -------------------------------------------------------- |
| [ready](offline-refund-element.md#ready)   | The created element is loaded and ready to accept input. |
| [change](offline-refund-element.md#change) | The element's state has changed.                         |

### Ready

The Ready event triggers when the element loads and is available to take user input.

{% tabs %}
{% tab title="Example" %}
```javascript

offlineRefund.on('ready', function(event) {
    //offline refund element is ready and can accept user input
});
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Response object" %}
```javascript
{
    elementType: "offlinerefund"
}
```
{% endtab %}
{% endtabs %}

### Change

A change event triggers when the offline refund element's state has changed. If using this element, you will only receive this event when the customer has filled out the form, and the data has been accepted. At this point, you may remove the element from your screen by calling `unmount()` or `destroy()`.

{% tabs %}
{% tab title="Example" %}
```javascript

offlineRefund.on('change', function(event) {
    console.log('offline refund change', event);
});
```
{% endtab %}
{% endtabs %}

| Key         | Value Description                           |
| ----------- | ------------------------------------------- |
| complete    | Whether the element is in a complete state. |
| elementType | The type of element.                        |

{% tabs %}
{% tab title="Response object" %}
```javascript

{
    complete: true,
    empty: false,
    elementType: "offlinerefund",
    error: null
}
```
{% endtab %}
{% endtabs %}

