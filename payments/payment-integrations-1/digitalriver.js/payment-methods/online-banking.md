---
description: Learn how to configure Online Banking (IBP) for DigitalRiver.js with Elements.
---

# Configuring Online Banking (IBP)

If you're using [DigitalRiver.js with Elements](../), you can create an [Online Banking](../../../supported-payment-methods/online-banking-ibp.md) payment method for your app or website in four easy steps:

* [Step 1: Build an Online Banking source request object](online-banking.md#step-1-build-an-online-banking-object)
* [Step 2: Create an Online Banking source or display](online-banking.md#step-2-create-an-online-banking-source-or-display)
* [Step 3: Authorize an Online Banking source](online-banking.md#step-3-authorize-an-online-banking-source)
* [Step 4: Use the authorized source](online-banking.md#step-4-use-the-authorized-source)

## Step 1: Build an Online Banking object

Build the Online Banking Source Request Details objects. The Online Banking Source Request object requires the following fields.

| Field           | Value                                                                                              |
| --------------- | -------------------------------------------------------------------------------------------------- |
| `type`          | onlineBanking                                                                                      |
| `sessionId`     | The payment session identifier.                                                                    |
| `owner`         | An [Owner object](common-payment-objects.md#owner-object).                                         |
| `onlineBanking` | An [Online Banking Source Details object](online-banking.md#online-banking-source-request-object). |

### Online Banking source details object

The Online Banking Details object requires the following fields.

{% code overflow="wrap" %}
```javascript
{
    "returnUrl": "https://example.com/success",
    "cancelUrl": "https://example.com/cancel",
    "bankCode": "123"
}
```
{% endcode %}

| Field       | Required/Optional | Description                                                                                                                                                                                                                                        |
| ----------- | ----------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `returnUrl` | Required          | Where you will redirect your customer to after authorization within the Bank authorization experience.                                                                                                                                             |
| `cancelUrl` | Required          | If you choose to utilize the full redirect flow, this is where your Customer will be redirected to after cancelling within the Online Banking experience.                                                                                          |
| `bankCode`  | Required          | The identifier of the bank the customer has chosen and will be redirected to when finished. If using the DigitalRiver.js Internet Banking Payment element, this populated for you. If constructing the request yourself, this is a required field. |

## Step 2: Create an Online Banking source or display

Choose one of the following options:

* [Create an Online Banking source using DigitalRiver.js](online-banking.md#create-an-online-banking-source-using-digitalriver-js)
* [Create your Online Banking display using DigitalRiver.js](online-banking.md#create-your-online-banking-display-using-digitalriver-js)

### Create an Online Banking source using DigitalRiver.js

To create an Online Banking payment source, use the DigitalRiver.js library to create and mount elements to the HTML container, or you can assemble the information and then send it using the standard calls in DigitalRiver.js.

### Create the Online Banking element using DigitalRiver.js functionality

The Online Banking element creation follows the same pattern as other elements and exposes the same customizations and events. However, to properly display an accurate list of available banks, you must provide an additional `onlineBanking` object which holds the country and currency appropriate for your Customer.

| Field                    | Value                                                 |
| ------------------------ | ----------------------------------------------------- |
| `onlineBanking.currency` | The currency your customer uses to purchase products. |
| `onlineBanking.country`  | The country where your customer resides.              |

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
{% endcode %}

To create an online banking source, you must reference the created element and the supplemental data in your [createSource ](../../../../developer-resources/reference/digitalriver-object.md#creating-sources)request. DigitalRiver.js will retrieve and assemble the request on your behalf.

{% hint style="info" %}
The `address` object must contain [postal code](../../../../integration-options/checkouts/creating-checkouts/providing-address-information.md#postal-code-validations) and [state/province](../../../../integration-options/checkouts/creating-checkouts/providing-address-information.md#states-and-province-validations) data that [adheres to a standardized format](../../../../integration-options/checkouts/creating-checkouts/providing-address-information.md#postal-code-and-state-province-validations).
{% endhint %}

{% code overflow="wrap" %}
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
            "cancelUrl": "https://myurl.com/cancel",
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
{% endcode %}

### Create your Online Banking display using DigitalRiver.js

If you decide not to use the out-of-the-box functionality provided with the Online Banking elements, you can use the `digitalriver.retrieveOnlineBankingBanks()` method to build your own experience.

### Retrieving available banks

DigitalRiver.js exposes a method that allows you to retrieve the available banks for a country and currency combination. If banks are available, DigitalRiver.js returns an array of objects. If banks are not available, DigitalRiver.js returns an empty array.

{% tabs %}
{% tab title="JSON" %}
{% code overflow="wrap" %}
```javascript
digitalriver.retrieveOnlineBankingBanks("DE","EUR").then(function(response) {
    //use the returned values to create your own display
});
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Retrieved banks

{% tabs %}
{% tab title="JSON" %}
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

With the retrieved banks, you can build an experience suitable for your needs.

{% tabs %}
{% tab title="JSON" %}
{% code overflow="wrap" %}
```javascript
<select>
    <option value="86">Sofortüberweisung</option>
    <option value="21">Giropay</option>
</select>
```
{% endcode %}
{% endtab %}
{% endtabs %}

Once you have reached a point in your flow where the customer has selected a bank, you can use the createSource function to assemble and pass the data to Digital River to create your payment.

{% hint style="warning" %}
**Important**: If you create an online banking source without using the DigitalRiver.js online banking element, you must pass an additional field `bankCode`.
{% endhint %}

{% tabs %}
{% tab title="JSON" %}
{% code overflow="wrap" %}
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
            "cancelUrl": "https://myurl.com/cancel",
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
{% endcode %}
{% endtab %}
{% endtabs %}

### Example Online Banking source

{% tabs %}
{% tab title="JSON" %}
{% code overflow="wrap" %}
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
        "cancelUrl": "https://chrismiller.me/dev/dr/test-dr/example/test-drive?locale=en_US&action=paymentFailue"
    },
    "onlineBanking": {
        "bankCode": "86"
    }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Step 3: Authorize an Online Banking source

When you create an Online Banking source, the customer is required to authorize the charge through their payment provider. You can accomplish this by redirecting the customer to their payment provider.

### Redirecting the customer for Online Banking authorization

To redirect your customer to the payment provider for authorization, use the `redirectUrl` parameter in your `createSource` response.

{% code overflow="wrap" %}
```javascript
window.location.href = sourceResponse.redirect.redirectUrl;
```
{% endcode %}

The payment provider will present the customer with the transaction details where they can authorize or cancel the transaction. A successful authorization redirects the customer to the Online Banking Return URL parameter you specified when you created the source.

Once authorized, the source state will change to chargeable.

{% code overflow="wrap" %}
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
{% endcode %}

## Step 4: Use the authorized source

Once authorized, you can use the source by [attaching it to a checkout](../../../payment-sources/using-the-source-identifier.md#attaching-sources-to-checkouts).

### Attach the source to a checkout

{% tabs %}
{% tab title="POST /checkouts/{id}" %}
{% code overflow="wrap" %}
```javascript
{
  "customerId": "5774321008",
  "sourceId": "src_a78cfeae-f7ae-4719-8e1c-d05ec04e4d37"
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Testing Online Banking (IBP)

See [Testing redirect payment methods](../../../../developer-resources/testing-scenarios.md#testing-redirect-payment-methods) for testing instructions.
