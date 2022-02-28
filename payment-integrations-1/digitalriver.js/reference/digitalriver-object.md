---
description: Learn how to use the DigitalRiver object.
---

# DigitalRiver object

## Creating an instance of Drop-in

### digitalriver.createDropin(configurationObject);

Use `createDropin` to create an instance of our Drop-in solution. This solution provides an all-in-one solution for accepting payments and ensuring compliance. Use this solution for a quick way to start accepting payments with little to no customization. For more information, see our page on [Drop-in](../../drop-in/).

## Creating Elements

### digitalriver.createElement();

Use this method to create an instance of an element that you can use to capture payment details. You can use the following Elements in conjunction with `createSource` to create a payment source.

| Element Type   | Description                               |
| -------------- | ----------------------------------------- |
| applepay       | Apple Pay                                 |
| cardCVV        | A card security code field                |
| cardExpiration | A credit card expiration field            |
| cardNumber     | A credit card number field                |
| googlepay      | Google Pay                                |
| konbini        | A Konbini select                          |
| onlineBanking  | An online banking select                  |
| offlineRefund  | An offline refund data collection element |
| paypal         | A PayPal element                          |

{% tabs %}
{% tab title="Example" %}
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
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="JavaScript" %}
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
{% endtab %}
{% endtabs %}

#### **Options**

| **Heading** | State      | Default Class         |
| ----------- | ---------- | --------------------- |
| classes     | base       | DRElement             |
| classes     | complete   | DRElement--complete   |
| classes     | empty      | DRElement--empty      |
| classes     | focus      | DRElement--focus      |
| classes     | invalid    | DRElement--invalid    |
| classes     | autofilled | DRElement--autofilled |

### digitalriver.Compliance.getDetails(businessEntityCode \[, locale]);

Use this method to retrieve localized strings that can be used to create the various disclosures required by Digital River.

| Parameter          | Required/Optional | Description                                                                                                                                                                                                                                                                                   | Accepted Values                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| ------------------ | ----------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| businessEntityCode | Required          | The business entity code of the entity facilitating the transaction.                                                                                                                                                                                                                          | DRES\_INC-ENTITY, DR\_WP-ENTITY, DR\_WPAB-ENTITY, C5\_INC-ENTITY, DR\_BRAZIL-ENTITY, DR\_BRAZIL2-ENTITY, DR\_CHINA-ENTITY, DR\_GMBH-ENTITY, DR\_INC-ENTITY, DR\_INDIA-ENTITY, DR\_IRELAND-ENTITY, DR\_JAPAN-ENTITY, DR\_KOREA-ENTITY, DR\_MEXICO-ENTITY, DR\_RUSSIA-ENTITY, DR\_TAIWAN-ENTITY, DR\_SARL-ENTITY, DR\_UK-ENTITY                                                                                                                                  |
| locale             | Optional          | The language associated with the returned data. If you do not provide a locale and you provided a default locale when you started the DigitalRiver.js library, the strings will be localized to that default value. If you did not provide a default locale, the default language is English. | ar-EG, cs-CZ, da-DK, de-AT, de-CH, de-DE, el-GR, en-AU, en-BE, en-CA, en-CH, en-DK, en-FI, en-GB, en-IE, en-IN, en-MY, en-NL, en-NO, en-NZ, en-PR, en-SE, en-SG, en-US, en-ZA, es-AR, es-CL, es-CO, es-EC, es-ES, es-MX, es-PE, es-VE, et-EE, fi-FI, fr-BE, fr-CA, fr-CH, fr-FR, hu-HU, it-CH, it-IT, iw-IL, ja-JP, ko-KR, lt-LT, lv-LV, nl-BE, nl-NL, no-NO, pl-PL, pt-BR, pt-PT, ro-RO, ru-RU, sk-SK, sl-SI, sr-YU, sv-SE, th-TH, tr-TR, zh-CN, zh-HK, zh-TW |

This method returns an object with various compliance strings and links that can be used to create a legal footer with various resources.

