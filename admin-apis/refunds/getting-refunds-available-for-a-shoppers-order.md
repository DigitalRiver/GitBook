---
description: Learn how to retrieve the refunds available for a shopper's order.
---

# Getting refunds available for a shopper's order

Use [`GET /orders/{orderId}refunds?token={the shopper's token}`](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Refund/paths/\~1orders\~1%7BorderId%7D\~1refunds-available/get) to get the refunds available for a shopper's order.

{% tabs %}
{% tab title="First Tab" %}
{% code overflow="wrap" %}
```http
curl --location --request GET 'https://api.digitalriver.com/orders/active/refunds-available?token={the shopper's token}' \
--header 'authorization: Basic ***\
...
```
{% endcode %}
{% endtab %}

{% tab title="Second Tab" %}
{% code overflow="wrap" %}
```json
{
	"currency": "USD",
	"lineItems": [
		{
			"lineItemId": "11035556604",
			"price": {
				"total": {
					"amount": {
						"value": 39.99,
						"formattedValue": "$39.99"
					},
					"amountAvailableForRefund": {
						"value": 39.99,
						"formattedValue": "$39.99"
					},
					"amountRefunded": {
						"value": 0.99,
						"formattedValue": "$0.99"
					}
				},
				"totalTax": {
					"amount": {
						"value": 3.99,
						"formattedValue": "$3.99"
					},
					"amountAvailableForRefund": {
						"value": 3.99,
						"formattedValue": "$3.99"
					},
					"amountRefunded": {
						"value": 0.99,
						"formattedValue": "$0.99"
					}
				},
				"totalShipping": {
					"amount": {
						"value": 4.99,
						"formattedValue": "$4.99"
					},
					"amountAvailableForRefund": {
						"value": 4.99,
						"formattedValue": "$4.99"
					},
					"amountRefunded": {
						"value": 0.99,
						"formattedValue": "$0.99"
					},
					"amountRefunded": {
						"value": 0.99,
						"formattedValue": "$0.99"
					}
				},
				"totalShippingTax": null,
				"totalDutiesAndTariffs": null,
				"totalDutiesAndTariffsTax": null,
				"totalFee": null,
				"totalFeeTax": null
			},
			"product": {
				"companyId": "demosft1",
				"externalId": "ext 1234"
			},
			"status": null
			},
			{
				"lineItemId": "11035556605",
				"price": {
					"total": {
						"amount": {
							"value": 39.99,  
							"formattedValue": "$39.99"
						},
						"amountAvailableForRefund": {
							"value": 39.99,
							"formattedValue": "$39.99"
						},
						"amountRefunded": {
							"value": 0.99,
							"formattedValue": "$0.99"
						}
					},
					"totalTax": {
						"amount": {
							"value": 3.99,
							"formattedValue": "$3.99"
						},
						"amountAvailableForRefund": {
							"value": 3.99,
							"formattedValue": "$3.99"
						},
						"amountRefunded": {
							"value": 0.99,
							"formattedValue": "$0.99"
						}
					},
					"totalShipping": {
						"amount": {
							"value": 4.99,
							"formattedValue": "$4.99"
						},
					"price": {
						"total": {
							"amount": {
								"value": 39.99,
								"formattedValue": "$39.99"
							},
							"amountAvailableForRefund": {
								"value": 39.99,
								"formattedValue": "$39.99"
							},
							"amountRefunded": {
								"value": 0.99,
								"formattedValue": "$0.99"
							}
					}, 
            "totalTax": {
							"amount": {
								"value": 3.99,
								"formattedValue": "$3.99"
							},
							"amountAvailableForRefund": {
								"value": 3.99,
								"formattedValue": "$3.99"
							},
							"amountRefunded": {
								"value": 0.99,
								"formattedValue": "$0.99"
							}
						},
						"totalShipping": {
							"amount": {
								"value": 4.99,
								"formattedValue": "$4.99"
							},
							"amountAvailableForRefund": {
								"value": 4.99,
								"formattedValue": "$4.99"
							},
							"amountRefunded": {
								"value": 0.99,
								"formattedValue": "$0.99"
							}
						},
						"totalShippingTax": null,
						"totalDutiesAndTariffs": null,
						"totalDutiesAndTariffsTax": null,
						"totalFee": null,
						"totalFeeTax": null
					},
					"status": null
}
```
{% endcode %}
{% endtab %}
{% endtabs %}
