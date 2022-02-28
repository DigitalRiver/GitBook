---
description: Learn the basics of payment sessions and how to migrate your integration.
---

# Payment sessions

A payment session tracks a customer's order and payment throughout the checkout flow. Although you're not required to, we highly [recommend you use payment sessions](payment-sessions.md#why-use-payment-sessions) to reduce the complexity of building DigitalRiver.js payment collection flows and to [comply with PSD2 and Strong Customer Authentication (SCA)](https://info.digitalriver.com/rs/348-QUY-258/images/Digital\_River\_Guide\_to\_PSD2\_Compliance\_2020.pdf) regulations.&#x20;

[Migrating to payment sessions](payment-sessions.md#migrating-to-payment-sessions) is relatively straightforward and mostly involves [updating the code](payment-sessions.md#update-your-code) for each of your approved payment methods.

## Why use payment sessions?

Payment sessions allow you to [comply with PSD2 and SCA regulations](https://info.digitalriver.com/rs/348-QUY-258/images/Digital\_River\_Guide\_to\_PSD2\_Compliance\_2020.pdf). When using payment sessions to [create credit card sources](payment-sessions.md#credit-card), applicable PSD2 transactions automatically collect the required authentication data from the customer.

Payment sessions also simplify source creation by reducing the data you're required to provide. If you don't use payment sessions, you'll need to copy data returned in the response and ensure it is properly formatted before passing it to the [create source method](digitalriver.js/reference/digitalriver-object.md#digitalriver-createsource-element-sourcedata). &#x20;

When [creating a source with payment sessions](payment-sessions.md#creating-a-source-with-payment-sessions), however, you can provide the unique identifier of the session, thereby minimizing the data you must transfer.&#x20;

They also allow you to [gain access to Drop-in](drop-in/drop-in-integration-guide.md), which lessens your front-end development burden. For each transaction, Drop-in needs to [retrieve the available payment methods](payment-sessions.md#retrieving-available-payment-methods), and the payment session flow supports this functionality.

## Creating a source with payment sessions

When creating a source, specify the `sessionId` in the payload that you pass to the DigitalRiver.js [create source method](digitalriver.js/reference/digitalriver-object.md#creating-sources). Alternatively, if you're using the recommended [Drop-in solution](drop-in/), you set the payment session identifier in the [configuration object](drop-in/drop-in-integration-guide.md#step-5-configure-hydrate) that you pass to the [create Drop-in method](drop-in/drop-in-integration-guide.md#step-6-allow-the-shopper-to-interact-with-hydrate).

In both cases, the details required to create the source are retrieved from the payment session. We then return a source object to you.&#x20;

{% tabs %}
{% tab title="JavaScript" %}
```javascript
let payload = {
    "sessionId": "ea03bf6f-84ef-4993-b1e7-b7d5ecf71d1f",
    "type": "payPal",
    "payPal": {
        "returnUrl": "https://yourReturnUrl.com",
        "cancelUrl": "https://yourCancelUrl.com"
    }
}
 
digitalriver.createSource(payload).then(function(result) {
     
    if(result.state === "chargeable") {
        sendToBackEnd(result);
    } else {
        doErrorScenario();
    }
});
```
{% endtab %}
{% endtabs %}

## Retrieving available payment methods

With the `retrieveAvailablePaymentMethods` in DigitalRiver.js, payment sessions allow you to [return the payment methods available for each transaction](digitalriver.js/reference/digitalriver-object.md#retrieving-available-payment-methods). You can then display these to the customer during the checkout process.

The method also returns the data required to use one-click payment methods like Apple Pay and Google Pay, as well as the data needed to retrieve compliance information via the DigitalRiver.js [compliance methods](digitalriver.js/reference/digitalriver-object.md#digitalriver-compliance-getdetails-businessentitycode-locale).&#x20;

{% tabs %}
{% tab title="JavaScript" %}
```javascript
digitalriver.retrieveAvailablePaymentMethods({
    "sessionId": "ea03bf6f-84ef-4993-b1e7-b7d5ecf71d1f"
}).then(function(result) {
    //do something with the data
});
```
{% endtab %}
{% endtabs %}

## Migrating to payment sessions

Although we generally recommend that you use [Drop-in](drop-in/) to integrate payments, you can also migrate your existing integration directly to payment sessions.&#x20;

Once you have completed this migration process, you'll need to [build your SCA workflows](building-your-workflows.md) using Drop-in or [Elements](digitalriver.js/reference/elements.md).&#x20;

### Enable payment sessions

To enable payment sessions for the Commerce API, you'll need to contact your Account Manager. Once enabled, you'll see the following hash table returned in your Cart responses:

{% tabs %}
{% tab title="JSON" %}
```javascript
{
    ...
    "paymentSession": {
        "id": "8af78166-e526-40bd-9c95-1071d161a94a",
        "clientSecret": "8af78166-e526-40bd-9c95-1071d161a94a_4179e432-b714-4451-9137-ac08a1d9af19",
        "status": "requires_source"
    }
    ...
}
```
{% endtab %}
{% endtabs %}

### Update your code

You'll need to update your code to fully integrate with payment sessions. For each payment method supported by DigitalRiver.js, add the `sessionId` parameter to the payload that you pass to the `createSource` method.&#x20;

The parameters to remove are specific to each payment method. These parameters, along with example code, are listed in the following sections: [Credit Card](payment-sessions.md#credit-card), [PayPal](payment-sessions.md#paypal), [PayPal Billing](payment-sessions.md#paypal-billing), [PayPal Credit](payment-sessions.md#paypal-credit), [SEPA Direct Debit](digitalriver.js/payment-methods/direct-debit.md), [Wire Transfer](payment-sessions.md#wire-transfer), [Cash on Delivery - Japan](payment-sessions.md#cash-on-delivery-japan), [Payco - Korea Payments](payment-sessions.md#payco-korea-payments), [Bank Transfer - Korea Payments](payment-sessions.md#bank-transfer-korea-payments), [Online Banking - IBP](payment-sessions.md#online-banking-ibp), [bPay](payment-sessions.md#bpay), [Konbini](payment-sessions.md#konbini), [Klarna](payment-sessions.md#klarna), [Klarna Recurring](payment-sessions.md#klarna-recurring), [TreviPay](digitalriver.js/payment-methods/trevipay.md).

#### Credit Card

For credit cards, you add `sessionId` to the payload but do not remove any existing parameters.&#x20;

The following tabs provide code examples of how sources are created without and with payment sessions.

{% tabs %}
{% tab title="Without payment sessions" %}
```javascript
var payload = {
    "type": "creditCard",
    "owner": {
        firstName: "John",
        lastName: "Doe",
        email: "john.doe@digitalriver.com",
        phoneNumber: "000-000-0000",
        address: {
            line1: "10380 Bren Road West",
            line2: "Suite 123",
            city: "Minnetonka",
            state: "MN",
            postalCode: "55343",
            country: "US"
        }
    }
}
 
digitalriver.createSource(cardCVV, payload).then(function(result) {
    if (result.error) {
        //handle errors
    } else {
        var source = result.source;
        //send source to back end
        sendToBackend(source);
    }
});
```
{% endtab %}

{% tab title="With payment sessions" %}
```javascript
var payload = {
    "sessionId": "ea03bf6f-84ef-4993-b1e7-b7d5ecf71d1f",
    "type": "creditCard",
    "owner": {
        firstName: "John",
        lastName: "Doe",
        email: "john.doe@digitalriver.com",
        phoneNumber: "000-000-0000",
        address: {
            line1: "10380 Bren Road West",
            line2: "Suite 123",
            city: "Minnetonka",
            state: "MN",
            postalCode: "55343",
            country: "US"
        }
    }
}
 
digitalriver.createSource(cardCVV, payload).then(function(result) {
    if (result.error) {
        //handle errors
    } else {
        var source = result.source;
        //send source to back end
        sendToBackend(source);
    }
});
```
{% endtab %}
{% endtabs %}

#### PayPal

For PayPal, you add `sessionId` to the payload and remove `amount`,  `currency`, `payPal.items`, `payPal.taxAmount`, `payPal.shippingAmount`, `payPal.amountsEstimated`, `payPal.requestShipping`, and `payPal.shipping`.

The following tabs provide code examples of how sources are created without and with payment sessions.

{% tabs %}
{% tab title="Without payment sessions" %}
```javascript
var payload = {
    "type": "payPal",
    "amount": 120.99,
    "currency": "USD",
    "payPal": {
        "returnUrl": "http://mypage.com",
        "cancelUrl": "https://mypage.com/cancel",
        "items": [{
                "name": "Cell Phone (Unlocked)",
                "quantity": 1,
                "unitAmount": 100
            },
            {
                "name": "Headphones",
                "quantity": 1,
                "unitAmount": 15
            }
        ],
        "taxAmount": 0.99,
        "shippingAmount": 5,
        "amountsEstimated": true,
        "requestShipping": true,
        "shipping": {
            "recipient": "John Doe",
            "phoneNumber": "952-555-1212",
            "address": {
                "line1": "54321 Fake St.",
                "line2": "Apt. 3C",
                "city": "Minnetonka",
                "state": "MN",
                "country": "US",
                "postalCode": "55341"
            }
        }
    }
}
  
  
digitalriver.createSource(payload).then(function(result) {
    if (result.error) {
        //handle errors
    } else {
        var source = result.source;
        //send source to back end
        sendToBackend(source);
    }
});
```
{% endtab %}

{% tab title="With payment sessions" %}
```javascript
var payload = {
    "type": "payPal",
    "sessionId": "ea03bf6f-84ef-4993-b1e7-b7d5ecf71d1f",
    "payPal": {
        "returnUrl": "http://mypage.com",
        "cancelUrl": "https://mypage.com/cancel"
    }
}
  
digitalriver.createSource(payload).then(function(result) {
    if (result.error) {
        //handle errors
    } else {
        var source = result.source;
        //send source to back end
        sendToBackend(source);
    }
});
```
{% endtab %}
{% endtabs %}

#### PayPal Billing

For PayPal Billing, you add `sessionId` to the payload and remove `amount`, `currency`, `payPalBilling.items`, `payPalBilling.taxAmount`, `payPalBilling.shippingAmount`, `payPalBilling.amountsEstimated`, `payPalBilling.requestShipping`, and `payPalBilling.shipping`.

The following tabs provide code examples of how sources are created without and with payment sessions.

{% tabs %}
{% tab title="Without payment sessions" %}
```javascript
var payload = {
    "type": "payPalBilling",
    "amount": 120.99,
    "currency": "USD",
    "payPal": {
        "returnUrl": "http://mypage.com",
        "cancelUrl": "https://mypage.com/cancel",
        "items": [{
                "name": "Cell Phone (Unlocked)",
                "quantity": 1,
                "unitAmount": 100
            },
            {
                "name": "Headphones",
                "quantity": 1,
                "unitAmount": 15
            }
        ],
        "taxAmount": 0.99,
        "shippingAmount": 5,
        "amountsEstimated": true,
        "requestShipping": true,
        "shipping": {
            "recipient": "John Doe",
            "phoneNumber": "952-555-1212",
            "address": {
                "line1": "54321 Fake St.",
                "line2": "Apt. 3C",
                "city": "Minnetonka",
                "state": "MN",
                "country": "US",
                "postalCode": "55341"
            }
        }
    }
}
  
  
digitalriver.createSource(payload).then(function(result) {
    if (result.error) {
        //handle errors
    } else {
        var source = result.source;
        //send source to back end
        sendToBackend(source);
    }
});
```
{% endtab %}

{% tab title="With payment sessions" %}
```javascript
var payload = {
    "type": "payPalBilling",
    "sessionId": "ea03bf6f-84ef-4993-b1e7-b7d5ecf71d1f",
    "payPal": {
        "returnUrl": "http://mypage.com",
        "cancelUrl": "https://mypage.com/cancel"
    }
}
  
digitalriver.createSource(payload).then(function(result) {
    if (result.error) {
        //handle errors
    } else {
        var source = result.source;
        //send source to back end
        sendToBackend(source);
    }
});
```
{% endtab %}
{% endtabs %}

#### PayPal Credit

For PayPal Credit, you add `sessionId` to the payload and remove `amount`,  `currency`, `payPal.items`, `payPal.taxAmount`, `payPal.shippingAmount`, `payPal.amountsEstimated`, `payPal.requestShipping`, and `payPal.shipping`.

The following tabs provide code examples of how sources are created without and with payment sessions.

{% tabs %}
{% tab title="Without payment sessions" %}
```javascript
var payload = {
    "type": "payPalCredit",
    "amount": 120.99,
    "currency": "USD",
    "payPal": {
        "returnUrl": "http://mypage.com",
        "cancelUrl": "https://mypage.com/cancel",
        "items": [{
                "name": "Cell Phone (Unlocked)",
                "quantity": 1,
                "unitAmount": 100
            },
            {
                "name": "Headphones",
                "quantity": 1,
                "unitAmount": 15
            }
        ],
        "taxAmount": 0.99,
        "shippingAmount": 5,
        "amountsEstimated": true,
        "requestShipping": true,
        "shipping": {
            "recipient": "John Doe",
            "phoneNumber": "952-555-1212",
            "address": {
                "line1": "54321 Fake St.",
                "line2": "Apt. 3C",
                "city": "Minnetonka",
                "state": "MN",
                "country": "US",
                "postalCode": "55341"
            }
        }
    }
}
  
  
digitalriver.createSource(payload).then(function(result) {
    if (result.error) {
        //handle errors
    } else {
        var source = result.source;
        //send source to back end
        sendToBackend(source);
    }
});
```
{% endtab %}

{% tab title="With payment sessions" %}
```javascript
var payload = {
    "type": "payPalCredit",
    "sessionId": "ea03bf6f-84ef-4993-b1e7-b7d5ecf71d1f",
    "payPal": {
        "returnUrl": "http://mypage.com",
        "cancelUrl": "https://mypage.com/cancel"
    }
}
  
digitalriver.createSource(payload).then(function(result) {
    if (result.error) {
        //handle errors
    } else {
        var source = result.source;
        //send source to back end
        sendToBackend(source);
    }
});
```
{% endtab %}
{% endtabs %}

#### SEPA Direct Debit

For SEPA Direct Debit, you add `sessionId` to the payload and remove `amount` and `currency`.&#x20;

The following tabs provide code examples of how sources are created without and with payment sessions.

{% tabs %}
{% tab title="Without payment sessions" %}
```javascript
let payload = {
    "type": "directDebit",
    "amount": 100,
    "currency": "EUR",
    "owner": {
        firstName: "John",
        lastName: "Doe",
        email: "test@digitalriver.com",
        phoneNumber: "000-000-0000",
        address: {
            line1: "123 Main Street",
            line2: "",
            city: "Paris",
            postalCode: "14390",
            country: "FR"
        }
    },
    "directDebit": {
        "returnUrl": "https://mypage.com"
    }
}
 
digitalriver.createSource(payload).then(function(result) {
 
    if (result.error) {
        //handle errors
    } else {
        var source = result.source;
        //send source to back end
        sendToBackend(source);
    }
});
```
{% endtab %}

{% tab title="With payment sessions" %}
```javascript
var payload = {
    "type": "directDebit",
    "sessionId": "ea03bf6f-84ef-4993-b1e7-b7d5ecf71d1f",
    "owner": {
        firstName: "John",
        lastName: "Doe",
        email: "test@digitalriver.com",
        phoneNumber: "000-000-0000",
        address: {
            line1: "123 Main Street",
            line2: "",
            city: "Paris",
            postalCode: "14390",
            country: "FR"
        }
    },
    "directDebit": {
        "returnUrl": "https://mypage.com"
    }
}
  
digitalriver.createSource(payload).then(function(result) {
    if (result.error) {
        //handle errors
    } else {
        var source = result.source;
        //send source to back end
        sendToBackend(source);
    }
});
```
{% endtab %}
{% endtabs %}

#### Wire Transfer

For Wire Transfer, you add `sessionId`to the payload and remove `amount` and `currency`.&#x20;

The following tabs provide code examples of how sources are created without and with payment sessions.

{% tabs %}
{% tab title="Without payment sessions" %}
```javascript
let payload = {
    "type": "wireTransfer",
    "amount": 100,
    "currency": "EUR",
    "owner": {
        firstName: "John",
        lastName: "Doe",
        email: "test@digitalriver.com",
        phoneNumber: "000-000-0000",
        address: {
            line1: "123 Main Street",
            line2: "",
            city: "Paris",
            postalCode: "14390",
            country: "FR"
        }
    },
    "wireTransfer": {
    }
}
 
digitalriver.createSource(payload).then(function(result) {
 
    if (result.error) {
        //handle errors
    } else {
        var source = result.source;
        //send source to back end
        sendToBackend(source);
    }
});
```
{% endtab %}

{% tab title="With payment sessions" %}
```javascript
var data = {
    "type": "wireTransfer",
    "sessionId": "ea03bf6f-84ef-4993-b1e7-b7d5ecf71d1f",
    "owner": {
        firstName: "John",
        lastName: "Doe",
        email: "test@digitalriver.com",
        phoneNumber: "000-000-0000",
        address: {
            line1: "123 Main Street",
            line2: "",
            city: "Paris",
            postalCode: "14390",
            country: "FR"
        }
    },
    "wireTransfer": {
    }
}
  
digitalriver.createSource(data).then(function(result) {
    if (result.error) {
        //handle errors
    } else {
        var source = result.source;
        //send source to back end
        sendToBackend(source);
    }
});
```
{% endtab %}
{% endtabs %}

#### Cash on Delivery - Japan

For Cash on Delivery - Japan, you add `sessionId` to the payload and remove `amount`  and `currency`.&#x20;

The following tabs provide code examples of how sources are created without and with payment sessions.

{% tabs %}
{% tab title="Without payment sessions" %}
```javascript
let payload = {
    "type": "codJapan",
    "amount": 100,
    "currency": "EUR",
    "owner": {
        firstName: "John",
        lastName: "Doe",
        email: "test@digitalriver.com",
        phoneNumber: "000-000-0000",
        address: {
            line1: "123 Main Street",
            line2: "",
            city: "Paris",
            postalCode: "14390",
            country: "FR"
        }
    },
    "codJapan": {
    }
}
 
digitalriver.createSource(payload).then(function(result) {
 
    if (result.error) {
        //handle errors
    } else {
        var source = result.source;
        //send source to back end
        sendToBackend(source);
    }
});
```
{% endtab %}

{% tab title="With payment sessions" %}
```javascript
var payload = {
    "type": "codJapan",
    "sessionId": "ea03bf6f-84ef-4993-b1e7-b7d5ecf71d1f",
    "owner": {
        firstName: "John",
        lastName: "Doe",
        email: "test@digitalriver.com",
        phoneNumber: "000-000-0000",
        address: {
            line1: "123 Main Street",
            line2: "",
            city: "Paris",
            postalCode: "14390",
            country: "FR"
        }
    },
    "codJapan": {
    }
}
  
digitalriver.createSource(payload).then(function(result) {
    if (result.error) {
        //handle errors
    } else {
        var source = result.source;
        //send source to back end
        sendToBackend(source);
    }
});
```
{% endtab %}
{% endtabs %}

#### Payco - Korea Payments

For Payco - Korea Payments, you add `sessionId` to the payload and remove `amount`  and `currency`. &#x20;

The following tabs provide code examples of how sources are created without and with payment sessions.

{% tabs %}
{% tab title="Without payment sessions" %}
```javascript
let payload = {
    "type": "payco",
    "amount": 100,
    "currency": "KRW",
    "owner": {
        firstName: "John",
        lastName: "Doe",
        email: "test@digitalriver.com",
        address: {
            line1: "1234 Fake Street",
            line2: "Yaum-dong",
            city: "Ulsan-si",
            state: "Kyongsangnamdo",
            postalCode: "100-011",
            country: "KR"
        }
    },
    "payco": {
        "returnUrl": "https://yourReturnUrl.com"
    }
}
 
digitalriver.createSource(payload).then(function(result) {
 
    if (result.error) {
        //handle errors
    } else {
        var source = result.source;
        //send source to back end
        sendToBackend(source);
    }
});
```
{% endtab %}

{% tab title="With payment sessions" %}
```javascript
var payload = {
    "type": "payco",
    "sessionId": "ea03bf6f-84ef-4993-b1e7-b7d5ecf71d1f",
    "owner": {
        firstName: "John",
        lastName: "Doe",
        email: "test@digitalriver.com",
        address: {
            line1: "1234 Fake Street",
            line2: "Yaum-dong",
            city: "Ulsan-si",
            state: "Kyongsangnamdo",
            postalCode: "100-011",
            country: "KR"
        }
    },
    "payco": {
        "returnUrl": "https://yourReturnUrl.com"
    }
}
  
digitalriver.createSource(payload).then(function(result) {
    if (result.error) {
        //handle errors
    } else {
        var source = result.source;
        //send source to back end
        sendToBackend(source);
    }
});
```
{% endtab %}
{% endtabs %}

#### Bank Transfer - Korea Payments

For Bank Transfer - Korea Payments, you add `sessionId` to the payload and remove `amount`  and `currency`.&#x20;

The following tabs provide code examples of how sources are created without and with payment sessions.

{% tabs %}
{% tab title="Without payment sessions" %}
```javascript
let payload = {
    "type": "bankTransfer",
    "amount": 100,
    "currency": "KRW",
    "owner": {
        firstName: "John",
        lastName: "Doe",
        email: "test@digitalriver.com",
        address: {
            line1: "1234 Fake Street",
            line2: "Yaum-dong",
            city: "Ulsan-si",
            state: "Kyongsangnamdo",
            postalCode: "100-011",
            country: "KR"
        }
    },
    "bankTransfer": {
        "returnUrl": "https://yourReturnUrl.com"
    }
}
 
digitalriver.createSource(payload).then(function(result) {
 
    if (result.error) {
        //handle errors
    } else {
        var source = result.source;
        //send source to back end
        sendToBackend(source);
    }
});
```
{% endtab %}

{% tab title="With payment sessions" %}
```javascript
var payload = {
    "type": "bankTransfer",
    "sessionId": "ea03bf6f-84ef-4993-b1e7-b7d5ecf71d1f",
    "owner": {
        firstName: "John",
        lastName: "Doe",
        email: "test@digitalriver.com",
        address: {
            line1: "1234 Fake Street",
            line2: "Yaum-dong",
            city: "Ulsan-si",
            state: "Kyongsangnamdo",
            postalCode: "100-011",
            country: "KR"
        }
    },
    "bankTransfer": {
        "returnUrl": "https://yourReturnUrl.com"
    }
}
  
digitalriver.createSource(payload).then(function(result) {
    if (result.error) {
        //handle errors
    } else {
        var source = result.source;
        //send source to back end
        sendToBackend(source);
    }
});
```
{% endtab %}
{% endtabs %}

#### Online Banking - IBP

For Online Banking - IBP, you add `sessionId` to the payload and remove  `amount` and `currency`.  &#x20;

The following tabs provide code examples of how sources are created without and with payment sessions.

{% tabs %}
{% tab title="Without payment sessions" %}
```javascript
let payload = {
    "type": "onlineBanking",
    "amount": 100,
    "currency": "EUR",
    "owner": {
        "firstName": "John",
            "lastName": "Doe",
            "email": "john.doe@digitalriver.com",
            "phoneNumber": "000-000-0000",
            "address": {
                "line1": "52-58 Neue Mainzer Straße",
                "line2": "",
                "city": "Frankfurt am Main",
                "state": "HE",
                "postalCode": "60311",
                "country": "DE"
            }
        },
        "onlineBanking": {
            "returnUrl": "https://myurl.com/success",
            "cancelUrl": "https://myurl.com/cancel",
            "bankCode": "82"
        }
}
 
digitalriver.createSource(payload).then(function(result) {
 
    if (result.error) {
        //handle errors
    } else {
        var source = result.source;
        //send source to back end
        sendToBackend(source);
    }
});
```
{% endtab %}

{% tab title="With payment sessions" %}
```javascript
var payload = {
    "type": "onlineBanking",
    "sessionId": "ea03bf6f-84ef-4993-b1e7-b7d5ecf71d1f",
    "owner": {
        "firstName": "John",
            "lastName": "Doe",
            "email": "john.doe@digitalriver.com",
            "phoneNumber": "000-000-0000",
            "address": {
                "line1": "52-58 Neue Mainzer Straße",
                "line2": "",
                "city": "Frankfurt am Main",
                "state": "HE",
                "postalCode": "60311",
                "country": "DE"
            }
        },
        "onlineBanking": {
            "returnUrl": "https://myurl.com/success",
            "cancelUrl": "https://myurl.com/cancel",
            "bankCode": "82"
        }
}
 
  
digitalriver.createSource(payload).then(function(result) {
    if (result.error) {
        //handle errors
    } else {
        var source = result.source;
        //send source to back end
        sendToBackend(source);
    }
});
```
{% endtab %}
{% endtabs %}

#### bPay

For bPay, you add `sessionId` to the payload and remove `amount`  and `currency`. &#x20;

The following tabs provide code examples of how sources are created without and with payment sessions.

{% tabs %}
{% tab title="Without payment sessions" %}
```javascript
let payload = {
    "type": "bPay",
    "amount": 120.99,
    "currency": "AUD",
    "owner": {
        "firstName": "John",
        "lastName": "Doe",
        "email": "john.doe@digitalriver.com",
        "phoneNumber": "000-000-0000",
        "address": {
            "line1": "3 Bridge Lane",
            "line2": "",
            "city": "Sydney",
            "state": "NSW",
            "postalCode": "2000",
            "country": "AU"
        }
    },
    "bPay": {}
}
 
digitalriver.createSource(payload).then(function(result) {
 
    if (result.error) {
        //handle errors
    } else {
        var source = result.source;
        //send source to back end
        sendToBackend(source);
    }
});
```
{% endtab %}

{% tab title="With payment sessions" %}
```javascript
var payload = {
    "type": "bPay",
    "sessionId": "ea03bf6f-84ef-4993-b1e7-b7d5ecf71d1f",
    "owner": {
        "firstName": "John",
        "lastName": "Doe",
        "email": "john.doe@digitalriver.com",
        "phoneNumber": "000-000-0000",
        "address": {
            "line1": "3 Bridge Lane",
            "line2": "",
            "city": "Sydney",
            "state": "NSW",
            "postalCode": "2000",
            "country": "AU"
        }
    },
    "bPay": {}
}
 
  
digitalriver.createSource(payload).then(function(result) {
    if (result.error) {
        //handle errors
    } else {
        var source = result.source;
        //send source to back end
        sendToBackend(source);
    }
});
```
{% endtab %}
{% endtabs %}

#### Konbini

For Konbini, you add `sessionId` to the payload and remove `amount`  and `currency`.

The following tabs provide code examples of how sources are created without and with payment sessions.

{% tabs %}
{% tab title="Without payment sessions" %}
```javascript
let payload = {
    "type": "konbini",
    "amount": 120.99,
     "currency": "JPY",
        "owner": {
            "firstName": "John",
            "lastName": "Doe",
            "email": "john.doe@digitalriver.com",
            "phoneNumber": "000-000-0000",
            "address": {
                "line1": "6 Chome-10-1 Roppongi, Minato",
                "state": "Tokyo",
                "postalCode": "106-0032",
                "country": "JP"
            }
        },
        "konbini": {
            "storeId": "010"
        }
}
 
digitalriver.createSource(payload).then(function(result) {
 
    if (result.error) {
        //handle errors
    } else {
        var source = result.source;
        //send source to back end
        sendToBackend(source);
    }
});
```
{% endtab %}

{% tab title="With payment sessions" %}
```javascript
var payload = {
    "type": "konbini",
    "sessionId": "ea03bf6f-84ef-4993-b1e7-b7d5ecf71d1f",
    "owner": {
         "firstName": "John",
            "lastName": "Doe",
            "email": "john.doe@digitalriver.com",
            "phoneNumber": "000-000-0000",
            "address": {
                "line1": "6 Chome-10-1 Roppongi, Minato",
                "state": "Tokyo",
                "postalCode": "106-0032",
                "country": "JP"
            }
        },
        "konbini": {
            "storeId": "010"
        }
}
 
  
digitalriver.createSource(payload).then(function(result) {
    if (result.error) {
        //handle errors
    } else {
        var source = result.source;
        //send source to back end
        sendToBackend(source);
    }
});
```
{% endtab %}
{% endtabs %}

#### Klarna

For Klarna, you add `sessionId` to the payload and remove `amount`, `currency`, `klarnaCredit.items`, `klarnaCredit.locale`, `klarnaCredit.discountAmount`, `klarnaCredit.taxAmount`,  `klarnaCredit.shippingAmount`, `klarnaCredit.shipping`, `klarnaCredit.accountId`, `klarnaCredit.accountCreatedDate`, `klarnaCredit.accountUpdatedDate`, `klarnaCredit.hasPaidBefore`, `klarnaCredit.subscriptionDescription`, `klarnaCredit.subscriptionStartDate`, `klarnaCredit.subscriptionEndDate`, `klarnaCredit.autoRenewal`, and `klarnaCredit.affiliateName`. &#x20;

The following tabs provide code examples of how sources are created without and with payment sessions.

{% tabs %}
{% tab title="Without payment sessions" %}
```javascript
let payload = {
    "type": "klarnaCredit",
    "owner": {
        "firstName": "John",
        "lastName": "Doe",
        "email": "email@email.org",
        "phoneNumber": "9522253720",
        "address": {
            "line1": "line1",
            "line2": "line2",
            "city": "Minnetonka",
            "state": "MN",
            "country": "US",
            "postalCode": "55410"
        }
    },
    "amount": "101.50",
    "currency": "USD",
    "klarnaCredit": {
        "returnUrl": "http://example.com/return",
        "cancelUrl": "http://example.com/cancel",
        "taxAmount": 0,
        "shippingAmount": 5.75,
        "items": [{
            "name": "Happy Ball",
            "quantity": "1",
            "unitAmount": "94.25",
            "subscriptionInfo": {
                "autoRenewal": true,
                "freeTrial": false
            }
        },
        {
            "name": "Happy Ball1",
            "quantity": "2",
            "unitAmount": "0.75"
        }],
        "locale": "en_US",
        "shipping": {
            "recipient": "Guy Incognito",
            "phoneNumber": "9522253720",
            "address": {
                "line1": "line1",
                "line2": "line2",
                "city": "Minnetonka",
                "state": "MN",
                "country": "US",
                "postalCode": "55410"
            },
            "email": "test_email@email.org"
        },
        "accountId": "456789",
        "accountCreatedDate": "2020-11-24T15:20:00.000Z",
        "accountUpdatedDate": "2012-11-25T15:30:00.001Z",
        "hasPaidBefore": false,
        "subscriptionDescription": "Klarna Credit Recurring",
        "subscriptionStartDate": "2019-10-24T15:00:00.030Z",
        "subscriptionEndDate": "2021-10-24T15:00:00.030Z",
        "autoRenewal": "false",
        "affiliateName": "Sample Affiliate"
    }
}
 
digitalriver.createSource(payload).then(function(result) {
 
    if (result.error) {
        //handle errors
    } else {
        var source = result.source;
        //send source to back end
        sendToBackend(source);
    }
});
```
{% endtab %}

{% tab title="With payment sessions" %}
```javascript
var payload = {
  "type" : "klarnaCredit",
  "owner" : {
    "firstName" : "firstName",
    "lastName" : "lastName",
    "email" : "email@email.org",
    "phoneNumber" : "9522253720",
    "address" : {
      "line1" : "line1",
      "line2" : "line2",
      "city" : "Minnetonka",
      "state" : "MN",
      "country" : "US",
      "postalCode" : "55410"
    }
  },
  "sessionId" : "3aa75613-9596-438a-9604-67e20016aa96",
  "klarnaCredit" : {
    "returnUrl" : "http://example.org/return",
    "cancelUrl" : "http://example.org/cancel"
  }
}
 
  
digitalriver.createSource(payload).then(function(result) {
    if (result.error) {
        //handle errors
    } else {
        var source = result.source;
        //send source to back end
        sendToBackend(source);
    }
});
```
{% endtab %}
{% endtabs %}

#### Klarna Recurring

For Klarna Recurring, you add `sessionId` to the payload and remove `amount`, `currency`, `klarnaCreditRecurring.items`, `klarnaCreditRecurring.locale`, `klarnaCreditRecurring.discountAmount`, `klarnaCreditRecurring.taxAmount`, `klarnaCreditRecurring.shippingAmount`, `klarnaCreditRecurring.shipping`, `klarnaCreditRecurring.accountId`, `klarnaCreditRecurring.accountCreatedDate`, `klarnaCreditRecurring.accountUpdatedDate`, `klarnaCreditRecurring.hasPaidBefore`, `klarnaCreditRecurring.subscriptionDescription`, `klarnaCreditRecurring.subscriptionStartDate`, `klarnaCreditRecurring.subscriptionEndDate`, `klarnaCreditRecurring.autoRenewal`, and `klarnaCreditRecurring.affiliateName`.&#x20;

The following tabs provide code examples of how sources are created without and with payment sessions.

{% tabs %}
{% tab title="Without payment sessions" %}
```javascript
let payload = {
    "type": "klarnaCreditRecurring",
    "owner": {
        "firstName": "John",
        "lastName": "Doe",
        "email": "email@email.org",
        "phoneNumber": "9522253720",
        "address": {
            "line1": "line1",
            "line2": "line2",
            "city": "Minnetonka",
            "state": "MN",
            "country": "US",
            "postalCode": "55410"
        }
    },
    "amount": "101.50",
    "currency": "USD",
    "klarnaCreditRecurring": {
        "returnUrl": "http://example.com/return",
        "cancelUrl": "http://example.com/cancel",
        "taxAmount": 0,
        "shippingAmount": 5.75,
        "items": [{
            "name": "Happy Ball",
            "quantity": "1",
            "unitAmount": "94.25",
            "subscriptionInfo": {
                "autoRenewal": true,
                "freeTrial": false
            }
        },
        {
            "name": "Happy Ball1",
            "quantity": "2",
            "unitAmount": "0.75"
        }],
        "locale": "en_US",
        "shipping": {
            "recipient": "Guy Incognito",
            "phoneNumber": "9522253720",
            "address": {
                "line1": "line1",
                "line2": "line2",
                "city": "Minnetonka",
                "state": "MN",
                "country": "US",
                "postalCode": "55410"
            },
            "email": "test_email@email.org"
        },
        "accountId": "456789",
        "accountCreatedDate": "2020-11-24T15:20:00.000Z",
        "accountUpdatedDate": "2012-11-25T15:30:00.001Z",
        "hasPaidBefore": false,
        "subscriptionDescription": "Klarna Credit Recurring",
        "subscriptionStartDate": "2019-10-24T15:00:00.030Z",
        "subscriptionEndDate": "2021-10-24T15:00:00.030Z",
        "autoRenewal": "false",
        "affiliateName": "Sample Affiliate"
    }
}
 
digitalriver.createSource(payload).then(function(result) {
 
    if (result.error) {
        //handle errors
    } else {
        var source = result.source;
        //send source to back end
        sendToBackend(source);
    }
});
```
{% endtab %}

{% tab title="With payment sessions" %}
```javascript
var payload = {
  "type" : "klarnaCreditRecurring",
  "owner" : {
    "firstName" : "firstName",
    "lastName" : "lastName",
    "email" : "email@email.org",
    "phoneNumber" : "9522253720",
    "address" : {
      "line1" : "line1",
      "line2" : "line2",
      "city" : "Minnetonka",
      "state" : "MN",
      "country" : "US",
      "postalCode" : "55410"
    }
  },
  "sessionId" : "3aa75613-9596-438a-9604-67e20016aa96",
  "klarnaCreditRecurring" : {
    "returnUrl" : "http://example.org/return",
    "cancelUrl" : "http://example.org/cancel"
  }
}
 
  
digitalriver.createSource(payload).then(function(result) {
    if (result.error) {
        //handle errors
    } else {
        var source = result.source;
        //send source to back end
        sendToBackend(source);
    }
});
```
{% endtab %}
{% endtabs %}

###
