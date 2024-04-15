---
description: Learn how to use the invoice attribute element
---

# Invoice attribute element

The invoice attribute element collects customer data needed for e-invoicing purposes and then uses that data to create an invoice attribute.

For more details on how to use the element with specific [selling entities](../../../integration-options/checkouts/creating-checkouts/selling-entities.md), refer to the [Handling e-invoicing requirements](../../../integration-options/checkouts/creating-checkouts/handling-e-invoicing-requirements.md) page.

## How it works

To use the element, you'll typically collect enough information from customers during [checkouts](../../../integration-options/checkouts/creating-checkouts/) so that Digital River can determine the appropriate [selling entity](../../../integration-options/checkouts/creating-checkouts/selling-entities.md). At this point, you can [create an invoice attribute element](invoice-attribute-element.md#createelement-invoiceattribute-options).

This prompts [DigitalRiver.js](../../../payments/payment-integrations-1/digitalriver.js/reference/) to call to our [country specification service](../../../integration-options/checkouts/creating-checkouts/country-specs.md) to get the schemas it needs to build a data collection form. Once the form loads on your front end, customers select the appropriate options, enter their personal information, and click the submit button.

DigitalRiver.js then packages the form's data in a create invoice attribute request sent to our tax service. If that service successfully creates an invoice attribute, you receive the [on complete](invoice-attribute-element.md#on-complete-handler) event. That event's payload contains the invoice attribute's unique identifier.&#x20;

You use this identifier to associate the invoice attribute with the [checkout](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts). Our tax service then attempts to validate the invoice attribute, and, if that validation proves successful, the object's data is added to the checkout.

At the time of [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) creation, our tax service once again validates the invoice attribute and Digital River's commerce system persists this object data. This allows our reporting services to periodically retrieve this data and transmit it to third-party e-invoicing services integrated with the appropriate tax agencies in each supported country.

For information on how to use the element to meet invoicing requirements in these countries, refer to the [Handling e-invoicing requirements](../../../integration-options/checkouts/creating-checkouts/handling-e-invoicing-requirements.md) page.&#x20;

## Localizing the invoice attribute element

When [instantiating a DigitalRiver object](../digital-river-publishable-api-key.md) for use with the invoice attribute element, you can either set `locale` to `en-US` or `zh-TW`.

{% code overflow="wrap" %}
```javascript
let digitalriver = new DigitalRiver("YOUR_PUBLIC_API_KEY", {
     "locale": "zh-TW"
})r
```
{% endcode %}

For both localization options, the following shows what the element presents to Taiwan-based customers who use a citizen digital certificate carrier.&#x20;

{% hint style="info" %}
Note that the element also helps customers properly format their entries for certain fields.
{% endhint %}

{% tabs %}
{% tab title="en-US: English (United States)" %}
![](<../../../.gitbook/assets/image (38).png>)


{% endtab %}

{% tab title="zh-TW: Chinese (Taiwan)" %}
![](<../../../.gitbook/assets/image (99).png>)
{% endtab %}
{% endtabs %}

## `createElement('invoiceAttribute', options)`

Once you [instantiate a Digital River object](../digital-river-publishable-api-key.md), you can use it to create an invoice attribute element.