{% tabs %}
{% tab title="Example" %}
```javascript
{
    "disclosure": {
        "businessEntity": {
            "name": "Digital River Inc.",
            "id": "DR_INC-ENTITY"
        },
        "resellerDisclosure": {
            "localizedText": "<a href=\"https://store.digitalriver.com/store/defaults/en_US/DisplayDRAboutDigitalRiverPage/eCommerceProvider.Digital%20River%20Inc.\" target=\"_blank\" class=\"dr_resellerDisclosure\">Digital River Inc.</a> is the authorized reseller and merchant of the products and services offered within this store.",
            "url": "https://store.digitalriver.com/store/defaults/en_US/DisplayDRAboutDigitalRiverPage/eCommerceProvider.Digital%20River%20Inc."
        },
        "termsOfSale": {
            "localizedText": "Terms of Sale",
            "url": "https://store.digitalriver.com/store/defaults/en_US/DisplayDRTermsAndConditionsPage/eCommerceProvider.Digital%20River%20Inc."
        },
        "privacyPolicy": {
            "localizedText": "Privacy Policy",
            "url": "https://store.digitalriver.com/store/defaults/en_US/DisplayDRPrivacyPolicyPage/eCommerceProvider.Digital%20River%20Inc."
        },
        "cookiePolicy": {
            "localizedText": "Cookies",
            "url": "https://store.digitalriver.com/store/defaults/en_US/DisplayDRCookiesPolicyPage/eCommerceProvider.Digital%20River%20Inc."
        },
        "cancellationRights": {
            "localizedText": "Cancellation Right",
            "url": "https://store.digitalriver.com/store/defaults/en_US/DisplayDRTermsAndConditionsPage/eCommerceProvider.Digital%20River%20Inc.#cancellationRight"
        },
        "legalNotice": {
            "localizedText": "Legal Notice",
            "url": "https://store.digitalriver.com/store/defaults/en_US/DisplayDRContactInformationPage/eCommerceProvider.Digital%20River%20Inc."
        },
        "confirmDisclosure": {
            "localizedText": "By submitting my order, I agree to the <a href=\"https://store.digitalriver.com/store/defaults/en_US/DisplayDRTermsAndConditionsPage/eCommerceProvider.Digital%20River%20Inc.\" target=\"_blank\" class=\"dr_termsAndConditions\">Terms of Sale</a> and the <a href=\"https://store.digitalriver.com/store/defaults/en_US/DisplayDRPrivacyPolicyPage/eCommerceProvider.Digital%20River%20Inc.\" target=\"_blank\" class=\"dr_privacyPolicy\">Privacy Policy</a> of Digital River Inc.."
        },
        "autorenewalPlanTerms": {
            "localizedText": "By checking the box below and completing your purchase, you expressly authorize and permit Digital River to automatically renew your purchased license or subscription for successive renewal terms each equal in length to the initial term specified above, at the purchase price for your initial term (plus taxes and fees, less any applicable discounts) using the payment information you provided for your initial purchase, until you cancel. At least one email will be sent to you to remind you of each upcoming renewal. We may change the renewal price as of the next renewal date if we provide you with prior notice of the change by email (you can elect to cancel automatic renewal as described below if you do not agree to the change). The Digital River <a href=\"https://store.digitalriver.com/store/defaults/en_US/DisplayDRTermsAndConditionsPage/eCommerceProvider.Digital%20River%20Inc.\" target=\"_blank\" class=\"dr_termsAndConditions\">Terms of Sale</a> and <a href=\"https://store.digitalriver.com/store/defaults/en_US/DisplayDRPrivacyPolicyPage/eCommerceProvider.Digital%20River%20Inc.\" target=\"_blank\" class=\"dr_privacyPolicy\">Privacy Policy</a> will apply to each renewal transaction. You may cancel your auto-renewal plan at any time by logging into the account interface (access information will be included in your order confirmation email or on the Customer Service Help page), selecting your product, and selecting the option to disable automatic renewal.<br/><br/>I agree that Digital River may store my payment information for future purchases including the processing of any subsequent subscription renewals which may occur following the date of this order."
        },
        "saveCardMandate": {
            "localizedText": "Yes, please save this account and payment information for future purchases."
        },
        "californiaPrivacyRights": {
            "localizedText": "Your California Privacy Rights",
            "url": "https://store.digitalriver.com/store/defaults/en_US/DisplayCCPAPage"
        }
    }
}
```
{% endtab %}
{% endtabs %}

