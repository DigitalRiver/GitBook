---
description: Learn about the order dispute and chargeback process
---

# Disputes and chargebacks

A chargeback is a [charge](../../developer-resources/digital-river-api-reference/payment-charges.md) that is reversed by a customer's bank. In the Digital River APIs, chargebacks can occur on credit cards and [debit cards](../../payments/payment-integrations-1/digitalriver.js/payment-methods/direct-debit.md) as well as certain types of [wire transfer](https://www.digitalriver.com/payment-types/wire-transfer/), [bank transfer](https://www.digitalriver.com/payment-types/bank-transfer/), [buy now pay later](https://www.digitalriver.com/payment-types/buy-now-pay-later/), and [digital wallet](https://www.digitalriver.com/payment-types/digital-wallet/) payments.

Chargeback requests received by Digital River most often originate with customers noticing what they believe to be an unauthorized transaction on their statement and then contacting their bank to dispute the charge. Other common reasons for chargeback requests include:

* A credit was not processed by an expected date
* The ordered goods never arrived or the service was not provided
* The merchandise was defective or not as described
* A service was not performed as expected

Once the dispute process is initiated, the bank, acting on behalf of the customer, may contact the merchant and ask for more details. Depending on the results of that inquiry, the bank then sends a separate request to the payment processors that either seeks additional information or pushes for a chargeback. The payment processors, serving as intermediaries, relay the bank's request to Digital River.

