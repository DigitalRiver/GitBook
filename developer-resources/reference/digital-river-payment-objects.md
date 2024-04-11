---
description: Learn how to use the Digital River payment objects.
---

# Digital River payment objects

An object is a collection of properties, and a property is an association between a name (or key) and a value. DigitalRiver.js uses objects to collect data.

## Billing address object

This object contains the customer's billing address.

{% tabs %}
{% tab title="Billing address object" %}
```javascript
{
    "name": "John Smith",
    "firstName": "John",
    "lastName": "Smith",
    "phone": "952-555-1111",
    "email": "jsmith@digitalriver.com",
    "address": {
      "line1": "10380 Bren Rd W",
      "line2": "string",
      "city": "Minnetonka",
      "postalCode": "55129",
      "state": "MN",
      "country": "US"
    }
}
```
{% endtab %}
{% endtabs %}

## Shipping address object

This object contains the customer's shipping address.

{% tabs %}
{% tab title="Shipping Address object" %}
```javascript
{
    "name": "John Smith",
    "firstName": "John",
    "lastName": "Smith",
    "phone": "952-555-1111",
    "email": "jsmith@digitalriver.com",
    "address": {
      "line1": "10380 Bren Rd W",
      "line2": "string",
      "city": "Minnetonka",
      "postalCode": "55129",
      "state": "MN",
      "country": "US"
    }
}
```
{% endtab %}
{% endtabs %}

## Contact information object

This object contains the customer's contact information.

{% tabs %}
{% tab title="Contact Information object" %}
```javascript
{
    "name": "John Smith",
    "phone": "952-555-1111",
    "email": "jsmith@digitalriver.com"
}
```
{% endtab %}
{% endtabs %}

## Payment request object

This object contains the payment request.

{% tabs %}
{% tab title="Payment Request object" %}
{% code overflow="wrap" %}
```javascript
var paymentRequestData = digitalriver.paymentRequest({
    country: "US",
    currency: "USD",
    total: {
        label: "Demo Total",
        amount: 300
    },
    displayItems: [{
        amount: 100,
        label: "Item"
    }, {
        amount: 200,
        label: "Better Item"
    }],
    shippingOptions: [{
        id: "free-shipping",
        label: "Free Shipping",
        detail: "Arrives in 5 to 7 days",
        amount: 0
    }, {
        id: "overnight-shipping",
        label: "Overnight Shipping",
        detail: "Arrives in 5 to 7 days",
        amount: 1000
    }],
    requestShipping: true,
    style: {
        buttonType: "plain",
        buttonColor: "light",
        buttonLanguage: "en"
    }
});
```
{% endcode %}
{% endtab %}
{% endtabs %}

