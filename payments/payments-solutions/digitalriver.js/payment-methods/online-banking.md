---
description: >-
  Online Banking, also sometimes called Internet Bank Payment (IBP), is a
  Browser Redirect processing method where customers authorize a debit from
  their bank account.
---

# Online Banking (IBP)

Online Banking allows customers to use the online banking service provided by their bank.

## Configuring Online Banking for DigitalRiver.js

Create an Online Banking payment method for your app or website in four easy steps:

* [Step 1: Build an Online Banking source request object](online-banking.md#step-1-build-online-banking-objects)
* [Step 2: Create an Online Banking source or display](online-banking.md#step-2-create-an-online-banking-source-or-display)
* [Step 3: Authorize an Online Banking source](online-banking.md#step-3-authorize-an-online-banking-source)
* [Step 4: Use the authorized source](online-banking.md#step-4-use-the-authorized-source)

### Step 1: Build Online Banking objects

Build the Online Banking Source Request Details objects. The Online Banking Source Request object requires the following fields.

| Field           | Value                                                                                               |
| --------------- | --------------------------------------------------------------------------------------------------- |
| `type`          | onlineBanking                                                                                       |
| `sessionId`     | The payment session identifier.                                                                     |
| `owner`         | An [Owner object](common-payment-objects.md#owner-object).                                          |
| `onlineBanking` |  An [Online Banking Source Details object](online-banking.md#online-banking-source-request-object). |

#### Online Banking source details object

The Online Banking Details object requires the following fields.

```javascript
{
    "returnUrl": "https://example.com/success",
    "bankCode": "123"
}
```

| Field       | Required/Optional | Description                                                                                                                                                                                                                                        |
| ----------- | ----------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `returnUrl` | Required          | Where you will redirect your customer to after authorization within the Bank authorization experience.                                                                                                                                             |
| `cancelUrl` | Required          | If you choose to utilize the full redirect flow, this is where your Customer will be redirected to after cancelling within the Online Banking experience.                                                                                          |
| `bankCode`  | Required          | The identifier of the bank the customer has chosen and will be redirected to when finished. If using the DigitalRiver.js Internet Banking Payment element, this populated for you. If constructing the request yourself, this is a required field. |

### Step 2: Create an Online Banking source or display

Choose one of the following options:

* [Create an Online Banking source using DigitalRiver.js](online-banking.md#create-an-online-banking-source-using-digitalriver-js)
* [Create your Online Banking display using DigitalRiver.js](online-banking.md#create-your-online-banking-display-using-digitalriver-js)

#### Create an Online Banking source using DigitalRiver.js

To create an Online Banking payment source, use the DigitalRiver.js library to create and mount elements to the HTML container, or you can assemble the information and then send it using the standard calls in DigitalRiver.js.

#### Create the Online Banking element using DigitalRiver.js functionality

The Online Banking element creation follows the same pattern as other elements and exposes the same customizations and events. However, to properly display an accurate list of available banks, you must provide an additional `onlineBanking` object which holds the country and currency appropriate for your Customer.

| Field                    | Value                                                 |
| ------------------------ | ----------------------------------------------------- |
| `onlineBanking.currency` | The currency your customer uses to purchase products. |
| `onlineBanking.country`  | The country where your customer resides.              |

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
        currency: "EUR",
        country: "DE",
    }
};
 
var onlineBankingElement = digitalriver.createElement('onlinebanking', onlineBankingOptions);
onlineBankingElement.mount('online-banking');
```

To create an online banking source, you must reference the created element and the supplemental data in your [createSource ](../../../../general-resources/reference/digitalriver-object.md#digitalriver-createsource-element-sourcedata)request. DigitalRiver.js will retrieve and assemble the request on your behalf.

```javascript
var data = {
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
            "bankCode": "82"
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

#### Create your Online Banking display using DigitalRiver.js

If you decide not to use the out-of-the-box functionality provided with the Online Banking elements, you can use the `digitalriver.retrieveOnlineBankingBanks()` method to build your own experience.

#### Retrieving available banks

DigitalRiver.js exposes a method that allows you to retrieve the available banks for a country and currency combination. If banks are available, DigitalRiver.js returns an array of objects. If banks are not available, DigitalRiver.js returns an empty array.

{% tabs %}
{% tab title="JSON" %}
```javascript
digitalriver.retrieveOnlineBankingBanks("DE","EUR").then(function(response) {
    //use the returned values to create your own display
});
```
{% endtab %}
{% endtabs %}

#### Retrieved banks

{% tabs %}
{% tab title="JSON" %}
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

With the retrieved banks, you can build an experience suitable for your needs.

{% tabs %}
{% tab title="JavaScript" %}
```javascript
<select>
    <option value="86">Sofortüberweisung</option>
    <option value="21">Giropay</option>
</select>
```
{% endtab %}
{% endtabs %}

Once you have reached a point in your flow where the customer has selected a bank, you can use the createSource function to assemble and pass the data to Digital River to create your payment.

{% hint style="warning" %}
**Important**:  If you create an online banking source without using the DigitalRiver.js online banking element, you must pass an additional field `bankCode`.
{% endhint %}

{% tabs %}
{% tab title="JSON" %}
```javascript
var sourceData = {
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
            "bankCode": "82"
        }
 
        digitalriver.createSource(sourceData).then(function(result) {
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

#### Example Online Banking source

{% tabs %}
{% tab title="JSON" %}
```javascript
{
    "clientId": "gc",
    "channelId": "drdod15",
    "liveMode": false,
    "id": "8c4ef38f-d156-4e9d-bb37-bdb8849ef54b",
    "sessionId": "ea03bf6f-84ef-4993-b1e7-b7d5ecf71d1f",    
    "clientSecret": "8c4ef38f-d156-4e9d-bb37-bdb8849ef54b_0906601e-8a4b-42e1-962a-35333dd9b22d",
    "type": "onlineBanking",
    "reusable": false,
    "owner": {
        "firstName": "John",
        "lastName": "Doe",
        "email": "john.doe@digitalriver.com",
        "phoneNumber": "000-000-0000",
        "address": {
            "line1": "10380 Bren Road West",
            "line2": "Suite 123",
            "city": "Minnetonka",
            "state": "MN",
            "country": "DE",
            "postalCode": "55343"
        }
    },
    "amount": "100.00",
    "currency": "EUR",
    "state": "pending_redirect",
    "creationIp": "209.87.180.1",
    "createdTime": "2019-09-13T18:01:42.092Z",
    "updatedTime": "2019-09-13T18:01:42.092Z",
    "flow": "redirect",
    "redirect": {
        "redirectUrl": "https://api.digitalriver.com:443/payments/redirects/c0447656-3d11-4dda-a472-43057565160f?apiKey=pk_hc_e03ee62c0d964bb3ac75595b1203d13c",
        "returnUrl": "https://chrismiller.me/dev/dr/test-dr/example/test-drive?locale=en_US&action=paymentSuccess",
    },
    "onlineBanking": {
        "bankCode": "86"
    }
}
```
{% endtab %}
{% endtabs %}

### Step 3: Authorize an Online Banking source

When you create an Online Banking source, the customer is required to authorize the charge through their payment provider. You can accomplish this by redirecting the customer to their payment provider.

#### Redirecting the customer for Online Banking authorization

To redirect your customer to the payment provider for authorization, use the `redirectUrl` parameter in your `createSource` response.

```javascript
window.location.href = sourceResponse.redirect.redirectUrl;
```

The payment provider will present the customer with the transaction details where they can authorize or cancel the transaction. A successful authorization redirects the customer to the Online Banking Return URL parameter you specified when you created the source.&#x20;

Once authorized, the source state will change to chargeable.

```javascript
{
    "clientId": "gc",
    "channelId": "drdod15",
    "liveMode": false,
    "id": "8c4ef38f-d156-4e9d-bb37-bdb8849ef54b",
    "sessionId": "ea03bf6f-84ef-4993-b1e7-b7d5ecf71d1f",    
    "clientSecret": "8c4ef38f-d156-4e9d-bb37-bdb8849ef54b_0906601e-8a4b-42e1-962a-35333dd9b22d",
    "type": "onlineBanking",
    "reusable": false,
    "owner": {
        "firstName": "John",
        "lastName": "Doe",
        "email": "john.doe@digitalriver.com",
        "phoneNumber": "000-000-0000",
        "address": {
            "line1": "10380 Bren Road West",
            "line2": "Suite 123",
            "city": "Minnetonka",
            "state": "MN",
            "country": "DE",
            "postalCode": "55343"
        }
    },
    "amount": "100.00",
    "currency": "EUR",
    "state": "chargeable",
    "creationIp": "209.87.180.1",
    "createdTime": "2019-09-13T18:01:42.092Z",
    "updatedTime": "2019-09-13T18:01:42.092Z",
    "flow": "redirect",
    "redirect": {
        "redirectUrl": "https://api.digitalriver.com:443/payments/redirects/c0447656-3d11-4dda-a472-43057565160f?apiKey=pk_hc_e03ee62c0d964bb3ac75595b1203d13c",
        "returnUrl": "https://chrismiller.me/dev/dr/test-dr/example/test-drive?locale=en_US&action=paymentSuccess",
    },
    "onlineBanking": {
        "bankCode": "86"
    }
}
```

### Step 4: Use the authorized source

Once authorized, you can use the source by [attaching it to a cart](../../../sources/#attaching-a-payment-method-to-an-order-or-cart).

{% tabs %}
{% tab title="POST /v1/shoppers/me/carts/active/apply-payment-method" %}
```javascript
{
  "paymentMethod": {
    "sourceId": "e7ba0595-059c-460c-bad8-2812123b9313"
  }
}
```
{% endtab %}
{% endtabs %}

## Supported online banking options

{% hint style="info" %}
The following banks are subject to availability from our provider.
{% endhint %}

| IBP Banks                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              | Country     | Country Code | Currency |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------- | ------------ | -------- |
| <p><strong>EPS</strong> </p><p>The banks participating in the EPS scheme are: </p><ul><li>Raiffeisen Bankengruppe</li><li>Erste Bank und Sparkassen</li><li>Bankhaus Spängler</li><li>Die österreichischen Volksbanken, Immo-Bank, Gärtnerbank</li><li>Hypo Tirol Bank AG</li><li>HYPO Banken - Raiffeisen Rechenzentrum</li><li>BAWAG P.S.K.</li><li>Bank für Ärzte und Freie Berufe AG</li><li>Niederösterreichische Landesbank-Hypothekenbank AG</li><li>Vorarlberger Landes- und Hypothekenbank AG</li><li>Hypo Alpe-Adria-Bank AG</li><li>Investkredit Bank AG</li><li>VR-Bank Braunau</li><li> Schoellerbank AG</li><li>Bankhaus Schelhammer &#x26; Schattera AG</li><li>Österreichische Apothekerbank reg.Gen.m.b.H.</li></ul><p>In addition Bank Austria AG technically participates in the scheme, but not commercially in the solution provided by DRWP.</p> | Austria     | AT           | EUR      |
| <p>Sofort </p><p>GiroPay</p>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           | Germany     | DE           | EUR      |
| Nordea, Spankki, Säästöpankki, Danske, Aktia, OP Pohjola                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | Finland     | FI           | EUR      |
| <p>iDEAL</p><ul><li>ABN AMRO</li><li>Bunq bank</li><li>ING</li><li>Moneyou</li><li>Rabobank</li><li>SNS Bank</li><li>ASN Bank</li><li>Regio Bank</li><li>Triodos Bank</li><li>Knab Bank</li><li>Van Lanschot Bank</li><li>Svenska Handelsbanken (In progress of adding)</li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      | Netherlands | NL           | EUR      |
| <ul><li>Dotpay</li><li>Pekao24Przelew</li><li>Plac z ING</li><li>Millennium - Platnosci Internetowe</li><li>Pay with Alior Bank</li><li>Place z Citi Handlowy</li><li>Plac z BOS</li><li>mTransfer</li><li>Place z Inteligo</li><li>Przelew24</li><li>Pocztowy24</li><li>BLIK</li><li>Banki Spoldzielcze</li><li>Place z Plus Bank</li><li>Idea Cloud</li><li>EnveloBank</li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     | Poland      | PL           | PLN      |
| Handelsbanken, Swedbank                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                | Sweden      | SE           | SEK      |

## Supported markets

For information on supported markets and currencies for Drop-in and DigitalRiver.js, go to:&#x20;

* **Payment Method Guide:** [digitalriver.com/payment-method-guide](https://www.digitalriver.com/payment-method-guide/)
* **Country Guide:** [digitalriver.com/country-guide/](https://www.digitalriver.com/country-guide/)
