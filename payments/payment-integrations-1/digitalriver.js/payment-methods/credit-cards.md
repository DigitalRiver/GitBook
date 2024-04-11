---
description: Learn how to configure Credit Cards for DigitalRiver.js with Elements.
---

# Configuring Credit Cards

If you're using [DigitalRiver.js with Elements](../), you can create a [Credit Card](../../../supported-payment-methods/credit-cards.md) payment method for your app or website in three easy steps:

* [Step 1: Build a Credit Card Source Request object](credit-cards.md#step-1-build-a-credit-card-source-request-object)
* [Step 2: Create a Credit Card source using DigitalRiver.js](credit-cards.md#step-2-create-a-credit-card-source-using-digitalriver-js)
* [Step 3: Use the authorized source](credit-cards.md#step-3-use-the-authorized-source)

## Step 1: Build a Credit Card source request object

The Credit Card Source Request object requires the following fields.

| Field     | Value                                |
| --------- | ------------------------------------ |
| type      | creditCard                           |
| sessionId | The payment session identifier.      |
| owner     | An [Owner object](broken-reference). |

## Step 2: Create a Credit Card source using DigitalRiver.js

### Create the elements

Use the DigitalRiver.js library to create and mount elements to the HTML container.

{% code overflow="wrap" %}
```javascript
var options = {
        style: {
        base: {
            color: "#fff",
            fontFamily: "Arial, Helvetica, sans-serif",
            fontSize: "16px",
        }
    }
}
  
//Create your elements
var cardNumber = digitalriver.createElement('cardnumber', options);
var cardExpiration = digitalriver.createElement("cardexpiration", options);
var cardCVV = digitalriver.createElement("cardcvv", options);
  
//Place the created elements on the page.
cardNumber.mount('card-number');
cardExpiration.mount('card-expiration');
cardCVV.mount('card-cvv');
```
{% endcode %}

### Create the source

To create a credit card payment source, you must reference the created element and the supplemental data in your [createSource ](broken-reference)request. DigitalRiver.js will retrieve and assemble the request on your behalf.

{% hint style="info" %}
The address object must contain [postal code](../../../../integration-options/checkouts/creating-checkouts/providing-address-information.md#postal-code-validations) and [state/province](../../../../integration-options/checkouts/creating-checkouts/providing-address-information.md#states-and-province-validations) data that [adheres to a standardized format](../../../../integration-options/checkouts/creating-checkouts/providing-address-information.md#postal-code-and-state-province-validations).
{% endhint %}

{% code overflow="wrap" %}
```javascript
var payload = {
    "type": "creditCard",
    "sessionId": "69a47e2c-f8b3-4173-9c0d-40332abcaf98",    
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

    digitalriver.createSource(cardCVV,payload).then(function(result) {
            if(result.error) {
                //handle errors
            } else {
                var source = result.source;
                //send source to back end
                sendToBackend(source);
            }
    });
```
{% endcode %}

### Credit Card source example

{% code overflow="wrap" %}
```javascript
{
    "clientId": "gc",
    "channelId": "drdod15",
    "liveMode": false,
    "id": "b9914aea-d045-4160-8bd9-12277ee333b1",
    "sessionId": "69a47e2c-f8b3-4173-9c0d-40332abcaf98",    
    "clientSecret": "b9914aea-d045-4160-8bd9-12277ee333b1_a2214aea-d045-4160-8bd9-12277ee333b1",
    "type": "creditCard",
    "reusable": false,
    "owner": {
        "firstName": "Destany",
        "lastName": "Hackett",
        "email": "Jimmy.Trantow63@gmail.com",
        "phoneNumber": "000-000-0000",
        "address": {
            "line1": "1283 Cummings Squares",
            "line2": "Suite 917",
            "city": "Russelview",
            "state": "CO",
            "country": "US",
            "postalCode": "85501-4084"
        }
    },
    "state": "chargeable",
    "creationIp": "209.87.178.4",
    "createdTime": "2019-05-22T01:41:59.241Z",
    "updatedTime": "2019-05-22T01:41:59.241Z",
    "flow": "standard",
    "creditCard": {
        "brand": "Visa",
        "expirationMonth": 2,
        "expirationYear": 2022,
        "lastFourDigits": "1111",
        "paymentIdentifier": "13159976250000000000000500658101"
    }
}
```
{% endcode %}

## Step 3: Use the authorized source

Once authorized, you can use the source by either [attaching it to a checkout](broken-reference) or [attaching it to a customer](broken-reference) for multiple uses.

### Option 1. Attach the source to a checkout

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

### Option 2. Attach the source to a customer

{% tabs %}
{% tab title="POST /customers/{id}/sources/{sourcesId}" %}
{% code overflow="wrap" %}
```javascript
{
  "paymentOption": {
    "nickName": "My Token",
    "isDefault": "true",
    "sourceId": "61033d62-c0f4-4a7e-b844-07daf26ba84e"
  }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Testing Credit Cards

See [Testing standard payment methods](../../../../developer-resources/testing-scenarios.md#testing-standard-payment-methods) for testing instructions.