| Attribute       | Required | Type                                                                                                                           | Description                                                                                                                                                                                                   |
| --------------- | -------- | ------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| country         | Required | String                                                                                                                         | The country code for the Payment Request session.                                                                                                                                                             |
| currency        | Required | String                                                                                                                         | The three-digit ISO currency code to supply to the Payment Request session. All amounts contained within the Payment Request will use this currency.                                                          |
| total           | Required | A [Payment Request Total Time object](digital-river-payment-objects.md#payment-request-total-item-object)                      | The Payment Request total amount displayed to the customer as part of the Payment Request interface.                                                                                                          |
| displayItems    | Required | An array of [Payment Request Display Item objects](digital-river-payment-objects.md#payment-request-display-item-object)       | The Payment Request displays items to the customer as part of the Payment RPequest interface.                                                                                                                 |
| shippingOptions | Optional | An array of [Payment Request Shipping Option objects](digital-river-payment-objects.md#payment-request-shipping-option-object) | The Payment Request interface displays the Shipping Options field to the customer if you set the `requestShipping` parameter to true. The first item in the array is the default or selected shipping option. |
| requestShipping | Required | Boolean                                                                                                                        | If true, you must provide an array of shipping options from which the customer can choose.                                                                                                                    |
| style           | Optional | A [Payment Request Style Option object](digital-river-payment-objects.md#payment-request-style-option-object)                  | This attribute allows you to control the style of the button presented to the customer.                                                                                                                       |

## Payment request total item object

This object contains the payment request total.

{% tabs %}
{% tab title="Payment Request Total Item object" %}
```javascript
{
    label: "Order Total",
    amount: 100,
    isPending: false
}
```
{% endtab %}
{% endtabs %}

| Field     | Required | Description                                                                                                                                                                                        |
| --------- | -------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| label     | Required | The label appears next to the Total Amount of the order on the Payment Sheet.                                                                                                                      |
| amount    | Required | The amount of the Order displayed on the Payment Sheet.                                                                                                                                            |
| isPending | Optional | If the Shipping Total, Tax Amount, or something similar is still pending, you can change this amount in the future. If you don't provide an updated value, the system treats this amount as Final. |

## Payment request style option object

This object contains the style information for the payment request.

{% tabs %}
{% tab title="Payment Request Style Option object" %}
```javascript
{
        buttonType: "plain",
        buttonColor: "light",
        buttonLanguage: "en"
    }
```
{% endtab %}
{% endtabs %}

| Field          | Required | Description                                                                                                        |
| -------------- | -------- | ------------------------------------------------------------------------------------------------------------------ |
| buttonType     | Optional | The type of button. If you don't specify a button type, the system uses the default button type.                   |
| buttonColor    | Optional | The color of the button. If you don't specify a button color, the system uses the default color for the button.    |
| buttonLanguage | Optional | The language for the button's label. If you don't specify a language, the DigitalRiver.js uses English by default. |

## Payment request display item object

This object contains the payment request information for the item.

{% tabs %}
{% tab title="Payment Request Display Item object" %}
```javascript
{
        buttonType: "plain",
        buttonColor: "light",
        buttonLanguage: "en"
    }
```
{% endtab %}
{% endtabs %}

| Field     | Required | Description                                                                                                                                                                                         |
| --------- | -------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| label     | Required | This label appears next to the Line Item of the order on the Payment Sheet.                                                                                                                         |
| amount    | Required | This amount appears on the Payment Sheet for this Line Item.                                                                                                                                        |
| isPending | Optional | If the Shipping Total, Tax Amount, or something similar is still pending, you can change this amount in the future. If you do not provide an updated value, the system treats this amount as Final. |

## Payment request shipping option object

This object contains the shipping option for the payment request.

{% tabs %}
{% tab title="Payment Request Shipping Option object" %}
```javascript
{
    id: "overnight-shipping",
    label: "Overnight Shipping",
    amount: 10,
    detail: "Will arrive tomorrow morning"
}
```
{% endtab %}
{% endtabs %}

| Field  | Required | Description                                                                                                                                                                                     |
| ------ | -------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| id     | Required | Once a customer selects a shipping option from the Payment Sheet, DigitalRiver.js returns the shipping option ID. This ID should correspond to something within your Order Management platform. |
| label  | Required | The label appears as part of the Shipping Option on the Payment Sheet.                                                                                                                          |
| amount | Required | The amount that appears on the Payment Sheet for this Shipping Option.                                                                                                                          |
| detail | Required | A long description of the Shipping Option that appears on the Payment Sheet.                                                                                                                    |

## Payment request details update object

Use this object to respond to a shipping address change or a shipping option change event sent from the Payment request session.

| Field           | Type                                                                                                                           | Required | Description                                                                                                                                                                                                                                                                                         |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------ | -------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| status          | String                                                                                                                         | Required | <p>Use this field to control the flow and error display within the Payment Request session. The values are as follows:</p><ul><li><strong>Success</strong>—Allows the Payment Request to proceed.</li><li><strong>Failure</strong>—Prevents the change requested. Shows an error message.</li></ul> |
| error           | [Payment Request Details Update Error object](digital-river-payment-objects.md#payment-request-details-update-error-object)    | Optional | These items will appears as the updated items in the Payment Request interface.                                                                                                                                                                                                                     |
| total           | [Payment Request Total Item object](digital-river-payment-objects.md#payment-request-total-item-object)                        | Optional | The new total amount, if applicable.                                                                                                                                                                                                                                                                |
| displayItems    | An array of [Payment Request Display Item objects](digital-river-payment-objects.md#payment-request-display-item-object)       | Optional | These items will appears as the updated items in the Payment Request interface.                                                                                                                                                                                                                     |
| shippingOptions | An array of [Payment Request Shipping Option objects](digital-river-payment-objects.md#payment-request-shipping-option-object) | Optional | The Payment Request interface displays the Shipping Options field to the customer if you set the `requestShipping` parameter to true. The first item in the array is the default or selected shipping option.                                                                                       |

{% tabs %}
{% tab title="Successful Payment Request Details Update object" %}
{% code overflow="wrap" %}
```javascript
{
    status: 'success',
    error: {
    },
    total: {
        label: "Order Total",
        amount: 100,
        isPending: false
    },
    displayItems: [
        {
            label: "Line Item Label (Product Name)",
            amount: 100,
            isPending: false
        },
        {
            label: "Shipping Amount",
            amount: 10,
            isPending: false
        },
    ],
    shippingOptions: [
        {
            id: "standard-shipping",
            label: "Standard Shipping",
            amount: 0,
            detail: "Will arrive in 7-10 days."
        },
        {
            id: "overnight-shipping",
            label: "Overnight Shipping",
            amount: 10,
            detail: "Will arrive tomorrow morning"
        }
    ]
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Unsuccessful Payment Request Details Update object" %}
{% code overflow="wrap" %}
```javascript
{
    status: 'failure',
    error: {
        message: 'We can only ship to the US, Canada and Mexico.'
    }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Unsucessful Payment Request Details Update Error object with errors" %}
{% code overflow="wrap" %}
```javascript
{
    status: 'failure',
    error: {
        message: 'We can only ship to the US, Canada and Mexico.',
        fields: {
            addressLine: 'Your address is invalid.',
            city: 'Your city is invalid.',
            country: 'Your country is invalid',
            phone: 'Your phone is invalid.',
            postalCode: 'Your postal code is invalid.',
            recipient: 'Your recipient value is invalid. Please supply a different one.',
            region: 'Your region value is invalid. Please supply a different one.',
        }
    }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Payment request details update error object

Use this object to display a specific error message to the customer as part of a Details Update message to the Payment Request session.

{% hint style="info" %}
The Payment request details update error object is only available for Apple Pay.
{% endhint %}

{% tabs %}
{% tab title="Payment Request Details Update Error object" %}
{% code overflow="wrap" %}
```javascript
{
    message: "An Error has occurred. Please try again.",
    fields: {
        addressLine: 'Your address is invalid.',
        city: 'Your city is invalid.',
        country: 'Your country is invalid',
        phone: 'Your phone is invalid.',
        postalCode: 'Your postal code is invalid.',
        recipient: 'Your recipient value is invalid. Please supply a different one.',
        region: 'Your region value is invalid. Please supply a different one.',
    }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Details update error message

Use this optional string message to display a specific error message to your customer. This allows you to provide a better experience when correcting error scenarios.

### Details update error fields

Use the following fields to display specific error information to the customer about what is wrong with their address Information.

| Field       | Payment Request Mapped Field | Required |
| ----------- | ---------------------------- | -------- |
| addressLine | addressLine                  | Optional |
| city        | city                         | Optional |
| state       | region                       | Optional |
| postalCode  | postalCode                   | Optional |
| country     | country                      | Optional |
| recipient   | recipient                    | Optional |

## Payment request response object

This object contains the response to the payment request.

| Field              | Type                                                                                            | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| ------------------ | ----------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| error              | Boolean                                                                                         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| source             | [Payment Request Source object](digital-river-payment-objects.md#payment-request-source-object) | The payment source created using the details provided by the payment session.                                                                                                                                                                                                                                                                                                                                                                                                  |
| billingAddress     | [Billing Address object](digital-river-payment-objects.md#billing-address-object)               | The billing address provided by the customer.                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| shippingAddress    | [Shipping Address object](digital-river-payment-objects.md#shipping-address-object)             | The shipping address provided by the customer.                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| contactInformation | [Contact Information object](digital-river-payment-objects.md#contact-information-object)       | The contact information provided by the customer.                                                                                                                                                                                                                                                                                                                                                                                                                              |
| shippingOption     | String                                                                                          | The customer's chosen shipping option.                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| complete           | Function                                                                                        | <p>Call this function once you have processed the returned data. This function receives a string with the following values:</p><ul><li><strong>Success</strong>—Indicates the payment successfully processed. The user agent may or may not indicate success to the user. Use this value to dismiss the payment interface.</li><li><strong>Failure</strong>—Indicates the payment failed to process. The user agent may or may not indicate the failure to the user.</li></ul> |

## Payment request source object

This object contains the source object for the payment request.

{% tabs %}
{% tab title="Payment Request Source object" %}
{% code overflow="wrap" %}
```javascript
{
    "error": false,
    "source": {
        "id": "5sdfd42a-1b02-471f-8c20-d9f7bb446d42",
        "clientId": "gc",
        "channelId": "drdod15",
        "type": "creditCard",
        "usage": "single",
        "owner": {
            "firstName": "firstName",
            "lastName": "lastName",
            "email": "email@email.org",
            "referenceId": "testOrderID_payserv1",
            "address": {
                "line1": "1234 First St.",
                "city": "Minnetonka",
                "state": "MN",
                "country": "US",
                "postalCode": "55410"
            }
        },
        "amount": "100.00",
        "currency": "USD",
        "status": "chargeable",
        "creationIp": "67.216.237.4",
        "creationDate": "2018-08-22T19:46:09.725Z",
        "flow": "standard",
        "creditCard": {
            "brand": "Visa",
            "expirationMonth": 12,
            "expirationYear": 2025,
            "lastFourDigits": "1111"
        }
    },
    "billingAddress": {
        "name": "John Smith",
        "firstName": "John",
        "lastName": "Smith",
        "phone": "952-111-1111",
        "email": "jsmith@digitalriver.com"
        "address": {
            "line1": "10380 Bren Rd W",
            "line2": "string",
            "city": "Minnetonka",
            "postalCode": "55129",
            "state": "MN",
            "country": "US"
        }
    },
    "shippingAddress": {
        "name": "John Smith",
        "firstName": "John",
        "lastName": "Smith",
        "phone": "952-111-1111",
        "email": "jsmith@digitalriver.com"
        "address": {
            "line1": "10380 Bren Rd W",
            "line2": "string",
            "city": "Minnetonka",
            "postalCode": "55129",
            "state": "MN",
            "country": "US"
        }
    },
    "contactInformation": {
        "name": "John Smith",
        "phone": "952-111-1111",
        "email": "jsmith@digitalriver.com"
    },
    "shippingOption": {
        id: "overnight-shipping",
        label: "Overnight Shipping",
        amount: 10,
        detail: "Will arrive tomorrow morning"
    },
    complete: function() {


    }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Change event error object

Digital River returns this Error object returns with the change event when Digital River detects an error with an Element. This object contains a type, code, and message.

{% tabs %}
{% tab title="Change Event Error object" %}
```javascript
{
    "type": "validation_error",
    "code": "invalid_card_number",
    "message": "Your card number is invalid."
}
```
{% endtab %}
{% endtabs %}

### Create source error object

Digital River returns this Error object within the `createSource` method if Digital River detects an error with the tokenization request. This object contains a type and an array of detailed messages explaining the error.

{% tabs %}
{% tab title="Create Source Error object" %}
{% code overflow="wrap" %}
```javascript
{
    "type": "bad_request",
    "errors": [{
           "code": "invalid_parameter",
           "parameter": "owner.firstName",
           "message": "'' is not a valid owner.firstname."
    },
    {
            "code": "currency_unsupported",
            "parameter": "currency",
            "message": "currency 'xyz' is not supported."
    }]
}
```
{% endcode %}
{% endtab %}
{% endtabs %}
