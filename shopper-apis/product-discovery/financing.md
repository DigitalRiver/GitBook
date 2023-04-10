---
description: Learn how to get financing information for a specific product.
---

# Financing

Financing allows a shopper to pay for goods and services in installments over time. Clients receive payment in full once the fulfiller ships the order. It is a shopper installment loan approved for an exact amount. Financing occurs at the cart/order level. The loan includes VAT and shipping. A financing payment method does not support deposits and deferred payments.

Financing programs have proven to increase the average order value (AOV), attachment rates (shoppers select additional products for financing), and conversion rate/lift. Shoppers are more likely to complete a purchase given this financing option.

When enabled, financing shows the monthly bill payment, billing terms, and payment promotion codes to the shopper. When a shopper checks out, they can choose the finance option as a payment method for specific products.

## Getting the financing information for a product

Use the [`GET /v1/shoppers/me/product/{produtId}/financing`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Financing/paths/\~1v1\~1shoppers\~1me\~1product\~1%7BproductId%7D\~1financing/get) request to get the financing information for a specific [product identifier](../../general-resources/common-shoppers-and-admin-apis-reference/product-identifier.md) (`productId`). See the [Financing query parameters](../../general-resources/shopper-apis-reference/financing.md#financing-query-parameters) for more information.

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```http
curl --location --request GET 'https://api.digitalriver.com/v1/shoppers/me/product/{productId}/financing' \
--header 'authorization: bearer ***\
...
```
{% endcode %}
{% endtab %}

{% tab title="200 OK response" %}
{% code overflow="wrap" %}
```json
{
  "uri": "https://api.digitalriver.com/v1/shoppers/me/products/73248500/financing",
  "financingTerm": [
    {
      "id": 1324500,
      "totalRepayable": {
        "currency": "USD",
        "value": "19.99"
      },
      "formattedTotalRepayable": "$8.92",
      "creditAmount": {
        "currency": "USD",
        "value": "19.99"
      },
      "formattedCreditAmount": "$7.20",
      "monthlyPaymentAmount": {
        "currency": "USD",
        "value": "19.99"
      },
      "formattedMonthlyPaymentAmount": "$0.08",
      "durationInMonths": 120,
      "interestRatePct": 0.04500000178813934,
      "interestRatePctForDisplay": 4.5,
      "effectiveInterestRate": 0.04500000178813934,
      "effectiveInterestRateForDisplay": 4.5,
      "description": "4.5% for 120 months"
    }
  ]
}
```
{% endcode %}
{% endtab %}
{% endtabs %}
