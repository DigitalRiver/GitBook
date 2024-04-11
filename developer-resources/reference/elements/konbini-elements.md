---
description: Learn how to use Konbini elements.
---

# Konbini elements

With DigitalRiver.js, you can create a Konbini element that will automatically retrieve and build a select dropdown that can be styled and placed on your page like other DigitalRiver.js elements.

## **Creating a Konbini element**

To create a Konbini element, you should use the `createElement` function exposed through the DigitalRiver object. This object follows the same pattern and allows for the same [custom classes](./#custom-classes) and [styles ](./#custom-styles)as other elements.

{% tabs %}
{% tab title="Example" %}
```javascript
var konbiniOptions = {
    classes: {
        base: "DRElement",
        complete: "konbini-complete",
        empty: "konbini-empty",
        focus: "konbini-focus"
    },
    style: {
        base: {
            color: '#495057',
            height: '35px',
            fontSize: '1rem',
            fontFamily: 'apple-system,BlinkMacSystemFont,Segoe UI,Roboto,Helvetica Neue,Arial,sans-serif',
            // fontWeight: 'lighter',
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
    }
};


let konbini = digitalriverpayments.createElement('konbini', konbiniOptions);
```
{% endtab %}
{% endtabs %}

## **Konbini element functions**

### konbini.mount();

Call this function to place the created Konbini element on your page.

{% tabs %}
{% tab title="Example" %}
```javascript
<div id="konbini"></div>

konbini.mount('konbini');
```
{% endtab %}
{% endtabs %}

### konbini.unmount();

Call this function to remove the Konbini element from your page. The element may be re-added to your page by calling `mount()`.

{% tabs %}
{% tab title="Example" %}
```javascript
konbini.unmount();
```
{% endtab %}
{% endtabs %}

### konbini.destroy();

Call this function to remove the Konbini element from your page as well as remove its functionality. You cannot re-add the destroyed element to your page via `mount()`.

{% tabs %}
{% tab title="Example" %}
```javascript
konbini.destroy();
```
{% endtab %}
{% endtabs %}

### konbini.update();

Call this function to update the Konbini element's data.

{% tabs %}
{% tab title="Example" %}
```javascript
let konbiniOptions = {
    classes: {
        base: "DRElement",
        complete: "konbini-complete",
        empty: "konbini-empty",
        focus: "konbini-focus"
    },
    style: {
        base: {
            color: '#495057',
            height: '35px',
            fontSize: '1rem',
            fontFamily: 'apple-system,BlinkMacSystemFont,Segoe UI,Roboto,Helvetica Neue,Arial,sans-serif',
            // fontWeight: 'lighter',
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
    }
};


konbini.update(konbiniOptions);
```
{% endtab %}
{% endtabs %}

## Konbini element events - konbini.on('event', handler);

Use this functionality to monitor events that can be used to build and enhance your purchase flow.

| Event                                | Triggered When                                                       |
| ------------------------------------ | -------------------------------------------------------------------- |
| [ready](konbini-elements.md#ready)   | The created element is loaded and ready to accept an update request. |
| [focus](konbini-elements.md#focus)   | The element has gained focus.                                        |
| [blur](konbini-elements.md#blur)     | The element has lost focus.                                          |
| [change](konbini-elements.md#change) | The element's state has changed.                                     |

#### Ready

The Ready event triggers when the Konbini Element has loaded and is available to take an `update()` call.

{% tabs %}
{% tab title="Example" %}
```javascript
konbini.on('ready', function(event) {
    //konbini element is ready and can accept an update call
});
```
{% endtab %}
{% endtabs %}

In addition to the type of element returned in the ready function, the online banking element returns `hasAvailableBanks`. This Boolean reflects whether the currency and country combination specified has banks available for payment. If this is false, there are no banks available for payment.

| Key                | Value                                                                           |
| ------------------ | ------------------------------------------------------------------------------- |
| elementType        | onlinebanking                                                                   |
| hasAvailableStores | A true or false value signaling whether there are stores available for payment. |

{% tabs %}
{% tab title="Response object" %}
```javascript
{
    elementType: "konbini",
    hasAvailableStores: true
}
```
{% endtab %}
{% endtabs %}

### Focus

A Focus event triggers when the element gains focus.

{% tabs %}
{% tab title="Example" %}
```javascript
konbini.on('focus', function(event) {
    //receive the event
}
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Response object" %}
```javascript
{
    elementType: "konbini"
}
```
{% endtab %}
{% endtabs %}

### Blur

A Blur event triggers when the Konbini element no longer has focus.

{% tabs %}
{% tab title="Example" %}
```javascript
konbini.on('blur', function(event) {
    //receive the event
}
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Response object" %}
```javascript
{
    elementType: "konbini"
}
```
{% endtab %}
{% endtabs %}

### Change

A Change event triggers when the Konbini element's state has changed. When using this element, you will only receive this event when the customer selects a store.

{% tabs %}
{% tab title="Example" %}
```javascript
konbini.on('change', function(event) {
    console.log('konbini change', event);
});
```
{% endtab %}
{% endtabs %}

| Key         | Value Description                           |
| ----------- | ------------------------------------------- |
| complete    | Whether the element is in a complete state. |
| empty       | Whether the element is empty.               |
| elementType | The element type.                           |
| error       | An error object (if applicable).            |
| value       | The value of the selected option.           |

{% tabs %}
{% tab title="Response object" %}
```javascript
{
    complete: true,
    empty: false,
    elementType: "konbini",
    error: null,
    value: "86"
}
```
{% endtab %}
{% endtabs %}

In this flow, you can use the `createSource` method to create a source using the Konbini element.
