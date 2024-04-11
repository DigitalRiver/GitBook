---
description: >-
  Create a Tax Identifier collection element that will automatically collect and
  validate tax identifiers.
---

# Tax Identifier element

With DigitalRiver.js, you can create a Tax Identifier collection element that will automatically collect and validate the tax identifier formats for a specific transaction, which can be styled and placed on your page like other DigitalRiver.js elements.

## Creating a Tax Identifier element

To create a Tax Identifier element, use the `createElement` function exposed through the Digital River object. This object follows the same pattern and allows for the same custom classes and styles as other elements.

The Tax Identifier element also requires an additional `taxIdentifier` object which accepts:

| Attribute     | Description                                                                                                           | Required/Optional                                                                             |
| ------------- | --------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------- |
| sessionId     | The Payment Session ID. If used, the response will automatically filter to be applicable to the specific transaction. | Required if country and sellingEntity are not provided.                                       |
| country       | The country code that represents the expected billing and/or shipping address of the customer.                        | Required if sessionId is not provided.                                                        |
| sellingEntity | The Digital River selling entity which is facilitating the transaction.                                               | Optional if sessionId is not provided. If not provided, a default entity will be selected.    |
| type          | Either "individual" or "business"                                                                                     | Optional. If the type is provided, the rendered inputs will be limited to the specified type. |

{% tabs %}
{% tab title="Example" %}
{% code overflow="wrap" %}
```javascript
var options = {
	taxIdentifier: {
		country: "IT"
    },
    classes: {
        base: "DRElement",
        complete: "taxId-complete",
        empty: "taxId-empty",
        focus: "taxId-focus",
        invalid: "taxId-invalid"
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

let taxIdentifier = digtialriver.createElement("taxidentifier", options);
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Tax Identifier element functions

Learn how to trigger Tax Identifier element functions.

To create a Tax Identifier element, use the `createElement` function exposed through the Digital River object. This object follows the same pattern and allows for the same custom classes and styles as other elements.

The Tax Identifier element also requires an additional `taxIdentifier` object which accepts:

| Attribute     | Description                                                                                                           | Required/Optional                                                                          |
| ------------- | --------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------ |
| sessionId     | The Payment Session ID. If used, the response will automatically filter to be applicable to the specific transaction. | Required if country and sellingEntity are not provided.                                    |
| country       | The country code that represents the expected billing and/or shipping address of the customer.                        | Required if sessionId is not provided.                                                     |
| sellingEntity | The Digital River selling entity which is facilitating the transaction.                                               | Optional if sessionId is not provided. If not provided, a default entity will be selected. |

{% tabs %}
{% tab title="Example" %}
{% code overflow="wrap" %}
```javascript
var options = {
	taxIdentifier: {
		country: "IT"
    },
    classes: {
        base: "DRElement",
        complete: "taxId-complete",
        empty: "taxId-empty",
        focus: "taxId-focus",
        invalid: "taxId-invalid"
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

let taxIdentifier = digtialriver.createElement("taxidentifier", options);
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Tax Identifier element events

{% code overflow="wrap" %}
```javascript
taxIdentifier.on("event", handler);
```
{% endcode %}

Use this functionality to listen to events that you can use to build and enhance your purchase flow.

| Event  | Triggered When                                                       |
| ------ | -------------------------------------------------------------------- |
| ready  | The created element is loaded and ready to accept an update request. |
| focus  | The element has gained focus.                                        |
| blur   | The element has lost focus.                                          |
| change | The element's state has changed.                                     |

### Ready

A Ready event triggers when a Tax Identifier has loaded and is available to take an `update()` call.

{% tabs %}
{% tab title="Example" %}
{% code overflow="wrap" %}
```javascript
taxIdentifier.on("ready", function(event) { 
    //tax identifier element is ready and can accept an update call 
});
```
{% endcode %}
{% endtab %}
{% endtabs %}

| Key                             | Value                                                                                                                                                       |
| ------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
| elementType                     | taxidentifier                                                                                                                                               |
| hasTaxIdentifier                | Whether there are applicable tax identifiers. If true, you should mount and display the tax identifier element. If false, you should not mount the element. |
| businessTaxIdentifierRequired   | Whether a business tax identifier is required for this transaction or country/entity combination.                                                           |
| individualTaxIdentifierRequired | Whether an individual tax identifier is required for this transaction or country/entity combination.                                                        |

{% tabs %}
{% tab title="Ready Response object" %}
```javascript
{
      elementType: "taxidentifier",
    hasTaxIdentifier: true,
    businessTaxIdentifierRequired: true,
    individualTaxIdentifierRequired: true
}
```
{% endtab %}
{% endtabs %}

### Focus

A Focus event triggers when the Tax Identifier element gains focus.

{% tabs %}
{% tab title="Example" %}
```javascript
taxIdentifier.on("focus", function(event) { 
    //receive the event 
    }
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Focus Response object" %}
```javascript
{ 
     elementType: "taxidentifier" 
}
```
{% endtab %}
{% endtabs %}

### Blur

A Blur event triggers when the Tax Identifier element loses focus.

{% tabs %}
{% tab title="Example" %}
```javascript
taxIdentifier.on("blur", function(event) {
        //receive the event 
}
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Blur Response object" %}
```javascript
{
    elementType: "taxidentifier"
}
```
{% endtab %}
{% endtabs %}

### Change

A Change event triggers when the Tax Identifier element changes state.

{% tabs %}
{% tab title="Example" %}
```javascript
taxIdentifier.on("change", function(event) { 
     console.log("tax identifier change", event);
});
```
{% endtab %}
{% endtabs %}

| Key         | Value Description                                                                                             |
| ----------- | ------------------------------------------------------------------------------------------------------------- |
| complete    | Whether the element is in a complete state. The value entered in the field matches a valid identifier format. |
| empty       | Whether the element is empty.                                                                                 |
| elementType | The element type.                                                                                             |
| error       | An error object (if applicable).                                                                              |
| identifier  | Information about the identifier being provided. This object will contain a value, type, and customerType.    |

{% tabs %}
{% tab title="Change Response object" %}
```javascript
{
    complete: true,
    empty: false,
    elementType: "taxidentifier",
    error: null,
    identifier: {
                "value": 'IT11223433',
                "type": "it_natural",
                "customerType": "individual"
                }
}
```
{% endtab %}
{% endtabs %}

If an error is detected, a Change error object is returned.

{% tabs %}
{% tab title="Invalid Change Response Object" %}
```javascript
{
    complete: true,
    empty: false,
    elementType: "taxidentifier",
    "error": {
        "type": "validation_error",
            "code": "invalid_tax_identifier",
            "message": "Your tax identifier is invalid."
    },
    identifier: {
        "value": null,
        "type": "it_natural",
                "customerType": "individual"
        }
}
```
{% endtab %}
{% endtabs %}
