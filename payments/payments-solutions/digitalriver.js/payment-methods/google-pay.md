---
description: >-
  The Google Pay payment method allows a merchant to request any credit or debit
  card stored in their customer’s Google Pay account.
---

# Google Pay

This payment method adds another layer of ease-of-purchase for consumers to quickly complete transactions from their Google Wallet. All currencies are available in supported countries.&#x20;

This guide describes how to create and customize a Google Pay element for your shoppers.

You can find an example of integration [here](https://drh.img.digitalriver.com/DRHM/Storefront/Site/drdod15/pb/multimedia/googlepay.html).

## Configuring Google Pay for DigitalRiver.js

Create a Google Pay payment method for your app or website in two easy steps:

* [Step 1: Create a Google Pay source using DigitalRiver.js](google-pay.md#step-1-create-a-google-pay-source-using-digital-river-js)
* [Step 2: Use the authorized source](google-pay.md#step-2-use-the-authorized-source)

### Step 1: Create a Google Pay source using Digital River.js

To create a Google Pay payment source, follow the instructions for [DigitalRiver.js reference guide](../reference/).

#### Create a Google Pay element

After setting up your library per the [DigitalRiver.js reference guide](../reference/), create a Google Pay element with any customizations you would like to apply.

```javascript
var paymentRequestData = digitalriver.paymentRequest({
        country: "US",
        currency: "USD",
        total: {
            label: "Order Total",
            amount: 100
        },
        displayItems: lineItems,
        shippingOptions: shippingOptions,
        style: {
            buttonType: "plain",
            buttonColor: "dark",
            buttonLanguage: "en"
        },
        "sessionId": "9f180964-9da4-43ac-b8e0-ae54d832b03c"
    });
   
   
var googlepay = digitalriver.createElement('googlepay', paymentRequestData);
```

#### Configure the Google Pay element to handle events

The Google Pay element will surface events, which will give you more information to facilitate what is happening within the Google Pay experience.

These events include:

| Event                                                                                         | Triggered When                                                                                                                                            |
| --------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [ready](../reference/elements/google-pay-elements.md#ready)                                   | The created element is loaded and ready to accept an update request.                                                                                      |
| [click](../reference/elements/google-pay-elements.md#click)                                   | A shopper clicked the element's button.                                                                                                                   |
| [cancel](../reference/elements/google-pay-elements.md#cancel)                                 | The customer has canceled the experience.                                                                                                                 |
| [shippingoptionchange](../reference/elements/google-pay-elements.md#shipping-option-change)   | The customer has chosen a different shipping option than was previously selected. You should use this data to re-price your order totals (if applicable). |
| [shippingaddresschange](../reference/elements/google-pay-elements.md#shipping-address-change) | The customer has chosen a different address than was previously selected. You should use this data to re-price your order totals (if applicable).         |
| [source](../reference/elements/google-pay-elements.md#source)                                 | The customer has authorized the payment and a source, and DigitalRiver.js returned associated data.                                                       |

{% hint style="info" %}
**Note**: To use Google Pay, you must listen to, at minimum, the Source event.
{% endhint %}

```javascript
googlepay.on('source', function(event) {
    var source = result.source;
  
    //pass the source to your back end for further processing. 
 
 
    //once verified that the source is created successfully, complete the Google Pay session by answering with a success message
    event.complete('success');
});
 
 
googlepay.on('shippingaddresschange', function(event) {
    var shippingAddress = event.shippingAddress;
   
   
    //create a Payment Request Details Update Object
    var newDetails = createPaymentRequestDetailsUpdateObject();
       
    event.updateWith(newDetails);
});
```

The Shipping Address Changed and Shipping Method Changed events require a response of updated details to present to the Shopper. This system expects the response to be in the format of a [Payment Request Details Update object](../reference/digital-river-payment-objects.md#payment-request-details-update-error-object).

#### Place the elements on the page

The following example shows how to place the elements on the page. For more information on placing elements on a page, see Google Pay example.

```javascript
if (googlepay.canMakePayment()) {
    googlepay.mount("googlepay-element");
    document.getElementById('googlepay-element').style.display = 'block';
}
```

#### Receive the source event and use the source

```javascript
googlepay.on('source', function(event) {
    var source = result.source;
  
    //pass the source to your back end for further processing. 
 
 
    //once verified that the source is created successfully, complete the Google Pay session by answering with a success message
    event.complete('success');
});
```

#### Google Pay example

The source event will surface a Source plus other details provided from Google Pay like the shopper's billing address, shipping address, and the contact information in the response.

{% tabs %}
{% tab title="Source example" %}
```javascript
{
    "clientId": "gc",
    "channelId": "drdod15",
    "liveMode": false,
    "id": "a8bc045d-5aa0-44e0-9082-63244af3685c",
    "clientSecret": "9864191e-7c43-4b6a-808d-312f049adfbb_addd191e-7c43-4b6a-808d-312f049adfbb",
    "type": "googlePay",
    "reusable": false,
    "owner": {
        "firstName": "John",
        "lastName": "Doe",
        "email": "jdoe@digitalriver.com",
        "address": {
            "line1": "10380 Bren Road W",
            "line2": "",
            "city": "Minnetonka",
            "state": "MN",
            "country": "US",
            "postalCode": "55343"
        }
    },
    "state": "chargeable",
    "creationIp": "67.216.237.4",
    "createdTime": "2019-04-26T16:28:55.763Z",
    "updatedTime": "2019-04-26T16:28:55.763Z",
    "flow": "standard",
    "googlePay": {
        "expirationMonth": 2,
        "expirationYear": 2022,
        "lastFourDigits": "1111",
        "paymentIdentifier": "13159976250000000000000500658103",
        "brand": "Visa"
    }
}
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Response example" %}
```javascript
{
    "error": null,
    "source": {
        "clientId": "gc",
        "channelId": "drdod15",
        "liveMode": false,
        "id": "9864191e-7c43-4b6a-808d-312f049adfbb",
    "clientSecret": "9864191e-7c43-4b6a-808d-312f049adfbb_addd191e-7c43-4b6a-808d-312f049adfbb",          
        "type": "googlePay",
        "reusable": false,
        "owner": {
            "firstName": "John",
            "lastName": "Doe",
            "email": "jdoe@digitalriver.com",
            "phoneNumber": "000-000-0000",
            "address": {
                "line1": "10380 Bren Road W",
                "line2": "",
                "city": "Minnetonka",
                "state": "MN",
                "country": "US",
                "postalCode": "55343"
            }
        },
        "state": "chargeable",
        "creationIp": "209.87.174.4",
        "createdTime": "2019-05-22T03:40:32.779Z",
        "updatedTime": "2019-05-22T03:40:32.779Z",
        "flow": "standard",
        "googlePay": {
            "expirationMonth": 2,
            "expirationYear": 2022,
            "paymentIdentifier": "13159976250000000000000500658103",
            "brand": "Visa",
            "lastFourDigits": "1111"
        }
    },
    "billingAddress": {
        "address": {
            "line1": "10380 Bren Road W",
            "line2": "",
            "city": "Minnetonka",
            "postalCode": "55343",
            "state": "MN",
            "country": "US"
        },
        "name": "John Doe",
        "firstName": "John",
        "lastName": "Doe",
        "phone": "+16519895326",
        "email": "jdoe@digitalriver.com"
    },
    "shippingAddress": {
        "name": "John Doe",
        "firstName": "John",
        "lastName": "Doe",
        "phone": "+16519895326",
        "email": "jdoe@digitalriver.com",
        "address": {
            "line1": "10380 Bren Road W",
            "line2": "",
            "city": "Minnetonka",
            "state": "MN",
            "country": "US",
            "postalCode": "55343"
        }
    },
    "contactInformation": {
        "name": "John Doe",
        "phone": "+16519895326",
        "email": "jdoe@digitalriver.com"
    },
    "elementType": "googlepay"
}
```
{% endtab %}
{% endtabs %}

### Step 2: Use the authorized source

Once authorized, you can use the source by [attaching it to a cart](../../../sources/#attaching-a-payment-method-to-an-order-or-cart) or [attaching it to a shopper](../../../sources/#attaching-a-payment-method-to-a-customer).

#### Option 1. Attach the source to a cart

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

#### Option 2. Attach the source to a shopper

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

#### Google Pay example

The following example shows how to place a Google Pay element on your page. Use this in conjunction with the [DigitalRiver.js reference guide](../reference/) to build your solution.

{% tabs %}
{% tab title="HTML" %}
```markup
<script src="https://js.digitalriverws.com/v1/DigitalRiver.js"></script>
<div id="googlepay-element"></div>
```
{% endtab %}
{% endtabs %}

```javascript
var digitalriver = new DigitalRiver('YOUR_API_KEY');
 
 
var googlePrData = getBasePrData();
var googlePayRequestData = digitalriver.paymentRequest(googlePrData);
 
var googlepay = digitalriver.createElement("googlepay", googlePayRequestData);
if (googlepay.canMakePayment()) {
    googlepay.mount("googlepay-element");
    document.getElementById('googlepay-element').style.display = 'block';
}
 
googlepay.on('source', function(event) {
    console.log("Received Event", event);
    console.log("GOT GOOGLE PAY SOURCE");
    event.complete('success');
 
    var source = event.source;
    console.log(source);
});
 
googlepay.on('shippingaddresschange', function(event) {
    console.log("Received Shipping Address Change Event", event);
 
    var shippingAddress = event.shippingAddress;
    console.log("Shipping Address", shippingAddress);
 
    var newDetails = getPrUpdateObject();
    console.log('Updating PR With', newDetails);
 
    event.updateWith(newDetails);
});
 
googlepay.on('shippingoptionchange', function(event) {
    console.log("Received Shipping Option Change Event", event);
 
    var shippingOption = event.shippingOption;
    console.log("Shipping Option", shippingOption);
 
    var newDetails = getPrUpdateObject();
    console.log('Updating PR With', newDetails);
 
    event.updateWith(newDetails);
});
 
googlepay.on('click', function(event) {
    console.log("Received Event", event);
});
 
function getBasePrData() {
    return {
        country: "US",
        currency: "USD",
        total: {
            label: "Demo Total",
            amount: 300
        },
        displayItems: [{
            amount: 100,
            label: "Item"
        }, {
            amount: 200,
            label: "Better Item"
        }],
        requestShipping: true,
        shippingOptions: [{
            id: "free-shipping",
            label: "Free Shipping",
            detail: "Arrives in 5 to 7 days",
            amount: 0
        }, {
            id: "overnight-shipping",
            label: "Overnight Shipping",
            detail: "Arrives in 5 to 7 days",
            amount: 1000
        }],
        style: {
            buttonType: "plain",
            buttonColor: "light-outline",
            buttonLanguage: "en"
        },
        waitOnClick: false
    };
}
 
function getPrUpdateObject() {
    return {
        "status": "success",
        "total": {
            "label": "New Total",
            "amount": 1020.10
        },
        "displayItems": [{
                "amount": 1000,
                "label": "Big Screen TV",
            },
            {
                "amount": 20.10,
                "label": "Shipping and Handling"
            }
        ],
        "shippingOptions": [{
            id: "free-shipping",
            label: "Free Shipping",
            detail: "Arrives in 5 to 7 days",
            amount: 0,
            selected: true
        }, {
            id: "overnight-shipping",
            label: "Overnight Shipping",
            detail: "Arrives in 5 to 7 days",
            amount: 1000
        }]
    }
}
```

## Supported markets

For information on supported markets and currencies for Drop-in and DigitalRiver.js, go to:&#x20;

* **Payment Method Guide:** [digitalriver.com/payment-method-guide](https://www.digitalriver.com/payment-method-guide/)
* **Country Guide:** [digitalriver.com/country-guide/](https://www.digitalriver.com/country-guide/)