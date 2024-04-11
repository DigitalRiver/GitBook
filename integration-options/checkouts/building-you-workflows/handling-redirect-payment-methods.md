---
description: >-
  Gain a better understanding of how to handle transactions funded with a
  redirect payment method
---

# Handling redirect payment methods

If you're using [Drop-in payments](../../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md) with [Direct Integrations](../) and customers opt to fund a transaction with a [payment method](../../../payments/supported-payment-methods/) whose resulting [source](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources) has a [`flow`](../../../payments/payment-sources/#authentication-flow) of `redirect`, such as [Bancontact](../../../payments/supported-payment-methods/bancontact.md), [Klarna](../../../payments/supported-payment-methods/klarna.md), [SEPA Direct Debit](../../../payments/supported-payment-methods/sepa-direct-debit.md), and [TreviPay](../../../payments/supported-payment-methods/trevipay.md), they must be redirected to the payment provider where they either approve or cancel the transfer of funds.

To do this, we recommend that, in most cases, you first submit the [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) and then redirect the customer.&#x20;

{% hint style="info" %}
To access a full list of payment methods that require a submit then redirect flow, refer to the table on [Supported payment methods](../../../payments/supported-payment-methods/).
{% endhint %}

On this page, you find:

* [A high-level overview of how to implement a submit and redirect flow](handling-redirect-payment-methods.md#how-to-implement-a-submit-then-redirect-flow)
* [A sequence diagram that depicts the interactions between the participants](handling-redirect-payment-methods.md#submit-and-redirect-sequence-diagram)

## How to implement a submit then redirect flow

In the  [`createDropin()`](../../../developer-resources/reference/digitalriver-object.md#creating-an-instance-of-drop-in) method's [configuration object](../../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md#configuring-drop-in-payments), set the [`redirect`](../../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md#dropinviadigitalriver.js-disablingredirectswithindropin) object's `disableAutomaticRedirects` to `true` and assign the same value to both `returnUrl` and `cancelUrl`.

If customers select a redirect payment method, the `data` returned by [`onSuccess`](../../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md#onsuccess) contains a [source](../../../payments/payment-sources/) whose [`state`](../../../payments/payment-sources/#source-state) is `pending_redirect`. When you receive this event, retrieve `source.id` from `data`.

```javascript
let digitalRiver = new DigitalRiver("Your public API key", {
    "locale": "en-GB"
});
                        
let configuration = {
    "sessionId": "fe50c56f-88a4-4961-8142-7d4784b87264",
    "options": {
        "flow": "checkout",
        "redirect": {
            "disableAutomaticRedirects": true,
            "returnUrl": "https://mywebsite.com/paymentCallBack.html",
            "cancelUrl": "https://mywebsite.com/paymentCallBack.html"
        },
        ...
    }, 
    onSuccess: function(data) {
       //send sourceId to your backend
       var sourceId = data.source.id;
    }, 
    ...
}
                                    
let dropin = digitalriverpayments.createDropin(configuration);
dropin.mount("drop-in");
```

Next, pass this identifier in a server-side [attach source to checkout request](../../../payments/payment-sources/using-the-source-identifier.md#attaching-sources-to-checkouts).

```
curl --location --request POST 'https://api.digitalriver.com/checkouts/c2aabaee-e414-40cc-93f6-9b4d17eef863/sources/7592e047-da55-4c7a-bbe1-14c182d0533b' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer 'Your secret API key' \
...
--data ''
```

This operation moves the checkout's [`payment.session.state`](../creating-checkouts/payment-sessions.md#session-state) to [`requires_confirmation`](../creating-checkouts/payment-sessions.md#requires\_confirmation).&#x20;

{% code title="Checkout" %}
```json
{
    "id": "c2aabaee-e414-40cc-93f6-9b4d17eef863",
    "createdTime": "2023-07-20T19:15:37Z",
    "currency": "EUR",
    "email": "jdoe@digitalriver.com",
    "shipTo": {
        "address": {
            "line1": "Alexanderplatz, Panoramastraße 1A",
            "city": "Berlin",
            "postalCode": "10178",
            "country": "DE"
        },
        "name": "Jane Doe",
        "email": "jdoe@digitalriver.com"
    },
    "shipFrom": {
        "address": {
            "country": "NL"
        }
    },
    "billTo": {
        "address": {
            "line1": "Alexanderplatz, Panoramastraße 1A",
            "city": "Berlin",
            "postalCode": "10178",
            "country": "DE"
        },
        "name": "Jane Doe",
        "email": "jdoe@digitalriver.com"
    },
    "totalAmount": 62.48,
    "subtotal": 52.5,
    "totalFees": 0.0,
    "totalTax": 9.98,
    "totalImporterTax": 0.0,
    "totalDuty": 0.0,
    "totalDiscount": 0.0,
    "totalShipping": 22.5,
    "items": [
        {
            "id": "7028d30b-3d18-4b1d-8fb8-d0200e88327d",
            "skuId": "3af0dc03-99cb-42a5-a45f-c48232c96314",
            "productDetails": {
                "id": "3af0dc03-99cb-42a5-a45f-c48232c96314",
                "name": "Kazual Comfort",
                "eccn": "EAR99",
                "taxCode": "5216",
                "image": "https://lh3.googleusercontent.com/RyMm66xn1ulmmpk2cacCHYNwB17NGzwqCKazGiWThEId9VVIO_BlEiSFX1FybZzw2ElyOX8=s85",
                "description": "Biscuits to keep your puppy happy and health"
            },
            "amount": 30.0,
            "quantity": 3,
            "tax": {
                "rate": 0.19,
                "amount": 5.7
            },
            "importerTax": {
                "amount": 0.0
            },
            "duties": {
                "amount": 0.0
            },
            "fees": {
                "amount": 0.0,
                "taxAmount": 0.0
            },
            "shipping": {
                "amount": 22.5,
                "taxAmount": 4.28
            }
        }
    ],
    "shippingChoice": {
        "amount": 22.5,
        "description": "standard",
        "serviceLevel": "SG",
        "taxAmount": 4.28
    },
    "updatedTime": "2023-07-20T19:18:24Z",
    "locale": "en_US",
    "customerType": "individual",
    "sellingEntity": {
        "id": "DR_IRELAND-ENTITY",
        "name": "Digital River Ireland Ltd."
    },
    "liveMode": false,
    "payment": {
        "sources": [
            {
                "id": "7592e047-da55-4c7a-bbe1-14c182d0533b",
                "type": "klarnaCredit",
                "amount": 62.48,
                "owner": {
                    "firstName": "Jane",
                    "lastName": "Doe",
                    "email": "jdoe@digitalriver.com",
                    "address": {
                        "line1": "Alexanderplatz, Panoramastraße 1A",
                        "city": "Berlin",
                        "postalCode": "10178",
                        "country": "DE"
                    }
                },
                "klarnaCredit": {
                    "shipping": {
                        "recipient": "Jane Doe",
                        "address": {
                            "line1": "Alexanderplatz, Panoramastraße 1A",
                            "city": "Berlin",
                            "country": "DE",
                            "postalCode": "10178"
                        },
                        "email": "jdoe@digitalriver.com"
                    },
                    "token": "343456789012341",
                    "redirectUrl": "https://api.digitalriverws.com:443/payments/redirects/96d0f08a-e0ca-4587-b184-93bddeec0812?apiKey=pk_test_a45b91ba4f984df7a229b2ab5941ce1c",
                    "returnUrl": "https://en.wikipedia.org/wiki/Main_Page",
                    "cancelUrl": "https://en.wikipedia.org/wiki/Main_Page",
                    "offline": false
                }
            }
        ],
        "session": {
            "id": "b9abd9fd-5664-4533-a8ae-e5758663f748",
            "amountContributed": 62.48,
            "amountRemainingToBeContributed": 0.0,
            "state": "requires_confirmation",
            "clientSecret": "b9abd9fd-5664-4533-a8ae-e5758663f748_7a85f52e-5491-4069-be1e-26c238456071"
        }
    }
}
```
{% endcode %}

At this point, retrieve the [checkout](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) data you need—such as `currency`, `totalAmount`, `subTotal`, `totalTax`, `shipTo`, `shippingChoice`,`payment.sources[]`, and relevant `items[].productDetails`—to build a review page. &#x20;

If, after reviewing the transaction's details, customers click your submit order button, handle that event by passing the [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) `id` to your server and sending it in the body of a [create order request](../../../order-management/creating-and-updating-an-order.md#creating-an-order-with-the-checkout-identifier).

{% code title="POST /orders" %}
```
curl --location 'https://api.digitalriver.com/orders' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer 'Your secret API key' \
...
--data '{
    "checkoutId": "c2aabaee-e414-40cc-93f6-9b4d17eef863"
}'  
```
{% endcode %}

If you get back a `201 Created`, and the [order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) [`state`](../../../developer-resources/digital-river-api-reference/orders/the-order-lifecycle.md#order-states-and-events) is `pending_payment`, then check [`payment.session.state`](../creating-checkouts/payment-sessions.md#session-state). &#x20;

{% code title="Order" %}
```json
{
    "id": "240354510336",
    ...
    "payment": {
        ...
        "session": {
            "id": "1b682138-ce9f-46ec-8b5e-94b710128cd9",
            "amountContributed": 37.5,
            "amountRemainingToBeContributed": 0.0,
            "state": "pending_redirect",
            "clientSecret": "1b682138-ce9f-46ec-8b5e-94b710128cd9_c45043e2-39bc-4c0d-9fc2-fece4f6298c3",
            "nextAction": {
                "action": "redirect",
                "data": {
                    "redirectUrl": "https://api.digitalriver.com:443/payments/redirects/3fab742c-a7e8-4a90-8951-86d071fa070d?apiKey=pk_test_a45b91ba4f984df7a229b2ab5941ce1c"
                }
            }
        }
    },
    "state": "pending_payment",
    ...
}
```
{% endcode %}

If its value is `pending_redirect`, and `payment.session.nextAction.data.redirectUrl` is a non-null value, then redirect to this url, which is the third-party provider's interface, where customers either approve or cancel payment.

{% hint style="success" %}
If the order's `state` is `pending_payment` and the `payment.session.state` is  `pending_funds`, refer to [Handling delayed payment methods](handling-delayed-payment-methods.md).&#x20;
{% endhint %}

Once customers complete either of these actions, they're redirected to the endpoint you assigned to `cancelUrl` and/or `returnUrl`.&#x20;

When this resource loads, call a function that initiates a server-side request and send the [order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) identifier and `refresh` in the path. &#x20;

```
curl --location --request POST 'https://api.digitalriver.com/orders/240354510336/refresh' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer <Secret API key>' \
...
--data-raw ''
```

If you get a `200 OK`, check the order's [`state`](../../../developer-resources/digital-river-api-reference/orders/the-order-lifecycle.md#order-states-and-events) and [`payment.session.state`](../creating-checkouts/payment-sessions.md#session-state).

{% code title="Order" %}
```json
{
    "id": "275469160336",
    ...
    "payment": {
        ...
        "session": {
            "id": "b9abd9fd-5664-4533-a8ae-e5758663f748",
            "amountContributed": 62.48,
            "amountRemainingToBeContributed": 0.0,
            "state": "complete",
            "clientSecret": "b9abd9fd-5664-4533-a8ae-e5758663f748_7a85f52e-5491-4069-be1e-26c238456071"
        }
    },
    "state": "accepted",
    "stateTransitions": {
        "accepted": "2023-07-20T19:34:41Z",
        "pending_payment": "2023-07-20T19:25:42Z"
    },
    ...
}
```
{% endcode %}

If (1) [`state`](../../../developer-resources/digital-river-api-reference/orders/the-order-lifecycle.md#order-states-and-events) is `accepted` or `in_review` or (2) `state` is `pending_payment` and [`payment.session.state`](../creating-checkouts/payment-sessions.md#session-state) is `pending` or `pending_funds`, then a [`charges[]`](../../../developer-resources/digital-river-api-reference/payment-charges.md) on the [`sources[]`](../../../payments/payment-sources/) whose [`flow`](../../../payments/payment-sources/#authentication-flow) is `redirect` has been successfully authorized, and you should display an order confirmation page and send a[ confirmation email](../../../order-management/customer-notifications.md#order-confirmation).

At this point, you can initiate [fulfillment operations](../../../order-management/fulfillments.md).&#x20;

Any other (1) [`state`](../../../developer-resources/digital-river-api-reference/orders/the-order-lifecycle.md) value or (2) combination of `state` and [`payment.session.state`](../creating-checkouts/payment-sessions.md#session-state) values indicates that the [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) can't be recovered. As a result, you'll need to recreate the [checkout](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) and send customers back to the payment collection stage. For details, refer to [Handling rejected orders](../../../order-management/resubmitting-an-order.md).&#x20;

## Submit and redirect sequence diagram

The scope of the following diagram is limited to the operations described above in [How to implement a submit then redirect flow](handling-redirect-payment-methods.md#how-to-implement-a-submit-then-redirect-flow).

{% file src="../../../.gitbook/assets/Submit then redirect.png" %}

To view a diagram that more comprehensively covers the checkout, payment authorization and fulfillment process, refer to [Core Commerce flow (with submit then redirect)](../../../general-resources/standards-and-certifications/integration-checklists/#core-commerce-flow-with-submit-then-redirect).&#x20;

