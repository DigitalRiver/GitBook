---
description: >-
  Learn how to configure Alipay+ (cross-border) for DigitalRiver.js with
  Elements
---

# Configuring Alipay+ (cross-border)

If you're using[ DigitalRiver.js with Elements](../), you can create an Alipay+ (cross-border) payment method for your app or website in four easy steps:

* [Step 1: Alipay+ (cross-border) Source Details object](configuring-alipay+-cross-border.md#step-1-build-an-alipay+-cross-border-source-request-object)
* [Step 2: Create the Alipay+ (cross-border) source using DigitalRiver.js](configuring-alipay+-cross-border.md#step-2-create-the-alipay+-cross-border-source-using-digitalriver.js)
* [Step 3: Authorize an Alipay+ (cross-border) source](configuring-alipay+-cross-border.md#step-3-authorize-an-alipay+-cross-border-source)
* [Step 4: Use the Authorized source](alipay.md#step-4-use-the-authorized-source)

## Step 1: Build an Alipay+ (cross-border) source request object

Build an Alipay+ (cross-border) Source Request object. The Alipay+ Source Request object requires the following fields.

| Field       | Value                                                                                                                                                                           |
| ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `type`      | `alipayCn`                                                                                                                                                                      |
| `sessionId` | The payment session identifier.                                                                                                                                                 |
| `owner`     | An [Owner object](common-payment-objects.md#owner-object).                                                                                                                      |
| `alipayCn`  | An [Alipay+ (cross-border) Source Details object](configuring-alipay+-cross-border.md#alipay+-cross-border-source-details-object) that includes the details of the transaction. |

### Alipay+ (cross-border) source details object

{% code overflow="wrap" %}
```javascript
{
    "returnUrl": "https://example.com"
}
```
{% endcode %}

| Field     | Required/Optional | Description                                                                                                                  |
| --------- | ----------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| returnUrl | Required          | Where you will redirect your customer after the customer authorizes or cancels within the Alipay+ (cross-border) experience. |

## Step 2: Create the Alipay+ (cross-border) source using DigitalRiver.js

Use the DigitalRiver.js library to create and mount elements to the HTML container.

{% hint style="info" %}
The `address` object must contain postal code and state/province data that [adheres to a standardized format](../../../../shopper-apis/cart/creating-or-updating-a-cart/providing-address-information.md) using the `state` attribute. Note that the `state` attribute listed below corresponds to the `countrySubdivision` attribute used when providing address information. The payment session manages the correct field name on the backend.
{% endhint %}

{% code overflow="wrap" %}
```javascript
let alipayCnSourceData = {
                "type": "alipayCn",
                "sessionId": "3c9473b0-630d-4f20-af61-63d3aa8acb35",
                "owner": {
                    "firstName": "Donglei",
                    "lastName": "Ye",
                    "email": "j2r23ux28qj@temporary-mail.net",
                    "phoneNumber": "13063725095",
                    "address": {
                        "line1": "Wei Bai Chang",
                        "city": "ShunDe District)",
                        "state": "Guangdong",
                        "country": "CN",
                        "postalCode": "528322"
                    }
                },
                "alipayCn": {
                    "returnUrl": redirectUrl
                }
            }
 
digitalriver.createSource(alipayCn+SourceData ).then(function(result) {
    if (result.error) {
        //handle errors as something went wrong
    } else {
        var source = result.source;
     
        //do something with the created source
    }
});
```
{% endcode %}

### Alipay+ (cross-border) source example

{% code overflow="wrap" %}
```javascript
{
    "clientId": "gc",
    "channelId": "drdod15",
    "liveMode": false,
    "id": "5ce08114-143b-4bf6-ae0e-6fc501ee0c24",
    "clientSecret": "5ce08114-143b-4bf6-ae0e-6fc501ee0c24_a468b08e-2c47-4531-82af-d48d80ff6dcc",
    "type": "alipayCn",
    "reusable": false,
    "owner": {
        "firstName": "Donglei",
        "lastName": "Ye",
        "email": "j2r23ux28qj@temporary-mail.net",
        "phoneNumber": "13063725095",
        "address": {
            "line1": "Wei Bai Chang",
            "city": "ShunDe District)",
            "state": "Guangdong",
            "country": "CN",
            "postalCode": "528322"    
        }
    },
    "amount": "10.00",
    "currency": "CNY",
    "state": "pending_redirect",
    "creationIp": "10.81.3.92",
    "createdTime": "2020-02-26T02:48:11.508Z",
    "updatedTime": "2020-02-26T02:48:11.508Z",
    "flow": "redirect",
    "redirect": {
        "redirectUrl": "https://api.digitalriverws.com:443/payments/redirects/51314834-9bf9-483f-b3a7-4b36a14d3f5c?apiKey=pk_hc_e03ee62c0d964bb3ac75595b1203d13c",
        "returnUrl": "returnUrl.com"
    },
    "alipayCn+": {}
}
```
{% endcode %}

## Step 3: Authorize an Alipay+ (cross-border) source

When you create an Alipay+ (cross-border) source, the customer is required to authorize the charge through their payment provider. You can accomplish this by redirecting the customer to their payment provider.

### Redirecting the customer for authorization

To redirect your customer to the payment provider for authorization, use the `redirectUrl` parameter in your `createSource` response.

```javascript
window.location.href = sourceResponse.redirect.redirectUrl;
```

The payment provider will present the customer with the transaction details to authorize, or cancel the transaction. A successful authorization redirects the customer to the Alipay Return URL parameter you specified when you created the source.

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

```
{% endcode %}
{% endtab %}
{% endtabs %}
