---
description: Gain a basic understanding of how to add a Prebuilt Checkout to your site
---

# Implementing a Prebuilt Checkout

Prebuilt Checkout is a customizable checkout experience that allows you to connect an upstream commerce system with Digital River's [local pricing](offering-local-pricing.md), [logistics](using-a-shipping-endpoint.md), [subscriptions](processing-subscription-acquisitions.md), [payment](../../payments/payment-integrations-1/), fraud detection, tax exemption, and disclosure services.

The Prebuilt Checkout solution reduces the complexity of integrating with the [Digital River APIs](https://www.digitalriver.com/docs/digital-river-api-reference/) and our front-end libraries, thereby shortening your time to deployment.

![](<../../.gitbook/assets/image (56).png>)

Once customers [build a cart](drop-in-checkout.md#building-a-cart) and [initiate checkout](drop-in-checkout.md#initiating-checkout), a Prebuilt Checkout integration needs to:

* [Define a checkout-session request](drop-in-checkout.md#configuring-a-checkout-session)
* [Create a checkout-session](drop-in-checkout.md#creating-a-checkout-session)
* Use the [checkout-session identifier](drop-in-checkout.md#the-checkout-session-identifier) to [create a Prebuilt Checkout](drop-in-checkout.md#creating-a-drop-in-checkout-modal)
* [Handle the checkout session order created event](drop-in-checkout.md#handling-the-checkout-session-order-created-event)

## Building a cart

During the early stages of an ecommerce transaction, customers land on your storefront, review products and build a cart. Unless you [engage our local pricing service](offering-local-pricing.md), Digital River is typically not involved in these early pre-checkout interactions. However, once customers [initiate checkout](drop-in-checkout.md#initiating-checkout), you'll need to start interacting with Prebuilt Checkout.

## Initiating checkout

Add a click event listener to each checkout button on your site. Handle the event by [defining a checkout-session request](drop-in-checkout.md#configuring-a-checkout-session), passing that request data to your back-end server, and then securely [sending a create checkout-session request](drop-in-checkout.md#creating-a-checkout-session).

Digital River returns a unique [checkout-session identifier](drop-in-checkout.md#the-checkout-session-identifier) that you must pass, along with an optional [configuration object](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/configuring-prebuilt-checkout/), to a [create checkout window method](drop-in-checkout.md#creating-a-drop-in-checkout-modal) on your front-end.

## Configuring a checkout-session

For details, refer to the [Checkout-sessions](../../developer-resources/digital-river-api-reference/checkout-sessions.md) page.

## Creating a checkout-session

To create a checkout-session, send your [secret API key](../../developer-resources/api-structure.md#confidential-keys) and [request payload](../../developer-resources/digital-river-api-reference/checkout-sessions.md) in a [`POST /drop-in/checkout-sessions`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createDropInCheckoutSession).

```
curl --location --request POST 'https://api.digitalriver.com/drop-in/checkout-sessions' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer <secret API key>' \
...
--data-raw '{
    "currency": "USD",
    "customerType": "individual",
    "taxInclusive": false,
    "items": [
        {
            "skuId": "b535d75a-a6ee-4f63-be4d-c2e2537efec7",
            "quantity": 1,
            "price": 5
        }
    ],
    "shipFrom": {
        "address": {
            "line1": "10380 Bren Rd W",
            "line2": "",
            "city": "Minnetonka",
            "postalCode": "55129",
            "state": "MN",
            "country": "US"
        }
    },
    "options": {
        "shippingMethods": [
            {
                "amount": 5,
                "description": "standard",
                "serviceLevel": "SG"
            },
            {
                "amount": 15,
                "description": "next day",
                "serviceLevel": "ND"
            }
        ],
        "addresses": [
            {
                "address": {
                    "line1": "10380 Bren Rd W",
                    "line2": "line 2",
                    "city": "Minnetonka",
                    "postalCode": "55129",
                    "state": "MN",
                    "country": "US"
                },
                "name": "John Smith",
                "phone": "952-111-1111",
                "email": "jsmith@digitalriver.com",
                "organization": "Digital River",
                "additionalAddressInfo": {
                    "neighborhood": "Centro",
                    "division": "営業部",
                    "phoneticName": "ヤマダ タロ"
                }
            },
            {
                "address": {
                    "line1": "62 Trinity Crescent",
                    "line2": "",
                    "city": "WHITCHURCH",
                    "postalCode": "CF4 9ZB",
                    "country": "GB"
                },
                "name": "Anna Brawner",
                "phone": "07854319925",
                "email": "anna@dr.com",
                "organization": "Digital River",
                "additionalAddressInfo": {
                    "neighborhood": "Centro",
                    "division": "営業部",
                    "phoneticName": "ヤマダ タロ"
                }
            }
        ]
    }
}'
```

## The checkout-session identifier

A `201 Created` response to your [create checkout-session request](drop-in-checkout.md#creating-a-checkout-session) contains a unique `id`.

```json
{
    "id": "eb3b9cc3-d068-4300-9488-c88c0341b5db"
    ...
}
```

Use this checkout-session identifier to [create a Prebuilt Checkout](drop-in-checkout.md#creating-a-drop-in-checkout-modal).

## Creating a Prebuilt Checkout <a href="#creating-a-drop-in-checkout-modal" id="creating-a-drop-in-checkout-modal"></a>

Make sure you [include DigitalRiverCheckout.js](../../developer-resources/digitalrivercheckout.js-reference/including-digitalrivercheckout.js.md) by adding the following `script` to your checkout page.

```html
<script src="https://checkout.digitalriverws.com/v1/DigitalRiverCheckout.js"></script>
```

Use your [public API key](../../developer-resources/api-structure.md#public-keys) to create a [`DigitalRiverCheckout` object](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/).

Next, you'll most likely want to [build a configuration object](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/configuring-prebuilt-checkout/).&#x20;

Then, depending on whether you'd like Prebuilt Checkout to display in a [modal](https://en.wikipedia.org/wiki/Modal\_window) or an [iframe](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/iframe), pass that object and the [checkout session identifier](drop-in-checkout.md#the-checkout-session-identifier) to either [`createModal()`](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/#create-an-instance-of-the-checkout-modal) or [`embed()`](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/#embed-checkoutsessionid-config), respectively.&#x20;

{% tabs %}
{% tab title="Modal" %}
```javascript
document.getElementById('YOUR_CHECKOUT_BUTTON_ID').addEventListener('click', async (event) => {
  
   //Invokes a client defined function that creates a checkout session
   const checkoutSessionId = await createCheckoutSession();
  
   // Creates a Prebuilt Checkout and displays it in a modal window
   drCheckout.createModal(checkoutSessionId, config);
});
```
{% endtab %}

{% tab title="Inline Frame" %}
```javascript
document.getElementById('YOUR_CHECKOUT_BUTTON_ID').addEventListener('click', async (event) => {
  
   //Invokes a client defined function that creates a checkout session
   const checkoutSessionId = await createCheckoutSession();
  
   // Creates a Prebuilt Checkout and displays it in an iframe
   drCheckout.embed(checkoutSessionId, config);
});
```
{% endtab %}
{% endtabs %}

## Prebuilt Checkout window <a href="#drop-in-checkout-modal-window" id="drop-in-checkout-modal-window"></a>

After [`createModal()`](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/#create-an-instance-of-the-checkout-modal) or [`embed()`](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/#embed-checkoutsessionid-config) is invoked, the checkout window opens and [`onReady`](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/configuring-prebuilt-checkout/#onready) executes.&#x20;

Depending on how the [checkout-session](../../developer-resources/digital-river-api-reference/checkout-sessions.md) is configured, the experience takes customers through various stages:

* [Name and address collection stage](drop-in-checkout.md#name-and-address)
* [Shipping choice collection stage](drop-in-checkout.md#shipping-choice)
* [Tax identification number collection stage](drop-in-checkout.md#tax-identifiers)
* [Payment stage](drop-in-checkout.md#payment)
* [Order confirmation stage](drop-in-checkout.md#order-confirmation)

### Name and address stage <a href="#name-and-address" id="name-and-address"></a>

In this stage, customers are always required to provide their name, phone number, email and billing address.

Other required inputs, and available options, depend on whether the checkout involves:

* [Physical and/or digital products](drop-in-checkout.md#digital-and-physical-products)
* [Registered customers](drop-in-checkout.md#registered-customers)
* [Customers conducting a B2B transaction](drop-in-checkout.md#business-to-business-transactions)

Once customers successfully submit the required information, [`onAddressComplete`](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/configuring-prebuilt-checkout/#onaddresscomplete) executes.

#### Digital and physical products

If any [`items[]`](../../developer-resources/digital-river-api-reference/checkout-sessions.md#product-data) in the [checkout-session](../../developer-resources/digital-river-api-reference/checkout-sessions.md) represent [physical products](../../product-management/skus.md#how-products-are-classified-as-physical-or-digital), customers are prompted for shipping information. Once validated, Digital River uses it to populate the [checkout-session's](../../developer-resources/digital-river-api-reference/checkout-sessions.md) `shipTo` and `billTo`.&#x20;

{% hint style="info" %}
Customers are given the option to input different billing information during the [payment stage](drop-in-checkout.md#payment).&#x20;
{% endhint %}

In checkouts that only contain [digital products](../../product-management/skus.md#how-products-are-classified-as-physical-or-digital), the experience doesn’t ask for shipping details. Instead, it simply prompts customers for billing information.

{% tabs %}
{% tab title="Physical products" %}
![](<../../.gitbook/assets/Shipping information (guest customer).png>)
{% endtab %}

{% tab title="Digital only products" %}
![](<../../.gitbook/assets/Billing information (guest customer) (1).png>)
{% endtab %}
{% endtabs %}

#### Registered customers

If you send [`customerId`](../../developer-resources/digital-river-api-reference/checkout-sessions.md#customer-identifier) in the [create checkout-session request](drop-in-checkout.md#creating-a-checkout-session), customers are given the option to save their shipping and billing information for use in future checkouts. Additionally, if you pass [`options.addresses[]`](../../developer-resources/digital-river-api-reference/checkout-sessions.md#saved-addresses), customers are presented with these saved addresses for convenience purposes.

{% tabs %}
{% tab title="Save address option" %}
<figure><img src="../../.gitbook/assets/image (16) (1).png" alt=""><figcaption></figcaption></figure>
{% endtab %}

{% tab title="Saved addresses" %}
<figure><img src="../../.gitbook/assets/image (86).png" alt=""><figcaption></figcaption></figure>
{% endtab %}
{% endtabs %}

#### Business to business transactions

If the [checkout-session's](../../developer-resources/digital-river-api-reference/checkout-sessions.md) [`customerType`](../../developer-resources/digital-river-api-reference/checkout-sessions.md#customer-type) is `business`, then customers must provide their company's name when entering both shipping and billing information.

{% tabs %}
{% tab title="Shipping information" %}
<figure><img src="../../.gitbook/assets/image (64).png" alt=""><figcaption></figcaption></figure>
{% endtab %}

{% tab title="Billing information" %}
<figure><img src="../../.gitbook/assets/image (44).png" alt=""><figcaption></figcaption></figure>
{% endtab %}
{% endtabs %}

If you activate the [auto collect customer type ](../../developer-resources/digital-river-api-reference/checkout-sessions.md#auto-collect-customer-type)feature, then customers are shown a checkbox that asks them whether they’d like to make the purchase on behalf of a business.&#x20;

If [`items[]`](../../developer-resources/digital-river-api-reference/checkout-sessions.md#product-data) contains physical goods, then this toggle is displayed in the shipping information form. Otherwise, when [`items[]`](../../developer-resources/digital-river-api-reference/checkout-sessions.md#product-data) are all digital, customers are presented with this option while supplying their billing information.

<figure><img src="../../.gitbook/assets/Auto collect 4.png" alt=""><figcaption></figcaption></figure>

### Shipping choice stage <a href="#shipping-choice" id="shipping-choice"></a>

In transactions that contain [physical products](../../product-management/skus.md#how-products-are-classified-as-physical-or-digital), the experience next prompts the user to make a shipping choice. For each [`options.shippingMethods[]`](../../developer-resources/digital-river-api-reference/checkout-sessions.md#shipping-methods) in the [checkout-session](../../developer-resources/digital-river-api-reference/checkout-sessions.md), customers are always shown its `description` and `amount`.

![](<../../.gitbook/assets/Shipping choice (static).png>)

Once customers input their shipping choice, [`onDeliveryComplete`](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/configuring-prebuilt-checkout/#ondeliverycomplete) executes.

### Tax identifiers stage <a href="#tax-identifiers" id="tax-identifiers"></a>

In [applicable checkouts](../checkouts/creating-checkouts/tax-identifiers.md#supported-tax-identifiers), the experience prompts the customer for a tax identification number.

In guest checkouts, customers can enter a tax identifier but are not given the option to save the value to their account.

![](<../../.gitbook/assets/tax identifiers (guest customer) (1).png>)

[Registered customers](../../developer-resources/digital-river-api-reference/checkout-sessions.md#registered-customers) with applicable, saved tax identifiers can either select one of the values presented to them or enter a new one.

![](<../../.gitbook/assets/tax identifiers (registered customer) (1).png>)

Registered customers who have no stored, transaction-applicable tax identifiers can save a new value for use in future checkouts. If they select this option, Digital River saves the tax identifier to the [customer’s record](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Customers).

![](<../../.gitbook/assets/tax identifiers (registered customer with save for later option).png>)

In [countries that require tax identifiers](../checkouts/creating-checkouts/tax-identifiers.md#supported-tax-identifiers), customers must enter a value before proceeding to the [payment stage](drop-in-checkout.md#payment).&#x20;

### Payment stage <a href="#payment" id="payment"></a>

In the payment collection stage, customers are only shown [payment methods](../../payments/supported-payment-methods/) that are appropriate to the transaction. Depending on how you configure the [checkout-session](../../developer-resources/digital-river-api-reference/checkout-sessions.md) and on your [Digital River Dashboard](../../administration/dashboard/) settings, the experience can also:

* [Present saved payment methods](drop-in-checkout.md#saved-payment-methods)
* [Save payment methods for future purchases](drop-in-checkout.md#save-a-payment-method-for-future-purchases)
* [Display custom consents](drop-in-checkout.md#custom-consents).

Once customers provide payment, agree to the terms, and successfully submit the order, [`onCheckoutComplete`](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/configuring-prebuilt-checkout/#oncheckoutcomplete) is called.&#x20;

#### Saved payment methods

If you pass a [`customerId`](../../developer-resources/digital-river-api-reference/checkout-sessions.md#customer-identifier) in the [create checkout session request](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createDropInCheckoutSession), we retrieve and display any transaction-applicable payment [`sources[]`](../../payments/payment-sources/) that are saved to the referenced [customer](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Customers).&#x20;

![](<../../.gitbook/assets/image (19) (1).png>)

#### Save a payment method for future purchases

Prebuilt Checkout can ask customers whether they'd like to save a payment method for future purchases.&#x20;

To activate this feature, you must pass [`customerId`](../../developer-resources/digital-river-api-reference/checkout-sessions.md#customer-identifier) in the [create checkout session request](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions/operation/createDropInCheckoutSession).&#x20;

{% hint style="info" %}
If the resource you reference doesn't exist in your account, then Digital River creates a new [customer](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Customers) and assigns it the identifier you passed.&#x20;
{% endhint %}

If the payment method selected by customers supports [reusability](../../payments/payment-sources/#reusable-or-single-use), then customers are asked whether they'd like to save it for future purchases. If they opt to do so, then, after Digital River creates the [source](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources), we save it to that [customer](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Customers).&#x20;

<figure><img src="../../.gitbook/assets/Save for future.png" alt=""><figcaption></figcaption></figure>

#### Custom consents

For each displayed payment method, Prebuilt Checkout presents users with the terms of sale and privacy policy of the designated [selling entity](../checkouts/creating-checkouts/selling-entities.md).&#x20;

If you [save your own consents in the Dashboard](../../administration/dashboard/settings/prebuilt-checkout.md#create-a-prebuilt-checkout-configuration), then they are appended to Digital River's disclosures. Customers must accept all these terms and disclosures before they are allowed to complete the purchase. &#x20;

{% hint style="info" %}
To [determine what disclosures customers accepted](drop-in-checkout.md#determining-what-disclosures-customers-accepted), you can [configure a webhook](../../order-management/events-and-webhooks-1/webhooks/creating-a-webhook.md) to listen for the [event](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events) with a [`type`](../../order-management/events-and-webhooks-1/events-1/#event-types) of [`checkout_session.order.created`](../../order-management/events-and-webhooks-1/events-1/event-types.md#checkout\_session.order.created).
{% endhint %}

{% tabs %}
{% tab title="Digital River only disclosures" %}
If you don't [save customized consents in Dashboard](../../administration/dashboard/settings/prebuilt-checkout.md#create-a-prebuilt-checkout-configuration), then Prebuilt Checkout only displays Digital River's disclosures.

![](<../../.gitbook/assets/image (37).png>)
{% endtab %}

{% tab title="Combined disclosures" %}
If you [save consents in Dashboard](../../administration/dashboard/settings/prebuilt-checkout.md#create-a-prebuilt-checkout-configuration), then Prebuilt Checkout displays Digital River's disclosures, along with yours as well.

![](<../../.gitbook/assets/image (28).png>)
{% endtab %}
{% endtabs %}

### Order confirmation stage <a href="#order-confirmation" id="order-confirmation"></a>

There are a variety of ways to [configure the order confirmation stage](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/configuring-prebuilt-checkout/#customize-order-confirmation). The following is an example of the default option.

<figure><img src="../../.gitbook/assets/order confirmation (1).png" alt=""><figcaption></figcaption></figure>
