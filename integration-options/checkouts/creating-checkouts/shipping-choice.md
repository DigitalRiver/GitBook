---
description: Learn how to set and use a customer's shipping choice in checkouts
---

# Handling shipping choice

[Checkouts](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) with [physical products](../../../product-management/skus.md#how-products-are-classified-as-physical-or-digital) must contain a `shippingChoice`. This data structure allows you to define the delivery method selected by customers at checkout-time. After you [set `shippingChoice`](shipping-choice.md#setting-shipping-choice), you can [use the returned shipping tax amount](shipping-choice.md#using-shipping-choice) to update the checkout totals you display to customers.

## Setting shipping choice

In [`POST/checkouts`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createCheckouts) and [`POST/checkouts/{id}`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/updateCheckouts) requests, you can send the following data in `shippingChoice`:

* [A unique shipping identifier](shipping-choice.md#unique-shipping-identifier)
* [A shipping amount](shipping-choice.md#shipping-amount)
* [A shipping method's description and service level](shipping-choice.md#shipping-description-and-service-level)
* [The duty payment terms of the selected shipping method](shipping-choice.md#shipping-terms)

{% code title="POST/checkouts/{id}" %}
```javascript
curl --location --request POST 'https://api.digitalriver.com/checkouts/04ea45eb-2bb8-4ea9-a772-37e5fbd5d1fe' \
...
--data-raw '{
    "shipFrom": {
        "address": {
            "country": "US"
        }
    },
    "shippingChoice": {
        "id": "123",
        "amount": 5,
        "description": "standard",
        "serviceLevel": "SG",
        "shippingTerms": "DDP"
    }
}'
```
{% endcode %}

You're not required to send `shippingChoice` in either [create](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createCheckouts) or [update](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createCheckouts) checkout requests. But if any of a checkout's [`items[]`](describing-the-items/) contain a [physical product](../../../product-management/skus.md#how-products-are-classified-as-physical-or-digital) and `shippingChoice` isn't set when you [convert the checkout to an order](../../../order-management/creating-and-updating-an-order.md#creating-an-order-with-the-checkout-identifier), you receive a `400 Bad Request`.

{% tabs %}
{% tab title="400 Bad Request" %}
```javascript
{
    "type": "bad_request",
    "errors": [
        {
            "code": "invalid_shipping_choice",
            "parameter": "shippingChoice",
            "message": "Could not get Shipping Options for order"
        }
    ]
}
```
{% endtab %}
{% endtabs %}

### Unique shipping identifier

A [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) `shippingChoice.id` is typically a pass through value from your fulfillment or logistics provider. You're not required to provide this identifier.

If you don't send `shippingChoice.id` in the request, then Digital River doesn't generate an identifier that gets returned in the response.

### Shipping amount

You can use a [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) `shippingChoice.amount` to pass the estimated cost of a customer's shipping method selection. This value should be inclusive of handling and fees.

{% hint style="info" %}
Whether Digital River adds taxes to or extracts taxes from `shippingChoice.amount` is dependent on how you set the checkout's `taxInclusive` flag. For details, refer to the [Configuring taxes](configuring-taxes.md) page.
{% endhint %}

When [creating](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createCheckouts) or [updating](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/updateCheckouts) checkouts that contain [physical products](../../../product-management/skus.md#how-products-are-classified-as-physical-or-digital), if you send `shippingChoice` but fail to send `shippingChoice.amount`, then a `400 Bad Request` is returned.

{% tabs %}
{% tab title="400 Bad Request" %}
```javascript
{
    "type": "bad_request",
    "errors": [
        {
            "code": "internal_error",
            "message": "Client must provide shipping Cost"
        }
    ]
}
```
{% endtab %}
{% endtabs %}

### Shipping description and service level

In a [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) `shippingChoice`, you can use `serviceLevel` and `description` to describe the shipping method selected by the customer.

In [third-party coordinated fulfillments](../../../order-management/fulfillments.md#third-party-coordinated-fulfillments), you're not required to pass either of these values, but they can be useful for reporting purposes. Additionally, since it helps Digital River better detect fraud, we highly recommend that you send `serviceLevel` .

### Shipping terms

You can designate a [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) `shippingChoice.shippingTerms` as either [`DAP`](shipping-choice.md#delivered-at-place-dap) or [`DDP`](shipping-choice.md#delivered-duty-paid-ddp). The default value is `DDP`.

#### Delivered at place (DAP)

If you pass `shippingTerms` that are `DAP`, then duties and import taxes are not returned in checkouts.

For more information, refer to [triggering the landed cost feature](landed-costs.md#triggering-the-landed-cost-feature) on the [Landed cost](landed-costs.md) page.

This means that when the products are delivered, customers may be presented with a bill for any outstanding importation costs. Customers typically must pay these costs before the carrier transfers ownership.

In [checkouts](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) with `DAP` duty payment terms, you should inform customers that import charges are collected upon delivery.

You should also keep in mind that transactions which are not paid in full at the point of sale have higher rejection and return rates. This is because customers may be unaware of the outstanding balance or the outstanding balance is higher than they anticipated and, in response, they either refuse the delivery altogether or accept the products and then request a return.

#### Delivered duty paid (DDP)

If you pass `shippingTerms` that are `DDP`, and the [necessary preconditions](landed-costs.md#triggering-the-landed-cost-feature) exist to activate the [landed cost feature](landed-costs.md#digital-rivers-landed-cost-feature), then estimated duties and import taxes are returned in checkouts.

This allows you to present customers with the [full landed cost](landed-costs.md#what-is-landed-cost) of a transaction, thereby eliminating "surprise" charges at the time of delivery.

For more information, refer to the following sections on the [Landed cost](landed-costs.md) page:

* [Triggering the landed cost feature](landed-costs.md#triggering-the-landed-cost-feature)
* [How landed cost is represented in checkouts](landed-costs.md#how-landed-cost-is-represented)
* [The guaranteed landed cost feature](landed-costs.md#guaranteed-landed-cost-feature)

## Using shipping costs <a href="#using-shipping-choice" id="using-shipping-choice"></a>

Once you collect a customer's shipping method choice, and add `shippingChoice.amount` to the [checkout](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts), Digital River makes a tax computation and returns that value in `shippingChoice.taxAmount`. For each of a [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) `items[]`, Digital River also returns a `shipping` object that contains an `amount` and a `taxAmount`.

{% hint style="info" %}
All of a [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) taxes, including `shippingChoice.taxAmount`, are aggregated into `totalTax`.&#x20;
{% endhint %}

{% code title="Checkout" lineNumbers="true" %}
```json
{
    ...
    "totalShipping": 5.0,
    "items": [
        {
            ...
            "shipping": {
                "amount": 2.5,
                "taxAmount": 0.2
            }
        },
        {
            ...
            "shipping": {
                "amount": 2.5,
                "taxAmount": 0.2
            }
        }
    ],
    "shippingChoice": {
        "amount": 5.0,
        "description": "standard",
        "serviceLevel": "SG",
        "taxAmount": 0.4
    },
    ...
}
```
{% endcode %}

Each time you update the [checkout](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts), we recommend that you retrieve `shippingChoice.amount` or `totalShipping` and display this value to customers in the transaction details section of your UI. To provide customers more granularity on shipping costs, you might also decide to display each line item's `shipping.amount` and `shipping.taxAmount`.
