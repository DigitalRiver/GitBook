---
description: Create a payment form using DigitalRiver.js.
---

# Elements integration guide



Use DigitalRiver.js to create a payment form that securely collects sensitive payment details.

To see a custom payment form example, go to [Payment form example](https://drh.img.digitalriver.com/DRHM/Storefront/Site/drdod15/pb/multimedia/quick-start-form.html).

To populate the fields in this example, click Populate Sample Data In Form. Then enter `4444222233331111` in the Credit Card field, `10/23` in the Expiration field, and `123` in the CVV field, and click Create Credit Card Source.

Integrate the DigitalRiver.js into your app or website in four easy steps:

1. [Include DigitalRiver.js on your page](quick-start.md#step-1.-include-digitalriver.js-on-your-page).
2. [Create your payment form](quick-start.md#step-2.-create-your-payment-form).
3. [Create and embed elements](quick-start.md#step-3.-create-and-embed-elements).
4. [Use DigitalRiver.js to create a payment source](quick-start.md#step-4.-use-digitalriver.js-to-create-a-payment-source).

## Step 1. Include DigitalRiver.js on your page

To use DigitalRiver.js as part of your experience, you must include the library and your API key. The key shown in the following example is your public API key. The DigitalRiver.js `digitalriver.createSource()` or `digitalriver.createElement()` methods use the `var` that you assigned.

{% code title="HTML" overflow="wrap" %}
```markup
<script src="https://js.digitalriverws.com/v1/DigitalRiver.js"></script>
 
 
//Set Your API Key and Start DigitalRiver.js
var digitalriver = new DigitalRiver('YOUR_PUBLIC_API_KEY');
```
{% endcode %}

## Step 2. Create your payment form

DigitalRiver.js provides and hosts HTML elements that you can place in your payments form to collect credit card details securely. You can seamlessly integrate these elements into an outside-hosted experience.

{% code title="HTML" overflow="wrap" %}
```markup
<form id="payment-form">
    <div class="row">
        <label for="card-number">Credit Card</label>
        <div id="card-number" class="field"></div>
 
 
        <label for="card-expiration">Credit Card Expiration</label>
        <div id="card-expiration" class="field"></div>
 
 
        <label for="card-security-code">Credit Card Security Code</label>
        <div id="card-security-code" class="field"></div>
 
 
        <div id="errors"></div>
    </div>
</form>
```
{% endcode %}

## Step 3. Create and embed elements

Use the DigitalRiver.js library to [create ](../../../general-resources/reference/digitalriver-object.md#creating-elements)and [mount ](../../../general-resources/reference/elements/#element.mount)an element to the container created in [step 2](quick-start.md#step-2.-create-your-payment-form).

{% code title="HTML" overflow="wrap" %}
```markup
var options = {
    style: {
        base: {
            color: "#fff",
            fontFamily: "Arial, Helvetica, sans-serif",
            fontSize: "16px",
        }
    }
}
 
 
//Create your Card Number element
var cardNumber = digitalriver.createElement('cardnumber', options);
 
 
//Place the Card Number element within the container created above.
cardNumber.mount('card-number');
```
{% endcode %}

Follow the same pattern for additional credit card fields.

{% code title="HTML" overflow="wrap" %}
```markup
//Create your Card Expiration element
var cardExpiration = digitalriver.createElement('cardexpiration', options);
 
 
//Place the Card Expiration element within the container created above.
cardExpiration.mount('card-expiration');
 
 
//Create your Card Security Code element
var cardSecurityCode = digitalriver.createElement('cardcvv', options);
 
//Place the Card Security Code element within the container created above.
cardSecurityCode.mount('card-security-code');
```
{% endcode %}

## Step 4. Use DigitalRiver.js to create a payment source

Digital River securely transmits credit card details captured by DigitalRiver.js for tokenization. You can use these payment sources in downstream API calls to place orders or save credit cards for later purchases.

Create an event handler to interact with the DigitalRiver.js library on submit and then create a payment source. Use the [`createSource()`](../../../general-resources/reference/digitalriver-object.md#creating-sources) method to tokenize the customer's details and payment information.

{% hint style="info" %}
**Prerequisite**:  To create a Payment Source for a credit card, you must either know or capture the billing address information for the entered credit card. The `createSource()` method submits this information and uses it to create a payment source.
{% endhint %}

{% code title="HTML" overflow="wrap" %}
```markup
// Create a token or display an error when submitting the form.
    var paymentForm = document.getElementById('payment-form');
 
    paymentForm.addEventListener('submit', function(event) {
        event.preventDefault();
 
        var payload = {
          "type": "creditCard",
          "owner": {
                firstName: document.getElementById('firstName').value,
                lastName: document.getElementById('lastName').value,
                email: document.getElementById('email').value,
                address: {
                    line1: document.getElementById('address').value,
                    line2: document.getElementById('address2').value,
                    city: document.getElementById('city').value,
                    state: document.getElementById('state').value,
                    postalCode: document.getElementById('zip').value,
                    country: document.getElementById('country').value
                }
            }
        }  
     
        digitalriver.createSource(cardNumber, payload).then(function(result) {
 
            if(result.error) {
                //Something went wrong, display the error message to the customer
                handleErrors(result.error.message);
            } else {
                //Success! You can now send the token to your server for use in downstream API calls.
                sendToMyServer(result.source);
            }
        });
    });
```
{% endcode %}

