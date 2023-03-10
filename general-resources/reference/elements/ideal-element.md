---
description: Learn how to use the iDEAL element.
---

# iDEAL element

You can create an iDEAL element that will automatically get a user's agreement and [IBAN number ](iban-element.md#creating-an-iban-element)for single-use and recurring transactions.&#x20;

## Creating an iDEAL element

To create an iDEAL element, use the `createElement` function exposed through the DigitalRiver Object. This object follows the same pattern and allows for the same [custom classes](./#custom-classes) and [styles ](./#custom-styles)as other elements.

The iDEAL element also requires an additional `ideal` object which accepts:

| Attribute   | Description            | Required/Optional |
| ----------- | ---------------------- | ----------------- |
| `sessionId` | The Payment Session ID | Required          |

{% code title="Example" %}
```json
var options = {
	ideal: {
		sessionId: "ee63194d-f681-40d6-9ec2-0943232799be"
    },
    classes: {
        base: "DRElement",
        complete: "custom-complete",
        empty: "custom-empty",
        focus: "custom-focus",
        invalid: "custom-invalid"
    },
    style: {
        base: {
            color: "#495057",
            height: "35px",
            fontSize: "1rem",
            fontFamily: "apple-system,BlinkMacSystemFont,Segoe UI,Roboto,Helvetica Neue,Arial,sans-serif",
            ":hover": {
                color: "#ccc",
            }
        },
        complete: {
            ":hover": {
                color: "#495057",
            },
        },
         empty: {
            ":hover": {
                color: "#495057",
            },
        },
        focus: {
            ":hover": {
                color: "#495057",
            },
        },
        invalid: {
                color: "red"
        }
   }
};

let ideal = digtialriver.createElement("ideal", options);
```
{% endcode %}

## iDEAL element functions

### ideal.mount();

Call this function to place the created iDEAL element on your page.

If your session is not recurring, nothing will display and the payment source created will not be able to be used for subscription usage.

If your session is recurring, the element will display a checkbox that will allow the user to agree to authorize recurring subscription payments.

If the user does not check the box, the payment source created will not be able to be used for subscription usage.

If the user does check the box, they will be required to enter their IBAN number and the payment source created will be able to be used for subscription usage.

{% code title="Example" %}
```json
<div id="ideal"></div>

ideal.mount('ideal');
```
{% endcode %}

### ideal.unmount();

Call this function to remove the iDEAL element from your page. The element may be re-added to your page by calling `mount()`.

{% code title="Example" %}
```json
ideal.unmount();
```
{% endcode %}

### ideal.destroy();

Call this function to remove the iDEAL element from your page as well as remove its functionality. You cannot re-add the destroyed element to your page via `mount()`.

{% code title="Example" %}
```json
ideal.destroy();
```
{% endcode %}

## iDEAL element events - ideal.on('event', handler);

Use this functionality to monitor events that can be used to build and enhance your purchase flow.

| Event    | Triggered When                   |
| -------- | -------------------------------- |
| `ready`  | The created element is loaded.   |
| `change` | The element's state has changed. |

### Ready

The Ready event triggers when the iDEAL Element has loaded.

{% code title="Example" %}
```json
ideal.on('ready', function(event) {
    //ideal element is ready
});
```
{% endcode %}

{% code title="Response object" %}
```json
 {
    "elementType": "ideal"
}
```
{% endcode %}

### Change

A change event triggers when the iDEAL element's state has changed. When using this element, you will only receive this event when the customer agrees to recurring billing and has entered an IBAN number.

{% code title="Example" %}
```json
ideal.on('change', function(event) {
    console.log('ideal change', event);
});
```
{% endcode %}

### Response object

| Key           | Value Description                                                          |
| ------------- | -------------------------------------------------------------------------- |
| `elementType` | The element type                                                           |
| `iban`        | An iban object containing the status of the IBAN field when it is present. |

#### IBAN Object

| Key        | Value Description                              |
| ---------- | ---------------------------------------------- |
| `complete` | Whether the IBAN field is in a complete state. |
| `empty`    | Whether the IBAN field is empty.               |
| `error`    | An error object (if applicable).               |

### Response object - IBAN complete

{% code title="Example" %}
```json
{
    "elementType": "ideal",
    "iban": {
        "complete": true,
        "empty": false,
        "error": null
    }
}
```
{% endcode %}

### Response object - IBAN error

{% code title=" Example" %}
```json
{
    "elementType": "ideal",
    "iban": {
        "complete": false,
        "empty": false,
        "error": {
            "type": "validation_error",
            "code": "incomplete_iban",
            "message": "Please enter the account number without spaces or dashes."
        }
    }
}
```
{% endcode %}

In this flow, you can now use the [createSource()](../digitalriver-object.md#createsource-element-sourcedata) method to create a source using the iDEAL element.
