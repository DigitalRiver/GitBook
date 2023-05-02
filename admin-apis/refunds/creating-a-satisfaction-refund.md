---
description: Learn how to create a satisfaction refund.
---

# Creating a satisfaction refund

There are two ways to create a refund. A Customer Service Representative (CRS) can [initiate a satisfaction refund](https://help.digitalriver.com/help/gc/Customer-Service/Initiating-a-refund.htm#HowToInitiateARefund) through Global Commerce, or you can [create a satisfaction refund programmatically](creating-a-satisfaction-refund.md#creating-a-satisfaction-refund-programmatically).

## Creating a satisfaction refund programmatically

The following [`POST /orders/{orderid}/refunds`](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Refund/paths/\~1orders\~1%7BorderId%7D\~1refunds/post) request requires the customer token and sets the `type` to `productRefund`, the `category` to `PRODUCT_LEVEL_PRODUCT`, the reason to `CUSTOMER_SATISFACTION_ISSUE`, the comments to `Test Product Refund`, and `refundAmount`.

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```javascript
curl --location --request POST 'https://api.digitalriver.com/orders/{orderid}/refunds?token={the customer's token}' \
--header 'authorization: Basic ***\
...
--data-raw '{
    "type": "productRefund",
    "category": "PRODUCT_LEVEL_PRODUCT",
    "reason": "CUSTOMER_SATISFACTION_ISSUE",
    "comments": "Test Product Refund",
    "lineItems": [
        {
            "lineItemId": "51274910082",
            "refundAmount": {
                "value": 139.23,
                "currency": "EUR"
            }
        }
    ]
}

}'
```
{% endcode %}
{% endtab %}

{% tab title="200 OK response" %}
A successful request returns a `200 OK` response.

{% code overflow="wrap" %}
```json
{
    "refunds": [
        {
            "id": "7613660289",
            "status": "ReturnAcknowledged",
            "reason": "CUSTOMER_SATISFACTION_ISSUE",
            "comments": "Satisfaction Refund Api-Test Product Refund",
            "type": "LineItemLevelSatisfactionRefund",
            "category": null,
            "generationDate": "Wed Sep 29 20:10:51 CDT 2021",
            "generatedBy": "automation-HostAdmin",
            "origin": "CUSTOMER_SERVICE",
            "overrides": "OVERRIDE_EXCEEDS_MAX_ITEM_LEVEL_REFUND_PCT",
            "policy": "NothingRequired",
            "currency": "EUR",
            "totalRefunded": {
                "value": 0.0,
                "formattedValue": "0.00EUR"
            },
            "outstanding": {
                "value": 139.23,
                "formattedValue": "139.23EUR"
            },
            "totalRequested": {
                "value": 139.23,
                "formattedValue": "139.23EUR"
            },
            "lineItems": [
                {
                    "status": "ReturnAcknowledged",
                    "expectedQuantity": 0,
                    "returnedQuantity": 0,
                    "type": "Physical",
                    "notes": "Nothing Required",
                    "date": "Wed Sep 29 20:10:51 CDT 2021",
                    "product": {
                        "companyId": "fitbit",
                        "id": "5423986700",
                        "externalId": "507BKBK"
                    },
                    "lineItemId": "51274910082"
                }
            ]
        }
    ]
}
```
{% endcode %}
{% endtab %}
{% endtabs %}