| Attribute                 | Description                                                                                                                                                                      |
| ------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `businessEntity`          | Details about the business entity.                                                                                                                                               |
| `resellerDisclosure`      | Digital River reseller statement and links.                                                                                                                                      |
| `termsOfSale`             | Localized Terms of Sale and a link to the Digital River terms and conditions page.                                                                                               |
| `privacyPolicy`           | Localized Privacy Policy and a link to the Digital River privacy policy page.                                                                                                    |
| `cookiePolicy`            | Localized Cookie Policy and a link to the Digital River cookie policy page.                                                                                                      |
| `cancellationRights`      | Localized Cancellation Rights and a link to the Digital River page explaining the shopper's cancellation rights.                                                                 |
| `legalNotice`             | Localized Legal Notice and a link to the Digital River page with our legal notice details.                                                                                       |
| `confirmDisclosure`       | A localized string with our confirmation disclosure statement. This should be placed next to your confirm order button.                                                          |
| `autorenewalPlanTerms`    | Localized Autorenewal Plan Terms and a link to the Digital River page with our Terms of Sale.                                                                                    |
| `saveCardMandate`         | The save payment agreement for future purchases                                                                                                                                  |
| `californiaPrivacyRights` | California Privacy Rights identifier in English and a link to the Digital River page explaining the shopper's rights in California. This is only applicable to the en-US locale. |
| `warrantyInformation`     | Warranty Information in Italian and a link to the Digital River page explaining warranty information to residents of Italy. This is only applicable to the it-IT locale.         |

## Creating sources

