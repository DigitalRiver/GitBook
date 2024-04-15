---
description: >-
  Learn how to customize and stylize elements to seamlessly integrate them into
  your user experience or purchase flow.‌
---

# Elements

An Element is a UI component that [DigitalRiver.js](../../../payments/payment-integrations-1/digitalriver.js/reference/) creates to collect sensitive customer information without having the data touch your servers. You can customize and stylize these components to seamlessly integrate them into your user experience or purchase flow. The library collects and tokenizes the data contained in these elements without exposing you to PCI-compliance liability.‌

## element.mount();

Use this function to place the created elements on your page. The function accepts an identifier of a container div. The library will load the created element within the specified container.

{% tabs %}
{% tab title="Example" %}
{% code overflow="wrap" %}
```javascript
<form id="payment-form">
    <div id="card-number"></div>
    <div id="card-expiration"></div>
    <div id="card-cvv"></div>
    <button type="submit">Submit</button>
</form>


cardNumber.mount('card-number');
cardExpiration.mount('card-expiration');
cardCVV.mount('card-cvv');
```
{% endcode %}
{% endtab %}
{% endtabs %}

## element.on();

Use this function to listen to events that you can use to build and enhance your purchase flow.

| Event                                                 | Trigger When                                                                                                                                              | Applies To                                                              |
| ----------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------- |
| [​blur​](./#blur)                                     | The element has lost focus.                                                                                                                               | cardnumber, cardexpiration, cardcvv, onlinebanking                      |
| [​cancel​](./#cancel)                                 | The customer has canceled the experience.                                                                                                                 | applepay, googlepay                                                     |
| [​change​](./#change)                                 | The element's state has changed.                                                                                                                          | cardnumber, cardexpiration, cardcvv, onlinebanking                      |
| [click​](./#click)                                    | A shopper clicked the element's button.                                                                                                                   | applepay, googlepay                                                     |
| [focus](./#focus)​                                    | The element has gained focus.                                                                                                                             | cardnumber, cardexpiration, cardcvv, onlinebanking                      |
| ​[ready​](./#ready)                                   | The created element is loaded and ready to accept an update request.                                                                                      | cardnumber, cardexpiration, cardcvv, applepay, googlepay, onlinebanking |
| [return](./#return)                                   | The customer has pressed the Return key while focused in the input field.                                                                                 | cardnumber, cardexpiration, cardcvv                                     |
| ​[shippingaddresschange](./#shipping-address-change)​ | The customer has chosen a different address than was previously selected. You should use this data to re-price your order totals (if applicable).         | applepay, googlepay                                                     |
| [​shippingoptionchange​](./#shipping-option-change)   | The customer has chosen a different shipping option than was previously selected. You should use this data to re-price your order totals (if applicable). | applepay, googlepay                                                     |
| [​source​](./#source)                                 | The customer has authorized the payment and a source, and DigitalRiver.js returned associated data.                                                       | applepay, googlepay                                                     |

### Blur

A Blur event triggers when an element loses focus.

{% tabs %}
{% tab title="Example" %}
{% code overflow="wrap" %}
```javascript
cardNumber.on('blur', function(event) {
    console.log('card number blur', event);
});
```
{% endcode %}
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Response object" %}
{% code overflow="wrap" %}
```javascript
{
    elementType: "cardnumber"
}
{
    elementType: "cardnumber"
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Cancel

A Cancel event occurs when the customer closes the Apple Pay Element Payment Request interface.

{% tabs %}
{% tab title="Example" %}
{% code overflow="wrap" %}
```javascript
applepay.on('cancel', function(event) {
    //do stuff
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Response object" %}
{% code overflow="wrap" %}
```javascript
{
    elementType: "applepay"
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Change

A Change event triggers when an element changes state.‌

If an error is detected, Digital River will return a [Change Event Error object](../error-types-codes-and-objects.md#change-event-error-object) with the event payload.

{% tabs %}
{% tab title="Example" %}
{% code overflow="wrap" %}
```javascript
cardNumber.on('change', function(event) {
    console.log('card number change', event);
});
```
{% endcode %}
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Response object" %}
{% code overflow="wrap" %}
```javascript
{
    brand: "unknown",
    complete: false,
    empty: true,
    elementType: "cardnumber",
    error: null
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

#### **Invalid element change event example**

{% tabs %}
{% tab title="Change Response Object Error - Invalid" %}
{% code overflow="wrap" %}
```javascript
{
    brand: "unknown",
    complete: true,
    empty: false,
    elementType: "cardnumber",
    "error": {
        "type": "validation_error",
        "code": "invalid_card_number",
        "message": "Your card number is invalid."
    }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

#### **Incomplete element change event example**

{% tabs %}
{% tab title="Change Response Object Error - Incomplete" %}
{% code overflow="wrap" %}
```javascript
{
    brand: "unknown",
    complete: false,
    empty: false,
    elementType: "cardnumber",
    error: {
        "type": "validation_error",
        "code": "incomplete_card_number",
        "message": "Your card number is incomplete."
    }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

#### **Error types, codes, messages**

| Error Scenario                                             | Error Type       | Error Code                   | Error Message                               |
| ---------------------------------------------------------- | ---------------- | ---------------------------- | ------------------------------------------- |
| Credit Card Number field is incomplete.                    | validation-error | invalid\_card\_number        | Your card number is invalid.                |
| Credit Card Number field is complete but invalid.          | validation-error | incomplete\_card\_number     | Your card number is incomplete.             |
| Card Security Code is incomplete                           | validation-error | invalid\_expiration\_month   | Your card's expiration month is invalid.    |
| Card Security Code is complete but invalid.                | validation-error | invalid\_expiration\_year    | Your card's expiration year is in the past. |
| Card Expiration field is incomplete.                       | validation-error | invalid\_expiration\_date    | Your card's expiration date is invalid.     |
| Card Expiration Date is complete but the date is invalid.  | validation-error | incomplete\_expiration\_date | Your card's expiration date is incomplete.  |
| Card Expiration Date is complete but has an invalid year.  | validation-error | invalid\_security\_code      | Your card's security code is invalid.       |
| Card Expiration Date is complete but has an invalid month. | validation-error | incomplete\_security\_code   | Your card's security code is incomplete.    |

#### **Card brands**‌

The following table lists the supported credit card brands.

| Brand              | Key                |
| ------------------ | ------------------ |
| Visa               | visa               |
| MasterCard         | mastercard         |
| American Express   | amex               |
| Diners Club        | dinersclub         |
| Discover           | discover           |
| UnionPay           | unionpay           |
| JCB                | jcb                |
| Maestro            | maestro            |
| Forbrugsforeningen | forbrugsforeningen |
| Dankort            | dankort            |

### Click

A Click event occurs when the customer clicks an Apple Pay Element.

{% tabs %}
{% tab title="Example" %}
{% code overflow="wrap" %}
```javascript
applepay.on('click', function(event) {
    //do stuff
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Response object" %}
{% code overflow="wrap" %}
```javascript
{
    elementType: "applepay"
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Focus

A Focus event triggers when an element gains focus.

{% tabs %}
{% tab title="Example" %}
{% code overflow="wrap" %}
```javascript
cardNumber.on('ready', function(event) {
    console.log('card number ready', event);
});
```
{% endcode %}
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Response object" %}
{% code overflow="wrap" %}
```javascript
{    
    elementType: "cardnumber"
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Ready

A Ready event triggers when an element is ready and able to receive `blur()`, `focus()`, or `update()` calls.

{% tabs %}
{% tab title="Example" %}
{% code overflow="wrap" %}
```javascript
cardNumber.on('focus', function(event) {
    console.log('card number focus', event);
});
```
{% endcode %}
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Response object" %}
{% code overflow="wrap" %}
```javascript
{
    elementType: "cardnumber"
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Return

A Return event triggers when a customer presses the Return key while the input field has focus.

{% tabs %}
{% tab title="Example" %}
{% code overflow="wrap" %}
```javascript
cardNumber.on('return', function(event) {
    console.log('card number return', event);
});
```
{% endcode %}
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Response object" %}
{% code overflow="wrap" %}
```javascript
{
    elementType: "cardnumber"
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Shipping address change

A Shipping Address Change event occurs when the Customer has selected a different Shipping Address within the Payment Request interface. The event will create the following object structure.

| Key             | Type                                                                                                                  | Description                                                                                                                                                                                                  |
| --------------- | --------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| updateWith      | Function                                                                                                              | Calling this function with a [Payment Request Details Update object](../digital-river-payment-objects.md#payment-request-details-update-object) merges your updates into the current Payment Request object. |
| shippingAddress | A [Payment Request Details Update object​](../digital-river-payment-objects.md#payment-request-details-update-object) | <p>​</p><p>A <a href="../digital-river-payment-objects.md#shipping-address-object">Shipping Address object</a> that contains the customer's Shipping Address.</p>                                            |

{% tabs %}
{% tab title="Example" %}
{% code overflow="wrap" %}
```javascript
applepay.on('shippingaddresschange', function(event) {
    var shippingAddress = event.shippingAddress;


    //create a Payment Request Details Update Object
    var newDetails = createPaymentRequestDetailsUpdateObject();

    event.updateWith(newDetails);
});
```
{% endcode %}
{% endtab %}
{% endtabs %}

#### **Apple Pay shipping address change object**

{% tabs %}
{% tab title="Example" %}
{% code overflow="wrap" %}
```javascript
{
    shippingAddress: {
        "name": "John Smith",
        "firstName": "John",
        "lastName": "Smith",
        "phone": "952-111-1111",
        "email": "jsmith@digitalriver.com",
        "address": {
            "line1": "10380 Bren Rd W",
            "line2": "string",
            "city": "Minnetonka",
            "postalCode": "55129",
            "state": "MN",
            "country": "US"
        }
    },
    "updateWith": function(data) {
        callback(data);
    }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Shipping option Change

A Shipping Option Change event occurs when the Customer has selected a different Shipping Option within the Payment Request interface. The event will emit the following object structure.

| Key            | Type                                                                                                                  | Description                                                                                                                                                                                                                                                                      |
| -------------- | --------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| updateWith     | Function                                                                                                              | Calling this function with a [Payment Request Details Update object](../digital-river-payment-objects.md#payment-request-details-update-error-object) merges your updates into the current [Payment Request object](../digital-river-payment-objects.md#payment-request-object). |
| shippingOption | A [Payment Request Details Update object​](../digital-river-payment-objects.md#payment-request-details-update-object) | <p>​</p><p>​</p><p>A <a href="../digital-river-payment-objects.md#payment-request-shipping-option-object">Payment Request Shipping Option object</a> that contains the customer's chosen Shipping Option.</p>                                                                    |

{% tabs %}
{% tab title="Example" %}
{% code overflow="wrap" %}
```javascript
applepay.on('shippingoptionchange', function(event) {
    var shippingOption = event.shippingOption;


    //create a Payment Request Details Update Object
    var newDetails = createPaymentRequestDetailsUpdateObject();
    event.updateWith(newDetails);
});
```
{% endcode %}
{% endtab %}
{% endtabs %}

#### **Apple Pay shipping option change object**

{% tabs %}
{% tab title="Example" %}
{% code overflow="wrap" %}
```javascript
{
    "shippingOption": {
        "id": "overnight-shipping",
        "label": "Overnight Shipping",
        "amount": 100,
        "detail": "Get this in 1 business day."
    },
    "updateWith": function(data) {
        callback(data);
    }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Source

A Source event occurs when the Customer completes their interaction with the Payment Request interface and creates a Payment Source. The emitted object will be a [Payment Request Response object](../digital-river-payment-objects.md#payment-request-response-object).

{% tabs %}
{% tab title="Example" %}
{% code overflow="wrap" %}
```javascript
googlepay.on('source', function(result) {
    var source = result.source;

    //pass the source to your back end for further processing
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Element functions

Use these functions to trigger functionality within the specified Element to further enhance your purchase flow experience.‌

### element.blur();

This function triggers the `blur()` event. This will remove the focus from the element.

{% tabs %}
{% tab title="Example" %}
{% code overflow="wrap" %}
```javascript
cardNumber.blur();
```
{% endcode %}
{% endtab %}
{% endtabs %}

### element.clear();

This function clears the contents of the element.

{% tabs %}
{% tab title="JavaScript" %}
{% code overflow="wrap" %}
```javascript
cardNumber.clear();
```
{% endcode %}
{% endtab %}
{% endtabs %}

### element.focus();

This function triggers the `focus()` event and places the focus on the element.

{% tabs %}
{% tab title="JavaScript" %}
{% code overflow="wrap" %}
```javascript
cardNumber.focus();
```
{% endcode %}
{% endtab %}
{% endtabs %}

### element.destroy();

This function destroys the element. Removes the element and all of its associated data so you cannot use it again. You must create a new element if you want to restore the associated data.

{% tabs %}
{% tab title="Example" %}
{% code overflow="wrap" %}
```javascript
cardNumber.destroy();
```
{% endcode %}
{% endtab %}
{% endtabs %}

### element.unmount();

This function removes the element from the Document Object Module (DOM). The element and its associated data still exists. You can place it on the page again by calling its `mount()` function.

{% tabs %}
{% tab title="Example" %}
{% code overflow="wrap" %}
```javascript
cardNumber.unmount();
```
{% endcode %}
{% endtab %}
{% endtabs %}

### element.update(options);

This function updates the element with any included options. This can include custom styles and classes.

{% tabs %}
{% tab title="Example" %}
{% code overflow="wrap" %}
```javascript
var options = {
    classes: {
        base: "DRElement",
        complete: "complete",
        empty: "empty",
        focus: "focus",
        invalid: "invalid",
        webkitAutofill: "autofill"
    },
    style: {
        base: {
            color: "#fff",
            fontFamily: "Arial, Helvetica, sans-serif",
            fontSize: "20px",
            fontSmoothing: "auto",
            fontStyle: "italic",
            fontVariant: "normal",
            letterSpacing: "3px"
        },
        empty: {
            color: "#fff"
        },
        complete: {
            color: "green"
        },
        invalid: {
            color: "red"
        }
    }
};

cardNumber.update(options);
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Styling an element container

### Custom classes

You can specify custom classes as part of a `Class` object included within the `Options` object when you create or update an element. If you do not provide custom classes, the system uses the default options.

{% tabs %}
{% tab title="Example" %}
{% code overflow="wrap" %}
```javascript
var options = {
    classes: {
        base: "DRElement",
        complete: "complete",
        empty: "empty",
        focus: "focus",
        invalid: "invalid",
        webkitAutofill: "autofill"
    }
}

var cardNumber = elements.create("cardnumber", options);
```
{% endcode %}
{% endtab %}
{% endtabs %}

#### **Available custom classes**

| Class Type      | ID             | Applies When                                                                                                                  | Default Class Name        |
| --------------- | -------------- | ----------------------------------------------------------------------------------------------------------------------------- | ------------------------- |
| Base            | base           | The Element is in its base state. The user either has not entered anything into the input field or is currently typing.       | DRElement                 |
| Complete        | complete       | The Element is in its complete state. The user has input value, and it meets the basic validation requirements of that field. | DRElement--complete       |
| Empty           | empty          | The Element is empty. The Element once had value but is now empty.                                                            | DRElement--empty          |
| Focus           | focus          | The Element has focus.                                                                                                        | DRElement--focus          |
| Invalid         | invalid        | The Element has value, but it does not meet the basic validation requirements of the field.                                   | DRElement--invalid        |
| WebKit Autofill | webkitAutofill | A saved card stored in a browser automatically fills this element.                                                            | DRElement-webkit-autofill |

### Custom styles

You can specify custom styles as part of a `Style` object included within the `Options` object when creating or updating an Element. If you don't provide custom styles, the system uses the browser defaults.

{% tabs %}
{% tab title="Example" %}
{% code overflow="wrap" %}
```javascript
var options = {
    style: {
        base: {
            color: "#fff",
            fontFamily: "Arial, Helvetica, sans-serif",
            fontSize: "20px",
            fontSmoothing: "auto",
            fontStyle: "italic",
            fontVariant: "normal",
            letterSpacing: "3px"
        },
        empty: {
            color: "#fff"
        },
        complete: {
            color: "green"
        },
        invalid: {
            color: "red",
        }
    }
}


var cardNumber = elements.create('cardnumber', options);
```
{% endcode %}
{% endtab %}
{% endtabs %}

#### **Available custom style classes**

| ID             | Class Name      | Description                                                          |
| -------------- | --------------- | -------------------------------------------------------------------- |
| base           | Base            | All other variants inherit from this style.                          |
| complete       | Complete        | Applied when the Element has valid input.                            |
| empty          | Empty           | Applied when the Element has no customer input.                      |
| focus          | Focus           | Applied when the Element has focus.                                  |
| invalid        | Invalid         | Applied when the Element has invalid input.                          |
| webKitAutofill | Webkit Autofill | Applied when the Element has been filled automatically by a browser. |

#### **Available custom styles**

| Style           | ID             | Type   | Example                         |
| --------------- | -------------- | ------ | ------------------------------- |
| Box Shadow      | boxShadow      | string | inset 0 0 0px 1000px #fff       |
| Text Color      | color          | string | "#fff"                          |
| Font Family     | fontFamily     | string | "Arial, Helvetica, sans-serif", |
| Font Size       | fontSize       | string | "20px"                          |
| Font Smoothing  | fontSmoothing  | string | "antialiased"                   |
| Font Style      | fontStyle      | string | "bold"                          |
| Font Variant    | fontVariant    | string | "normal"                        |
| Letter Spacing  | letterSpacing  | string | "2px"                           |
| Text Align      | textAlign      | string | "center"                        |
| Text Decoration | textDecoration | string | "underline"                     |
| Text Shadow     | textShadow     | string | "2px 2px #ff0000"               |
| Font Weight     | fontWeight     | string | "400"                           |
| Padding         | padding        | string | "2px"                           |
| Padding Top     | paddingTop     | string | "2px"                           |
| Padding Right   | paddingRight   | string | "2px"                           |
| Padding Bottom  | paddingBottom  | string | "2px"                           |
| Padding Left    | paddingLeft    | string | "2px"                           |

### Pseudo-classes

| Class             | ID                | Type   |
| ----------------- | ----------------- | ------ |
| :hover            | :hover            | string |
| :focus            | :focus            | string |
| ::placeholder     | ::placeholder     | string |
| ::selection       | ::selection       | string |
| :-webkit-autofill | :-webkit-autofill | string |
| :disabled         | :disabled         | string |

### Other customizable attributes

| Attribute        | ID              | Type    | Example       | Description                                                                                                                                                                                                              |
| ---------------- | --------------- | ------- | ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Placeholder Text | placeholderText | string  | "Card Number" | You may override the placeholder text that appears in `cardnumber`, `cardexpiration`, `cardcvv`, and `onlinebanking` element types. If you specify a `placeholderText` attribute, localization will not be applied.      |
| Mask             | mask            | boolean | true/false    | You may choose to mask the contents of the DigitalRiver.js Element after a proper number and card security code has been implemented. If enabled, only the last 4 digits of the card number will be exposed in the view. |
