---
description: >-
  In Direct Integrations, gain a better understanding of how to handle
  transactions funded with a delayed payment method
---

# Handling delayed payment methods

If customers opt to fund a transaction with a [payment method](../../../payments/supported-payment-methods/) whose resulting [source](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources) has a [`flow`](../../../payments/payment-sources/#authentication-flow) of `receiver`, such as [Konbini](../../../payments/supported-payment-methods/konbini.md) or [Wire Transfer](../../../payments/supported-payment-methods/wire-transfer.md), they must be given instructions on how to push the funds to the payment provider.&#x20;

{% hint style="success" %}
This page is only applicable to those who build their checkout experience using the [Direct Integrations](../) approach. If you implement a [low-code checkout option](../../low-code-checkouts/), then Digital River displays the delayed payment instructions to customers.
{% endhint %}

To provide customers with these instructions, first [submit the create order request](../../../order-management/creating-and-updating-an-order.md#creating-an-order-with-the-checkout-identifier). If you get back a `201 Created` and [`state`](../../../order-management/orders/the-order-lifecycle.md#order-states-and-events) is `pending_payment`, then check the value of [`payment.session.nextAction.action`](../creating-checkouts/payment-sessions.md#next-action).&#x20;

{% hint style="info" %}
For details on other `state` values and how to handle them, refer to [Handling the `POST/ orders` response](../../../order-management/creating-and-updating-an-order.md#processing-the-post-orders-response).&#x20;
{% endhint %}

{% tabs %}
{% tab title="Order" %}
{% code title="201 Created" %}
```json
{
    "id": "239809940336",
    "createdTime": "2022-09-16T21:16:18Z",
    "currency": "USD",
    "email": "jdoe@digitalriver.com",
    "shipTo": {
        "address": {
            "line1": "1234 Any Road W",
            "city": "Minneapolis",
            "postalCode": "10115",
            "state": "MN",
            "country": "DE"
        },
        "name": "Chase Marshall"
    },
    "shipFrom": {
        "address": {
            "country": "CA"
        }
    },
    "billTo": {
        "address": {
            "line1": "10380 Bren Road West",
            "line2": "Ichikawa-shi",
            "city": "Minnetonka",
            "postalCode": "55346",
            "state": "MN",
            "country": "US"
        },
        "name": "Fred Flintstone",
        "phone": "000-000-0000",
        "email": "test@digitalriver.com"
    },
    "totalAmount": 29.75,
    "subtotal": 25.0,
    "totalFees": 0.0,
    "totalTax": 4.75,
    "totalImporterTax": 0.0,
    "totalDuty": 0.0,
    "totalDiscount": 0.0,
    "totalShipping": 5.0,
    "items": [
        {
            "id": "167661230336",
            "skuId": "face64e4-2017-431e-93e6-30ca951e1f5a",
            "productDetails": {
                "id": "face64e4-2017-431e-93e6-30ca951e1f5a",
                "name": "Test Product",
                "countryOfOrigin": "US",
                "partNumber": "face64e4-2017-431e-93e6-30ca951e1f5a"
            },
            "amount": 10.0,
            "quantity": 1,
            "state": "created",
            "stateTransitions": {
                "created": "2022-09-16T21:16:18Z"
            },
            "tax": {
                "rate": 0.19,
                "amount": 1.9
            },
            "importerTax": {
                "amount": 0.0
            },
            "duties": {
                "amount": 0.0
            },
            "availableToRefundAmount": 0.0,
            "fees": {
                "amount": 0.0,
                "taxAmount": 0.0
            },
            "sellerTaxIdentifier": "DE246495190",
            "shipping": {
                "amount": 5.0,
                "taxAmount": 0.95
            }
        },
        {
            "id": "167661240336",
            "skuId": "c3e15ba7-d44a-43e9-83c2-99a20b90be3a",
            "productDetails": {
                "id": "c3e15ba7-d44a-43e9-83c2-99a20b90be3a",
                "name": "SaaS",
                "countryOfOrigin": "US"
            },
            "amount": 10.0,
            "quantity": 1,
            "state": "created",
            "stateTransitions": {
                "created": "2022-09-16T21:16:18Z"
            },
            "tax": {
                "rate": 0.19,
                "amount": 1.9
            },
            "importerTax": {
                "amount": 0.0
            },
            "duties": {
                "amount": 0.0
            },
            "availableToRefundAmount": 0.0,
            "fees": {
                "amount": 0.0,
                "taxAmount": 0.0
            },
            "sellerTaxIdentifier": "IE6426071C",
            "shipping": {
                "amount": 0.0,
                "taxAmount": 0.0
            }
        }
    ],
    "shippingChoice": {
        "amount": 5.0,
        "description": "standard",
        "serviceLevel": "SG",
        "taxAmount": 0.95
    },
    "updatedTime": "2022-09-16T21:16:18Z",
    "locale": "en_US",
    "customerType": "business",
    "sellingEntity": {
        "id": "DR_IRELAND-ENTITY",
        "name": "Digital River Ireland Ltd."
    },
    "liveMode": false,
    "payment": {
        "sources": [
            {
                "id": "9c00d78c-dbad-4303-b366-7e0a49c322e7",
                "type": "wireTransfer",
                "amount": 29.75,
                "owner": {
                    "firstName": "Fred",
                    "lastName": "Flintstone",
                    "email": "test@digitalriver.com",
                    "address": {
                        "line1": "10380 Bren Road West",
                        "line2": "Ichikawa-shi",
                        "city": "Minnetonka",
                        "postalCode": "55346",
                        "state": "MN",
                        "country": "US"
                    }
                },
                "wireTransfer": {
                    "accountHolder": "Global Collect BV",
                    "bankName": "Rabobank N.A.",
                    "city": "Ontario",
                    "country": "US",
                    "referenceId": "890701505439",
                    "accountNumber": "0487369908",
                    "swiftCode": "RABOUS66XXX"
                }
            }
        ],
        "session": {
            "id": "afaed310-419f-4ced-912c-6830a98c7384",
            "amountContributed": 29.75,
            "amountRemainingToBeContributed": 0.0,
            "state": "pending_funds",
            "clientSecret": "afaed310-419f-4ced-912c-6830a98c7384_be3c1baa-5120-4739-8d5c-602966bff8df",
            "nextAction": {
                "action": "show_payment_instructions",
                "data": {
                    "sourceId": "9c00d78c-dbad-4303-b366-7e0a49c322e7",
                    "sourceClientSecret": "9c00d78c-dbad-4303-b366-7e0a49c322e7_246ed54a-0dfc-41f0-9e98-14036adf642e"
                }
            }
        }
    },
    "state": "pending_payment",
    "stateTransitions": {
        "pending_payment": "2022-09-16T21:16:20Z"
    },
    "requestToBeForgotten": false,
    "capturedAmount": 0.0,
    "cancelledAmount": 0.0,
    "availableToRefundAmount": 0.0,
    "checkoutId": "b9be1d80-fe76-4df0-bb43-a58e35f1e766"
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

If [`action`](../creating-checkouts/payment-sessions.md#next-action) is `show_payment_instructions`, then retrieve `sourceId` and `sourceClientSecret` from `nextAction.data` and use them to configure the [create delayed payment instructions element](../../../developer-resources/reference/elements/delayed-payment-instructions-element.md#creating-a-delayed-payment-instructions-element) method.

```javascript
let options = {
    "sourceId": "f853f415-7f85-4695-bd93-7f479efdc4a8",
    "sourceClientSecret": "f853f415-7f85-4695-bd93-7f479efdc4a8_abec5143-4f72-486c-b377-34d31ddb3c13"
}
 
let delayedPaymentInstructions = digitalRiver.createElement('delayedpaymentinstructions', options);
```

{% hint style="info" %}
If an [order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) `state` is `pending_payment` and `action` is `redirect`, refer to [Handling redirect payment methods](handling-redirect-payment-methods.md).
{% endhint %}

Next call [`mount()`](../../../developer-resources/reference/elements/delayed-payment-instructions-element.md#delayedpaymentinstructions-mount) to display the element on your order confirmation page. Alternatively, you may want to include a link on the order confirmation page that redirects customers to another page and displays the element there.

```javascript
<div id="delayed-payment-container"></div>
...
delayedPaymentInstructions.mount("delayed-payment-container");
```

When [on ready ](../../../developer-resources/reference/elements/delayed-payment-instructions-element.md#ready)executes, the instructions are displayed to customers.

```javascript
delayedPaymentInstructions.on('ready', function(event) {
    //delayed payment instructions element is ready
});
```

Once the instructions are loaded in the designated container, they usually contain the number of days that customers have to push payment.

{% tabs %}
{% tab title="HTML" %}
```html
<div id="delayed-payment-container">
    <div id="delayedpaymentinstructions-c4906e5d-bcc4-482d-aa23-24775f73f035" class="DR-delayed-payment-instructions-container">
    <p>Thank you for your order. Please pay at a local branch of the store that you selected.<br><br>The payment will be processed by Digital River, K.K. on our behalf.<br><br>Your order will not be available or shipped until payment has been received and processed.</p>
    <p id="DR-konbiniAmountAndReferenceId">
        <strong>Amount:</strong> 30.00 USD
        <br>
        <strong>Reference Number:</strong> 100001
        <br>
        <strong>Store:</strong> セブン‐イレブン
        <br>
        </p><p>Please verify your order, and complete payment within 7 days after your order date. <br><br>As soon as the payment is received and confirmed, the product will be made available or shipped. <br><br></p>
    <p></p>
  </div>
</div>
```


{% endtab %}

{% tab title="UX" %}
<figure><img src="../../../.gitbook/assets/image (100).png" alt=""><figcaption></figcaption></figure>
{% endtab %}
{% endtabs %}

If customers follow the instructions and payment is successfully authorized, you'll need to handle the [event](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events) with a [`type`](../../../order-management/events-and-webhooks-1/events-1/#event-types) of [`order.accepted`](../../../order-management/events-and-webhooks-1/events-1/event-types.md#order.accepted). Otherwise, if they don't make payment within the allotted time, make sure you're set up to handle [`order.cancelled`](../../../order-management/events-and-webhooks-1/events-1/event-types.md#order.cancelled).