When creating sources, you have the option of selecting a [method that accepts an element](digitalriver-object.md#createsource-element-sourcedata) or using a [method that doesn't require an element](digitalriver-object.md#createsource-sourcedata). Both methods however require that you provide source data to tokenize. When configuring this data, you can also [specify a future use](digitalriver-object.md#specifying-a-sources-future-use) for the source.&#x20;

For both versions, the `createSource()` method returns a promise that contains a `Result` object.  The `Result` object, in turn, contains one of two possible objects:‌

* **source** — A `Source` object created by Digital River.
* **error** — An [error object](error-types-codes-and-objects.md#create-source-error-object) that indicates a problem with the tokenization request. It provides the data you must correct before attempting to create a source again.&#x20;

### createSource(sourceData);

Use the `createSource(sourceData)` method to create a payment source that contains information you can safely use with other Digital River APIs. This includes immediate sources (if PCI compliant), redirect sources, or delayed sources. See [Payment methods](../payment-methods/) for more information on the structure of these requests.‌

In the following example, the method takes a single argument. The `sourceData` contains the data that you want Digital River to tokenize.

{% tabs %}
{% tab title="Example" %}
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
{% endtab %}
{% endtabs %}

A successful response returns a `source` with a unique `id`.

{% tabs %}
{% tab title="Source response" %}
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
{% endtab %}
{% endtabs %}

An unsuccessful response returns an `error` with information on what needs to be corrected.

{% tabs %}
{% tab title="Error response" %}
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
{% endtab %}
{% endtabs %}

### createSource(element, sourceData);

Use the `createSource(element, sourceData)` method to create a tokenized source that you can safely transmit to the backend for use in downstream API calls. This method requests two parameters:‌

* **element** — A `Element` object created using the [Elements](elements.md) portion of this library.
* **sourceData** — The source data that you want Digital River to tokenize. See [Common payment sources](../payment-methods/common-payment-sources.md) for more information on the required source data.

In the following example, the method takes both a source data and element argument.

{% tabs %}
{% tab title="Example" %}
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
{% endtab %}
{% endtabs %}

A successful response returns a `source` with a unique `id`.

{% tabs %}
{% tab title="Source response" %}
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
{% endtab %}
{% endtabs %}

An unsuccessful response returns an `error` with information on what needs to be corrected.

{% tabs %}
{% tab title="Error response" %}
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
{% endtab %}
{% endtabs %}

### Specifying a source's future use

When creating a source using DigitalRiver.js, you should identify the types of transactions it will likely be used for in the future. This increases the probability that these future transactions will be approved. The `usage` value you select should be the one that mostly closely corresponds to your business model. The available options are [subscription](digitalriver-object.md#subscription), [convenience](digitalriver-object.md#convenience), and [unscheduled](digitalriver-object.md#unscheduled).

#### Subscription

Set `usage` to `subscription` when you create sources that are used primarily for recurring transactions, made at regular intervals for a product or a service.

#### **Convenience**

The `convenience` setting applies mainly to saved payment sources that are used for one-off transactions. These are sources where customers are typically present during the checkout flow and want to quickly access their payment information. Select this option if you don't offer [subscriptions](digitalriver-object.md#subscription) or don't have [unscheduled](digitalriver-object.md#unscheduled) merchant initiated transactions

#### Unscheduled

Set `usage` to `unscheduled` when you create sources for unscheduled merchant initiated transactions. These are contracts that occur on a non-fixed schedule using stored card information. Automatic top-ups are an example of one such transaction. They occur whenever a customer's balance drops below a pre-defined amount.

## Retrieving sources

### digitalriver.retrieveSource(sourceId, sourceClientSecret);

Use this method to retrieve a source with the front-end DigitalRiver.js library. This method takes two parameters:‌

* **sourceId**—The unique ID of the source you want to retrieve.
* **sourceClientSecret**—The `clientSecret` value of the source you are trying to retrieve. This is specific to the source.

The `digitalriver.createSource()` returns a Promise that includes a `Result` object. (See the following source response example.) The Result object will have either:‌

* **result.source**—If this object is not null, it will contain the `Source` object you requested.
* **result.error**— If this object is not null, it will contain an `Error` object with details on the specific error.

{% tabs %}
{% tab title="Example" %}
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
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Source response" %}
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
{% endtab %}
{% endtabs %}

## Authenticating sources

The authenticate source method determines whether the saved payment source selected by a customer during the checkout process requires [Strong Customer Authentication](../../psd2-and-sca/) (SCA).

You can use this method when [building workflows](../../building-your-workflows.md) that allow customers to retrieve saved payment information during [one-off purchases](../../building-your-workflows.md#customer-selects-saved-credit-card-during-checkout) and [subscription acquisitions](../../building-your-workflows.md#customer-saves-credit-card-details-during-subscription-acquisition-checkout). &#x20;

The [standard version of the method](digitalriver-object.md#DigitalRiverJS-digitalriver.authenticateSource\(data\);) accepts a configuration object that contains the data we need to authenticate the source.&#x20;

| Parameter            | Required/Optional | Description                                                                                                                                 |
| -------------------- | ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| `sessionId`          | Required          | The [payment session](../../payment-sessions.md) identifier of this transaction.                                                            |
| `sourceId`           | Required          | The identifier of the payment source used in this transaction.                                                                              |
| `sourceClientSecret` | Required          | The source client secret for this transaction.                                                                                              |
| `returnUrl`          | Required          | The return URL where the customer is directed when 3D Secure 1 is required. If the value is not provided, we use the current page location. |

{% hint style="danger" %}
Do not log, embed in URLs, or expose the `sourceClientSecret` to anyone other than the customer. On any page that includes the secret, ensure that [TLS](https://en.wikipedia.org/wiki/Transport\_Layer\_Security) is enabled.
{% endhint %}

The [other version of the authenticate source method](digitalriver-object.md#DigitalRiverJS-digitalriver.authenticateSource\(data\);-1) accepts this same data plus an optional CVV [Element](elements.md) type.

After you call either version of this method, Digital River automatically handles the SCA requirements. Once the customer completes the necessary authentication or we determine that authentication isn't required, the method resolves and the checkout flow can continue.

More specifically, the method returns a promise which is resolved by a source authentication result object. The following are the possible results and the recommended actions:

| `status`                      | Description                                                                                                                                              |
| ----------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `complete`                    | The customer successfully completed the steps necessary to authenticate the source. You can now submit the order.                                        |
| `authentication_not_required` | Digital River determined that the payment source didn't require authentication for this particular payment session. You can now submit the order.        |
| `failed`                      | Source authentication failed. The source can still be used in the transaction but may be declined. You should attempt to authenticate the source again.  |

### authenticateSource(data) <a href="#digitalriverjs-digitalriver.authenticatesource-data" id="digitalriverjs-digitalriver.authenticatesource-data"></a>

You can use this method to [authenticate a payment source](digitalriver-object.md#authenticating-sources) before it is applied to a transaction.&#x20;

```javascript
digitalriver.authenticateSource({
    "sessionId": "65b1e2c2-632c-4240-8897-195ca22ce108",
    "sourceId": "ee90c07c-5549-4a6b-aa5f-aabe29b1e97a",
    "sourceClientSecret": "ee90c07c-5549-4a6b-aa5f-aabe29b1e97a_51afe818-0e7f-46d7-8257-b209b20f4d8",
    "returnUrl": "https://returnurl.com"
});
```

The following is an example response when a source is successfully authenticated:&#x20;

```javascript
{
    "status": "complete"
}
```

### authenticateSource(\[cvvElement], data) <a href="#digitalriverjs-digitalriver.authenticatesource-data" id="digitalriverjs-digitalriver.authenticatesource-data"></a>

In this alternative version of the method to [authenticate sources](digitalriver-object.md#authenticating-sources), you can provide an optional CVV [Element](elements.md) type (assuming it is correctly [created](digitalriver-object.md#creating-elements) and [mounted](elements.md#element-mount)). By setting this parameter, the value contained in the field of the CVV Element is included in the authentication request.

```javascript
digitalriver.authenticateSource(cvvElement, {
    "sessionId": "65b1e2c2-632c-4240-8897-195ca22ce108",
    "sourceId": "ee90c07c-5549-4a6b-aa5f-aabe29b1e97a",
    "sourceClientSecret": "ee90c07c-5549-4a6b-aa5f-aabe29b1e97a_51afe818-0e7f-46d7-8257-b209b20f4d8",
    "returnUrl": "https://returnurl.com"
});
```

The following is an example response when a source is successfully authenticated:&#x20;

```javascript
{
    "status": "complete"
}
```

## **Updating sources**

### **digitalriver.updateSource(\[element,] sourceData);**

Use this method to update details on a source.&#x20;

{% hint style="warning" %}
When updating a source, you can update the owner and the expiration details for [Credit Cards](broken-reference) only.  If you need to update a non-Credit Card (**creditCard**) payment type,  use [createSource](digitalriver-object.md#createsource-sourcedata).
{% endhint %}

This method takes two parameters:‌

* `element`—An optional card expiration element for using the Elements portion of this library.
* `sourceData`—A required data object which contains additional data that is required to update the payment source.

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
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Source Response" %}
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
{% endtab %}
{% endtabs %}

#### **Updating only address information**

{% tabs %}
{% tab title="Example" %}
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
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Source Response" %}
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
{% endtab %}
{% endtabs %}

#### **Updating only card expiration information**

{% tabs %}
{% tab title="Example" %}
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
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Source Response" %}
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
{% endtab %}
{% endtabs %}

#### **Update error**‌

If there is a problem with the update request, an error object will be returned in the response.

{% tabs %}
{% tab title="Source Errors" %}
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
{% endtab %}
{% endtabs %}

## Retrieving available payment methods

### digitalriver.retrieveAvailablePaymentMethods(\[filters]);

Use this method to retrieve an array of available payment methods. You can use this to filter and determine applicable payment methods while building your checkout flows. The `filters` object is optional.

| Attribute         | Required/Optional | Description                                                                                                    |
| ----------------- | ----------------- | -------------------------------------------------------------------------------------------------------------- |
| currency          | Optional          | The currency of the transaction.                                                                               |
| country           | Optional          | The country of the billing addresses associated with this transaction.                                         |
| supportsStorage   | Optional          | Whether the payment supports storage.                                                                          |
| supportsRecurring | Optional          | Whether the payment method supports recurring payments.                                                        |
| supportsFreeTrial | Optional          | Whether the payment method supports free trials.                                                               |
| sessionId         | Optional          | The Payment Session ID. If used, the response will return the payment methods which apply to your transaction. |

&#x20;**Retrieve available payment methods response without using session ID**

The following example shows a request with no filters applied.

{% tabs %}
{% tab title="Request Example" %}
```javascript
digitalriver.retrieveAvailablePaymentMethods().then(function(result) {
    //do something with the result, this could include showing or hiding specific payment methods that are applicable to the display
});
```
{% endtab %}
{% endtabs %}

The following response includes all payment methods that you configured for your account.

{% tabs %}
{% tab title="Response Example" %}
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
            "type": "bPay",
            "flow": "receiver",
            "supportsRecurring": false,
            "supportsFreeTrial": false,
            "images": {
                "iconImage": "https://ui1.img.digitalrivercontent.net/Storefront/images/paymentMethodLogos/bpay.png"
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
{% endtab %}
{% endtabs %}

#### Retrieve available payment methods response using filters <a href="#digitalriverjs-retrieveavailablepaymentmethodsresponsewithusingfilters" id="digitalriverjs-retrieveavailablepaymentmethodsresponsewithusingfilters"></a>

The following example shows a request using filters.

{% tabs %}
{% tab title="Request Example" %}
```javascript
digitalriver.retrieveAvailablePaymentMethods({
    "currency": "USD",
    "country": "US",
    "supportsRecurring": true
}).then(function(result) {
    //do something with the result, this could include showing or hiding specific payment methods that are applicable to the display
});
```
{% endtab %}
{% endtabs %}

The following response only returns payment methods that are available in the US, use the USD currency, and supports recurring payment. &#x20;

{% tabs %}
{% tab title="Response example" %}
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
{% endtab %}
{% endtabs %}

#### Retrieve available payment methods response with a Session ID  <a href="#digitalriverjs-retrieveavailablepaymentmethodsresponsewithasessionidspecified" id="digitalriverjs-retrieveavailablepaymentmethodsresponsewithasessionidspecified"></a>

If you specify a Payment Session ID, you will only receive the payment methods which apply to your transaction.

{% tabs %}
{% tab title="Request Example" %}
```javascript
digitalriver.retrieveAvailablePaymentMethods({
    "sessionId": "d3941a36-6821-4d93-be23-6190226ae5f7"
}).then(function(result) {
    //do something with the result, this could include showing or hiding specific payment methods that are applicable to the display
});
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Response Example" %}
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
{% endtab %}
{% endtabs %}

### Credit card logos

If you want to display the credit card payment logo on your website, you can use the following URLs to add the appropriate brand logo image to your website:

{% hint style="info" %}
**Best Practices**: To ensure you're always using the latest logo, link to the URL instead of downloading the image to your website.
{% endhint %}

* **Visa** ![](broken-reference) \
  **URL**: [https://ui1.img.digitalrivercontent.net/Storefront/images/creditCardLogos/visa.png](https://ui1.img.digitalrivercontent.net/Storefront/images/creditCardLogos/visa.png)
* **Mastercard** ![](broken-reference) \
  **URL**: [https://ui1.img.digitalrivercontent.net/Storefront/images/creditCardLogos/mastercard.png](https://ui1.img.digitalrivercontent.net/Storefront/images/creditCardLogos/mastercard.png)
* **American Express** ![](broken-reference) \
  **URL**: [https://ui1.img.digitalrivercontent.net/Storefront/images/creditCardLogos/amex.png](https://ui1.img.digitalrivercontent.net/Storefront/images/creditCardLogos/amex.png)
* **Discover** ![](broken-reference)  \
  **URL**: [https://ui1.img.digitalrivercontent.net/Storefront/images/creditCardLogos/discover.png](https://ui1.img.digitalrivercontent.net/Storefront/images/creditCardLogos/discover.png)
* **JCB** ![](broken-reference) \
  **URL**: [https://ui1.img.digitalrivercontent.net/Storefront/images/creditCardLogos/jcb.png](https://ui1.img.digitalrivercontent.net/Storefront/images/creditCardLogos/jcb.png)
* **Maestro** ![](broken-reference) \
  **URL**: [https://ui1.img.digitalrivercontent.net/Storefront/images/creditCardLogos/maestro.png](https://ui1.img.digitalrivercontent.net/Storefront/images/creditCardLogos/maestro.png)
* **UnionPay** ![](broken-reference) \
  **URL**: [https://ui1.img.digitalrivercontent.net/Storefront/images/creditCardLogos/unionpay.png](https://ui1.img.digitalrivercontent.net/Storefront/images/creditCardLogos/unionpay.png)

## Retrieving available banks for Online Banking

### digitalriver.retrieveOnlineBankingBanks(countryCode, currency);

Use this method to retrieve an array of available banks for a combination of [ISO 3166-1 alpha-2](https://en.wikipedia.org/wiki/ISO\_3166-1\_alpha-2) country code and [ISO 4217](https://en.wikipedia.org/wiki/ISO\_4217) currency code.‌

This method returns an array that will either be empty if no banks are available or will contain objects with Issuer IDs and Bank Names. DigitalRiver.js uses this data when creating an Online Banking source. This method is useful if you would like to build a bank selector yourself instead of using the Online Banking element.

{% tabs %}
{% tab title="Example" %}
```javascript
digitalriver.retrieveOnlineBankingBanks("DE","EUR").then(function(result) {
    //do something with the banks, this could include building a selector or something else
});
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Source response" %}
```javascript
[{
    "bankCode": "86",
    "bankName": "Sofortüberweisung"
}, {
    "bankCode": "21",
    "bankName": "Giropay"
}]
```
{% endtab %}
{% endtabs %}

###