Once Digital River receives the relayed request, we move the [order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) [`state`](../../developer-resources/digital-river-api-reference/orders/the-order-lifecycle.md#order-states-and-events) into `dispute`, create an `order.dispute` event, and populate `stateTransitions.dispute` with a timestamp. This is true whether the bank is requesting a chargeback or simply seeking more information.

{% code title="order.dispute" %}
```
{
    "id": "6747186a-9b84-4d6e-bccb-a5a0c4530e5d",
    "type": "order.dispute",
    "data": {
        "object": {
            "id": "1005692492420",
            "createdTime": "2022-02-15T06:36:50Z",
            "currency": "USD",
            "email": "testing@test.com",
            "shipTo": {
                "address": {
                    "line1": "1 Broadway Ave",
                    "city": "Lincoln",
                    "postalCode": "68501",
                    "state": "NE",
                    "country": "US"
                },
                "name": "John Doe",
                "email": "Test@testing.com"
            },
            "shipFrom": {
                "address": {
                    "line1": "Address",
                    "city": "TesterVille2",
                    "postalCode": "12345",
                    "state": "MN",
                    "country": "US"
                }
            },
            "billTo": {
                "address": {
                    "line1": "10380 Bren Road West",
                    "city": "Minnetonka",
                    "postalCode": "55343",
                    "state": "MN",
                    "country": "US"
                },
                "name": "Jane Doe",
                "email": "jdoe@digitalriver.com"
            },
            "totalAmount": 0.32,
            "subtotal": 0.3,
            "totalFees": 0.0,
            "totalTax": 0.02,
            "totalImporterTax": 0.0,
            "totalDuty": 0.0,
            "totalDiscount": 0.0,
            "totalShipping": 0.2,
            "items": [
                {
                    "id": "1006284504120",
                    "skuId": "a2fd1787-041f-418a-8dc4-f8a92fb31f3f",
                    "amount": 0.1,
                    "quantity": 1,
                    "state": "created",
                    "stateTransitions": {
                        "created": "2022-02-15T06:36:50Z",
                        "fulfilled": "2022-02-15T06:37:14Z"
                    },
                    "tax": {
                        "rate": 0.0725,
                        "amount": 0.01
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
                    }
                }
            ],
            "shippingChoice": {
                "amount": 0.2,
                "description": "Client provides-Standard Ground - US",
                "serviceLevel": "Client provides shipping service",
                "taxAmount": 0.01
            },
            "updatedTime": "2022-02-17T21:10:22Z",
            "locale": "en_US",
            "customerType": "individual",
            "sellingEntity": {
                "id": "C5_INC-ENTITY",
                "name": "DR globalTech Inc."
            },
            "liveMode": true,
            "payment": {
                "charges": [
                    {
                        "id": "951cbb9b-7e41-4d03-80ae-75eec2ba00c4",
                        "createdTime": "2022-02-15T06:36:35Z",
                        "currency": "USD",
                        "amount": 0.32,
                        "state": "complete",
                        "captured": true,
                        "captures": [
                            {
                                "id": "d59e31a0-7c79-4426-947a-51dcfb66409c",
                                "createdTime": "2022-02-15T06:37:57Z",
                                "amount": 0.32,
                                "state": "complete"
                            }
                        ],
                        "refunded": false,
                        "sourceId": "2ecc1ab3-5880-4e00-8a87-d231a4709c25",
                        "type": "customer_initiated"
                    }
                ],
                "sources": [
                    {
                        "id": "2ecc1ab3-5880-4e00-8a87-d231a4709c25",
                        "type": "creditCard",
                        "amount": 0.32,
                        "owner": {
                            "firstName": "Jane",
                            "lastName": "Doe",
                            "email": "jdoe@digitalriver.com",
                            "address": {
                                "line1": "10380 Bren Road West",
                                "city": "Minnetonka",
                                "postalCode": "55343",
                                "state": "MN",
                                "country": "US"
                            }
                        },
                        "creditCard": {
                            "brand": "Visa",
                            "expirationMonth": 12,
                            "expirationYear": 2024,
                            "lastFourDigits": "1406",
                            "fundingSource": "prepaid"
                        }
                    }
                ],
                "session": {
                    "id": "8159c06d-8dc1-45ce-910c-f2d442c39041",
                    "amountContributed": 0.32,
                    "amountRemainingToBeContributed": 0.0,
                    "state": "complete",
                    "clientSecret": "8159c06d-8dc1-45ce-910c-f2d442c39041_d00695b2-71ab-48ef-9bc3-8660f045b627"
                }
            },
            "state": "dispute",
            "stateTransitions": {
                "dispute": "2022-02-17T21:10:22Z",
                "fulfilled": "2022-02-15T06:37:14Z",
                "accepted": "2022-02-15T06:36:57Z",
                "complete": "2022-02-15T23:28:31Z"
            },
            "fraudState": "review_opened",
            "fraudStateTransitions": {
                "review_opened": "2022-02-17T21:10:22Z",
                "passed": "2022-02-15T06:36:57Z"
            },
            "requestToBeForgotten": false,
            "capturedAmount": 0.32,
            "cancelledAmount": 0.0,
            "availableToRefundAmount": 0.21,
            "invoicePDFs": [
                {
                    "id": "bd19832f-6136-4af1-b96b-1ff874e78c7f",
                    "url": "https://api.digitalriver.com/files/bd19832f-6136-4af1-b96b-1ff874e78c7f/content",
                    "liveMode": false
                }
            ],
            "checkoutId": "bde55f0a-27fe-4562-8852-93e7df022360"
        }
    },
    "liveMode": true,
    "createdTime": "2022-02-17T21:10:27.642913Z",
    "digitalriverVersion": "2021-12-13"
}
```
{% endcode %}

While an [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) is in `dispute`, you're not allowed to [capture or cancel payment](../informing-digital-river-of-a-fulfillment.md), [issue refunds](refunds/issuing-refunds.md) or [process returns](returns/) on that order.

If you attempt to submit a [`POST/fulfillments`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createFulfillments), [`POST/refunds`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createRefunds) or [`POST/returns`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createReturns) while an [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) is in `dispute`, then the following errors are returned:

{% tabs %}
{% tab title="POST/fulfillments" %}
{% code title="409 Conflict" %}
```javascript
{
    "type": "conflict",
    "errors": [
        {
            "code": "order_not_submitted",
            "parameter": "orderId",
            "message": "Order '1002363590082' has not been submitted."
        }
    ]
}
```
{% endcode %}
{% endtab %}

{% tab title="POST/refunds" %}
{% code title="400 Bad Request" %}
```javascript
{
    "type": "bad_request",
    "errors": [
        {
            "code": "invalid_parameter",
            "parameter": "order",
            "message": "A refund cannot be performed while there is a dispute on the order."
        }
    ]
}
```
{% endcode %}
{% endtab %}

{% tab title="POST/returns" %}
{% code title="409 Conflict" %}
```javascript
{
    "type": "conflict",
    "errors": [
        {
            "code": "invalid_parameter",
            "parameter": "order",
            "message": "A return cannot be performed while there is a dispute on the order."
        }
    ]
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

Digital River's chargeback team then works with the merchant to investigate the disputed transaction and prepare a response. This typically involves gathering proof of delivery receipts, customer acceptance emails, order invoices, as well as any other relevant documentation, and then sending that information to the payment processors so they can relay it to the bank.

Once the dispute is resolved, the [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) resumes its [lifecycle](../../developer-resources/digital-river-api-reference/orders/the-order-lifecycle.md), transitioning to a non-dispute `state`. This results in the creation of an `order.dispute.resolved` event.

```
{
    "id": "8412380f-1b8f-42c7-a6ee-8d0f46e251b3",
    "type": "order.dispute.resolved",
    "data": {
        "object": {
            "id": "1005692492420",
            "createdTime": "2022-02-15T06:36:50Z",
            "currency": "USD",
            "email": "testing@test.com",
            "shipTo": {
                "address": {
                    "line1": "1 Broadway Ave.",
                    "city": "Lincoln",
                    "postalCode": "68501",
                    "state": "NE",
                    "country": "US"
                },
                "name": "John Doe",
                "email": "Test@testing.com"
            },
            "shipFrom": {
                "address": {
                    "line1": "Address",
                    "city": "TesterVille2",
                    "postalCode": "12345",
                    "state": "MN",
                    "country": "US"
                }
            },
            "billTo": {
                "address": {
                    "line1": "10380 Bren Road West",
                    "city": "Minnetonka",
                    "postalCode": "55343",
                    "state": "MN",
                    "country": "US"
                },
                "name": "Jane Doe",
                "email": "jdoe@digitalriver.com"
            },
            "totalAmount": 0.32,
            "subtotal": 0.3,
            "totalFees": 0.0,
            "totalTax": 0.02,
            "totalImporterTax": 0.0,
            "totalDuty": 0.0,
            "totalDiscount": 0.0,
            "totalShipping": 0.2,
            "items": [
                {
                    "id": "1006284504120",
                    "skuId": "a2fd1787-041f-418a-8dc4-f8a92fb31f3f",
                    "amount": 0.1,
                    "quantity": 1,
                    "state": "fulfilled",
                    "stateTransitions": {
                        "created": "2022-02-15T06:36:50Z",
                        "fulfilled": "2022-02-17T21:16:35Z"
                    },
                    "tax": {
                        "rate": 0.0725,
                        "amount": 0.01
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
                    }
                }
            ],
            "shippingChoice": {
                "amount": 0.2,
                "description": "Client provides-Standard Ground - US",
                "serviceLevel": "Client provides shipping service",
                "taxAmount": 0.01
            },
            "updatedTime": "2022-02-17T21:16:35Z",
            "locale": "en_US",
            "customerType": "individual",
            "sellingEntity": {
                "id": "C5_INC-ENTITY",
                "name": "DR globalTech Inc."
            },
            "liveMode": true,
            "payment": {
                "charges": [
                    {
                        "id": "951cbb9b-7e41-4d03-80ae-75eec2ba00c4",
                        "createdTime": "2022-02-15T06:36:35Z",
                        "currency": "USD",
                        "amount": 0.32,
                        "state": "complete",
                        "captured": true,
                        "captures": [
                            {
                                "id": "d59e31a0-7c79-4426-947a-51dcfb66409c",
                                "createdTime": "2022-02-15T06:37:57Z",
                                "amount": 0.32,
                                "state": "complete"
                            }
                        ],
                        "refunded": false,
                        "sourceId": "2ecc1ab3-5880-4e00-8a87-d231a4709c25",
                        "type": "customer_initiated"
                    }
                ],
                "sources": [
                    {
                        "id": "2ecc1ab3-5880-4e00-8a87-d231a4709c25",
                        "type": "creditCard",
                        "amount": 0.32,
                        "owner": {
                            "firstName": "Jane",
                            "lastName": "Doe",
                            "email": "jdoe@digitalriver.com",
                            "address": {
                                "line1": "10380 Bren Road West",
                                "city": "Minnetonka",
                                "postalCode": "55343",
                                "state": "MN",
                                "country": "US"
                            }
                        },
                        "creditCard": {
                            "brand": "Visa",
                            "expirationMonth": 12,
                            "expirationYear": 2024,
                            "lastFourDigits": "1406",
                            "fundingSource": "prepaid"
                        }
                    }
                ],
                "session": {
                    "id": "8159c06d-8dc1-45ce-910c-f2d442c39041",
                    "amountContributed": 0.32,
                    "amountRemainingToBeContributed": 0.0,
                    "state": "complete",
                    "clientSecret": "8159c06d-8dc1-45ce-910c-f2d442c39041_d00695b2-71ab-48ef-9bc3-8660f045b627"
                }
            },
            "state": "accepted",
            "stateTransitions": {
                "dispute": "2022-02-17T21:10:22Z",
                "fulfilled": "2022-02-15T06:37:14Z",
                "accepted": "2022-02-15T06:36:57Z",
                "complete": "2022-02-15T23:28:31Z"
            },
            "fraudState": "passed",
            "fraudStateTransitions": {
                "review_opened": "2022-02-17T21:10:22Z",
                "passed": "2022-02-15T06:36:57Z"
            },
            "requestToBeForgotten": false,
            "capturedAmount": 0.32,
            "cancelledAmount": 0.0,
            "availableToRefundAmount": 0.21,
            "invoicePDFs": [
                {
                    "id": "bd19832f-6136-4af1-b96b-1ff874e78c7f",
                    "url": "https://api.digitalriver.com/files/bd19832f-6136-4af1-b96b-1ff874e78c7f/content",
                    "liveMode": false
                }
            ],
            "checkoutId": "bde55f0a-27fe-4562-8852-93e7df022360"
        }
    },
    "liveMode": true,
    "createdTime": "2022-02-17T21:16:38.86963Z",
    "digitalriverVersion": "2021-12-13"
}
```

If no chargeback is issued, then the [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) reverts to its pre-dispute `state`. At this point, you can perform returns, refunds, as well as capture or cancel any remaining charges.

If a chargeback is granted, then a refund is issued to the payment method used by the customer to make the purchase. In these cases, an [order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) [`availableToRefundAmount`](refunds/issuing-refunds.md#checking-the-available-refund-amount) is either reduced or drops to `0`. In the event that [`availableToRefundAmount`](refunds/issuing-refunds.md#checking-the-available-refund-amount) is only reduced, any remaining amount can still be refunded to the customer by submitting a [`POST/refunds`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createRefunds).

When Digital River processes and completes a chargeback, we create a [sales transaction](../../financial-reporting/sales-transactions/) with a `type` of `fraud_chargeback` or `non_fraud_chargeback` and send you both a `sales_transaction.created` and `order.chargeback` event.
