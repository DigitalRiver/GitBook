---
description: Learn how to retrieve all returns for a specified order.
---

# Retrieving returns for a specified order

## Retrieve all returns for a specified order

Retrieve all returns for a specified order where 999999999 is the `orderId`.

{% hint style="info" %}
**Requirement**: Create an OAuth token before invoking the Returns API.
{% endhint %}

{% tabs %}
{% tab title="cURL" %}
```http
curl --location --request POST 'http://{host}/v1/shoppers/me/orders/{orderId}/returns' \
--header 'Content-Type:  application/json' \
--header 'authorization: bearer ***\
```
{% endtab %}
{% endtabs %}

A successful request returns a 200 response code:

{% tabs %}
{% tab title="JSON" %}
```javascript
{
	"returns": {
	"return": [
		{
			"id": 9999999999,
			"reason": "PHONE_ORDER_ERROR",
			"comments": "hello change it",
			"type": "LineItemLevelReturnProduct",
			"status": "PendingProductReturn",
			"generationDate": "2016-10-17T15:00:24.000Z",
			"generatedBy": "aianand",
			"origin": "CUSTOMER_SERVICE",
			"policy": "LOD",
			"dateRefunded": "In Process",
			"refundTotal": {
				"currency": "USD",
				"value": 0
			},
			"formattedRefundTotal": "0.00$",
			"outstandingTotal": {
				"currency": "USD",
				"value": 19.14
			},
			"formattedOutstandingTotal": "19.14$",
			"requestedTotal": {
				"currency": "USD",
				"value": 19.14
			},
			"formattedRequestedTotal": "19.14$",
			"returnLineItems": {
				"returnLineItem": [
					{
						"dueDate": "2016-10-25T04:59:59.000Z",
						"offerId": 464443297,
						"offerDiscount": "10%",
						"expectedQty": 1,
						"returnedQty": 0,
						"type": "Download",
						"notes": "LOD_OPEN2016-10-25T04:59:59.000Z",
						"date": "2016-10-17T15:00:25.000Z",
						"status": "PendingProductReturn",
					  "returnLITotal": {
							"currency": "USD",
							"value": 9.57
						},
						"formattedReturnLITotal": "9.57$",
						"lineItem": {
							"uri": "https://api.digitalriver.com/v1/shoppers/me/orders/order_ID/line-items/lin_item_ID"
						}
					},
			{
				"dueDate": "2016-10-25T04:59:59.000Z",
				"offerId": offer_ID,
				"offerDiscount": "10%",
				"expectedQty": 1,
				"returnedQty": 0,
				"type": "Download",
				"notes": "LOD_OPEN2016-10-25T04:59:59.000Z",
				"date": "2016-10-17T15:00:25.000Z",
				"status": "PendingProductReturn",
				"returnLITotal": {
					"currency": "USD",
					"value": 9.57
				},
				"formattedReturnLITotal": "9.57$",
				"lineItem": {
					"uri": "https://api.digitalriver.com/v1/shoppers/me/orders/order_ID/line-items/line_item_ID"
				}
			 }
			]
		 }
		}
	 ]
	}
}
```
{% endtab %}
{% endtabs %}

## Request the return of one or more line items in an order

Request the return of one or more line items in a specified order where 999999999 is the `orderId`.

{% tabs %}
{% tab title="cURL" %}
```http
curl --location --request POST 'http://{host}/v1/orders/{orderid}/returns' \
--header 'Content-Type:  application/json' \
--header 'authorization: bearer ***\
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="URI" %}
```http
POST /v1/shoppers/me/orders/9999999999/returns
```
{% endtab %}

{% tab title="Request header" %}
```http
Accept: application/json Authorization: bearer your_
access_token
```
{% endtab %}

{% tab title="Request body" %}
```
{
  "return": {
    "reason": "DUPLICATE_ORDER",
    "comments": "Duplicate Order",
    "acceptELOD": "true",
    "returnLineItems": {
      "returnLineItem": [
        {
          "lineItemQuantityIDs": [
            1
          ],
          "lineItem": {
            "id": "123",
            "quantity": 1
          }
        }
      ]
    }
  }
}
```
{% endtab %}
{% endtabs %}

A successful request returns a 200 response code:

{% tabs %}
{% tab title="Response header" %}
```http
HTTP/1.1 200 OK
```
{% endtab %}

{% tab title="Response body" %}
```javascript
{
  "returns": [
    {
      "return": [
        {
          "id": 6654727889,
          "reason": "DUPLICATE_ORDER",
          "comments": "Shopper initiated self service return-",
          "type": "LineItemLevelReturnProduct",
          "status": "RefundedWithoutReturn",
          "generationDate": "2020-01-30T17:37:09.000Z",
          "generatedBy": "56066c6b-139b-47ff-9b07-1c799c10ea75",
          "origin": "SHOPPER",
          "policy": "LOD",
          "dateRefunded": "In Process",
          "refundTotal": {
            "currency": "USD",
            "value": 0
          },
          "formattedRefundTotal": "0.00USD",
          "outstandingTotal": {
            "currency": "USD",
            "value": 107.53
          },
          "formattedOutstandingTotal": "107.53USD",
          "requestedTotal": {
            "currency": "USD",
            "value": 107.53
          },
          "formattedRequestedTotal": "107.53USD",
          "returnLineItems": {
            "returnLineItem": [
              {
                "dueDate": "2020-02-07T05:59:59.000Z",
                "expectedQty": 1,
                "returnedQty": 1,
                "type": 100409,
                "notes": "LOD_REFUNDED-2020-02-07T05:59:59.000Z",
                "date": "2020-01-30T17:37:09.000Z",
                "status": "RefundedWithoutReturn",
                "returnLITotal": {
                  "currency": "USD",
                  "value": 107.53
                },
                "formattedReturnLITotal": "107.53USD",
                "lineItem": {
                  "uri": "https://api.digitalriver.com/v1/shoppers/me/orders/793374880082/line-items/793451150082"
                }
              }
            ]
          }
        }
      ]
    }
  ]
}
```
{% endtab %}
{% endtabs %}

## formattedReturnLITotal

The value for `formattedReturnLITotal` in the response body is based on the locale and currency. For example, if the locale is `en_US` the currency is `USD`.

```javascript
    formattedReturnLITotal": "105.00USD",
```
