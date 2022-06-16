---
description: >-
  Apple Pay provides a fast and secure shopping experience where the consumer
  can quickly and seamlessly checkout with their Apple Touch authentication
  without login details or credentials.
---

# Apple Pay

Digital River will support Apple Pay as a payment method on the payment service and DigitalRiver.js. Apple Pay is currently available to consumers in 21 countries and currently is supported only on IOS devices (iPhones, Macs, and so on).‌

You can find an example of integration [here](https://drh.img.digitalriver.com/DRHM/Storefront/Site/drdod15/pb/multimedia/applepay.html) (only viewable on Apple devices).

## Configuring Apple Pay for DigitalRiver.js

Create an Apple Pay payment method for your app or website in three easy steps:‌

* [Step 1: Submit domain for Apple validation](apple-pay.md#step-1-submit-domain-for-apple-validation)
* [Step 2: Create an Apple Pay source using DigitalRiver.js](apple-pay.md#step-2-create-an-apple-pay-source-using-digital-river-js)
* [Step 3: ​Use the authorized source](apple-pay.md#step-3-use-the-authorized-source)

### Step 1: Submit domain for Apple validation

To offer Apple Pay on your website, you need to validate your domain with Apple before you can accept transactions. To complete the validation:

1. [Click to Download](http://drapi.io/docs/apple-pay/apple-developer-merchantid-domain-association) the `apple-developer-merchantid-domain-association` file.
2. Save the file to the following location on the domain where you want to offer Apple Pay:\
   \
   `/.well-known/apple-developer-merchantid-domain-association`\
   \
   Repeat this step for each additional domain where you want to offer Apple Pay. For example:\
   \
   `https://buy.mydomain.com/.well-known/apple-developer-merchantid-domain-association` \
   `https://shop.mydomain.com/.well-known/apple-developer-merchantid-domain-association` \
   `https://www.mydomain.com/.well-known/apple-developer-merchantid-domain-association`\
   \
   **Note**: You must serve the `apple-developer-merchantid-domain-association` file over HTTPS.
3. Contact your Digital River representative with the list of domains you want to register.

### Step 2: Create an Apple Pay source using Digital River.js

‌To create an Apple Pay payment source, please follow the [DigitalRiver.js reference guide](../reference/).‌

#### Create an Apple Pay element

After setting up your library per the [DigitalRiver.js reference guide](../reference/), create an Apple Pay element with any customizations you would like to apply.

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
   
   
var applepay = digitalriver.createElement('applepay', paymentRequestData);
```

#### Configure the Apple Pay element to handle events

The Apple Pay element will surface events, which will give you more information to facilitate what is happening within the Apple Pay experience.‌

These events include:

| Event                                                                                          | Triggered When                                                                                                                                            |
| ---------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
|  [ready](../reference/elements/apple-pay-elements.md#ready)​                                   | The created element is loaded and ready to accept an update request.                                                                                      |
| ​[click​](../reference/elements/apple-pay-elements.md#click)                                   | A shopper clicked the element's button.                                                                                                                   |
| ​[cancel](../reference/elements/apple-pay-elements.md#cancel)​                                 | The customer has canceled the experience.                                                                                                                 |
| ​[shippingoptionchange](../reference/elements/apple-pay-elements.md#shipping-option-change)​   | The customer has chosen a different shipping option than was previously selected. You should use this data to re-price your order totals (if applicable). |
| ​[shippingaddresschange](../reference/elements/apple-pay-elements.md#shipping-address-change)​ | The customer has chosen a different address than was previously selected. You should use this data to re-price your order totals (if applicable).         |
| ​[source](../reference/elements/apple-pay-elements.md#source)​                                 | The customer has authorized the payment and a source, and DigitalRiver.js returned associated data.                                                       |

{% hint style="info" %}
**Note**: To use Apple Pay, you must listen to, at minimum, the Shipping Address Changed and Source events.
{% endhint %}

```javascript
applepay.on('source', function(event) {
    var source = result.source;
  
    //pass the source to your back end for further processing. 
 
 
    //once verified that the source is created successfully, complete the Apple Pay session by answering with a success message
    event.complete('success');
});
 
 
applepay.on('shippingaddresschange', function(event) {
    var shippingAddress = event.shippingAddress;
   
   
    //create a Payment Request Details Update Object
    var newDetails = createPaymentRequestDetailsUpdateObject();
       
    event.updateWith(newDetails);
});
```

The Shipping Address Changed and Shipping Method Changed events require a response of updated details to present to the Shopper. This system expects the response to be in the format of a [Payment Request Details Update object](../reference/digital-river-payment-objects.md#payment-request-details-update-error-object).‌

#### Place the elements on the page

The following example shows how to place the elements on the page. For more information on placing elements on a page, see the [Apple Pay example](apple-pay.md#apple-pay-example).

```javascript
if (applepay.canMakePayment()) {
    applepay.mount("applepay-element");
    document.getElementById('applepay-element').style.display = 'block';
}
```

#### Apple Pay source and response examples

The source event will surface a Source plus other details provided by Apple Pay, like the billing address, shipping address, and contact information of the shopper.

{% tabs %}
{% tab title="Source example" %}
```javascript
{
    "clientId": "gc",
    "channelId": "drdod15",
    "liveMode": false,
    "id": "ee1c11e4-b947-45a2-b9d7-429a1154cfff",
    "clientSecret": "ee1c11e4-b947-45a2-b9d7-429a1154cfff_b99c11e4-b947-45a2-b9d7-429a1154cfff",
    "type": "applePay",
    "reusable": false,
    "owner": {
        "firstName": "John",
        "lastName": "Doe",
        "email": "john.doe@gmail.com",
        "address": {
            "line1": "10380 Bren Rd W",
            "line2": "",
            "city": "Hopkins",
            "state": "MN",
            "country": "US",
            "postalCode": "55343"
        }
    },
    "currency": "USD",
    "state": "chargeable",
    "creationIp": "67.216.233.5",
    "createdTime": "2019-04-26T16:30:33.984Z",
    "updatedTime": "2019-04-26T16:30:33.984Z",
    "flow": "standard",
    "applePay": {}
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
        "id": "ee1c11e4-b947-45a2-b9d7-429a1154cfff",
        "clientSecret": "ee1c11e4-b947-45a2-b9d7-429a1154cfff_b99c11e4-b947-45a2-b9d7-429a1154cfff",
        "type": "applePay",
        "reusable": false,
        "owner": {
            "firstName": "John",
            "lastName": "Doe",
            "email": "john.doe@gmail.com",
            "address": {
                "line1": "10380 Bren Rd W",
                "line2": "",
                "city": "Hopkins",
                "state": "MN",
                "country": "US",
                "postalCode": "55343"
            }
        },
        "currency": "USD",
        "state": "chargeable",
        "creationIp": "67.216.233.5",
        "createdTime": "2019-04-26T16:30:33.984Z",
        "updatedTime": "2019-04-26T16:30:33.984Z",
        "flow": "standard",
        "applePay": {}
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
        "phone": "+15559895326",
        "email": "jdoe@digitalriver.com"
    },
    "shippingAddress": {
        "name": "John Doe",
        "firstName": "John",
        "lastName": "Doe",
        "phone": "+15559895326",
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
        "phone": "+15559895326",
        "email": "test@digitalriver.com"
    },
    "elementType": "applePay"
}
```
{% endtab %}
{% endtabs %}

### Step 3: Use the authorized source

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

### Apple Pay example

The following example shows how to place an Apple Pay element on your page. Use this in conjunction with the [DigitalRiver.js reference guide](../reference/) to build your solution.HTML

{% tabs %}
{% tab title="HTML" %}
```markup
<script src="https://js.digitalriverws.com/v1/DigitalRiver.js"></script>
<div id="applepay-element"></div>
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Apple Pay example" %}
```javascript
var digitalriver = new DigitalRiver('YOUR_API_KEY');
 
 
var applePrData = getBasePrData();
var applePayRequestData = digitalriver.paymentRequest(applePrData);
 
var applepay = digitalriver.createElement("applepay", applePayRequestData);
if (applepay.canMakePayment()) {
    applepay.mount("applepay-element");
    document.getElementById('applepay-element').style.display = 'block';
}
 
applepay.on('source', function(event) {
    console.log("Received Event", event);
    console.log("GOT APPLE PAY SOURCE ID");
 
    event.complete('success');
 
    var source = event.source;
    console.log(source);
});
 
applepay.on('shippingaddresschange', function(event) {
    console.log("Received Shipping Address Change Event", event);
    var shippingAddress = event.shippingAddress;
    console.log("Shipping Address", shippingAddress);
 
    var newDetails = getPrUpdateObject();
    console.log('Updating PR With', newDetails);
    event.updateWith(newDetails);
});
 
applepay.on('cancel', function(event) {
    console.log("Received Event", event);
    console.log(event);
});
 
applepay.on('shippingoptionchange', function(event) {
    console.log("Received Shipping Option Change Event", event);
    var shippingOption = event.shippingOption;
    console.log("Shipping Option", shippingOption);
 
    var newDetails = getPrUpdateObject();
    console.log('Updating PR With', newDetails);
    event.updateWith(newDetails);
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
{% endtab %}
{% endtabs %}

## Supported markets <a href="#supported-geographies" id="supported-geographies"></a>

For information on supported markets and currencies for Drop-in and DigitalRiver.js, go to:&#x20;

* **Payment Method Guide:** [digitalriver.com/payment-method-guide](https://www.digitalriver.com/payment-method-guide/)
* **Country Guide:** [digitalriver.com/country-guide/](https://www.digitalriver.com/country-guide/)

