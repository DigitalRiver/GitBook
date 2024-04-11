---
description: Learn how to configure Apple Pay for DigitalRiver.js with Elements.
---

# Configuring Apple Pay

If you're using [DigitalRiver.js with Elements](../), you can create an [Apple Pay](../../../supported-payment-methods/apple-pay.md) payment method for your app or website in three easy steps:

* [Step 1: Submit domain for Apple validation](apple-pay.md#step-1-submit-domain-for-apple-validation)
* [Step 2: Create an Apple Pay source using DigitalRiver.js](apple-pay.md#step-2-create-an-apple-pay-source-using-digitalriver-js)
* [Step 3: ​Use the authorized source](apple-pay.md#step-3-use-the-authorized-source)

## Step 1: Submit domain for Apple validation

For details on validating your domain with Apple, refer to [How to configure](../../../supported-payment-methods/apple-pay.md#how-to-configure) on the [Apple Pay](../../../supported-payment-methods/apple-pay.md#how-to-configure) page.

1. [Click to Download](https://drapi.io/docs/apple-pay/apple-developer-merchantid-domain-association) the `apple-developer-merchantid-domain-association` file.
2. Save the file to the following location on the domain where you want to offer Apple Pay: `/.well-known/apple-developer-merchantid-domain-association` Repeat this step for each additional domain where you want to offer Apple Pay. For example: `https://buy.mydomain.com/.well-known/apple-developer-merchantid-domain-association https://shop.mydomain.com/.well-known/apple-developer-merchantid-domain-association https://www.mydomain.com/.well-known/apple-developer-merchantid-domain-association` \
   \
   **Note**: You must serve the `apple-developer-merchantid-domain-association` file over HTTPS.
3. Contact your Digital River representative with the list of domains you want to register.

## Step 2: Create an Apple Pay source using DigitalRiver.js

To create an Apple Pay payment source, please follow the [DigitalRiver.js reference guide](../quick-start.md).‌

### Create an Apple Pay element

After setting up your library per the [DigitalRiver.js reference guide](../quick-start.md), create an Apple Pay element with any customizations you would like to apply.

{% code overflow="wrap" %}
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
{% endcode %}

### Configure the Apple Pay element to handle events

The Apple Pay element will surface events, giving you more information to facilitate what is happening within the Apple Pay experience.‌

These events include:

| Event                                                                                                                       | Triggered When                                                                                                                                            |
| --------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [ready](../../../../developer-resources/reference/elements/apple-pay-elements.md#ready)​                                    | The created element is loaded and ready to accept an update request.                                                                                      |
| ​[click](../../../../developer-resources/reference/elements/apple-pay-elements.md#click)​                                   | A shopper clicked the element's button.                                                                                                                   |
| ​[cancel](../../../../developer-resources/reference/elements/apple-pay-elements.md#cancel)​                                 | The customer has canceled the experience.                                                                                                                 |
| ​[shippingoptionchange](../../../../developer-resources/reference/elements/apple-pay-elements.md#shipping-option-change)​   | The customer has chosen a different shipping option than was previously selected. You should use this data to re-price your order totals (if applicable). |
| ​[shippingaddresschange](../../../../developer-resources/reference/elements/apple-pay-elements.md#shipping-address-change)​ | The customer has chosen a different address than was previously selected. You should use this data to re-price your order totals (if applicable).         |
| ​[source](../../../../developer-resources/reference/elements/apple-pay-elements.md#source)​                                 | The customer has authorized the payment and a source, and DigitalRiver.js returned associated data.                                                       |

{% hint style="info" %}
**Note**: To use Apple Pay, you must listen to, at minimum, the Shipping Address Changed and Source events.
{% endhint %}

{% code overflow="wrap" %}
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
{% endcode %}

The Shipping Address Changed and Shipping Method Changed events require a response of updated details to present to the Shopper. This system expects the response to be in the format of a [Payment Request Details Update object](../../../../developer-resources/reference/digital-river-payment-objects.md#payment-request-details-update-error-object).‌

### Place the elements on the page

The following example shows how to place the elements on the page. For more information on placing elements on a page, see the [Apple Pay example](apple-pay.md#apple-pay-example).

{% code overflow="wrap" %}
```javascript
if (applepay.canMakePayment()) {
    applepay.mount("applepay-element");
    document.getElementById('applepay-element').style.display = 'blocck';
}
```
{% endcode %}

### Apple Pay source and response examples

The source event will surface a Source plus other shopper details Apple Pay provides, like the billing address, shipping address, and contact information.

{% hint style="info" %}
The `address` object must contain [postal code](../../../../integration-options/checkouts/creating-checkouts/providing-address-information.md#postal-code-validations) and [state/province](../../../../integration-options/checkouts/creating-checkouts/providing-address-information.md#states-and-province-validations) data that [adheres to a standardized format](../../../../integration-options/checkouts/creating-checkouts/providing-address-information.md#postal-code-and-state-province-validations).
{% endhint %}

{% code title="Source example" overflow="wrap" %}
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
{% endcode %}

{% code title="Response example" overflow="wrap" %}
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
        "firstName": "John ",
        "lastName": "Doe",
        "phone": "+16519895326",
        "email": "john.doe@gmail.com"
    },
    "shippingAddress": {
        "name": "John Doe",
        "firstName": "John ",
        "lastName": "Doe",
        "phone": "+16519895326",
        "email": "john.doe@gmail.com",
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
        "email": "john.doe@gmail.com"
    },
    "elementType": "applePay"
}‌
```
{% endcode %}

## Step 3: Use the authorized source

Once authorized, you can use the source by [attaching it to a checkout](../../../payment-sources/using-the-source-identifier.md#attaching-sources-to-checkouts).

{% tabs %}
{% tab title="POST /checkouts/{id}" %}
{% code overflow="wrap" %}
```javascript
{
  "customerId": "5774321008",
  "sourceId"
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Apple Pay example

The following example shows placing an Apple Pay element on your page. Use this in conjunction with the [DigitalRiver.js reference guide](../quick-start.md) to build your solution.

{% tabs %}
{% tab title="HTML" %}
{% code overflow="wrap" %}
```markup
<script src="https://js.digitalriverws.com/v1/DigitalRiver.js"></script>
<div id="applepay-element"></div>
```
{% endcode %}
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Apple Pay example" %}
{% code overflow="wrap" %}
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
{% endcode %}
{% endtab %}
{% endtabs %}

## Testing Apple Pay

See [Testing standard payment methods](../../../../developer-resources/testing-scenarios.md#testing-standard-payment-methods) for testing instructions.
