---
description: Learn how to apply discounts.
---

# Applying a discount

You can apply multiple [types of discounts](applying-a-discount.md#item-level-discount) to a transaction. On this page, you'll find information on how to give:&#x20;

* [Item-level discounts](applying-a-discount.md#line-item-discounts)
* [Discounts on entire purchases](applying-a-discount.md#entire-purchase-discounts)
* [Discounts on shipping costs](applying-a-discount.md#shipping-cost-discounts)

You can also read about [validation errors thrown by zero-value discounts](applying-a-discount.md#validation-errors-generated-by-zero-value-discounts).

## Types of discounts <a href="#item-level-discount" id="item-level-discount"></a>

Using [checkouts](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) or [invoices](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Invoices), you can apply discounts to (1) [line items](applying-a-discount.md#line-item-discounts), (2) an [entire purchase](applying-a-discount.md#entire-purchase-discounts), and (3) [shipping costs](applying-a-discount.md#shipping-cost-discounts). You can also [combine discount types](applying-a-discount.md#combined-discounts).

All the discount categories follow the same basic rules. For each, you specify an `amountOff` or `percentOff`. Digital River first applies the discount and then determines taxes based on that reduced amount. To determine the aggregate value of all applied discounts, check  `totalDiscount`.

### Line item discounts

For each [`items[]`](describing-the-items/) that you want to discount, set either a `percentOff` or `amountOff`.

To indicate how many products the discount should be applied to, assign an integer to  `discount.quantity`. If you don't define this parameter, then the discount is applied to the entire `quantity` of that `items[]`.&#x20;

In the following percent off request, `discount.quantity` is  `1`, so the discount isn't applied to the entire `quantity` of that `items[]`. In the amount off request, `discount.quantity` isn't defined, so the discount is applied to the entire `quantity`.

{% tabs %}
{% tab title="Percent off request" %}
```
curl https://api.digitalriver.com/checkouts \
    -u sk_test_db9682a2-b04a-4e94-8e11-35fe8ec0b324: \
    -d currency=usd \
    ...
    -d items[0][skuId]=09062016 \
    -d items[0][price]=10.00 \
    -d items[0][quantity]=3
    -d items[0][discount][percentOff]=10
    -d items[0][discount][quantity]=1
```
{% endtab %}

{% tab title="Amount off request" %}
```
curl https://api.digitalriver.com/checkouts \
    -u sk_test_db9682a2-b04a-4e94-8e11-35fe8ec0b324: \
    -d currency=usd \
    ...
    -d items[0][skuId]=09062016 \
    -d items[0][price]=10.00 \
    -d items[0][quantity]=3
    -d items[0][discount[amountOff]]=2
```
{% endtab %}
{% endtabs %}

In the response, each `items[].amount` is adjusted to reflect the discount and `totalDiscount` sums up all the markdowns for the transaction.

{% tabs %}
{% tab title="Percent off response" %}
```javascript
    ...
    "totalAmount": 31.18,
    "subtotal": 29.0,
    "totalFees": 0.0,
    "totalTax": 2.18,
    "totalDuty": 0.0,
    "totalDiscount": 1.0,
    "totalShipping": 0.0,
    "items": [
        {
            "skuId": "09062016",
            "amount": 29.0,
            "quantity": 3,
            "discount": {
                "percentOff": 10.0,
                "quantity": 1
            },
            "tax": {
                "rate": 0.07525,
                "amount": 2.18
            }
        }
    ],
    ...
```
{% endtab %}

{% tab title="Amount off response" %}
```javascript
    ...
    "totalAmount": 25.81,
    "subtotal": 24.0,
    "totalFees": 0.0,
    "totalTax": 1.81,
    "totalDuty": 0.0,
    "totalDiscount": 6.0,
    "totalShipping": 0.0,
    "items": [
        {
            "skuId": "09062016",
            "amount": 24.0,
            "quantity": 3,
            "discount": {
                "amountOff": 2.0,
                "quantity": 3
            },
            "tax": {
                "rate": 0.07525,
                "amount": 1.81
            }
        }
    ],
    ...
```
{% endtab %}
{% endtabs %}

### Entire purchase discounts

To reduce the cost of an entire transaction, define either `discount.percentOff` or `discount.amountOff` .

{% tabs %}
{% tab title="Percent off request" %}
```
curl https://api.digitalriver.com/checkouts \
    -u sk_test_db9682a2-b04a-4e94-8e11-35fe8ec0b324: \
    -d currency=usd \
    ...
    -d discount[percentOff]=20
    -d items[0][skuId]=09062016 \
    -d items[0][price]=10.00 \
    -d items[0][quantity]=4 \
    -d items[1][skuId]=11141976 \
    -d items[1][price]=20.00 \
    -d items[1][quantity]=2 \
```
{% endtab %}

{% tab title="Amount off request" %}
```
curl https://api.digitalriver.com/checkouts \
    -u sk_test_db9682a2-b04a-4e94-8e11-35fe8ec0b324: \
    -d currency=usd \
    ...
    -d discount[amountOff]=10
    -d items[0][skuId]=09062016 \
    -d items[0][price]=10.00 \
    -d items[0][quantity]=4 \
    -d items[1][skuId]=11141976 \
    -d items[1][price]=20.00 \
    -d items[1][quantity]=2 \
```
{% endtab %}
{% endtabs %}

Digital River aggregates all the `items[].amount` values, applies the discount to arrive at a `subTotal` and then uses that figure to compute a `totalTax`.&#x20;

{% tabs %}
{% tab title="Percent off response" %}
```javascript
    ...
    "totalAmount": 68.82,
    "subtotal": 64.0,
    "totalFees": 0.0,
    "totalTax": 4.82,
    "totalDuty": 0.0,
    "totalDiscount": 16.0,
    "totalShipping": 0.0,
    "discount": {
        "percentOff": 20.0
    },
    "items": [
        {
            "skuId": "09062016",
            "amount": 40.0,
            "quantity": 4,
            "tax": {
                "rate": 0.07525,
                "amount": 2.41
            }
        },
        {
            "skuId": "11141976",
            "amount": 40.0,
            "quantity": 2,
            "tax": {
                "rate": 0.07525,
                "amount": 2.41
            }
        }
    ],
    ...
```
{% endtab %}

{% tab title="Amount off response" %}
```javascript
    ...
    "totalAmount": 75.26,
    "subtotal": 70.0,
    "totalFees": 0.0,
    "totalTax": 5.26,
    "totalDuty": 0.0,
    "totalDiscount": 10.0,
    "totalShipping": 0.0,
    "discount": {
        "amountOff": 10.0
    },
    "items": [
        {
            "skuId": "09062016",
            "amount": 40.0,
            "quantity": 4,
            "tax": {
                "rate": 0.07525,
                "amount": 2.63
            }
        },
        {
            "skuId": "11141976",
            "amount": 40.0,
            "quantity": 2,
            "tax": {
                "rate": 0.07525,
                "amount": 2.63
            }
        }
    ],
    ...
```
{% endtab %}
{% endtabs %}

### Shipping cost discounts

You can also apply discounts to shipping costs. The following `POST /checkouts` demonstrates how to use `shippingDiscount` to specify either a `percentOff` or `amountOff`:

{% tabs %}
{% tab title="Percent off request" %}
```
curl https://api.digitalriver.com/checkouts \
     -u sk_test_db9682a2-b04a-4e94-8e11-35fe8ec0b324: \
     -d currency=usd \
     ...
     -d items[0][skuId]=09062016 \
     -d items[0][price]=10.00 \
     -d items[0][quantity]=3
     -d shippingChoice[amount]=8.00 \
     -d shippingChoice[description]="USPS: Priority (1 day delivery)" \
     -d shippingChoice[serviceLevel]= "SG"
     -d shippingDiscount[percentOff]=25
```
{% endtab %}

{% tab title="Amount off request" %}
```
curl https://api.digitalriver.com/checkouts \
     -u sk_test_db9682a2-b04a-4e94-8e11-35fe8ec0b324: \
     -d currency=usd \
     ...
     -d items[0][skuId]=09062016 \
     -d items[0][price]=10.00 \
     -d items[0][quantity]=3
     -d shippingChoice[amount]=8.00 \
     -d shippingChoice[description]="USPS: Priority (1 day delivery)" \
     -d shippingChoice[serviceLevel]= "SG"
     -d shippingDiscount[amountOff]=3.00
```
{% endtab %}
{% endtabs %}

Digital River applies the discount before calculating taxes and `totalDiscount` includes the shipping cost discount.

{% tabs %}
{% tab title="Percent off response" %}
```javascript
    ...
    "totalAmount": 38.71,
    "subtotal": 36.0,
    "totalFees": 0.0,
    "totalTax": 2.71,
    "totalDuty": 0.0,
    "totalDiscount": 2.0,
    "totalShipping": 8.0,
    "items": [
        {
            "skuId": "09062016",
            "amount": 30.0,
            "quantity": 3,
            "tax": {
                "rate": 0.07525,
                "amount": 2.26
            }
        }
    ],
    "shippingChoice": {
        "amount": 8.0,
        "description": "USPS: Priority (1 day delivery)",
        "serviceLevel": "SG",
        "taxAmount": 0.45
    },
    "shippingDiscount": {
        "percentOff": 25.0
    },
    ...
```
{% endtab %}

{% tab title="Amount off response" %}
```javascript
    ...
    "totalAmount": 37.64,
    "subtotal": 35.0,
    "totalFees": 0.0,
    "totalTax": 2.64,
    "totalDuty": 0.0,
    "totalDiscount": 3.0,
    "totalShipping": 8.0,
    "items": [
        {
            "skuId": "09062016",
            "amount": 30.0,
            "quantity": 3,
            "tax": {
                "rate": 0.07525,
                "amount": 2.26
            }
        }
    ],
    "shippingChoice": {
        "amount": 8.0,
        "description": "USPS: Priority (1 day delivery)",
        "serviceLevel": "SG",
        "taxAmount": 0.38
    },
    "shippingDiscount": {
        "amountOff": 3.0
    },
    ...
```
{% endtab %}
{% endtabs %}

### Combined discounts

If you include multiple [discount types](applying-a-discount.md#item-level-discount) in a request, Digital River first applies any line-item discounts and then the entire purchase markdown. Product and order-level discounts don't reduce shipping costs. If you want to give customers a break on their shipping, you'll need to apply a shipping discount.

## Validation errors generated by zero-value discounts

You must send a discount value greater than zero. This applies to all [types of discounts](applying-a-discount.md#item-level-discount).&#x20;

If you submit a `POST /checkouts`, `POST /checkouts/{id}` or `POST /invoices` and `amountOff` or `percentOff` is `0` or less, a `400 Bad Request` is returned.

{% tabs %}
{% tab title="Percent off" %}
```javascript
{
    "type": "bad_request",
    "errors": [
        {
            "code": "invalid_discount_percent",
            "parameter": "discount",
            "message": "The value must be an integer between 0.01 and 100.00 inclusive."
        }
    ]
}
```
{% endtab %}

{% tab title="Amount off" %}
```javascript
{
    "type": "bad_request",
    "errors": [
        {
            "code": "invalid_discount_amount",
            "parameter": "discount",
            "message": "The value 0.0 is not permitted."
        }
    ]
}
```
{% endtab %}
{% endtabs %}