This version of the `createElement()` method has two required parameters: `'invoiceAttribute'` and a [configuration object](invoice-attribute-element.md#invoice-attribute-element-configuration-object).

{% code overflow="wrap" %}
```javascript
let invoiceAttribute = digitalriver.createElement('invoiceAttribute', options)
```
{% endcode %}

### Invoice attribute element configuration object

The element's configuration object consists of a required [`invoiceAttribute`](invoice-attribute-element.md#invoice-attribute) and an optional [`classes`](invoice-attribute-element.md#classes) and [`style`](invoice-attribute-element.md#style). &#x20;

{% code overflow="wrap" %}
```javascript
const options = {
    invoiceAttribute: {
        sessionId: "e2f7e5ee-4c14-494f-bd14-2a9f3a375da3",
        // country, type and sellingEntity are not needed if sessionId is provided
        // country: "TW",
        // sellingEntity: "DR_TAIWAN-ENTITY"
        // type: "individual",
        // email: "jdoe@digitalriver.com"
    },
    classes: {
        base: "DRElement",
        complete: "invoiceAttribute-complete",
        empty: "invoiceAttribute-empty",
        focus: "invoiceAttribute-focus",
        invalid: "invoiceAttribute-invalid"
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
                color: "#dddddd",
            },
        },
        focus: {
            ":hover": {
                color: "#135bef",
            },
        },
        invalid: {
            color: "red"
        }
   }
};

let invoiceAttribute = digitalriver.createElement('invoiceAttribute', options)
```
{% endcode %}

#### `invoiceAttribute` <a href="#invoice-attribute" id="invoice-attribute"></a>

The configuration object's `invoiceAttribute` contains the following properties:

* `sessionId`: The transaction's [payment session](../../../integration-options/checkouts/creating-checkouts/payment-sessions.md) identifier. This value is required if you don't specify `country` and `sellingEntity`.  \
  \
  However, if you do pass `sessionId`, then your integration must have already collected the customer's shipping and/or billing information and used it to update the [checkout](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) with a `shipTo.address.country` and/or `billTo.address.country`. Once this is done, Digital River will have the data it needs to calculate the checkout's [`sellingEntity`](../../../integration-options/checkouts/creating-checkouts/selling-entities.md). \
  \
  When you fetch the checkout's [`payment.session.id`](../../../integration-options/checkouts/creating-checkouts/#payment-session-identifier) , pass that value to `sessionId`, and create the element, DigitalRiver.js looks up the transaction's country and selling entity in the payment session and calls  to the [Country Specs API](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Country-specifications) to retrieve the schemas needed to build the invoice attribute element's data entry forms.
* `country`: The shipping or billing address country of the customer getting the invoice. This value is only required if you don't specify `sessionId`.&#x20;
* `sellingEntity`: The [selling entity](../../../integration-options/checkouts/creating-checkouts/selling-entities.md) of the transaction. This value is only required if you don't specify `sessionId`.&#x20;
* `type`: This optional parameter represents the type of customer requesting the invoice.  The acceptable values are `individual` or `business`. You can either set `type` or set the [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) [`customerType`](../../../integration-options/checkouts/creating-checkouts/setting-the-customer-type.md) and then pass `sessionId`.\
  \
  This feature allows you to use the [on ready event](invoice-attribute-element.md#on-ready-handler) to determine, based on the customer's type, whether an invoice attribute is required. \
  \
  In the following example, the [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) `sellingEntity.id` is `DR_TAIWAN-ENTITY`. For individual customers, the [on ready event](invoice-attribute-element.md#on-ready-handler) indicates that an invoicing system exists and that customer's must supply their invoice information. The same event type indicates that no invoice attribute requirements exist for business customers&#x20;

{% tabs %}
{% tab title="Individual" %}
{% code title="on ready event" overflow="wrap" %}
```
{
    "hasInvoices": true,
    "invoiceRequired": true,
    "individual": [
        {
            "type": "tw_individual_mobile_barcode",
            "attributes": [
                {
                    "attributeName": "MOBILE_BARCODE",
                    "isRequired": true
                }
            ]
        },
        {
            "type": "tw_individual_citizen_cert",
            "attributes": [
                {
                    "attributeName": "CITIZEN_DIGITAL_CERT",
                    "isRequired": true
                }
            ]
        },
        {
            "type": "tw_individual_member_carrier",
            "attributes": [
                {
                    "attributeName": "MEMBER_CARRIER",
                    "isRequired": true
                }
            ]
        },
        {
            "type": "tw_individual_donate",
            "attributes": [
                {
                    "attributeName": "CHARITY_NAME",
                    "isRequired": true
                }
            ]
        }
    ],
    "hasIndividualInvoiceTypes": true,
    "elementType": "invoiceattribute"
}
```
{% endcode %}
{% endtab %}

{% tab title="Business" %}
{% code title="on ready event" %}
```
{
    "hasInvoices": false,
    "elementType": "invoiceattribute"
}

```
{% endcode %}
{% endtab %}
{% endtabs %}

* `email`: The element won't prompt a customer for their email address if specified. \
  \
  This is useful if your integration collects a customer's email address before creating the invoice attribute element. If this is the case, you can pass `email` and prevent customers from having to enter the same information twice during the checkout process. \
  \
  For example, if `invoiceAttribute` contains `email` and a customer getting a [Taiwanese eGUI](../../../integration-options/checkouts/creating-checkouts/handling-e-invoicing-requirements.md#background) selects the member carrier option (which requires an email address) , the element won't display that data collection field.&#x20;

{% tabs %}
{% tab title="email not specified" %}
![](<../../../.gitbook/assets/image (72).png>)
{% endtab %}

{% tab title="email specified" %}
![](<../../../.gitbook/assets/image (8) (1).png>)
{% endtab %}
{% endtabs %}

#### `classes`

For details, refer to [Custom classes](./#custom-classes)

#### `style`

For details, refer to [Custom styles](./#custom-styles)

## `mount()`

The `mount()` method displays the invoice attribute element in the container you designate. The method has one required parameter: the `id` of the `div` that should hold the element.&#x20;

{% code overflow="wrap" %}
```javascript
...
<div id="invoice-attribute"></div>
...
invoiceAttribute.mount('invoice-attribute');
...
```
{% endcode %}

If this method is successful, then the [on ready event](invoice-attribute-element.md#on-ready-handler) is triggered.

## `unmount()`

The `unmount()` method removes the invoice attribute element from the page. Once called, the element is no longer visible to customers. However, you can later re-add the element to `div` by invoking [`mount()`](invoice-attribute-element.md#mount).&#x20;

```javascript
...
invoiceAttribute.unmount();
...
```

## `destroy()`

The `destroy()` method removes the invoice attribute element from the page and deactivates the element's functionality. Once the method is invoked, you can't call [`mount()`](invoice-attribute-element.md#mount) to reactivate the element and make it visible.

```javascript
...
invoiceAttribute.destroy();
...
```

## `on('ready', handler)`

When the element opens and can accept user input, the on ready event is triggered. This version of `on()` has two required parameters: `'ready'` and an event handler. &#x20;

```javascript
invoiceAttribute.on('ready', function(event) {
  // element is ready and can accept user input
})
```

The `event` contains all the possible data fields that might be displayed to customers in the element. The fields that are displayed depend on what options customers select.

{% hint style="info" %}
The ready event is useful for information and testing purposes, but your integration doesn't necessarily have to implement any code to handle it.&#x20;
{% endhint %}

For example, the payload of the following on ready event indicates that the customer's country (Taiwan) has an e-invoicing system for individual customers and they must provide invoice information.

The element will ask customers whether to select the mobile barcode carrier, citizen digital certificate carrier, or member carrier option. It also allows customers to bypass the carrier option entirely and instead designate a charity.\
\
Whatever option customers select, the event indicates that the element won't allow them to submit the form until they've specified a value. &#x20;

{% code overflow="wrap" %}
```javascript
{
    "hasInvoices": true,
    "invoiceRequired": true,
    "individual": [
        {
            "type": "tw_individual_mobile_barcode",
            "attributes": [
                {
                    "attributeName": "MOBILE_BARCODE",
                    "isRequired": true
                }
            ]
        },
        {
            "type": "tw_individual_citizen_cert",
            "attributes": [
                {
                    "attributeName": "CITIZEN_DIGITAL_CERT",
                    "isRequired": true
                }
            ]
        },
        {
            "type": "tw_individual_member_carrier",
            "attributes": [
                {
                    "attributeName": "MEMBER_CARRIER",
                    "isRequired": true
                }
            ]
        },
        {
            "type": "tw_individual_donate",
            "attributes": [
                {
                    "attributeName": "CHARITY_NAME",
                    "isRequired": true
                }
            ]
        }
    ],
    "hasIndividualInvoiceTypes": true,
    "elementType": "invoiceattribute"
}
```
{% endcode %}

## `on('complete', handler)`

Once customers enter properly formatted data in all of the element's required fields and then submit the form, the on complete event is triggered. This version of `on()` requires two parameters: `'complete'` and an event handler. &#x20;

{% code overflow="wrap" %}
```javascript
invoiceAttribute.on('complete', function(event) {
     if(event.error) {
        //handle error
     } else {
        console.log('invoice attribute success', event);
        //send the invoice attribute's id to your back-end and attach it to the checkout
     }
});
```
{% endcode %}

If Digital River successfully creates an invoice attribute, then `event` contains that object.

{% code title="Ready event (success)" %}
```javascript
{
    "id": "94fe7ed9-f570-4049-aa37-979a50f0097d",
    "type": "tw_individual_donate",
    "attributes": {
        "CHARITY_NAME": "財團法人瑪利亞社會福利基金會",
        "CHARITY_CODE": "880"
    },
    "createdTime": "2022-06-06T21:17:41Z",
    "updatedTime": "2022-06-06T21:17:41Z",
    "liveMode": false,
    "elementType": "invoiceattribute"
}
```
{% endcode %}

You should handle on complete by passing the event's `id` to your back-end and using that value to set `invoiceAttributeId` in the body of a [`POST/checkouts/{id}`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/updateCheckouts) request. This associates the invoice attribute with the [checkout](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts).&#x20;

{% code overflow="wrap" %}
```
curl --location --request POST 'https://api.digitalriver.com/checkouts/7da8bcbc-a139-440e-a684-5eb5f1804995' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer <Secret API Key>' \
...
--data-raw '{
    "invoiceAttributeId": "de2c8ced-b788-463f-93fb-0b274bc7f9bf"
}'
```
{% endcode %}

You can also respond to the event by calling [`unmount()`](invoice-attribute-element.md#unmount) or [`destroy()`](invoice-attribute-element.md#destroy) to close the element and make it no longer visible to customers.

If the create invoice attribute request fails, then `event` contains an error.

{% code title="Ready event (fail)" %}
```javascript
{
    "error": {
        "type": "no_network",
        "errors": [
            {
                "message": "Please check your network connection."
            }
        ]
    },
    "elementType": "invoiceattribute"
}
```
{% endcode %}

Since the element validates the format of customer-entered data, errors are typically only returned when the invoice attribute service is unreachable, or customers are experiencing connection issues. In these cases, we recommend displaying a message such as “Something went wrong. Try again later” to customers.

## Complete example

{% code overflow="wrap" %}
```javascript
<html>
    <head>
        <link href="https://js.digitalriverws.com/v1/css/DigitalRiver.css" rel="stylesheet">
        <script src="https://js.digitalriverws.com/v1/DigitalRiver.js"></script>
    </head>
    <body>
        <div id="invoice-attribute"></div>

        <script>
            window.addEventListener('load', function() {
                const options = {
                    locale: 'zh-TW'
                }
                const digitalriver = new DigitalRiver(options);

                const invoiceAttributeOptions = {
                    invoiceAttribute: {
                        sessionId: "e2f7e5ee-4c14-494f-bd14-2a9f3a375da3",
                        // country and sellingEntity are not needed if sessionId is provided
                        // country: "CN",
                        // sellingEntity: "DR_CHINA-ENTITY"
                        // optional properties:
                        // type: "individual"
                        // email: "someone@somewhere.com"
                    },
                    classes: {
                        base: "DRElement",
                        complete: "invoiceAttribute-complete",
                        empty: "invoiceAttribute-empty",
                        focus: "invoiceAttribute-focus",
                        invalid: "invoiceAttribute-invalid"
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
                        }
                    }
                };

                let invoiceAttribute = digitalriver.createElement('invoiceAttribute', invoiceAttributeOptions);
                invoiceAttribute.mount('invoice-attribute');

                invoiceAttribute.on('ready', function(details) {
                    console.log(details);
                });

                invoiceAttribute.on('complete', function(details) {
                    if(event.error) {
        //handle error
     } else {
        if(event.error) {
        //handle error
     } else {
        console.log('invoice attribute success', event);
        //send the invoice attribute's id to your back-end and attach it to the checkout
     }
     }
                });
            });
        </script>
    </body>
```
{% endcode %}
