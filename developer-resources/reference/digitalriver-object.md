---
description: Learn how to use the DigitalRiver object
---

# DigitalRiver object

## Creating a DigitalRiver object

For details, refer to the [Initializing DigitalRiver.js](digital-river-publishable-api-key.md) page.

{% code overflow="wrap" %}
```javascript
let digitalRiver = new DigitalRiver("pk_test_fh9861t8b7384b7dke9e8dn4fb79808192", {
     "locale": "nl"
});
```
{% endcode %}

## Creating an instance of Drop-in

### `createDropin(config)` <a href="#digitalriver.createdropin-configurationobject" id="digitalriver.createdropin-configurationobject"></a>

Use `createDropin(`[`config`](../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md#configuring-drop-in-payments)`)` to create an instance of [Drop-in payments](../../payments/payment-integrations-1/drop-in/). For details, refer to the [Drop-in payments integration guide](../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md).&#x20;

## Creating elements

### `createElement(element, config)` <a href="#digitalriver.createelement" id="digitalriver.createelement"></a>

Use this method to create an instance of an [Element](elements/) that you can use to capture payment details. You can use the following Elements with [`createSource()`](digitalriver-object.md#creating-sources) to create a payment source.

| Element Type     | Description                                                                      |
| ---------------- | -------------------------------------------------------------------------------- |
| `amazonPay`      | [AmazonPay element](elements/amazon-pay-element.md)                              |
| `applepay`       | [Apple Pay element](elements/apple-pay-elements.md)                              |
| `cardCVV`        | A card security code field                                                       |
| `cardExpiration` | A credit card expiration field                                                   |
| `cardNumber`     | A credit card number field                                                       |
| `googlepay`      | [Google Pay element](elements/google-pay-elements.md)                            |
| `iban`           | [IBAN element](elements/iban-element.md)                                         |
| `ideal`          | [iDEAL element](elements/ideal-element.md)                                       |
| `konbini`        | [A Konbini element](elements/konbini-elements.md)                                |
| `onlineBanking`  | [An online banking element](elements/online-banking-elements.md)                 |
| `offlineRefund`  | [An offline refund data collection element](elements/offline-refund-elements.md) |
| `paypal`         | [A PayPal element](elements/paypal-elements.md)                                  |

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
            color: "red",
        }
    }
};


var cardNumber = digitalriver.createElement('cardnumber', options);
var cardExpiration = digitalriver.createElement('cardexpiration', options);
var cardCVV = digitalriver.createElement('cardcvv', options);
```
{% endcode %}
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="JavaScript" %}
{% code overflow="wrap" %}
```javascript
<div id="card-number" class="DRElement">
    <!-- The embedded Element iframe -->
    <iframe src="cardnumber.html"></iframe>
</div>


<div id="card-number" class="DRElement--complete">
    <!-- The embedded Element iframe -->
    <iframe src="cardnumber.html"></iframe>
</div>

<div id="card-number" class="DRElement--empty">
    <!-- The embedded Element iframe -->
    <iframe src="cardnumber.html"></iframe>
</div>

<div id="card-number" class="DRElement--focus">
    <!-- The embedded Element iframe -->
    <iframe src="cardnumber.html"></iframe>
</div>


<div id="card-number" class="DRElement--invalid">
    <!-- The embedded Element iframe -->
    <iframe src="cardnumber.html"></iframe>
</div>


<div id="card-number" class="DRElement--autofilled">
    <!-- The embedded Element iframe -->
    <iframe src="cardnumber.html"></iframe>
</div>
```
{% endcode %}
{% endtab %}
{% endtabs %}

#### **Options**

| Heading | State      | Default Class         |
| ------- | ---------- | --------------------- |
| classes | base       | DRElement             |
| classes | complete   | DRElement--complete   |
| classes | empty      | DRElement--empty      |
| classes | focus      | DRElement--focus      |
| classes | invalid    | DRElement--invalid    |
| classes | autofilled | DRElement--autofilled |

## Creating a payment request

For details, refer to the [Payment request object](digital-river-payment-objects.md#payment-request-object) in the [Digital River payment objects](digital-river-payment-objects.md) article.

## Creating sources

When creating sources, you can select a [method that accepts an element](digitalriver-object.md#createsource-sourcedata) or use a [method that doesn't require an element](digitalriver-object.md#createsource-element-sourcedata). Both methods, however, require that you provide source data to tokenize. When configuring this data, you can [specify a future source use](digitalriver-object.md#specifying-a-sources-future-use).

For both versions, the `createSource()` method returns a promise that contains a `Result` object. The `Result` object, in turn, contains one of two possible objects:‌

* **source** — A `Source` object created by Digital River.
* **error** — An [error object](error-types-codes-and-objects.md#create-source-error-object) that indicates a problem with the tokenization request. It provides the data you must correct before creating a source again.

### `createSource(sourceData)` <a href="#createsource-sourcedata" id="createsource-sourcedata"></a>

Use the `createSource(sourceData)` method to create a payment source that contains information you can safely use with other Digital River APIs. This includes immediate sources (if PCI compliant), redirect sources, or delayed sources. See [Configuring payment methods](../../payments/payment-integrations-1/digitalriver.js/payment-methods/) for more information on the structure of these requests.‌

In the following example, the method takes a single argument. The `sourceData` contains the data that you want Digital River to tokenize.

{% tabs %}
{% tab title="Example" %}
{% code overflow="wrap" %}
```javascript
var sourceData = {
        "type": "creditCard",
        "owner": {
            "firstName": "firstName",
            "lastName": "lastName",
            "email": "email@email.org",
            "address": {
                "line1": "1234 First St.",
                "city": "Minnetonka",
                "state": "MN",
                "country": "US",
                "postalCode": 55410
            }
        },
        "creditCard": {
            "number": "4444333322221111",
            "expirationMonth": 12,
            "expirationYear": 2025,
            "cvv": "123"
        }
    }


