---
description: Learn how to configure Bancontact for DigitalRiver.js with Elements.
---

# Configuring Bancontact

If you're using[ DigitalRiver.js with Elements](../), you can create a [Bancontact](../../../supported-payment-methods/bancontact.md) payment method for your app or website in four easy steps:

* [Step 1: Build a Bancontact Source Request object](configuring-bancontact.md#step-1-build-a-bancontact-source-request-and-details-object)
* [Step 2: Create a Bancontact source using DigitalRiver.js](configuring-bancontact.md#step-2-create-a-bancontact-source-using-digitalriver.js)
* [Step 3: Authorize the Bancontact source](configuring-bancontact.md#step-3-authorize-the-bancontact-source)
* [Step 4: Use the authorized source](configuring-bancontact.md#step-4-use-the-authorized-source)

## Step 1: Build a Bancontact Source Request and Details object

Build the Bancontact Source Request and Details objects.&#x20;

### Bancontact Source Request object

The Bancontact Source Request object requires the following fields.

| Field        | Value                                                                                             |
| ------------ | ------------------------------------------------------------------------------------------------- |
| `type`       | `bancontact`                                                                                      |
| `sessionId`  | The payment session identifier.                                                                   |
| `owner`      | An [Owner object](common-payment-objects.md#owner-object).                                        |
| `bancontact` | A [Bancontact Source Details object](configuring-bancontact.md#bancontact-source-details-object). |

### Bancontact Source Details object

The Bancontact Source Details object requires the following fields.

{% code overflow="wrap" %}
```javascript
{
    "returnUrl": "https://example.com"
}
```
{% endcode %}

| Field       | Required/Optional | Description                                                                                                                                                    |
| ----------- | ----------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `returnUrl` | Required          | If you choose to use the full redirect flow, this is where you will redirect your customer to after authorizing or canceling within the Bancontact experience. |

## Step 2: Create a Bancontact source using DigitalRiver.js

Use the DigitalRiver.js library to create and mount elements to the HTML container.

{% hint style="info" %}
The `address` object must contain postal code and state/province data that **** [adheres to a standardized format](../../../../cart/creating-or-updating-a-cart/providing-address-information.md) using the `state` attribute. Note that the `state` attribute listed below corresponds to the `countrySubdivision` attribute used when providing address information. The payment session manages the correct field name on the backend.
{% endhint %}

{% code overflow="wrap" %}
```javascript
let bancontactSourceData = {
    "sessionId": "9f70082c-48ad-4fe2-a280-8e6ef2601076",
    "type": "bancontact",
    "owner": {
        firstName: "Sabri",
        lastName: "Odink",
        email: "sodink@acme.com",
        phoneNumber: "0481 40 39297",
        address: {
            line1: "Rue du Commerce 335",
            line2: "",
            city: "Wondelgem",
            state: "East Flanders",            
            postalCode: "9032",
            country: "BE"
        }
    },
    "bancontact": {
        "returnUrl": "https://example.com?action=paymentSuccess"
    }
}
 
digitalriver.createSource(bancontactSourceData).then(function(result) {
    if (result.error) {
        //handle errors as something went wrong
    } else {
        var source = result.source;
     
        //do something with the created source
    }
});
```
{% endcode %}

### Bancontact source example

{% code overflow="wrap" %}
```javascript
{
    "clientId": "gc",
    "channelId": "drdod15",
    "liveMode": false,
    "sessionId": "9f70082c-48ad-4fe2-a280-8e6ef2601076",
    "id": "bddccfc7-4fa8-401b-b661-421cd5047792",
    "clientSecret": "bddccfc7-4fa8-401b-b661-421cd5047792_bdddssccfc7-4fa8-401b-b661-421cd5047792",
    "type": "bancontact",
    "reusable": false,
    "owner": {
        "firstName": "Sabri",
        "lastName": "Odink",
        "email": "sodink@acme.com"",
        "phoneNumber": "0481 40 39297",
        "address": {
            "line1": "Rue du Commerce 335",
            "city": "Wondelgem",
            "state": "East Flanders",
            "country": "BE",
            "postalCode": "9032"
        }
    },
    "amount": "778.39",
    "currency": "EUR",
    "state": "pending_redirect",
    "creationIp": "209.87.178.4",
    "createdTime": "2019-05-22T01:48:42.168Z",
    "updatedTime": "2019-05-22T01:48:42.168Z",
    "flow": "redirect",
    "redirect": {
        "redirectUrl": "https://api.digitalriver.com:443/payments/redirects/4e478578-843a-48a5-beef-66c0dae99f5d?apiKey=pk_test_6cb0fe9ce3124093a9ad906f6c589e2d",
        "returnUrl": "https://example.com?action=paymentSuccess"
    },
    "bancontact": {}
}
```
{% endcode %}

## Step 3: Authorize the Bancontact source

When you create a Bancontact source, the customer is required to authorize the charge through their payment provider. You can accomplish this by redirecting the customer to their payment provider.

### Redirecting the customer for Bancontact authorization

To redirect your customer to the payment provider for authorization, use the `redirectUrl` parameter in your `createSource` response.

```javascript
window.location.href = sourceResponse.redirect.redirectUrl;
```

The payment provider will present the customer with the transaction details and the customer can authorize, or cancel the transaction. A successful authorization redirects the customer to the Bancontact Return URL parameter you specified when you created the source.

Once authorized, the source state will change to `chargeable`.

{% code overflow="wrap" %}
```javascript
{
    "clientId": "gc",
    "channelId": "drdod15",
    "liveMode": false,
    "id": "bdcf5832-fc2c-4c79-92e0-85b261s18ae0",
    "clientSecret": "bdcf5832-fc2c-4c79-92e0-85b261s18ae0_adcf5832-fc2c-4c79-92e0-85b261s18ae0",
    "type": "bancontact",
    "reusable": false,
    "owner": {
        "firstName": "Sabri",
        "lastName": "Odink",
        "email": "sodink@acme.com"",
        "phoneNumber": "0481 40 39297",
        "address": {
            "line1": "Rue du Commerce 335",
            "city": "Wondelgem",
            "state": "East Flanders",
            "country": "BE",
            "postalCode": "9032"
        }
    },
    "amount": "100.00",
    "currency": "KRW",
    "state": "chargeable",
    "creationIp": "209.87.178.4",
    "createdTime": "2019-05-22T02:40:53.631Z",
    "updatedTime": "2019-05-22T02:40:53.631Z",
    "flow": "redirect",
    "redirect": {
        "redirectUrl": "https://api.digitalriver.com:443/payments/redirects/06e428cf-e23e-4ee9-b64f-ce17de062fd1?apiKey=pk_test_6cb0fe9ce312d093a9ad906f6c589e2d",
        "returnUrl": "https://example.com"
    },
    "bancontact": {}
}
```
{% endcode %}

## Step 4: Use the authorized source

Once authorized, you can use the source by [attaching it to a cart](../../../sources/#attaching-a-payment-method-to-an-order-or-cart).

{% tabs %}
{% tab title="POST /v1/shoppers/me/carts/active/apply-payment-method" %}
{% code overflow="wrap" %}
```javascript
{
  "paymentMethod": {
    "sourceId": "e7ba0595-059c-460c-bad8-2812123b9313"
  }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}
