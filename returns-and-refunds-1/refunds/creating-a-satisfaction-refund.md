---
description: Learn how to create a satisfaction refund.
---

# Creating a satisfaction refund

There are two ways to create a refund. A Customer Service Representative (CRS) can [initiate a satisfaction refund](https://help.digitalriver.com/help/gc/Customer-Service/Initiating-a-refund.htm#HowToInitiateARefund) through Global Commerce, or you can [create a satisfaction refund programmatically](creating-a-satisfaction-refund.md#creating-a-satisfaction-refund-programmatically).

## Creating a satisfaction refund programmatically

The following [`POST /orders/{orderid}/refunds`](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Refunds/paths/\~1orders\~1{orderId}\~1refunds/post) request requires the customer token and sets the `type` to `productRefund`, the `category` to `PRODUCT_LEVEL_PRODUCT`, the reason to `CUSTOMER_SATISFACTION_ISSUE`, the comments to `Test Product Refund`, and `refundAmount`.

{% tabs %}
{% tab title="cURL" %}
```javascript
curl --location --request POST 'http://{host}/orders/{orderid}/refunds?token={the customer's token}' \
--header 'Content-Type:  application/json' \
--header 'authorization: bearer ***\
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
{% endtab %}
{% endtabs %}

A successful request returns a 200 response code:

{% tabs %}
{% tab title="JSON" %}
```javascript
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
{% endtab %}
{% endtabs %}