digitalriver.createSource(sourceData).then(function(result) {
    if(result.error) {
        //handle error message
        var errorMessage = result.error.errors[0].message;
    } else {

        //send source to back end for processing
        var source = result.source;
    }
});
```
{% endcode %}
{% endtab %}
{% endtabs %}

A successful response returns a `source` with a unique `id`.

{% tabs %}
{% tab title="Source response" %}
{% code overflow="wrap" %}
```javascript
{
    "error": undefined,
    "source": {
        "id": "775d3ff1-99a3-4640-bd2c-24e4b6b13324",
        "type": "creditCard",
        "owner": {
            "firstName": "John",
            "lastName": "Doe",
            "email": "john.doe@yahoo.com",
            "referenceId": "",
            "address": {
                "line1": "10380 Bren Road W.",
                "line2": "Suite 929",
                "city": "Minnetonka",
                "state": "MN",
                "country": "US",
                "postalCode": "55343"
            }
        },
        "status": "chargeable",
        "creationIp": "67.256.231.1",
        "creationDate": "2018-08-22T19:21:59.26Z",
        "flow": "standard",
        "creditCard": {
            "brand": "Visa",
            "expirationMonth": 10,
            "expirationYear": 2019,
            "lastFourDigits": "1111"
        }
    }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

An unsuccessful response returns an `error` with information on what must be corrected.

{% tabs %}
{% tab title="Error response" %}
{% code overflow="wrap" %}
```javascript
{
    "error": {
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
    },
    source: undefined
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

### `createSource(element, sourceData)` <a href="#createsource-element-sourcedata" id="createsource-element-sourcedata"></a>

Use the `createSource(element, sourceData)` method to create a tokenized source to safely transmit to the backend for use in downstream API calls. This method requests two parameters:‌

* **element** — A `Element` object created using the [Elements](elements/) portion of this library.
* **sourceData** — The source data that you want Digital River to tokenize. See [Common payment sources](digital-river-payment-objects.md) for more information on the required source data.

The method uses source data and an element argument in the following example.

{% tabs %}
{% tab title="Example" %}
{% code overflow="wrap" %}
```javascript
var sourceData = {
        "type": "creditCard",
        "owner": {
            "firstName": "firstName",
            "lastName": "lastName",
            "email": "email@email.org",
            "address": {
                "line1": "1234 First St.",
                "city": "Minnetonka",
                "state": "MN",
                "country": "US",
                "postalCode": 55410
            }
        }
    }


digitalriver.createSource(cardNumber, sourceData).then(function(result) {
    if(result.error) {
        //handle error messages
        var errorMessage = result.error.errors[0].message;
    } else {
        //send source to back end for processing
        var source = result.source;
    }
});
```
{% endcode %}
{% endtab %}
{% endtabs %}

A successful response returns a `source` with a unique `id`.

{% tabs %}
{% tab title="Source response" %}
{% code overflow="wrap" %}
```javascript
{
    "error": undefined,
    "source": {
        "id": "775d3ff1-99a3-4640-bd2c-24e4b6b13324",
        "clientId": "gc",
        "channelId": "drdod15",
        "type": "creditCard",
        "owner": {
            "firstName": "Gwen",
            "lastName": "Sawayn",
            "email": "Felicita81@yahoo.com",
            "referenceId": "",
            "address": {
                "line1": "04644 Altenwerth Drives",
                "line2": "Suite 929",
                "city": "North Aurelia",
                "state": "NV",
                "country": "US",
                "postalCode": "93414-6991"
            }
        },
        "amount": "100.00",
        "currency": "USD",
        "status": "chargeable",
        "creationIp": "67.216.237.4",
        "creationDate": "2018-08-22T19:21:59.26Z",
        "flow": "standard",
        "creditCard": {
            "brand": "Visa",
            "expirationMonth": 10,
            "expirationYear": 2019,
            "lastFourDigits": "1111"
        }
    }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

An unsuccessful response returns an `error` with information on what must be corrected.

{% tabs %}
{% tab title="Error response" %}
{% code overflow="wrap" %}
```javascript
{
    "error": {
        "type": "validation_error",
        "errors": [{
            "code": "incomplete_card_number",
            "message": "Your card number is incomplete."
        }]
    },
    source: undefined
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Specifying a source's future use

When creating a source using DigitalRiver.js, you should identify the types of transactions it will likely use in the future. This increases the probability that these future transactions will be approved. The `usage` value you select should be the one that most closely corresponds to our business model. The available options are [subscription](digitalriver-object.md#subscription), [convenience](digitalriver-object.md#convenience), and [unscheduled](digitalriver-object.md#unscheduled).

#### Subscription

Set `usage` to `subscription` when you create sources primarily for recurring transactions made at regular intervals for a product or a service.

#### **Convenience**

The `convenience` setting applies mainly to saved payment sources used for one-off transactions. These are sources where customers are typically present during the checkout flow and want to access their payment information quickly. Select this option if you don't offer [subscriptions](digitalriver-object.md#subscription) or don't have [unscheduled](digitalriver-object.md#unscheduled) merchant-initiated transactions.

#### Unscheduled

Set `usage` to `unscheduled` when you create sources for unscheduled merchant-initiated transactions. These are contracts that occur on a non-fixed schedule using stored card information. Automatic top-ups are an example of one such transaction. They occur whenever a customer's balance drops below a pre-defined amount.

## Retrieving sources

### `retrieveSource(sourceId, sourceClientSecret)` <a href="#digitalriver.retrievesource-sourceid-sourceclientsecret" id="digitalriver.retrievesource-sourceid-sourceclientsecret"></a>

Use this method to retrieve a source with the front-end DigitalRiver.js library. This method takes two parameters:‌

* **sourceId**—The unique ID of the source you want to retrieve.
* **sourceClientSecret**—The `clientSecret` value of the source you are trying to retrieve. This is specific to the source.

The `digitalriver.createSource()` returns a Promise with a `Result` object. (See the following source response example.) The Result object will have either:‌

* **result.source**—If this object is not null, it will contain the `Source` object you requested.
* **result.error**— If this object is not null, it will contain an `Error` object with details on the specific error.

{% tabs %}
{% tab title="Example" %}
{% code overflow="wrap" %}
```javascript
digitalriver.retrieveSource("ee90c07c-5549-4a6b-aa5f-aabe29b1e97a","ee90c07c-5549-4a6b-aa5f-aabe29b1e97a_51afe818-0e7f-46d7-8257-b209b20f4d8").then(function(result) {
    if(result.error) {
        //handle error messages
        var errorMessage = result.error.errors[0].message;
    } else {
        //do something with the source
        var source = result.source;
    }
});
```
{% endcode %}
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Source response" %}
{% code overflow="wrap" %}
```javascript
{
    "error": undefined,
    "source": {
        "id": "775d3ff1-99a3-4640-bd2c-24e4b6b13324",
        "clientId": "gc",
        "channelId": "drdod15",
        "type": "creditCard",
        "usage": "single",
        "owner": {
            "firstName": "Gwen",
            "lastName": "Sawayn",
            "email": "Felicita81@yahoo.com",
            "referenceId": "",
            "address": {
                "line1": "04644 Altenwerth Drives",
                "line2": "Suite 929",
                "city": "North Aurelia",
                "state": "NV",
                "country": "US",
                "postalCode": "93414-6991"
            }
        },
        "amount": "100.00",
        "currency": "USD",
        "status": "chargeable",
        "creationIp": "67.216.237.4",
        "creationDate": "2018-08-22T19:21:59.26Z",
        "flow": "standard",
        "creditCard": {
            "brand": "Visa",
            "expirationMonth": 10,
            "expirationYear": 2019,
            "lastFourDigits": "1111"
        }
    }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Authenticating sources

The authenticate source method determines whether the saved payment source selected by a customer during the checkout process requires [Strong Customer Authentication](../../payments/psd2-and-sca/) (SCA).

You can use this method when [building workflows](../../integration-options/checkouts/building-you-workflows/) that allow customers to retrieve saved payment information during [one-off purchases](../../integration-options/checkouts/building-you-workflows/#customer-selects-saved-credit-card-during-checkout) and [subscription acquisitions](../../integration-options/checkouts/building-you-workflows/#customer-saves-credit-card-details-during-subscription-acquisition-checkout).

The [standard version of the method](digitalriver-object.md#digitalriverjs-digitalriver.authenticatesource-data) accepts a configuration object that contains the data we need to authenticate the source. Except for the `returnUrl`, you can set the parameters of this object by [retrieving the source](../../payments/payment-sources/retrieving-sources.md) and then [getting the required data](../../payments/payment-sources/using-the-source-identifier.md#authenticating-sources).

| Parameter            | Required/Optional | Description                                                                                                                                 |
| -------------------- | ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| `sessionId`          | Required          | The [payment session](../../integration-options/checkouts/creating-checkouts/payment-sessions.md) identifier of this transaction.           |
| `sourceId`           | Required          | The identifier of the [payment source](../../payments/payment-sources/) used in this transaction.                                           |
| `sourceClientSecret` | Required          | The source client secret used for this transaction.                                                                                         |
| `returnUrl`          | Required          | The return URL where the customer is directed when 3D Secure 1 is required. If the value is not provided, we use the current page location. |

{% hint style="danger" %}
Do not log, embed in URLs, or expose the `sourceClientSecret` to anyone other than the customer. On any page that includes the secret, ensure that [TLS](https://en.wikipedia.org/wiki/Transport\_Layer\_Security) is enabled.
{% endhint %}

The [other version of the authenticate source method](digitalriver-object.md#digitalriverjs-digitalriver.authenticatesource-data-1) accepts this same data plus an optional CVV [Element](elements/) type.

After you call either version of this method, Digital River automatically handles the SCA requirements. Once the customer completes the necessary authentication or we determine that authentication isn't required, the method resolves, and the checkout flow can continue.

The method returns a  source authentication result object with a promise. The following are the possible results and the recommended actions:

| Status                        | Description                                                                                                                                             |
| ----------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `complete`                    | The customer successfully completed the steps necessary to authenticate the source. You can now submit the order.                                       |
| `authentication_not_required` | Digital River determined that the payment source didn't require authentication for this payment session. You can now submit the order.                  |
| `failed`                      | Source authentication failed. The source can still be used in the transaction but may be declined. You should attempt to authenticate the source again. |

### `authenticateSource(data)` <a href="#digitalriverjs-digitalriver.authenticatesource-data" id="digitalriverjs-digitalriver.authenticatesource-data"></a>

This method can [authenticate a payment source](digitalriver-object.md#authenticating-sources) before applying it to a transaction.

{% code overflow="wrap" %}
```javascript
digitalriver.authenticateSource({
    "sessionId": "65b1e2c2-632c-4240-8897-195ca22ce108",
    "sourceId": "ee90c07c-5549-4a6b-aa5f-aabe29b1e97a",
    "sourceClientSecret": "ee90c07c-5549-4a6b-aa5f-aabe29b1e97a_51afe818-0e7f-46d7-8257-b209b20f4d8",
    "returnUrl": "https://returnurl.com"
});
```
{% endcode %}

The following is an example response when a source is successfully authenticated:

{% code overflow="wrap" %}
```javascript
{
    "status": "complete"
}
```
{% endcode %}

### `authenticateSource([cvvElement], data)` <a href="#digitalriverjs-digitalriver.authenticatesource-data" id="digitalriverjs-digitalriver.authenticatesource-data"></a>

In this alternative method to [authenticate sources](digitalriver-object.md#authenticating-sources), you can provide an optional CVV [Element](elements/) type (assuming it is correctly [created](digitalriver-object.md#creating-elements) and [mounted](elements/#element-mount)). By setting this parameter, the value contained in the field of the CVV Element is included in the authentication request.

{% code overflow="wrap" %}
```javascript
digitalriver.authenticateSource(cvvElement, {
    "sessionId": "65b1e2c2-632c-4240-8897-195ca22ce108",
    "sourceId": "ee90c07c-5549-4a6b-aa5f-aabe29b1e97a",
    "sourceClientSecret": "ee90c07c-5549-4a6b-aa5f-aabe29b1e97a_51afe818-0e7f-46d7-8257-b209b20f4d8",
    "returnUrl": "https://returnurl.com"
});
```
{% endcode %}

The following is an example response when a source is successfully authenticated:

{% code overflow="wrap" %}
```javascript
{
    "status": "complete"
}
```
{% endcode %}

## Updating sources

### **`updateSource([element,] sourceData)`** <a href="#digitalriver.updatesource-element-sourcedata" id="digitalriver.updatesource-element-sourcedata"></a>

Use this method to update details on a source.

{% hint style="warning" %}
When updating a source, you can only update the owner and the expiration details for Credit Cards. If you need to update a non-Credit Card (**creditCard**) payment type, use [createSource](digitalriver-object.md#createsource-sourcedata).
{% endhint %}

This method takes two parameters:‌

* `element`—An optional card expiration element for using the Elements portion of this library.
* `sourceData`—A required data object containing additional data required to update the payment source.

| Field        | Required | Type            | Description                                                                                                                                       |
| ------------ | -------- | --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| clientSecret | Required | String          | The Client Secret of the source you are updating.                                                                                                 |
| id           | Required | String          | The ID of the source you are updating.                                                                                                            |
| owner        | Optional | An Owner Object | <p>An object containing the Owner details.<br><strong>Note</strong>: You can only update the <code>owner</code> information for Credit Cards.</p> |

`digitalriver.updateSource()` returns a Promise that returns a result object. The result object will have either:‌

* `result.source`—A source object that was updated in the Payments Service
* `result.error`—An error occurred that must be corrected to update the source.

#### **Updating expiration and address information**

{% tabs %}
{% tab title="Example" %}
{% code overflow="wrap" %}
```javascript
//Create the element using DigitalRiver.js and place it on the page.
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
        }
  ...
}
var cardExpiration = digitalriver.createElement('cardexpiration', options);
cardExpiration.mount('card-expiration');


var sourceData = {
        "id": "14381d1c-8bff-4350-aeea-82b36f3a196c",
        "clientSecret": "14381d1c-8bff-4350-aeea-82b36f3a196c_14381d1c-8bff-4350-aeea-82b36f3a196c",
        "owner": {
            "firstName": "firstName",
            "lastName": "lastName",
            "email": "email@email.org",
            "address": {
                "line1": "1234 First St.",
                "city": "Minnetonka",
                "state": "MN",
                "country": "US",
                "postalCode": 55410
            }
        }
    }


digitalriver.updateSource(cardExpiration, sourceData).then(function(result) {
    if(result.error) {
        //handle error messages
        var errorMessage = result.error.errors[0].message;
    } else {
        //the source has been updated with new details
        var source = result.source;
    }
});
```
{% endcode %}
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Source Response" %}
{% code overflow="wrap" %}
```javascript
{
    "error": undefined,
    "source": {
        "id": "775d3ff1-99a3-4640-bd2c-24e4b6b13324",
        "clientId": "gc",
        "channelId": "drdod15",
        "type": "creditCard",
        "usage": "single",
        "owner": {
            "firstName": "firstName",
            "lastName": "lastName",
            "email": "email@email.org",
            "address": {
                "line1": "1234 First St.",
                "city": "Minnetonka",
                "state": "MN",
                "country": "US",
                "postalCode": 55410
            }
        },
        "status": "chargeable",
        "creationIp": "67.216.237.4",
        "creationDate": "2018-08-22T19:21:59.26Z",
        "flow": "standard",
        "creditCard": {
            "brand": "Visa",
            "expirationMonth": 10,
            "expirationYear": 2019,
            "lastFourDigits": "1111"
        }
    }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

#### **Updating only address information**

{% tabs %}
{% tab title="Example" %}
{% code overflow="wrap" %}
```javascript
var sourceData = {
        "id": "14381d1c-8bff-4350-aeea-82b36f3a196c",
        "clientSecret": "14381d1c-8bff-4350-aeea-82b36f3a196c_14381d1c-8bff-4350-aeea-82b36f3a196c",
        "owner": {
            "firstName": "firstName",
            "lastName": "lastName",
            "email": "email@email.org",
            "address": {
                "line1": "1234 First St.",
                "city": "Minnetonka",
                "state": "MN",
                "country": "US",
                "postalCode": 55410
            }
        }
    }


digitalriver.updateSource(sourceData).then(function(result) {
    if(result.error) {
        //handle error messages
        var errorMessage = result.error.errors[0].message;
    } else {
        //the source has been updated with new details
        var source = result.source;
    }
});
```
{% endcode %}
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Source Response" %}
{% code overflow="wrap" %}
```javascript
{
    "error": undefined,
    "source": {
        "id": "775d3ff1-99a3-4640-bd2c-24e4b6b13324",
        "clientId": "gc",
        "channelId": "drdod15",
        "type": "creditCard",
        "usage": "single",
        "owner": {
            "firstName": "firstName",
            "lastName": "lastName",
            "email": "email@email.org",
            "address": {
                "line1": "1234 First St.",
                "city": "Minnetonka",
                "state": "MN",
                "country": "US",
                "postalCode": 55410
            }
        },
        "status": "chargeable",
        "creationIp": "67.216.237.4",
        "creationDate": "2018-08-22T19:21:59.26Z",
        "flow": "standard",
        "creditCard": {
            "brand": "Visa",
            "expirationMonth": 10,
            "expirationYear": 2019,
            "lastFourDigits": "1111"
        }
    }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

#### **Updating only card expiration information**

{% tabs %}
{% tab title="Example" %}
{% code overflow="wrap" %}
```javascript
//Create the element using DigitalRiver.js and place it on the page.
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
        }

  ...
}
var cardExpiration = digitalriver.createElement('cardexpiration', options);

cardExpiration.mount('card-expiration');


var sourceData = {
        "id": "14381d1c-8bff-4350-aeea-82b36f3a196c",
        "clientSecret": "14381d1c-8bff-4350-aeea-82b36f3a196c_14381d1c-8bff-4350-aeea-82b36f3a196c"
    }


digitalriver.updateSource(cardExpiration, sourceData).then(function(result) {
    if(result.error) {
        //handle error messages
        var errorMessage = result.error.errors[0].message;
    } else {
        //the source has been updated with new details
        var source = result.source;
    }
});
```
{% endcode %}
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Source Response" %}
{% code overflow="wrap" %}
```javascript
{
    "error": undefined,
    "source": {
        "id": "775d3ff1-99a3-4640-bd2c-24e4b6b13324",
        "clientId": "gc",
        "channelId": "drdod15",
        "type": "creditCard",
        "usage": "single",
        "owner": {
            "firstName": "firstName",
            "lastName": "lastName",
            "email": "email@email.org",
            "address": {
                "line1": "1234 First St.",
                "city": "Minnetonka",
                "state": "MN",
                "country": "US",
                "postalCode": 55410
            }
        },
        "status": "chargeable",
        "creationIp": "67.216.237.4",
        "creationDate": "2018-08-22T19:21:59.26Z",
        "flow": "standard",
        "creditCard": {
            "brand": "Visa",
            "expirationMonth": 10,
            "expirationYear": 2019,
            "lastFourDigits": "1111"
        }
    }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

#### **Update error**‌

If there is a problem with the update request, an error object will be returned in the response.

{% tabs %}
{% tab title="Source Errors" %}
{% code overflow="wrap" %}
```javascript
{
    "error": {
        "type": "validation_error",
        "errors": [{
            "code": "incomplete_card_number",
            "message": "Your card number is incomplete."
        }]
    },
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Retrieving available payment methods

### `retrieveAvailablePaymentMethods([filters])` <a href="#digitalriver.retrieveavailablepaymentmethods-filters" id="digitalriver.retrieveavailablepaymentmethods-filters"></a>

Use this method to retrieve an array of available payment methods. You can use this to filter and determine applicable payment methods while building your checkout flows. The `filters` object is optional.

| Attribute         | Required/Optional | Description                                                                                                    |
| ----------------- | ----------------- | -------------------------------------------------------------------------------------------------------------- |
| currency          | Optional          | The currency of the transaction.                                                                               |
| country           | Optional          | The country of the billing addresses associated with this transaction.                                         |
| supportsStorage   | Optional          | Whether the payment supports storage.                                                                          |
| supportsRecurring | Optional          | Whether the payment method supports recurring payments.                                                        |
| supportsFreeTrial | Optional          | Whether the payment method supports free trials.                                                               |
| sessionId         | Optional          | The Payment Session ID. If used, the response will return the payment methods which apply to your transaction. |

**Retrieve available payment methods response without using session ID**

The following example shows a request with no filters applied.

{% tabs %}
{% tab title="Request Example" %}
{% code overflow="wrap" %}
```javascript
digitalriver.retrieveAvailablePaymentMethods().then(function(result) {
    //do something with the result, this could include showing or hiding specific payment methods that are applicable to the display
});
```
{% endcode %}
{% endtab %}
{% endtabs %}

The following response includes all payment methods that you configured for your account.

{% tabs %}
{% tab title="Response Example" %}
{% code overflow="wrap" %}
```javascript
{
    "paymentMethods": [
        {
            "type": "alipay",
            "flow": "redirect",
            "supportsRecurring": false,
            "supportsFreeTrial": false,
            "images": {
                "iconImage": "https://ui1.img.digitalrivercontent.net/Storefront/images/paymentMethodLogos/alipay.png"
            }
        },
        {
            "type": "applePay",
            "flow": "standard",
            "supportsRecurring": false,
            "supportsFreeTrial": false,
            "images": {
                "iconImage": "https://ui1.img.digitalrivercontent.net/Storefront/images/paymentMethodLogos/applepay.png"
            }
        },
        {
            "type": "bankTransfer",
            "flow": "redirect",
            "supportsRecurring": false,
            "supportsFreeTrial": false,
            "images": {
                "iconImage": "https://ui1.img.digitalrivercontent.net/Storefront/images/paymentMethodLogos/bankTransfer.png"
            }
        },
        {
            "type": "carrierFinancing",
            "flow": "standard",
            "supportsRecurring": false,
            "supportsFreeTrial": false,
            "images": {}
        },
        {
            "type": "codJapan",
            "flow": "standard",
            "supportsRecurring": false,
            "supportsFreeTrial": false,
            "images": {
                "iconImage": "https://ui1.img.digitalrivercontent.net/Storefront/images/paymentMethodLogos/codJapan.png"
            }
        },
        {
            "type": "creditCard",
            "flow": "standard",
            "supportsRecurring": true,
            "supportsFreeTrial": true,
            "images": {
                "iconImage": "https://ui1.img.digitalrivercontent.net/Storefront/images/paymentMethodLogos/creditcard.png"
            }
        },
        {
            "type": "creditInstallment",
            "flow": "redirect",
            "supportsRecurring": false,
            "supportsFreeTrial": false,
            "images": {},
            "terms": [
                {
                    "id": "8281",
                    "name": "4x installment for Cetelem",
                    "code": "4_months",
                    "underMinimumAmount": 0,
                    "overMaximumAmount": 0,
                    "durationMonths": 4,
                    "monthlyPaymentAmount": 25.21,
                    "monthlyPaymentWithFeesAmount": 30.21,
                    "orderTotal": 100,
                    "totalRepayable": 120.84,
                    "creditChargeAmount": 20.84,
                    "originationFeeAmount": 5,
                    "administrationFeeAmount": 0,
                    "nominalApr": 4,
                    "effectiveApr": 151.1
                }
            ]
        },
        {
            "type": "directDebit",
            "flow": "redirect",
            "supportsRecurring": true,
            "supportsFreeTrial": false,
            "images": {
                "iconImage": "https://ui1.img.digitalrivercontent.net/Storefront/images/paymentMethodLogos/directDebit.png"
            }
        },
        {
            "type": "directDebitGb",
            "flow": "redirect",
            "supportsRecurring": true,
            "supportsFreeTrial": false,
            "images": {
                "iconImage": "https://ui1.img.digitalrivercontent.net/Storefront/images/paymentMethodLogos/directDebitGb.png"
            }
        },
        {
            "type": "googlePay",
            "flow": "standard",
            "supportsRecurring": true,
            "supportsFreeTrial": true,
            "images": {
                "iconImage": "https://ui1.img.digitalrivercontent.net/Storefront/images/paymentMethodLogos/googlepay.png"
            }
        },
        {
            "type": "klarnaCredit",
            "flow": "redirect",
            "supportsRecurring": false,
            "supportsFreeTrial": false,
            "images": {
                "iconImage": "https://ui1.img.digitalrivercontent.net/Storefront/images/paymentMethodLogos/klarna.png"
            }
        },
        {
            "type": "klarnaCreditRecurring",
            "flow": "redirect",
            "supportsRecurring": true,
            "supportsFreeTrial": false,
            "images": {
                "iconImage": "https://ui1.img.digitalrivercontent.net/Storefront/images/paymentMethodLogos/klarnaRecurring.png"
            }
        },
        {
            "type": "konbini",
            "flow": "receiver",
            "supportsRecurring": false,
            "supportsFreeTrial": false,
            "images": {
                "iconImage": "https://ui1.img.digitalrivercontent.net/Storefront/images/paymentMethodLogos/konbini.png"
            }
        },
        {
            "type": "onlineBanking",
            "flow": "redirect",
            "supportsRecurring": false,
            "supportsFreeTrial": false,
            "images": {
                "iconImage": "https://ui1.img.digitalrivercontent.net/Storefront/images/paymentMethodLogos/onlineBanking.png"
            }
        },
        {
            "type": "payco",
            "flow": "redirect",
            "supportsRecurring": false,
            "supportsFreeTrial": false,
            "images": {
                "iconImage": "https://ui1.img.digitalrivercontent.net/Storefront/images/paymentMethodLogos/payco.png"
            }
        },
        {
            "type": "payPal",
            "flow": "redirect",
            "supportsRecurring": false,
            "supportsFreeTrial": false,
            "images": {
                "iconImage": "https://ui1.img.digitalrivercontent.net/Storefront/images/paymentMethodLogos/paypal.png"
            }
        },
        {
            "type": "payPalBilling",
            "flow": "redirect",
            "supportsRecurring": true,
            "supportsFreeTrial": true,
            "images": {
                "iconImage": "https://ui1.img.digitalrivercontent.net/Storefront/images/paymentMethodLogos/paypalBilling.png"
            }
        },
        {
            "type": "wireTransfer",
            "flow": "receiver",
            "supportsRecurring": false,
            "supportsFreeTrial": false,
            "images": {
                "iconImage": "https://ui1.img.digitalrivercontent.net/Storefront/images/paymentMethodLogos/wireTransfer.png"
            }
        }
    ]
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

#### Retrieve available payment methods response using filters <a href="#digitalriverjs-retrieveavailablepaymentmethodsresponsewithusingfilters" id="digitalriverjs-retrieveavailablepaymentmethodsresponsewithusingfilters"></a>

The following example shows a request using filters.

{% tabs %}
{% tab title="Request Example" %}
{% code overflow="wrap" %}
```javascript
digitalriver.retrieveAvailablePaymentMethods({
    "currency": "USD",
    "country": "US",
    "supportsRecurring": true
}).then(function(result) {
    //do something with the result, this could include showing or hiding specific payment methods that are applicable to the display
});
```
{% endcode %}
{% endtab %}
{% endtabs %}

The following response only returns payment methods available in the US, using the USD currency and supporting recurring payments.

{% tabs %}
{% tab title="Response example" %}
{% code overflow="wrap" %}
```javascript
{
    "paymentMethods": [
        {
            "type": "creditCard",
            "flow": "standard",
            "supportsRecurring": true,
            "supportsFreeTrial": true,
            "images": {
                "iconImage": "https://ui1.img.digitalrivercontent.net/Storefront/images/paymentMethodLogos/creditcard.png"
            }
        },
        {
            "type": "googlePay",
            "flow": "standard",
            "supportsRecurring": true,
            "supportsFreeTrial": true,
            "images": {
                "iconImage": "https://ui1.img.digitalrivercontent.net/Storefront/images/paymentMethodLogos/googlepay.png"
            }
        },
        {
            "type": "klarnaCreditRecurring",
            "flow": "redirect",
            "supportsRecurring": true,
            "supportsFreeTrial": false,
            "images": {
                "iconImage": "https://ui1.img.digitalrivercontent.net/Storefront/images/paymentMethodLogos/klarnaRecurring.png"
            }
        },
        {
            "type": "payPalBilling",
            "flow": "redirect",
            "supportsRecurring": true,
            "supportsFreeTrial": true,
            "images": {
                "iconImage": "https://ui1.img.digitalrivercontent.net/Storefront/images/paymentMethodLogos/paypalBilling.png"
            }
        }
    ]
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

#### Retrieve available payment methods response with a Session ID <a href="#digitalriverjs-retrieveavailablepaymentmethodsresponsewithasessionidspecified" id="digitalriverjs-retrieveavailablepaymentmethodsresponsewithasessionidspecified"></a>

If you specify a Payment Session ID, you will only receive the payment methods which apply to your transaction.

{% tabs %}
{% tab title="Request Example" %}
{% code overflow="wrap" %}
```javascript
digitalriver.retrieveAvailablePaymentMethods({
    "sessionId": "d3941a36-6821-4d93-be23-6190226ae5f7"
}).then(function(result) {
    //do something with the result, this could include showing or hiding specific payment methods that are applicable to the display
});
```
{% endcode %}
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Response Example" %}
{% code overflow="wrap" %}
```javascript
{
    "sessionInformation": {
        "currency": "EUR",
        "country": "FR",
        "amount": "450.00"
    },
    "paymentMethods": [
        {
            "type": "applePay",
            "flow": "standard",
            "supportsRecurring": false,
            "supportsFreeTrial": false,
            "images": {
                "iconImage": "https://ui1.img.digitalrivercontent.net/Storefront/images/paymentMethodLogos/applepay.png"
            }
        },
        {
            "type": "creditCard",
            "flow": "standard",
            "supportsRecurring": true,
            "supportsFreeTrial": true,
            "images": {
                "iconImage": "https://ui1.img.digitalrivercontent.net/Storefront/images/paymentMethodLogos/creditcard.png"
            }
        },
        {
            "type": "directDebit",
            "flow": "redirect",
            "supportsRecurring": true,
            "supportsFreeTrial": false,
            "images": {
                "iconImage": "https://ui1.img.digitalrivercontent.net/Storefront/images/paymentMethodLogos/directDebit.png"
            }
        },
        {
            "type": "googlePay",
            "flow": "standard",
            "supportsRecurring": true,
            "supportsFreeTrial": true,
            "images": {
                "iconImage": "https://ui1.img.digitalrivercontent.net/Storefront/images/paymentMethodLogos/googlepay.png"
            }
        },
        {
            "type": "wireTransfer",
            "flow": "receiver",
            "supportsRecurring": false,
            "supportsFreeTrial": false,
            "images": {
                "iconImage": "https://ui1.img.digitalrivercontent.net/Storefront/images/paymentMethodLogos/wireTransfer.png"
            }
        }
    ]
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Credit card logos

If you want to display the credit card payment logo on your website, you can use the following URLs to add the appropriate brand logo image to your website:

{% hint style="info" %}
**Best Practices**: To ensure you always use the latest logo, link to the URL instead of downloading the image to your website.
{% endhint %}

* **Visa** ![](../../.gitbook/assets/visa.png) **URL**: [https://ui1.img.digitalrivercontent.net/Storefront/images/creditCardLogos/visa.png](https://ui1.img.digitalrivercontent.net/Storefront/images/creditCardLogos/visa.png)
* **Mastercard** ![](../../.gitbook/assets/mastercard.png) **URL**: [https://ui1.img.digitalrivercontent.net/Storefront/images/creditCardLogos/mastercard.png](https://ui1.img.digitalrivercontent.net/Storefront/images/creditCardLogos/mastercard.png)
* **American Express** ![](../../.gitbook/assets/amex.png) **URL**: [https://ui1.img.digitalrivercontent.net/Storefront/images/creditCardLogos/amex.png](https://ui1.img.digitalrivercontent.net/Storefront/images/creditCardLogos/amex.png)
* **Discover** ![](../../.gitbook/assets/discover.png) **URL**: [https://ui1.img.digitalrivercontent.net/Storefront/images/creditCardLogos/discover.png](https://ui1.img.digitalrivercontent.net/Storefront/images/creditCardLogos/discover.png)
* **JCB** ![](../../.gitbook/assets/jcb.png) **URL**: [https://ui1.img.digitalrivercontent.net/Storefront/images/creditCardLogos/jcb.png](https://ui1.img.digitalrivercontent.net/Storefront/images/creditCardLogos/jcb.png)
* **Maestro** ![](../../.gitbook/assets/maestro.png) **URL**: [https://ui1.img.digitalrivercontent.net/Storefront/images/creditCardLogos/maestro.png](https://ui1.img.digitalrivercontent.net/Storefront/images/creditCardLogos/maestro.png)
* **UnionPay** ![](../../.gitbook/assets/unionpay.png) **URL**: [https://ui1.img.digitalrivercontent.net/Storefront/images/creditCardLogos/unionpay.png](https://ui1.img.digitalrivercontent.net/Storefront/images/creditCardLogos/unionpay.png)

## Retrieving available banks for Online Banking

### `retrieveOnlineBankingBanks(countryCode, currency)` <a href="#digitalriver.retrieveonlinebankingbanks-countrycode-currency" id="digitalriver.retrieveonlinebankingbanks-countrycode-currency"></a>

Use this method to retrieve an array of available banks for a combination of [ISO 3166-1 alpha-2](https://en.wikipedia.org/wiki/ISO\_3166-1\_alpha-2) country code and [ISO 4217](https://en.wikipedia.org/wiki/ISO\_4217) currency code.‌

This method returns an array that will either be empty if no banks are available or will contain objects with Issuer IDs and Bank Names. DigitalRiver.js uses this data when creating an Online Banking source. This method is useful if you want to build a bank selector instead of using the Online Banking element.

{% tabs %}
{% tab title="Example" %}
{% code overflow="wrap" %}
```javascript
digitalriver.retrieveOnlineBankingBanks("DE","EUR").then(function(result) {
    //do something with the banks, this could include building a selector or something else
});
```
{% endcode %}
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Source response" %}
{% code overflow="wrap" %}
```javascript
[{
    "bankCode": "86",
    "bankName": "Sofortüberweisung"
}, {
    "bankCode": "21",
    "bankName": "Giropay"
}]
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Getting compliance details <a href="#digitalriver.compliance.getdetails-businessentitycode-locale" id="digitalriver.compliance.getdetails-businessentitycode-locale"></a>

The [`DigitalRiver` object](digitalriver-object.md) exposes [`Compliance.getDetails()`](digitalriver-object.md#compliance.getdetails), which returns various disclosures, such as terms of sale, privacy policies, save payment agreements, and cancellation rights, that you can use to ensure sales adhere to compliance requirements.

### `Compliance.getDetails()`

`Compliance.getDetails()` accepts a configuration object, which consists of a [`language`](digitalriver-object.md#language), [`country`](digitalriver-object.md#country), and [`businessEntityCode`](digitalriver-object.md#businessentitycode), all of which are required. This increases the probability that Digital River can return appropriately translated disclosures that apply to the customer’s shopping country and the transaction’s [selling entity](../../integration-options/checkouts/creating-checkouts/selling-entities.md).

{% code overflow="wrap" %}
```javascript
let config = {
    'language': 'en',
    'country': 'DE',
    'businessEntityCode': 'DR_IRELAND-ENTITY'
  };

var complianceDetails = digitalRiver.Compliance.getDetails(config);
```
{% endcode %}

#### `language`&#x20;

A required string that determines the language each [`disclosure`](digitalriver-object.md#compliance.getdetails-response) is translated into. The value you assign this property doesn't affect which specific disclosures are returned, only how their text is rendered.&#x20;

For a list of accepted values, refer to [Supported languages](../supported-languages.md).

#### `country`

A required string, formatted as an [ISO 3166-1 alpha-2](https://en.wikipedia.org/wiki/ISO\_3166-1\_alpha-2) code, represents the customer's shopping country. Since legal requirements vary slightly from country to country, the value you assign this property determines which specific disclosures Digital River returns. For example, some `country` values return a customer's cancellation rights, while others do not.

If the transaction involves [physical products](../../product-management/skus.md#how-products-are-classified-as-physical-or-digital), `country` should ideally be the same as the customer’s ship to country. If customers only purchase [digital products](../../product-management/skus.md#how-products-are-classified-as-physical-or-digital), then you can use their billing country.

#### `businessEntityCode`

A required string that represents the transaction's designated [selling entity](../../integration-options/checkouts/creating-checkouts/selling-entities.md). Similar to `country`, this affects which disclosures Digital River returns.

{% hint style="success" %}
In [checkouts](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts), you can find this value in `sellingEntity.id`.
{% endhint %}

For a list of accepted values, refer to [Supported selling entities](../../integration-options/checkouts/creating-checkouts/selling-entities.md#supported-selling-entities).&#x20;

### `Compliance.getDetails()` response

[`Compliance.getDetails()`](digitalriver-object.md#compliance.getdetails) returns a [`disclosure`](digitalriver-object.md#disclosure) which contains individual disclosures, such as `termsOfSale` and `privacyPolicy`, that you can display to customers. However, Digital River returns an [error](digitalriver-object.md#error) if the function's parameters are missing or unsupported.

#### `disclosure`

In most cases, the nested objects in `disclosure` contain `localizedText` and the `url` of a Digital River-hosted document.&#x20;

{% tabs %}
{% tab title="Example disclosure " %}
In the following `disclosure`, the text is rendered in English, and the content applies to customers making a purchase in Germany that is facilitated by the Digital River Ireland Ltd. [selling entity](../../integration-options/checkouts/creating-checkouts/selling-entities.md).&#x20;

{% code overflow="wrap" %}
```json
{
    "businessEntity": {
        "name": "Digital River Ireland Ltd.",
        "id": "DR_IRELAND-ENTITY"
    },
    "autorenewalPlanTerms": {
        "localizedText": "By checking the box below and completing your purchase, you expressly authorize and permit Digital River to automatically renew your purchased license or subscription for successive renewal terms each equal in length to the initial term specified above, at the purchase price for your initial term (plus taxes and fees, less any applicable discounts) using the payment information you provided for your initial purchase, until you cancel. At least one email will be sent to you to remind you of each upcoming renewal. We may change the renewal price as of the next renewal date if we provide you with prior notice of the change by email (you can elect to cancel automatic renewal as described below if you do not agree to the change). The Digital River <a href=\"https://store.digitalriver.com/store/defaults/de_DE/DisplayDRTermsAndConditionsPage/eCommerceProvider.Digital%20River%20Ireland%20Ltd.\" target=\"_blank\" class=\"dr_termsAndConditions\">Terms of Sale</a> and <a href=\"https://store.digitalriver.com/store/defaults/de_DE/DisplayDRPrivacyPolicyPage/eCommerceProvider.Digital%20River%20Ireland%20Ltd.\" target=\"_blank\" class=\"dr_privacyPolicy\">Privacy Policy</a> will apply to each renewal transaction. You may cancel your auto-renewal plan at any time by logging into the account interface (access information will be included in your order confirmation email or on the Customer Service Help page), selecting your product, and selecting the option to disable automatic renewal.<br/><br/>I agree that Digital River may store my payment information for future purchases including the processing of any subsequent subscription renewals which may occur following the date of this order."
    },
    "saveCardMandate": {
        "localizedText": "Yes, please save this account and payment information for future purchases."
    },
    "idealRecurringAgreement": {
        "localizedText": "By clicking the box, you authorize Digital River to collect your first payment via iDEAL and use your IBAN to collect the subsequent subscription payments by SEPA direct debit. You can review your SEPA Direct Debit information after order submission. <br/><br/>As part of your rights, you are entitled to a refund from your bank under the terms and conditions of your agreement with your bank. A refund must be claimed within 8 weeks starting from the date on which your account was debited. "
    },
    "confirmDisclosure": {
        "localizedText": "By submitting my order, I agree to the <a href=\"https://store.digitalriver.com/store/defaults/en_IE/DisplayDRTermsAndConditionsPage/eCommerceProvider.Digital%20River%20Ireland%20Ltd.\" target=\"_blank\" class=\"dr_termsAndConditions\">Terms of Sale</a> and the <a href=\"https://store.digitalriver.com/store/defaults/en_IE/DisplayDRPrivacyPolicyPage/eCommerceProvider.Digital%20River%20Ireland%20Ltd.\" target=\"_blank\" class=\"dr_privacyPolicy\">Privacy Policy</a> of Digital River Ireland Ltd."
    },
    "privacyPolicy": {
        "localizedText": "Privacy Policy",
        "url": "https://store.digitalriver.com/store/defaults/en_IE/DisplayDRPrivacyPolicyPage/eCommerceProvider.Digital%20River%20Ireland%20Ltd."
    },
    "termsOfSale": {
        "localizedText": "Terms of Sale",
        "url": "https://store.digitalriver.com/store/defaults/en_IE/DisplayDRTermsAndConditionsPage/eCommerceProvider.Digital%20River%20Ireland%20Ltd."
    },
    "cookiePolicy": {
        "localizedText": "Cookies",
        "url": "https://store.digitalriver.com/store/defaults/en_IE/DisplayDRCookiesPolicyPage/eCommerceProvider.Digital%20River%20Ireland%20Ltd."
    },
    "legalNotice": {
        "localizedText": "Legal Notice",
        "url": "https://store.digitalriver.com/store/defaults/en_IE/DisplayDRContactInformationPage/eCommerceProvider.Digital%20River%20Ireland%20Ltd."
    },
    "cancellationRights": {
        "localizedText": "Cancellation Right",
        "url": "https://store.digitalriver.com/store/defaults/en_IE/DisplayDRTermsAndConditionsPage/eCommerceProvider.Digital%20River%20Ireland%20Ltd.#cancellationRight"
    },
    "resellerDisclosure": {
        "localizedText": "<a href=\"https://store.digitalriver.com/store/defaults/en_IE/DisplayDRAboutDigitalRiverPage/eCommerceProvider.Digital%20River%20Ireland%20Ltd.\" target=\"_blank\" class=\"dr_resellerDisclosure\">Digital River Ireland Ltd.</a> is the authorised retailer and merchant providing e-commerce services for this shop.",
        "url": "https://store.digitalriver.com/store/defaults/en_IE/DisplayDRAboutDigitalRiverPage/eCommerceProvider.Digital%20River%20Ireland%20Ltd."
    }
}
```
{% endcode %}
{% endtab %}

{% tab title="Description of individual disclosures " %}
* `businessEntity`: The [selling entity's ](../../integration-options/checkouts/creating-checkouts/selling-entities.md)name and identifier.
* `resellerDisclosure`: Digital River's reseller disclosure.
* `termsOfSale:` Digital River's terms of sale.&#x20;
* `privacyPolicy`: Digital River's privacy policy.&#x20;
* `cookiePolicy`: Digital River's cookie policy.&#x20;
* `cancellationRights`: An explanation of a customer's cancellation rights.&#x20;
* `legalNotice`: Digital River's legal notice.
* `confirmDisclosure`: Digital River's confirmation disclosure statement. Place this disclosure next to your confirm order button.
* `autorenewalPlanTerms`: Digital River's autorenewal terms.
* `idealRecurringAgreement`: Digital River's [iDEAL](../../payments/supported-payment-methods/ideal.md) recurring payment agreement.&#x20;
* `saveCardMandate`: The save payment methods for future purchases agreement.
* `californiaPrivacyRights`: An explanation of a customer's California privacy rights.&#x20;
* `invoiceAgreement`: Digital River's [e-invoicing](../../using-our-services/e-invoicing.md) agreement.&#x20;
* `warrantyInformation`: An explanation of warranty information, applicable for residents of Italy.&#x20;
{% endtab %}
{% endtabs %}

#### <mark style="background-color:orange;">`Error`</mark>

If [`language`](digitalriver-object.md#language), [`country`](digitalriver-object.md#country), or [`businessEntityCode`](digitalriver-object.md#businessentitycode) are not defined or are assigned an unsupported value, then [`Compliance.getDetails()`](digitalriver-object.md#compliance.getdetails) returns a console error.

```
Uncaught Error: businessEntityCode is missing or unsupported, country is missing or unsupported, language is missing or unsupported
```
