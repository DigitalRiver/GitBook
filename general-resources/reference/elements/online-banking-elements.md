---
description: Learn how to use the Online Banking elements.
---

# Online Banking elements

With DigitalRiver.js, you can create an Online Banking element that will automatically retrieve and build a select dropdown that can be styled and placed on your page like other DigitalRiver.js elements.

## Creating an Online Banking element

To create an Online Banking element, use the `createElement` function exposed through the DigitalRiver Object. This object follows the same pattern and allows for the same [custom classes](./#custom-classes) and [styles](./#custom-styles) as other elements.

{% tabs %}
{% tab title="Example" %}
{% code overflow="wrap" %}
```javascript
var onlineBankingOptions = {
    classes: {
        base: "DRElement",
        complete: "onlineBanking-complete",
        empty: "onlineBanking-empty",
        focus: "onlineBanking-focus"
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
    },
    onlineBanking: {
        currency: "USD",
        country: "US"
    }
};
 
 
onlineBanking = digitalriverpayments.createElement('onlinebanking', onlineBankingOptions);
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Online Banking element functions

### onlineBanking.mount();

Call this function to place the created Online Banking element on your page.

{% tabs %}
{% tab title="Example" %}
```javascript
<div id="online-banking"></div>
 
onlineBanking.mount('online-banking');
```
{% endtab %}
{% endtabs %}

### onlineBanking.unmount();

Call this function to remove the Online Banking element from your page. The element may be re-added to your page by calling `mount()`.

{% tabs %}
{% tab title="Example" %}
```javascript
onlineBanking.unmount();
```
{% endtab %}
{% endtabs %}

### onlineBanking.destroy();

Call this function to remove the Online Banking element from your page as well as remove its functionality. You cannot re-add the destroyed element to your page via `mount()`.

{% tabs %}
{% tab title="Example" %}
```javascript
onlineBanking.destroy();
```
{% endtab %}
{% endtabs %}

### onlineBanking.update();

Call this function to update the Online Banking element's data.

{% tabs %}
{% tab title="Example" %}
{% code overflow="wrap" %}
```javascript
let onlineBankingOptions = {
    classes: {
        base: "DRElement",
        complete: "onlineBanking-complete",
        empty: "onlineBanking-empty",
        focus: "onlineBanking-focus"
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
    },
    onlineBanking: {
        currency: currency,
        country: country
    }
};
 
 
onlineBanking.update(onlineBankingOptions);
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Online Banking element events — onlineBanking.on('event', handler);

The Online Banking Element can receive the following events by creating an event listener. Use this function to listen to events that can be used to build and enhance your purchase flow.

| Event                                       | Triggered When                                                       |
| ------------------------------------------- | -------------------------------------------------------------------- |
| [ready](online-banking-elements.md#ready)   | The created element is loaded and ready to accept an update request. |
| [focus](online-banking-elements.md#focus)   | A shopper clicked the element's button.                              |
| [blur](online-banking-elements.md#blur)     | The element has lost focus.                                          |
| [change](online-banking-elements.md#change) | The element's state has changed.                                     |

### Ready

The Ready event triggers when the Online Banking Element has loaded and is available to take an `update()` call.

{% tabs %}
{% tab title="Example" %}
```javascript
onlineBanking.on('ready', function(event) {
    //online banking element is ready and can accept an update call
});
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
**Note**: The online banking element ready listener has additional data that you can use to determine whether or not you should show the option to your customer.
{% endhint %}

&#x20;In addition to the type of element returned in the ready function, the online banking element returns `hasAvailableBanks`. This Boolean reflects whether the currency and country combination specified has banks available for payment. If this is false, there are no banks available for payment.

| Value             | Key                                                                                                                                          |
| ----------------- | -------------------------------------------------------------------------------------------------------------------------------------------- |
| elementType       | onlinebanking                                                                                                                                |
| hasAvailableBanks | A true or false value signals whether there are banks available for the currency and country combination provided when creating the element. |

{% tabs %}
{% tab title="Response object" %}
```javascript
{
    elementType: "onlinebanking",
    hasAvailableBanks: true
}
```
{% endtab %}
{% endtabs %}

### Focus

The Focus event triggers when the online banking element has focus.

{% tabs %}
{% tab title="Example" %}
```javascript
onlineBanking.on('focus', function(event) {
    //receive the event
}
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Response object" %}
```javascript
{
    elementType: "onlinebanking"
}
```
{% endtab %}
{% endtabs %}

### Blur

The Blur event triggers when the online banking element no longer has focus.

{% tabs %}
{% tab title="Example" %}
```javascript
onlineBanking.on('blur', function(event) {
    //receive the event
}
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Response object" %}
```javascript
{
    elementType: "onlinebanking"
}
```
{% endtab %}
{% endtabs %}

### Change

The Change event triggers when the online banking element's state has changed. If you use this element, you will only receive this event when the customer selects a bank.

{% tabs %}
{% tab title="Example" %}
```javascript
onlineBanking.on('change', function(event) {
    console.log('online banking change', event);
});
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Response object" %}
```javascript
{
    complete: true,
    empty: false,
    elementType: "onlinebanking",
    error: null,
    value: "86"
}
```
{% endtab %}
{% endtabs %}

| Key         | Value Description                                     |
| ----------- | ----------------------------------------------------- |
| complete    | Indicates whether the element is in a complete state. |
| empty       | Indicates whether the element is empty.               |
| elementType | The element type.                                     |
| error       | An error object (if applicable).                      |
| value       | The value of the selected option.                     |

In this flow, you can now use the `createSource` method to create a source using the online banking element.
