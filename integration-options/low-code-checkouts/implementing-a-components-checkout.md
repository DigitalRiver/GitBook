---
description: Acquire a basic understanding of how to integrate components
---

# Implementing a Components checkout

[Components](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/components/) are a [low-code checkout option](./) that consist of UI building blocks. They allow you to create customized checkout flows that connect to Digital River's address validation, [logistics](../../using-our-services/global-logistics.md), [local pricing](../../using-our-services/local-pricing.md), [payment processing](../../payments/payment-integrations-1/), [subscription](../../using-our-services/subscriptions.md), fraud detection, tax computation, and compliance services.&#x20;

[Components](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/components/) make it even easier to integrate with Digital River, reducing the amount of time you spend launching and managing your solution.

You can use all of the [available components](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/components/#supported-component-types) together to create traditional checkout flows. Alternatively, you might decide to use them selectively to construct specialized flows. For example, by pairing the [wallet component](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/components/wallet-component.md) with the [compliance component](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/components/compliance-component.md), you can offer customers an expedited checkout experience.&#x20;

On this page, you'll find information on:

* [Building a cart and initiating checkout](implementing-a-components-checkout.md#building-a-cart-and-initiating-checkout)&#x20;
* [Designing the checkout experience](implementing-a-components-checkout.md#designing-the-checkout-experience)
* [Executing a components checkout](implementing-a-components-checkout.md#executing-a-components-checkout)
* [Handling front-end events](implementing-a-components-checkout.md#handling-front-end-events)
* [Controlling the flow of the checkout](implementing-a-components-checkout.md#controlling-the-checkout-flow)
* [Submitting data collected by components](implementing-a-components-checkout.md#submitting-components)

After customers successfully complete the checkout process, your application also needs to [handle completed checkout-sessions](handling-completed-checkout-sessions.md).

## Building a cart and initiating checkout

During the early stages of an e-commerce transaction, customers land on your storefront, review products and build a cart. Unless you're engaging our [local pricing service](../../using-our-services/local-pricing.md), Digital River is typically not involved in these pre-checkout interactions. However, once customers initiate checkout, you'll need to start interacting with [components](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/components/).&#x20;

## Designing the checkout experience

For each component that you implement, your DOM needs to contain a unique HTML element to display it.&#x20;

```html
...
<div id="address-container" style="display: block"></div>
<div id="shipping-container" style="display: block"></div>
<div id="tax-identifier-container" style="display: block"></div>
<div id="payment-container" style="display: block"></div>
<div id="wallet-container" style="display: block"></div>
<div id="compliance-container" style="display: block"></div>
<div id="order-summary-container" style="display: block"></div>
<div>
    <div>
        <button id="previousButton" onclick="onPreviousButtonClick()">Previous</button>
    </div>
    <div>
        <button id="nextButton" onclick="onNextButtonClick()">Next</button>
    </div>
</div>
<div id="order-confirmation-container" style="display: none"></div>
...

```

The following example uses all of the [available components](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/components/#supported-component-types), but how you design your experience is highly customizable.

{% tabs %}
{% tab title="Address collection stage" %}
<figure><img src="../../.gitbook/assets/Address collection stage - web (2).png" alt=""><figcaption></figcaption></figure>
{% endtab %}

{% tab title="Shipping choice collection stage" %}
<figure><img src="../../.gitbook/assets/Shipping choice collection stage - web (4).png" alt=""><figcaption></figcaption></figure>
{% endtab %}

{% tab title="Tax identifier collection stage" %}
<figure><img src="../../.gitbook/assets/Tax id collection stage.jpg" alt=""><figcaption></figcaption></figure>
{% endtab %}

{% tab title="e-invoice collection stage" %}
<figure><img src="../../.gitbook/assets/Invoice collection stage.png" alt=""><figcaption></figcaption></figure>
{% endtab %}

{% tab title="Payment collection stage" %}
<figure><img src="../../.gitbook/assets/Payment collection stage - web.jpg" alt=""><figcaption></figcaption></figure>
{% endtab %}

{% tab title="Order confirmation stage" %}
![](<../../.gitbook/assets/Thank you stage - web.png>)
{% endtab %}
{% endtabs %}

<figure><img src="../../.gitbook/assets/Key (2).png" alt="" width="375"><figcaption></figcaption></figure>

If you implement multiple components that accept customer input, such as [address](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/components/address-component.md), [shipping](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/components/shipping-component.md), and [payment](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/components/payment-component.md), your experience should also contain buttons, or some other type of navigational control, that allows customers to move the checkout process forward and backward. These button's click events should activate your [checkout flow control](implementing-a-components-checkout.md#controlling-the-checkout-flow) functionality.

## Executing a components checkout

On your checkout page, you should:

* [Add the necessary scripts and style sheets](implementing-a-components-checkout.md#add-scripts-and-style-sheets)
* [Create a Digital River Checkout object](implementing-a-components-checkout.md#create-a-digital-river-checkout-object)
* [Invoke a custom-built function that initializes components](implementing-a-components-checkout.md#initialize-components)

### Add scripts and style sheets

In the `head` of your `html`, [add the DigitalRiverCheckout.js](../../developer-resources/digitalrivercheckout.js-reference/including-digitalrivercheckout.js.md) script. If you'd like, you can also include a `link` to the `DigitalRiver.css` style sheet.&#x20;

```html
<head>
    <title>Checkout Page</title>
    <script defer="defer" src="https://checkout.digitalriverws.com/v1/DigitalRiverCheckout.js"></script>
    <link rel="stylesheet" href="https://js.digitalriverws.com/v1/css/DigitalRiver.css" type="text/css"/>
</head>
```

### Create a Digital River Checkout object

Use your [public API key](../../administration/dashboard/developers/api-keys/) to [create a `DigitalCheckoutRiver` object](../../developer-resources/digitalrivercheckout.js-reference/initializing-digitalrivercheckout.js/).

```javascript
let digitalRiverCheckout = new DigitalRiverCheckout("YOUR_PUBLIC_API_KEY");
```

### Initialize components

When your checkout page loads, invoke an asynchronous function that initializes components.&#x20;

```javascript
...
initializeComponents();
...
```

The [async function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async\_function) you implement should:

* [Build a `components()` configuration object](implementing-a-components-checkout.md#build-a-configuration-object)
* [Pass that object to `components()`](implementing-a-components-checkout.md#create-the-components-object)
* [Create each individual component that you want to use](implementing-a-components-checkout.md#create-individual-components)
* [Mount each of those components](implementing-a-components-checkout.md#mount-individual-components)

```javascript
async function initializeComponents() {
    //Build a configuration object
    const configuration = {
        checkoutSessionId: await createComponentsCheckoutSession(),
        onReady: function (data) {
            //Handle event
        },
        onChange: function (data) {
            //Handle event
        },
        onSuccess: function (data) {
            //Handle event
        }
    }
    //Create components
    let components;
    components = digitalRiverCheckout.components(configuration);
    
    //Create the individual components
    paymentComponent = components.createComponent('payment');
    shippingComponent = components.createComponent('shipping');
    addressComponent = components.createComponent('address');
    walletComponent = components.createComponent('wallet');
    thankYouComponent = components.createComponent('thankyou');
    complianceComponent = components.createComponent('compliance');
    orderSummaryComponent = components.createComponent('ordersummary');
    
    //Mount the individual components
    paymentComponent.mount('payment-container');
    shippingComponent.mount('shipping-container');
    addressComponent.mount('address-container');
    walletComponent.mount('wallet-container');
    thankYouComponent.mount('order-confirmation-container');
    complianceComponent.mount('compliance-container');
    orderSummaryComponent.mount('order-summary-container');
}
```

#### Build a configuration object

To set `checkoutSessionId` in the [components configuration object](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/components/configuring-components.md), you should invoke an asynchronous function, wrapped by your [initialize components function](implementing-a-components-checkout.md#initialize-components), that defines a [checkout-session](../../developer-resources/digital-river-api-reference/checkout-sessions.md) on your front-end and then passes that data to your server so that it can [submit the create request](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions/operation/createDropInCheckoutSession).&#x20;

Alternatively, before loading your checkout page, you could define and create a [checkout-session](../../developer-resources/digital-river-api-reference/checkout-sessions.md) completely server-side. &#x20;

In either case, the function you implement needs to return the checkout-session's `id`.&#x20;

```javascript
function createComponentsCheckoutSession() {
  //Creates checkout-session
  //Returns checkout-session identifier
}
```

In the configuration object, you'll also need to define how you want to [handle callback methods](implementing-a-components-checkout.md#handling-front-end-events).&#x20;

```javascript
async function initializeComponents() {
    //Build a configuration object
    const configuration = {
        checkoutSessionId: await createComponentsCheckoutSession(),
        onReady: function (data) {
            //Handle event
        },
        onChange: function (data) {
            //Handle event
        },
        onSuccess: function (data) {
            //Handle event
        }
    }
    ...
}
```

#### Create the components object

Pass your [configuration object](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/components/configuring-components.md) to [`components()`](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/components/#creating-components).&#x20;

```javascript
async function initializeComponents() {
    ...
    //Create components
    let components;
    components = digitalRiverCheckout.components(configuration);
    ...
}
```

#### Create individual components

Use the object returned by `components()` to [create the individual components](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/components/#createcomponent-componenttype) that you want customers to interact with.&#x20;

```javascript
async function initializeComponents() {
    ...
    //Create the individual components
    paymentComponent = components.createComponent('payment');
    shippingComponent = components.createComponent('shipping');
    addressComponent = components.createComponent('address');
    walletComponent = components.createComponent('wallet');
    thankYouComponent = components.createComponent('thankyou');
    complianceComponent = components.createComponent('compliance');
    orderSummaryComponent = components.createComponent('ordersummary');
    ...
}
```

#### Mount individual components

For each component, pass the `id` of its HTML container to [`mount()`](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/components/#mount-elementid).&#x20;

```javascript
async function initializeComponents() {
    ...
    //Mount the individual components
    paymentComponent.mount('payment-container');
    shippingComponent.mount('shipping-container');
    addressComponent.mount('address-container');
    walletComponent.mount('wallet-container');
    thankYouComponent.mount('order-confirmation-container');
    complianceComponent.mount('compliance-container');
    orderSummaryComponent.mount('order-summary-container');
}
```

## Handling front-end events

Ensure you define how you'd like to handle the [ready](implementing-a-components-checkout.md#ready-events), [change](implementing-a-components-checkout.md#change-events), and [success](implementing-a-components-checkout.md#success-events) callback functions.

### Ready events

Some of the ways you might handle [`onReady`](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/components/configuring-components.md#onready) is by:&#x20;

* Using [`data.requiresShipping`](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/components/configuring-components.md#requiresshipping) to set a boolean variable that controls whether the [shipping component](implementing-a-components-checkout.md#shipping-component) needs to be displayed during the checkout process.
* Using [`data.showTaxIdentifiers`](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/components/configuring-components.md#showtaxidentifiers) to set a boolean that controls whether the [tax identifier component](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/components/tax-identifier-component.md) needs to be displayed.&#x20;
* Calling a function that [controls the flow of the checkout experience](implementing-a-components-checkout.md#controlling-the-checkout-flow).&#x20;

```javascript
...
onReady: function (data) {
  if (data.requiresShipping === false) { 
    //Update the variable that controls whether to display the shipping component
  }
  if (data.showTaxIdentifiers === false) {
    //Update the variable that controls whether to display the tax identifier component
  }
  //Call a function that determines the correct component(s) to display
},
...
```

### Change events

If you're using the [tax identifier component](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/components/tax-identifier-component.md), handle [`onChange`](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/components/configuring-components.md#onchange) by determining whether `optionalTaxIdentifiers[]` or `requiredTaxIdentifiers[]` exists in the returned `data`. If either does, set a variable that controls whether that component is displayed during the checkout process.

```javascript
onChange: function (data) {
    ...
    if (('optionalTaxIdentifiers' in data) || ('requiredTaxIdentifiers' in data)){
      //Set a display tax identifier component boolean variable to true
      //At some point in the checkout process, display the tax identifier component
    };
},
...
```

If, for whatever reason, you decide not to use the [order summary component](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/components/order-summary-component.md), you can also use [`onChange`](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/components/configuring-components.md#onchange) to update your custom-built order summary section. There are a variety of ways to do this.&#x20;

The example below retrieves `locale`, `currency`, `totalAmount`, `totalShipping`, `totalTax`, and `subTotal`, along with each `items[].amount`, from the `data` returned by `onChange` and then constructs [JavaScript Int.NumberFormat](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/Intl/NumberFormat) objects which are then used to set the `innerText` of the appropriate HTML element.

In this example, the `sku.image` and `sku.name` of each `items[]` is also displayed.&#x20;

```javascript
  ...
  onChange: function (data) {
    const locale = data.locale.replace('_', '-');
    document.getElementById('total').innerText =  new Intl.NumberFormat(locale, { style: 'currency', currency: data.currency }).format(data.totalAmount);
    document.getElementById('shipping').innerText =  new Intl.NumberFormat(locale, { style: 'currency', currency: data.currency }).format(data.totalShipping);
    document.getElementById('tax').innerText =  new Intl.NumberFormat(locale, { style: 'currency', currency: data.currency }).format(data.totalTax);
    document.getElementById('subtotal').innerText =  new Intl.NumberFormat(locale, { style: 'currency', currency: data.currency }).format(data.subtotal);
    document.getElementById('items').innerHTML = data.items.map( i => {
      return <div>
        <img style="height: 30px; width: 30px" src="${i.sku.image}"/> ${i.sku.name} - ${new Intl.NumberFormat(locale, { style: 'currency', currency: data.currency }).format(i.amount)}
      </div>
    });
  },
  ...
```

### Success events

One way to handle [`onSuccess`](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/components/configuring-components.md#onsuccess) is by passing an argument to your [control checkout flow function](implementing-a-components-checkout.md#controlling-the-checkout-flow), instructing it to display the [thank you component](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/components/thank-you-component.md).&#x20;

Alternatively, you could retrieve `order.id` (and whatever else you need) from `data` and use it to build your custom order confirmation page.&#x20;

```javascript
  ...
  onSuccess: function (data) {
    // Display the thank you component or a customized order confirmation page
  },
  ...
```

## Controlling the checkout flow

To control the flow of the checkout experience, you'll need to implement asynchronous functionality.

One possible approach is to define a function that checks a position enumeration, each value of which corresponds to a stage in the checkout process, and then, depending on the value, uses [`document`](https://developer.mozilla.org/en-US/docs/Web/API/Document) to access each HTML element in your experience that holds a component, displaying and hiding the appropriate ones. &#x20;

As you progress through the various checkout stages, make sure you also call `done()` to ensure that the customer's inputs are submitted and valid. For details, refer to [Submitting components](implementing-a-components-checkout.md#submitting-components).&#x20;

## Submitting components

Some of the [available components](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/components/#supported-component-types) collect data from customers. For a subset of these, Digital River handles submitting that data. For others, you must initiate the process.

For example, in the [payment component](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/components/payment-component.md), DigitalRiver.js handles the button click event by sending a create [source](../../payments/payment-sources/) request, performing any required [SCA](../../payments/psd2-and-sca/) or redirects to the payment provider, and then, assuming those processes are successful, requesting that the payment object be added to the [checkout-session's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions) `sources[]`.&#x20;

On the other hand, the [address](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/components/address-component.md), [shipping](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/components/shipping-component.md), [tax identifier](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/components/tax-identifier-component.md), and [invoice ](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/components/invoice-component.md)components require that you invoke a function that submits the data they collect and determines whether it's valid. Specifically, these components require that, inside of an [`async` function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async\_function), you call `done()` using the [`await`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/await) operator and then check the returned value to determine whether the checkout should advance to the next stage.

{% tabs %}
{% tab title="Address component" %}
<pre class="language-javascript"><code class="lang-javascript">...
<strong>const addressComponentStatus = await addressComponent.done();
</strong>if (!addressComponentStatus) {
  //Do not advance checkout to the next stage
  return;
} else {
  //Advance checkout to the next stage
}
...
</code></pre>
{% endtab %}

{% tab title="Tax identifier component" %}
```javascript
...
const taxIdentifierComponentStatus = await taxIdentifierComponent.done();
if (!taxIdentifierComponentStatus) {
  //Do not advance checkout to the next stage
  return;
} else {
  //Advance checkout to the next stage
}
...
```
{% endtab %}

{% tab title="Shipping component" %}
```javascript
...
const shippingComponentStatus = await shippingComponent.done();
if (!shippingComponentStatus) {
  //Do not advance checkout to the next stage
  return;
} else {
  //Advance checkout to the next stage
}
...
```
{% endtab %}

{% tab title="Invoice attribute component" %}
```javascript
...
const invoiceComponentStatus = await invoiceComponent.done();
if (!invoiceComponentStatus) {
  //Do not advance checkout to the next stage
  return;
} else {
  //Advance checkout to the next stage
}
...
```
{% endtab %}
{% endtabs %}

For details, refer to:

* [Submitting the address component](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/components/address-component.md#submitting-the-address-component)
* [Submitting the shipping component](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/components/shipping-component.md#submitting-the-shipping-component)
* [Submitting the tax identifier component](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/components/tax-identifier-component.md#submitting-the-tax-identifier-component)
* [Submitting the invoice attribute component ](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/components/invoice-component.md#submitting-the-invoice-component)
