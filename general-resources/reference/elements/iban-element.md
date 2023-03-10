---
description: Learn how to use the IBAN element.
---

# IBAN element

An IBAN, or International Bank Account Number, includes various numeric identifiers, such as account number and country code, which help financial institutions process international payments more quickly and without errors.

With DigitalRiver.js, you can create an IBAN element that will create a field to collect a shopper's IBAN number. The IBAN element can be styled and placed on your page like other DigitalRiver.js elements.

## Creating an IBAN element <a href="#creating-an-iban-element" id="creating-an-iban-element"></a>

To create an IBAN element, use the `createElement` function exposed through the DigitalRiver Object. This object follows the same pattern and allows for the same [custom classes](./#custom-classes) and [styles ](./#custom-styles)as other elements.

{% tabs %}
{% tab title="Example" %}
{% code overflow="wrap" %}
```javascript
var ibanOptions = {
    "classes": {
        "base": "DRElement",
        "complete": "iban-complete",
        "empty": "iban-empty",
        "focus": "iban-focus"
    },
    "style": {
        "base": {
            "color": "#495057",
            "height": "35px",
            "fontSize": "1rem",
            "fontFamily": "apple-system,BlinkMacSystemFont,Segoe UI,Roboto,Helvetica Neue,Arial,sans-serif",
            ":hover": {
                color: "#ccc",
            },
            "::placeholder": {
                color: "#495057"
            }
        },
        "focus": {
            ":hover": {
                "color": "#495057",
            },
        },
        "empty": {
            ":hover": {
                "color": "#495057",
            },
        },
        "complete": {
            ":hover": {
                "color": "#495057",
            },
        }
    }
};

var iban = digitalriverpayments.createElement('iban', ibanOptions);
```
{% endcode %}
{% endtab %}
{% endtabs %}

## ‌**IBAN element functions**

### ‌iban.mount();

‌Call this function to place the created IBAN element on your page.

{% tabs %}
{% tab title="Example" %}
```javascript
<div id="iban"></div>

iban.mount('iban');
```
{% endtab %}
{% endtabs %}

### ‌iban.unmount();

‌Call this function to remove the IBAN element from your page. The element may be re-added to your page by calling `mount()`.

{% tabs %}
{% tab title="Example" %}
```javascript
iban.unmount();
```
{% endtab %}
{% endtabs %}

### ‌iban.destroy();

‌Call this function to remove the IBAN element from your page, as well as remove its functionality. You cannot re-add the destroyed element to your page via `mount()`.

{% tabs %}
{% tab title="Example" %}
```
iban.destroy();
```
{% endtab %}
{% endtabs %}

## ‌IBAN element events - iban.on('event', handler);

‌The IBAN Element can receive the following events by creating an event listener. Use this function to listen to events that can be used to build and enhance your purchase flow.

| `​`[`ready`](iban-element.md#ready)`​`   | The created element is loaded and ready.     |
| ---------------------------------------- | -------------------------------------------- |
| ``[`​focus​`](iban-element.md#focus)``   | A shopper clicked the element's input field. |
| ``[`​blur​`](iban-element.md#blur)``     | The element has lost focus.                  |
| `​`[`change`](iban-element.md#change)`​` | The element's state has changed.             |

### ‌Ready

‌The Ready event triggers when the IBAN element has loaded.

{% tabs %}
{% tab title="Javascript" %}
```javascript
iban.on('ready', function(event) {
    //iban element is ready 
});
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Response" %}
```javascript
{
    elementType: "iban"
}
```
{% endtab %}
{% endtabs %}

### ‌Focus

The Focus event triggers when the IBAN element has focus.

{% tabs %}
{% tab title="Javascript" %}
```javascript
iban.on('focus', function(event) {
    //receive the event
}
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Response" %}
```javascript
{
    elementType: "iban"
}
```
{% endtab %}
{% endtabs %}

### ‌Blur

‌The Blur event triggers when the IBAN element no longer has focus.

{% tabs %}
{% tab title="Javascript" %}
```javascript
iban.on('blur', function(event) {
    //receive the event
}
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Response" %}
```javascript
{
    elementType: "iban"
}
```
{% endtab %}
{% endtabs %}

### ‌Change

‌The Change event triggers when the IBAN element's state has changed. If an error is detected, DigitalRiver.js will return a Change Event Error object with the event payload.

{% tabs %}
{% tab title="Javascript" %}
```javascript
iban.on('change', function(event) {
    console.log('iban change', event);
});
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Response" %}
```javascript
{
   "empty":false,
   "complete":true,
   "error":null,
   "elementType":"iban"
}
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Invalid response" %}
{% code overflow="wrap" %}
```javascript
{
   "empty":false,
   "complete":false,
   "error":{
      "type":"validation_error",
      "code":"incomplete_iban",
      "message":"Please enter the account number without spaces or dashes."
   },
   "elementType":"iban"
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

| Key           | Value Description                                     |
| ------------- | ----------------------------------------------------- |
| `complete`    | Indicates whether the element is in a complete state. |
| `empty`       | Indicates whether the element is empty.               |
| `elementType` | Identifies the element type.                          |
| `error`       | An error object (if applicable).                      |

In this flow, you can now use the `createSource` method to create a source using the IBAN element.
