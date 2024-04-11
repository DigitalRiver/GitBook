---
description: >-
  Gain a better understanding of the functionality that exists within the
  Prebuilt Checkout modal's configuration object
---

# Configuring Prebuilt Checkout

The [`createModal()`](../#create-an-instance-of-the-checkout-modal) and [`embed()`](../#embed-checkoutsessionid-config) functions, which are exposed by [`DigitalRiverCheckout`](../), accept an optional configuration object that allows you to define:

* [A container for Prebuilt Checkout](./#designating-a-container-for-an-inline-frame)
* [The overall checkout experience](./#defining-the-checkout-experience)
* [The payment experience](./#define-the-payment-experience)&#x20;
* [How your application handles callbacks](./#responding-to-front-end-events)
* [Customized actions](performing-actions.md)

```javascript
const config = {
    containerElementId: "PBC",
    options: options,
    paymentMethod: paymentMethod,
    onInit: (checkoutSession, actions) => {},
    onReady: () => {},
    onAddressComplete: (address, actions) => {},
    onDeliveryComplete: (shippingMethod) => {},
    onPaymentCancel: () => {},
    onCheckoutComplete: (order) => {},
    onError: () => {},
    onClose: () => {}
};
```

## Designating a container for an Inline Frame&#x20;

If you implement [`embed()`](../#embed-checkoutsessionid-config) and want Digital River to add the `iframe` which displays a [Prebuilt Checkout](../../../../integration-options/low-code-checkouts/drop-in-checkout.md#drop-in-checkout-modal-window) to a specific HTML element, then assign that element's identifier to `containerElementId`.&#x20;

```javascript
<body>
    <div id="PBC"></div>
</body>

const config = {
    containerElementId: "PBC",
    ...
};
```

## Defining the checkout experience

In `options`, you can control the appearance and behavior of a [Prebuilt Checkout](../../../../integration-options/low-code-checkouts/drop-in-checkout.md#drop-in-checkout-modal-window). Specifically, you can use `options` to:

* [Set the display mode](./#set-display-mode)
* [Stylize the modal](./#stylize-the-modal)
* [Localize the modal](./#localize-the-modal)
* [Customize order confirmation notifications](./#customize-order-confirmation)
* [Restrict shipping and billing countries](./#restrict-shipping-and-billing-countries)
* [Modify the text of the country drop-down menu's label](./#modify-the-text-of-the-country-drop-down-menus-label)

### Set display mode

In [`options`](./#defining-the-checkout-experience), the `displayMode`, whose value can either be `standard` (default) or `fullPage`, controls the size of the checkout window.&#x20;

```javascript
const options = {
  ...
  displayMode: 'fullPage',
  ...
};
```

A `standard` value results in a window whose dimensions are less than those of the browser window while `fullPage` expands the window to the edges of the browser window.&#x20;

### Stylize the modal

Set `style.experience` in [`options`](./#defining-the-checkout-experience) to alter the checkout window's logo, theme, borders, text fields, and fonts. For details, refer to [Defining experience](defining-experience.md).&#x20;

### Localize the experience <a href="#localize-the-modal" id="localize-the-modal"></a>

By default, Digital River localizes the [Prebuilt Checkout window](../../../../integration-options/low-code-checkouts/drop-in-checkout.md#drop-in-checkout-modal-window) based on the customer’s browser settings. But if you want to control the language of the experience, set `language` in [`options`](./#defining-the-checkout-experience). &#x20;

If you do define `options.language`, then Digital River assigns the same value to [`language`](../../../digital-river-api-reference/checkout-sessions.md#language) in the [checkout-session](../../../digital-river-api-reference/checkout-sessions.md).

```javascript
const options = {
  ...
  language: 'en-gb',
  ...
};
```

For a list of accepted values, refer to [Supported languages](../../../supported-languages.md).

### Customize order confirmation

By setting `thankYouPage` in [`options`](./#defining-the-checkout-experience), you can configure the [order confirmation stage](../../../../integration-options/low-code-checkouts/drop-in-checkout.md#order-confirmation).

* **Custom page**: To redirect customers to your own fully customized order confirmation page, pass the appropriate web address.

```javascript
const options = {
    ...
    thankYouPage: 'https://www.mysite.com/order-confirmation-page'
};
```

* **Default window**: To display Digital River's default order confirmation, omit `thankYouPage`. You can customize this default confirmation by calling [`replaceDefaultMessage()`](performing-actions.md#replacedefaultmessage-message-showcheckcircleicon), which is exposed by [`actions.thankYouPage`](performing-actions.md#thankyoupage).
* **Close window**: If you want the [Prebuilt Checkout window](../../../../integration-options/low-code-checkouts/drop-in-checkout.md#drop-in-checkout-modal-window) to immediately close after customers place an order, set `thankYouPage` to `none`.

### Restrict shipping and billing countries

By setting `shipToCountries` and/or `billToCountries` in [`options`](./#defining-the-checkout-experience), you can restrict the values displayed in the drop-down menus that customers use to select a country in the [name and address collection stage](../../../../integration-options/low-code-checkouts/drop-in-checkout.md#name-and-address).&#x20;

```javascript
const options = {
    ...
    shipToCountries: ['AT', 'BE', 'DE', 'ES', 'FR', 'IT'],
    billToCountries: ['DE', 'ES', 'FR', 'IT']
};
```

The values you pass must be formatted as two-letter [Alpha-2 country codes](https://www.iban.com/country-codes) as described in the [ISO 3166](https://www.iso.org/iso-3166-country-codes.html) international standard.

### Modify the text of the country drop-down menu's label

By adding `labelText.country.*` in [`options`](./#defining-the-checkout-experience), you can modify the text of the country drop-down menu's label in both the [shipping and billing information collection stage](../../../../integration-options/low-code-checkouts/drop-in-checkout.md#name-and-address).&#x20;

If a `country.*` matches [`language`](./#localize-the-modal), then Digital River updates the label's text.&#x20;

{% tabs %}
{% tab title="Configurations options" %}
```javascript
const config = {
  "options": {
    "labelText": {
      "country": {
        "en-us": "An American custom label",
        "en-gb": "A British custom label",
        "zh-tw": "寄送地",
        "zh-hk": "寄送地",
        "zh": "寄送地"
      }
    }, 
    "language": "en-gb"
  }
};
```
{% endtab %}

{% tab title="Modal" %}
<figure><img src="../../../../.gitbook/assets/PBC country label text.png" alt=""><figcaption></figcaption></figure>
{% endtab %}
{% endtabs %}

## Define the payment experience

In [Prebuilt Checkout's configuration object](./), you can use `paymentMethod` to control the appearance and behavior of the [payment collection stage](../../../../integration-options/low-code-checkouts/drop-in-checkout.md#payment). Specifically, `paymentMethod` allows you to style:

* [The overall payment experience](./#style-the-overall-payment-experience)
* [Credit cards](./#style-credit-cards)
* [Google Pay](./#style-google-pay)
* [Apple Pay](./#style-apple-pay)
* [PayPal](./#style-paypal)
* [Online banking](./#style-online-banking)

You can also use `paymentMethod` to:

* [Provide a link to a TreviPay enrollment form](./#link-to-trevipay-enrollment-form)
* [Enable and disable specific payment methods](./#filtering-payment-methods-shown-in-drop-in)

{% hint style="info" %}
[Drop-in payments](../../../../payments/payment-integrations-1/drop-in/) also uses the `paymentMethod` object; the only difference is that it's named [`paymentMethodConfiguration`](../../../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md#configuring-payment-methods-within-drop-in).
{% endhint %}

```javascript
const paymentMethod = {
    "style": {
        "base": {
            "color": "#495057",
            "height": "35px",
            "fontSize": "1rem",
            "fontFamily": "apple-system,BlinkMacSystemFont,Segoe UI,Roboto,Helvetica Neue,Arial,sans-serif",
            ":hover": {
                "color": "#137bee",
            },
            "::placeholder": {
                "color": "#999"
            },
            ":-webkit-autofill": {
                "color": "purple"
            },
            ":focus": {
                "color": "blue"
            }
        },
        "invalid": {
            "color": "#dc3545",
            ":-webkit-autofill": {
                "color": "#dc3545"
            }
        },
        "complete": {
            "color": "#28a745",
            ":hover": {
                "color": "#28a745",
            },
            ":-webkit-autofill": {
                "color": "#28a745"
            }
        },
        "empty": {
            "color": "#000000"
        }
    },
    "creditCard": {
        "cardNumberPlaceholderText": "Credit Card Number",
        "cardExpirationPlaceholderText": "MM/YY",
        "cardCvvPlaceholderText": "CVV",
        "style": styles,
        "mask": true
    },
    "onlineBanking": {
        "style": styles,
        "placeholderText": "Select a Bank",
    },
    "googlePay": {
        "style": {
            "buttonType": "plain",
            "buttonColor": "dark",
            "buttonLanguage": "en"
        }
    },
    "applePay": {
        "style": {
            "buttonType": "plain",
            "buttonColor": "dark",
            "buttonLanguage": "en"
        }
    },
    "payPal": {
        "style": {
            "label": "checkout",
            "size": "responsive",
            "color": "gold",
            "shape": "pill",
            "fundingicons": "false",
            "tagline": "false"
        },
    },
    "msts": { 
        "enrollmentUrl": "https://acmeUS.b2b.credit/en-US/apply?client_reference_id=Acme-123456&ecommerce_url=www.acme-returnURL.com", 
    },
    "enabledPaymentMethods": ["creditCard", "payPal"],
    "disabledPaymentMethods": ["klarna"]
}
```

#### Style the overall payment experience

To capture secure payment details, [Prebuilt Checkout](../../../../integration-options/low-code-checkouts/drop-in-checkout.md) wraps [elements](../../../reference/elements/), which have a predetermined style. But you can customize their look and feel by defining `style`.

For details, refer to [Styling an element container](../../../reference/elements/#styling-an-element-container).

#### Style credit cards

To configure how credit cards are displayed, define one or more of the nested objects in `creditCard`.&#x20;

* `style:` For details, refer to [Styling an element container](../../../reference/elements/#styling-an-element-container).
* `mask`: A boolean that determines whether card numbers and security codes get masked after they've been entered by users.
* `cardNumberPlaceholderText`: The placeholder that is shown in the card number field.&#x20;
* `cardExpirationPlaceholderText`: The placeholder that is shown in the card expiration date field.&#x20;
* `cardCvvPlacholderText`: The placeholder that is shown in the card security code field.&#x20;

{% hint style="info" %}
The values you assign to `cardNumberPlaceholderText`, `cardExpirationPlaceholderText`, and `cardCvvPlacholderText` are not localized.
{% endhint %}

#### Style Google Pay

For details on `googlePay.style`, refer to [Google Pay element styles and customization](../../../reference/elements/google-pay-elements.md#google-pay-element-styles-and-customization).

#### Style Apple Pay

For details on `applePay.style`, refer to [Apple Pay styles and customization](../../../reference/elements/apple-pay-elements.md#apple-pay-element-styles-and-customization).

#### Style PayPal

All the properties of `payPay.style`, which styles the [PayPal](../../../../payments/supported-payment-methods/paypal.md) button, are optional.

<table><thead><tr><th width="176.33333333333331">Property</th><th>Description</th><th>Accepted values</th></tr></thead><tbody><tr><td><code>label</code></td><td>Customizes the button's label.</td><td><code>paypal</code> (default), <code>pay</code>, <code>checkout</code>, and <code>buynow</code></td></tr><tr><td><code>color</code></td><td>Sets the color of the button.</td><td><code>gold</code> (default), <code>silver</code>, <code>black</code>, <code>white</code> and <code>blue</code></td></tr><tr><td><code>shape</code></td><td>Determines the shape of the button.</td><td><code>pill</code> (default) and <code>rect</code></td></tr><tr><td><code>fundingicons</code></td><td>A boolean that determines whether icons, which as a visual cue of the stored payment methods, display below the button.</td><td><code>true</code> or <code>false</code> (default)</td></tr><tr><td><code>tagline</code></td><td><p>A boolean that determines whether a PayPal slogan displays beneath the button.</p><p></p><p>For this feature to work, <code>fundingicons</code> must be <code>false</code>.<br></p></td><td><code>true</code> or <code>false</code> (default)</td></tr></tbody></table>

#### Style online banking

To configure the appearance of the [online banking](../../../../payments/supported-payment-methods/online-banking-ibp.md) payment method, define one or more of the nested objects in `onlineBanking`.

* `style:` For details, refer to [Styling an element container](../../../reference/elements/#styling-an-element-container).
* `placeholderText`: The placeholder that appears in the online banking selector.&#x20;

#### Link to TreviPay enrollment form

Use `msts.enrollmentUrl` to add a link to the [TreviPay enrollment URL](../../../../payments/supported-payment-methods/trevipay.md#trevipay-enrollment-form).

#### Enable and disable payment methods <a href="#filtering-payment-methods-shown-in-drop-in" id="filtering-payment-methods-shown-in-drop-in"></a>

To display and hide specific payment methods, provide a list of `enabledPaymentMethods` and `disabledPaymentMethods`.

{% hint style="info" %}
For details on how to format these values, refer to [Source types](../../../../payments/payment-sources/#supported-payment-methods).
{% endhint %}

If you don't populate either of these arrays, then, by default, [Prebuilt Checkout](../../../../integration-options/low-code-checkouts/drop-in-checkout.md#payment) displays all transaction-applicable payment methods. If `enabledPaymentMethods` contains a value that doesn't meet this precondition, then it's not presented as an option to customers.

## Responding to front-end events

In the [Prebuilt Checkout configuration object](./), you can define methods and assign them to its [`onInit`](./#oninit), [`onReady`](./#onready), [`onAddressComplete`](./#onaddresscomplete), [`onDeliveryComplete`](./#ondeliverycomplete), [`onCheckoutComplete`](./#oncheckoutcomplete), [`onClose`](./#onclose), and [`onError`](./#onerror) properties.&#x20;

As events occur during the checkout process, these methods are executed.

```javascript
const config = {
    ....
    onInit: (checkoutSession, actions) => {},
    onReady: () => {},
    onAddressComplete: (address, actions) => {},
    onDeliveryComplete: (shippingMethod) => {},
    onPaymentCancel: () => {},
    onCheckoutComplete: (order) => {},
    onError: () => {},
    onClose: () => {}
};
```

### `onInit`

The `onInit` method, which accepts `checkoutSession` and [`actions`](performing-actions.md), executes when Prebuilt Checkout initializes.&#x20;

```javascript
...
onInit = (checkoutSession, actions) => {},
...
```

### `onReady`

The `onReady` method executes when the [checkout-session](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions) is created and Prebuilt Checkout is loaded and ready for customer interaction.

```javascript
....
onReady: () => {},
...
```

### `onAddressComplete`

The `onAddressComplete` method, which accepts an optional `address` and [`actions`](performing-actions.md), executes when customers successfully submit their shipping and/or billing information and the [checkout-session's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions) `shipTo` and/or `billTo` is updated.&#x20;

<pre class="language-javascript"><code class="lang-javascript"><strong>...
</strong><strong>onAddressComplete: (address, actions) => {},
</strong><strong>...
</strong></code></pre>

If passed, then `onAddressComplete` returns `address`, which contains the customer’s `billing` and `shipping` data.&#x20;

```javascript
{
    "address": {
        "billing": {
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
            },
            "saveForLater": false
        },
        "shipping": {
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
            },
            "saveForLater": false
        }
    }
}
```

### `onDeliveryComplete`

The `onDeliveryComplete` method, which optionally accepts `shippingMethod`, executes when [customers submit their shipping method choice](../../../../integration-options/low-code-checkouts/drop-in-checkout.md#shipping-choice), and the [checkout-session's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions) `shippingChoice` is successfully updated.

```javascript
    ....
    onDeliveryComplete: (shippingMethod) => {},
    ....
```

If passed, then `onDeliveryComplete` returns a `shippingMethod` that contains the customer’s selection, along with its calculated `taxAmount`.

```javascript
{
    "amount": 5,
    "description": "standard",
    "serviceLevel": "SG",
    "taxAmount": 0.37
}
```

### `onCheckoutComplete`

The `onCheckoutComplete` method, which optionally accepts `order`, executes when [customers provide payment and submit the order](../../../../integration-options/low-code-checkouts/drop-in-checkout.md#payment), and Digital River adds [`sources[]`](../../../../payments/payment-sources/) to the [checkout-session](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions) and creates the [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders).

```javascript
    ....
    onCheckoutComplete: (order) => {
        console.log('[onCheckoutComplete callback]', order);
    },
    ....
```

If passed, then `onCheckoutComplete` returns the [`order`](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders).

```javascript
{
    "id": "1038474530082",
    "checkoutId": "978785ba-07fc-4acd-9eaa-960ab512766c",
    "checkoutSessionId": "41dc1898-81fa-43af-a128-480320a443f9",
    "createdTime": "2022-07-11T19:22:46Z",
    "currency": "USD",
    "email": "jsmith@digitalriver.com",
    "shipTo": {
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
        },
        "saveForLater": false
    },
    "shipFrom": {
        "address": {
            "line1": "10380 Bren Rd W",
            "city": "Minnetonka",
            "postalCode": "55129",
            "state": "MN",
            "country": "US"
        }
    },
    "billTo": {
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
        },
        "saveForLater": false
    },
    "totalAmount": 10.74,
    "subtotal": 10,
    "totalFees": 0,
    "totalTax": 0.74,
    "totalImporterTax": 0,
    "totalDuty": 0,
    "totalDiscount": 0,
    "totalShipping": 5,
    "items": [
        {
            "id": "50418820082",
            "sku": {
                "id": "b646aeaa-efe1-4fe4-a88f-73212b40381c",
                "name": "Widget",
                "eccn": "EAR99",
                "taxCode": "4323.310_A",
                "physical": true,
                "metadata": {
                    "customAttribute1": "some value"
                }
            },
            "amount": 5,
            "quantity": 1,
            "tax": {
                "rate": 0.07375,
                "amount": 0.37
            },
            "importerTax": {
                "amount": 0
            },
            "duties": {
                "amount": 0
            },
            "availableToRefundAmount": 0,
            "fees": {
                "amount": 0,
                "taxAmount": 0
            }
        }
    ],
    "shippingChoice": {
        "amount": 5,
        "description": "standard",
        "serviceLevel": "SG",
        "taxAmount": 0.37
    },
    "updatedTime": "2022-07-11T19:22:46Z",
    "locale": "en_US",
    "customerType": "individual",
    "sellingEntity": {
        "id": "C5_INC-ENTITY",
        "name": "DR globalTech Inc."
    },
    "payment": {
        "charges": [
            {
                "id": "c40a8740-fd56-41df-8ca3-0ebd12fcf9e7",
                "createdTime": "2022-07-11T19:22:49Z",
                "currency": "USD",
                "amount": 10.74,
                "state": "capturable",
                "captured": false,
                "refunded": false,
                "sourceId": "ab6078ef-deeb-4728-9217-ec81f0b70af6",
                "type": "customer_initiated"
            }
        ],
        "sources": [
            {
                "id": "ab6078ef-deeb-4728-9217-ec81f0b70af6",
                "type": "creditCard",
                "amount": 10.74,
                "owner": {
                    "firstName": "John",
                    "lastName": "Smith",
                    "email": "jsmith@digitalriver.com",
                    "address": {
                        "line1": "10380 Bren Rd W",
                        "line2": "line 2",
                        "city": "Minnetonka",
                        "postalCode": "55129",
                        "state": "MN",
                        "country": "US"
                    },
                    "organization": "Digital River",
                    "additionalAddressInfo": {
                        "neighborhood": "Centro",
                        "phoneticFirstName": "ヤマダ",
                        "phoneticLastName": "タロ",
                        "division": "営業部"
                    }
                },
                "creditCard": {
                    "brand": "Visa",
                    "expirationMonth": 12,
                    "expirationYear": 2023,
                    "lastFourDigits": "1111"
                }
            }
        ],
        "session": {
            "id": "98fbc79d-d649-4f6b-8e55-45bda0f542b9",
            "amountContributed": 10.74,
            "amountRemainingToBeContributed": 0,
            "state": "complete",
            "clientSecret": "98fbc79d-d649-4f6b-8e55-45bda0f542b9_652d201c-799e-4d35-928b-3ccc3ccf4635"
        }
    },
    "state": "accepted",
    "stateTransitions": {
        "accepted": "2022-07-11T19:22:51Z"
    },
    "fraudState": "passed",
    "fraudStateTransitions": {
        "passed": "2022-07-11T19:22:51Z"
    },
    "taxInclusive": false,
    "consents": {
        "termsOfService": true,
        "eula": true,
        "termsOfSale": true
    },
    "liveMode": false
}
```

### `onClose`

The `onClose` method, which optionally accepts `checkoutCompleted`, executes when customers close Prebuilt Checkout.

If passed, `checkoutCompleted` returns a boolean that indicates whether it closed before the checkout process is completed. If `true`, customers closed the window in the [order confirmation stage](../../../../integration-options/low-code-checkouts/drop-in-checkout.md#order-confirmation). If `false`, it was closed in an earlier stage.

```javascript
    ....
    onClose: (checkoutCompleted) => {}
```

### `onError`

The `onError` method, which optionally accepts `error`, executes when a problem occurs during the checkout process.

```javascript
    ....
    onError: (error) => {
          console.log('[onError callback]', error);
          console.log(error.errors[0].message);
        }
    ...
```

If passed, then `onError` returns an `error` that contains a `type` and an array of `errors[]`, each element of which provides more details on the triggering event.&#x20;

```json
{
    "type": "bad_request",
    "errors": [
        {
            "code": "invalid_parameter",
            "parameter": "address.postalCode",
            "message": "A required address parameter, postal code, is invalid."
        }
    ]
}
```
