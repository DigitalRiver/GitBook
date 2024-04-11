---
description: >-
  Gain a better understanding of Digital River's payment reauthorization feature
  and how you might use it to sell pre-ordered goods
---

# Payment reauthorizations

You have a higher risk of [chargebacks](returns-and-refunds-1/disputes-and-chargebacks.md) when selling pre-ordered goods or managing other types of delayed fulfillments. This is due to the often-lengthy period of time between payment authorization and [capture](../developer-resources/digital-river-api-reference/payment-charges.md#captures).

If you'd like to minimize your chargeback risks, your account can be setup so that Digital River never initiates the capture and settlement process without first possessing a valid authorization. There are however potential downsides to selecting this option. For details, refer to [Managing chargeback risks](payment-reauthorizations.md#managing-chargeback-risks).

Although Digital River's payment reauthorization feature has other use cases, this article mainly focuses on strategies you could use to [process checkouts and fulfillments that contain pre-ordered goods](payment-reauthorizations.md#pre-orders).

## Managing chargeback risks

An [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) whose [`state`](../developer-resources/digital-river-api-reference/orders/the-order-lifecycle.md#order-states-and-events) moves to `accepted` indicates that the issuing bank has given approval for the transaction to proceed. But that authorization remains valid for only a limited amount of time. If it expires before a [create fulfillment request](informing-digital-river-of-a-fulfillment.md#post-fulfillments) is submitted that results in Digital River attempting to fully or partially [capture](../developer-resources/digital-river-api-reference/payment-charges.md#captures) an order's [`charges[]`](../developer-resources/digital-river-api-reference/payment-charges.md), then the issuing bank may initiate a [late presentment chargeback](../general-resources/glossary.md#late-presentment-chargebacks).  &#x20;

To manage this, we can configure your account to be [chargeback risk tolerant](payment-reauthorizations.md#risk-tolerant) or [chargeback risk averse](payment-reauthorizations.md#risk-averse). The option you instruct your Digital River representative to select helps determine the balance between the frequency of chargebacks you receive and the amount of revenue you earn. &#x20;

### Risk tolerant

If your account is configured to be risk tolerant, then Digital River attempts to [capture](../developer-resources/digital-river-api-reference/payment-charges.md#captures) and settle using the original authorization, even when it has expired and we're unable to create a new one to replace it.  &#x20;

By default, all accounts are set up to be risk tolerant.&#x20;

In most cases, this option ensures your revenue opportunities are being optimized. It does however carry a slightly higher risk of [late presentment chargebacks](../general-resources/glossary.md#late-presentment-chargebacks). But these types of [chargebacks](returns-and-refunds-1/disputes-and-chargebacks.md) typically only occur in a small percentage of all [orders](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders).&#x20;

### Risk averse

If your account is configured to be risk averse, then Digital River only attempts to [capture](../developer-resources/digital-river-api-reference/payment-charges.md#captures) a [charge](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Charges) when (1) the original payment authorization has yet to expire or (2) we're able to secure a new authorization to replace the expired one. In other words, Digital River never attempts to force settle on an expired authorization.&#x20;

With this option, you can minimize [late presentment chargebacks](../general-resources/glossary.md#late-presentment-chargebacks). However, by setting up your account to be risk averse, you do run the risk of losing out on potential revenue. This is because a high percentage of expired authorization capture attempts are ultimately approved by the issuing bank.&#x20;

## Pre-orders

By allowing customers to pre-order goods, you can sell products that are not yet available or those that are out of stock. This can be useful if you want to generate excitement around an upcoming release or forecast demand for a new product.

In this section, you'll find information on how to [handle checkouts](payment-reauthorizations.md#handling-pre-order-checkouts) and [process fulfillments](payment-reauthorizations.md#processing-pre-order-fulfillments) that contain pre-ordered goods.&#x20;

### Handling pre-order checkouts

In the Digital River APIs, checkouts that involve pre-ordered goods don't require any unique customizations. This means you're not required to pass any additional data in [SKUs](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SKUs), [checkouts](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts), or [checkout-sessions](../developer-resources/digital-river-api-reference/checkout-sessions.md). &#x20;

With the pre-orders feature:

* You can select the [Direct Integration](../integration-options/checkouts/) or [Low-code checkouts](../integration-options/low-code-checkouts/) as your checkout solution.
* A [checkout](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) or [checkout-session's](../developer-resources/digital-river-api-reference/checkout-sessions.md) `items[]` can be [physical or digital](../product-management/skus.md#how-products-are-classified-as-physical-or-digital). Additionally, they can be a mix of pre-ordered and "normal" goods.&#x20;
* Customers checking out can either be guests or [registered in Digital River's system](../customer-management/customers.md).
* In registered [checkouts](../integration-options/checkouts/creating-checkouts/using-the-checkout-identifier.md#registered-checkouts-or-invoices) and [checkout-sessions](../developer-resources/digital-river-api-reference/checkout-sessions.md#registered-customers), the [primary payment source](../payments/payment-sources/using-the-source-identifier.md#primary-payment-sources) doesn't need to be saved to the [customer](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Customers).
* Customers can select from any of [our supported payment methods](../payments/supported-payment-methods/).&#x20;

### Processing pre-order fulfillments

Depending on whether your account is set up to be [risk tolerant](payment-reauthorizations.md#risk-tolerant) or [risk averse](payment-reauthorizations.md#risk-averse), the following sections outline, at a high-level, some possible approaches to fulfilling pre-ordered goods.&#x20;

The actual solution you implement is highly dependent on your fulfillment setup. For example, you'll likely need to analyze how your fulfiller and warehouses communicate, the responsiveness of that integration and at what points in the pipeline shipments can be cancelled.&#x20;

{% hint style="success" %}
Whichever [chargeback risk option](payment-reauthorizations.md#managing-chargeback-risks) you select, the [order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) `state` should be [`accepted`](creating-and-updating-an-order.md#handling-accepted-orders) before you initiate fulfillment operations.&#x20;
{% endhint %}

<figure><img src="../.gitbook/assets/Preorders - small (1).png" alt=""><figcaption></figcaption></figure>

#### Risk tolerant fulfillments

If your account is set up to be [risk tolerant](payment-reauthorizations.md#risk-tolerant), wait until the [order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) pre-ordered `items[]` are ready to be released and then instruct your fulfiller to ship them. Once your fulfiller notifies you that the goods are in transit, send Digital River a [`POST /fulfillments`](informing-digital-river-of-a-fulfillment.md#post-fulfillments) request that includes any [tracking data](informing-digital-river-of-a-fulfillment.md#tracking-data) they may have provided, along with the `quantity` of each `items[]` that's getting delivered.&#x20;

```json
curl --location --request POST 'https://api.digitalriver.com/fulfillments' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer <Secret API key>' \
...
--data-raw '{
    "orderId": "250956650336",
    "items": [
        {
            "itemId": "180179270336",
            "quantity": "2"
        }
    ],
    "trackingCompany": "Fedex",
    "trackingNumber": "Z10100002632653",
    "trackingUrl": "http://www.fedex.com/Tracking?tracknumbers=Z10100002632653"
}'
```

Whether Digital River (1) attempts to capture and settle on the original payment authorization because it has yet to expire, (2) successfully creates a new authorization to replace the expired one or (3) fails to create a new authorization and then force settles on the original, expired one, your request immediately returns a [fulfillment](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Fulfillments) and this results in the creation of an [event](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events) whose [`type`](events-and-webhooks-1/events-1/#event-types) is  `order.charge.capture.pending` and whose [`data.object`](events-and-webhooks-1/events-1/#event-data) is a [charge](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Charges).&#x20;

Both of these notifications indicate that Digital River is in the process of attempting to [capture](../developer-resources/digital-river-api-reference/payment-charges.md#captures) that [charge](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Charges).

{% tabs %}
{% tab title="Fulfillment" %}
```json
{
    "id": "ful_c80eed02-6664-4570-9f96-b0c91bf56f1e",
    "createdTime": "2023-01-03T20:17:17Z",
    "items": [
        {
            "quantity": 2,
            "cancelQuantity": 0,
            "skuId": "bda6f910-1135-4e28-bd7b-fd42b592e5e6",
            "itemId": "180179270336"
        }
    ],
    "orderId": "250956650336",
    "trackingCompany": "Fedex",
    "trackingNumber": "Z10100002632653",
    "trackingUrl": "http://www.fedex.com/Tracking?tracknumbers=Z10100002632653",
    "liveMode": false
}
```
{% endtab %}

{% tab title="Event" %}
```json
{
    "id": "f1ce58d1-eef2-4d42-8f42-902ae595bc86",
    "type": "order.charge.capture.pending",
    "data": {
        "object": {
            "id": "788f5e05-21df-40ef-aa57-dd30f2537b72",
            "createdTime": "2023-01-03T20:16:57Z",
            "currency": "USD",
            "amount": 27.01,
            "state": "processing",
            "orderId": "250956650336",
            "captured": true,
            "captures": [
                {
                    "id": "ab7c6657-0f4e-4a7c-ab12-97dab4d3d7aa",
                    "createdTime": "2023-01-03T20:17:19Z",
                    "amount": 27.01,
                    "state": "pending",
                    "fulfillmentId": "ful_c80eed02-6664-4570-9f96-b0c91bf56f1e"
                }
            ],
            "refunded": false,
            "sourceId": "b9b0cce6-a170-42da-9e64-cf3e34e22023",
            "paymentSessionId": "2d656f29-5ee4-472d-8466-07e5685c60cc",
            "type": "customer_initiated",
            "liveMode": false
        }
    },
    "liveMode": false,
    "createdTime": "2023-01-03T20:17:19.555734Z",
    "digitalriverVersion": "2021-12-13"
}
```
{% endtab %}
{% endtabs %}

Once the payment processor informs Digital River whether the [capture](../developer-resources/digital-river-api-reference/payment-charges.md#captures) succeeded or failed, we create an [event](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events) whose [`type`](events-and-webhooks-1/events-1/#event-types) is either `order.charge.capture.complete` or `order.charge.capture.failed`, respectively. &#x20;

Both of them could be used to trigger a function that updates the status of the payment in your system. Additionally, you might use the failed event's `captures[].fulfillmentId` to look up the [fulfillment](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Fulfillments) and then send a request to your fulfiller that attempts to cancel shipment of those goods. &#x20;

#### Risk averse fulfillments

If your account is set up to be [risk averse](payment-reauthorizations.md#risk-averse), wait until the [order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) pre-ordered `items[]` are ready to be released and then send Digital River a [`POST /fulfillments`](informing-digital-river-of-a-fulfillment.md#post-fulfillments) request that specifies the `quantity` of each `items[]` that's scheduled to be shipped.&#x20;

<pre class="language-json"><code class="lang-json">curl --location 'https://api.digitalriver.com/fulfillments' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer &#x3C;Your secret key>' \
<strong>--header 'Cookie: incap_ses_1164_1638494=wJA7XORjxj+de56Y81wnECTPLmUAAAAAcw3fjSPvsJPHwenpL9OI/g==; incap_ses_1534_1638494=/hPSMOaK7w7KTFIWa91JFZ3bLmUAAAAAHPBG8qox2FXXecPq/VN/9A==; nlbi_1638494=Ny5HJhNmOV4dDgfWvwbRrQAAAADj0b73/HZghorTOo7vClvB; nlbi_1638494_1914372=65A9PK9ExhPm9B9pvwbRrQAAAACALsnE+1WpHbkZHBURlxq7; visid_incap_1638494=ZgPNr8DiSPety37xbpnVqijUnmQAAAAAQUIPAAAAAAC6uhinP72rh9xkXa7aYFH+' \
</strong>--data '{
    "orderId": "291973150336",
    "items": [
        {
            "itemId": "225220780336",
            "quantity": "1"
        }
    ]
}'
</code></pre>

At this point, your integration should be setup to handle both [success](payment-reauthorizations.md#success-response) and [failure](payment-reauthorizations.md#failure-response) responses.&#x20;

#### **Success response**

If Digital River determines that the original payment authorization has yet to expire or (in the event that it's no longer valid) successfully creates a new authorization, then your `POST/ fulfillments` request immediately returns a [fulfillment](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Fulfillments) and this results in the creation of an [event](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events) whose [`type`](events-and-webhooks-1/events-1/#event-types) is `order.charge.capture.pending` and whose [`data.object`](events-and-webhooks-1/events-1/#event-data) is a [charge](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Charges).

{% tabs %}
{% tab title="Fulfillment" %}
```json
{
    "id": "ful_8b9cfa72-0f04-46a4-abfe-eed7066bf586",
    "createdTime": "2023-10-17T19:11:19Z",
    "items": [
        {
            "quantity": 1,
            "cancelQuantity": 0,
            "skuId": "d95b458d-1752-4729-b702-bf24a9fd3020",
            "itemId": "225220780336"
        }
    ],
    "orderId": "291973150336",
    "liveMode": false
}
```
{% endtab %}

{% tab title="Event" %}
```json
{
    "id": "0305c160-e4d6-4989-ab5c-2df51e8b52ec",
    "type": "order.charge.capture.pending",
    "data": {
        "object": {
            "id": "31be0455-c7ca-4ee0-9671-e27ac0b54934",
            "createdTime": "2023-10-17T19:11:02Z",
            "currency": "USD",
            "amount": 510.0,
            "state": "processing",
            "orderId": "291973150336",
            "captured": true,
            "captures": [
                {
                    "id": "8cab6d36-1a98-47a5-9866-a647cd40b1a6",
                    "createdTime": "2023-10-17T19:11:20Z",
                    "amount": 510.0,
                    "state": "pending",
                    "fulfillmentId": "ful_8b9cfa72-0f04-46a4-abfe-eed7066bf586"
                }
            ],
            "refunded": false,
            "sourceId": "b2a9e5c2-41bd-47af-934f-04bdbdc3446e",
            "paymentSessionId": "39fbb708-e186-4c49-a192-261e2c39c22f",
            "type": "customer_initiated",
            "liveMode": false
        }
    },
    "liveMode": false,
    "createdTime": "2023-10-17T19:11:20.718668Z",
    "digitalriverVersion": "2021-12-13"
}
```
{% endtab %}
{% endtabs %}

Both of these notifications indicate that we're in the process of attempting to [capture](../developer-resources/digital-river-api-reference/payment-charges.md#captures) the [charge](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Charges).&#x20;

At this point, you should send a request to your fulfiller instructing them to ship the goods and, once they notify you that they're in transit, [update the fulfillment with tracking data](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Fulfillments/operation/updateFulfillments).&#x20;

{% hint style="success" %}
Passing `trackingCompany`, `trackingNumber`, and `trackingUrl` in this update request helps Digital River detect fraud and manage chargeback risks.
{% endhint %}

```json
curl --location 'https://api.digitalriver.com/fulfillments/ful_8b9cfa72-0f04-46a4-abfe-eed7066bf586' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer <Your secret key>' \
--header 'Cookie: incap_ses_1164_1638494=wJA7XORjxj+de56Y81wnECTPLmUAAAAAcw3fjSPvsJPHwenpL9OI/g==; incap_ses_1534_1638494=/hPSMOaK7w7KTFIWa91JFZ3bLmUAAAAAHPBG8qox2FXXecPq/VN/9A==; nlbi_1638494=Ny5HJhNmOV4dDgfWvwbRrQAAAADj0b73/HZghorTOo7vClvB; nlbi_1638494_1914372=65A9PK9ExhPm9B9pvwbRrQAAAACALsnE+1WpHbkZHBURlxq7; visid_incap_1638494=ZgPNr8DiSPety37xbpnVqijUnmQAAAAAQUIPAAAAAAC6uhinP72rh9xkXa7aYFH+' \
--data '{
    "trackingCompany": "UPS",
    "trackingNumber": "Z10100002632653",
    "trackingUrl": "http://www.ups.com/Tracking?tracknumbers=Z10100002632653",
    "items": [
        {
            "itemId": 225220780336
        }
    ]
}'
```

Once the payment processor informs Digital River whether the [capture](../developer-resources/digital-river-api-reference/payment-charges.md#captures) succeeded or failed, we create an [event](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events) whose [`type`](events-and-webhooks-1/events-1/#event-types) is either `order.charge.capture.complete` or `order.charge.capture.failed`, respectively. &#x20;

Both of them could be used to trigger a function that updates the status of the payment in your system. Additionally, you might use the failed event's `captures[].fulfillmentId` to look up the [fulfillment](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Fulfillments) and then send a request to your fulfiller that attempts to cancel shipment of those goods.&#x20;

#### **Failure response**

If Digital River determines that the original payment authorization has expired and is unable to get the issuing bank to grant a new authorization, then your `POST/ fulfillments` request immediately returns an error with a [`code`](https://www.digitalriver.com/docs/digital-river-api-reference/#section/Response-status-codes/Error-codes) of `payment_authorization_failed` and this results in the creation of an [event](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events) whose [`type`](events-and-webhooks-1/events-1/#event-types) is `order.charge.reauth.failed` and whose [`data.object`](events-and-webhooks-1/events-1/#event-data) is the [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders). &#x20;

Both of these notifications indicate that we won't be able to [capture](../developer-resources/digital-river-api-reference/payment-charges.md#captures) the [charge](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Charges).

{% tabs %}
{% tab title="Error" %}
{% code title="409 Conflict" %}
```json
{
    "errors": [
        {
            "code": "payment_authorization_failed",
            "description": "Fulfillment cannot be processed because the payment authorization has expired",
            "parameter": "orderId"
        }
    ]
}
```
{% endcode %}
{% endtab %}

{% tab title="Event" %}
```json
{
    "id": "d83b5e90-249f-4050-8103-59de3132f68d",
    "type": "order.charge.reauth.failed",
    "data": {
        "object": {
            "id": "1066128630082",
            "createdTime": "2022-12-30T18:03:13Z",
            "currency": "USD",
            "email": "aa@fraud.com",
            "billTo": {
                "address": {
                    "line1": "1234 Fake St.",
                    "city": "Minnetonka",
                    "postalCode": "55341",
                    "state": "MN",
                    "country": "US"
                },
                "name": "Guy Incognito",
                "phone": "123456789",
                "email": "aa@fraud.com"
            },
            "totalAmount": 5.37,
            "subtotal": 5.0,
            "totalFees": 0.0,
            "totalTax": 0.37,
            "totalImporterTax": 0.0,
            "totalDuty": 0.0,
            "totalDiscount": 0.0,
            "totalShipping": 0.0,
            "items": [
                {
                    "id": "53039420082",
                    "skuId": "sku_3bb13d1d-1904-486b-9975-38f457c1b4c7",
                    "productDetails": {
                        "id": "sku_3bb13d1d-1904-486b-9975-38f457c1b4c7",
                        "name": "productName_test_fulDigital13",
                        "countryOfOrigin": "US"
                    },
                    "amount": 5.0,
                    "quantity": 1,
                    "metadata": {
                        "key11": "value",
                        "key12": "value"
                    },
                    "state": "created",
                    "stateTransitions": {
                        "created": "2022-12-30T18:03:13Z"
                    },
                    "tax": {
                        "rate": 0.07375,
                        "amount": 0.37
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
                    "shipping": {
                        "amount": 0.0,
                        "taxAmount": 0.0
                    }
                }
            ],
            "updatedTime": "2022-12-30T18:03:13Z",
            "locale": "en_US",
            "customerType": "individual",
            "sellingEntity": {
                "id": "C5_INC-ENTITY",
                "name": "DR globalTech Inc."
            },
            "liveMode": false,
            "payment": {
                "charges": [
                    {
                        "id": "cad13169-727f-4a48-bf0e-a0212475bf18",
                        "createdTime": "2022-12-30T18:03:16Z",
                        "currency": "USD",
                        "amount": 5.37,
                        "state": "capturable",
                        "captured": false,
                        "refunded": false,
                        "sourceId": "d3832f94-9fcd-458c-8f78-2c9d1f932f6f",
                        "type": "customer_initiated"
                    }
                ],
                "sources": [
                    {
                        "id": "d3832f94-9fcd-458c-8f78-2c9d1f932f6f",
                        "type": "creditCard",
                        "amount": 5.37,
                        "owner": {
                            "firstName": "Guy",
                            "lastName": "Incognito",
                            "email": "aa@fraud.com",
                            "address": {
                                "line1": "1234 Fake St.",
                                "city": "Minnetonka",
                                "postalCode": "55341",
                                "state": "MN",
                                "country": "US"
                            }
                        },
                        "creditCard": {
                            "brand": "Visa",
                            "expirationMonth": 10,
                            "expirationYear": 2022,
                            "lastFourDigits": "3676"
                        }
                    }
                ],
                "session": {
                    "id": "ab2ee4bc-7b30-4346-9fef-94e026f8edb6",
                    "amountContributed": 5.37,
                    "amountRemainingToBeContributed": 0.0,
                    "state": "complete",
                    "clientSecret": "ab2ee4bc-7b30-4346-9fef-94e026f8edb6_b8d8df52-111c-495c-9907-c7aad53e7cde"
                }
            },
            "state": "accepted",
            "stateTransitions": {
                "accepted": "2022-12-30T18:03:17Z"
            },
            "fraudState": "passed",
            "fraudStateTransitions": {
                "passed": "2022-12-30T18:03:17Z"
            },
            "requestToBeForgotten": false,
            "capturedAmount": 0.0,
            "cancelledAmount": 0.0,
            "availableToRefundAmount": 0.0,
            "checkoutId": "7c8c0525-e133-40a6-94d9-f0427266b5e1"
        }
    },
    "liveMode": false,
    "createdTime": "2022-12-30T18:03:23.12606Z",
    "digitalriverVersion": "2021-12-13"
}
```
{% endtab %}
{% endtabs %}

The `payment_authorization_failed` error could trigger a request to your fulfiller that instructs them to cancel the order before the goods are shipped.&#x20;

From the event, you could retrieve [`items[].productDetails`](../product-management/using-product-details.md), `payment.sources[]`, and other data and use it to populate a [payment failed notification](customer-notifications.md) (typically an email) that gets sent to the customer. If it's supported by your business model, you could also attempt to get a new payment method from the customer.&#x20;

{% hint style="warning" %}
If you have a transaction that contains multiple pre-ordered items, but they're not all ready to ship at the same time, and you send a [`POST /fulfillments`](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Fulfillments/operation/createFulfillments) with a partial `quantity` of these `items[]` that throws a payment authorization failed exception, then any subsequent capture attempts are also likely to fail. As result, in this particular scenario, we recommend that you cancel all of that transaction's pre-ordered items.&#x20;
{% endhint %}

## Testing reauthorizations

Our [payments mocker](../developer-resources/testing-scenarios.md) doesn't currently support testing reauthorizations in a [non-production environment](../developer-resources/api-structure.md#test-and-production-environments). However, once feature-specific test credit card numbers become available, we'll add them to the docs. &#x20;
