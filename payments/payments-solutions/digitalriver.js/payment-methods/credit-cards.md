---
description: >-
  The Credit Cards payment method is a fast and secure shopping experience where
  the consumer can purchase goods or services on credit.
---

# Credit Cards

The Credit Card payment method supports the following credit cards: American Express, Diners, Discover, JCB, Maestro, MasterCard, Union Pay, and Visa

You can find an example of integration [here](https://drh.img.digitalriver.com/DRHM/Storefront/Site/drdod15/pb/multimedia/creditcard.html).

## Configuring Credit Card payments for DigitalRiver.js

Create a Credit Card payment method for your app or website in three easy steps:

* [Step 1: Build a Credit Card source request object](credit-cards.md#step-1-build-a-credit-card-source-request-object)
* [Step 2: Create a Credit Card source using DigitalRiver.js](credit-cards.md#step-2-create-a-credit-card-source-using-digitalriver-js)
* [Step 3: Use the authorized source](credit-cards.md#step-3-use-the-authorized-source)

### Step 1: Build a Credit Card source request object

Build a Credit Card Source Request object. The Credit Card Source Request object requires the following fields.

| Field     | Value                                                       |
| --------- | ----------------------------------------------------------- |
| type      | creditCard                                                  |
| sessionId | The payment session identifier.                             |
| owner     |  An [Owner object](common-payment-objects.md#owner-object). |

### Step 2: Create a Credit Card source using DigitalRiver.js

#### Create the elements

Use the DigitalRiver.js library to create and mount elements to the HTML container.

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

#### Create the source

&#x20;To create a credit card payment source, you must reference the created element and the supplemental data in your [createSource ](../reference/digitalriver-object.md#digitalriver-createsource-element-sourcedata)request. DigitalRiver.js will retrieve and assemble the request on your behalf.

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

#### Credit Card source example

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

### Step 3: Use the authorized source

Once authorized, you can use the source by [attaching it to a cart](../../../sources/#attaching-a-payment-method-to-an-order-or-cart) or [attaching it to a shopper](../../../sources/#attaching-a-payment-method-to-a-customer).

#### Option 1: Attach the source to a cart

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

#### Option 2: Attach the source to a shopper

{% tabs %}
{% tab title="POST /v1/shoppers/me/payment-options" %}
```javascript
{
  "paymentOption": {
    "nickName": "My Token",
    "isDefault": "true",
    "sourceId": "61033d62-c0f4-4a7e-b844-07daf26ba84e"
  }
}
```
{% endtab %}
{% endtabs %}

## Supported markets

For information on supported markets and currencies for Drop-in and DigitalRiver.js, go to:&#x20;

* **Payment Method Guide:** [digitalriver.com/payment-method-guide](https://www.digitalriver.com/payment-method-guide/)
* **Country Guide:** [digitalriver.com/country-guide/](https://www.digitalriver.com/country-guide/)
