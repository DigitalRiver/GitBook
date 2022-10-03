---
description: Learn how to retrieve refunds available for an order.
---

# Retrieving refunds available for an order

Retrieve the refunds available for a specific order like this where you provide the customer's token:

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```http
curl --location --request POST 'http://{host}/orders/active/refunds-available?token={the customer's token}' \
--header 'Content-Type:  application/json' \
--header 'authorization: bearer ***\
```
{% endcode %}
{% endtab %}
{% endtabs %}

A successful request returns a 200 response code:

{% tabs %}
{% tab title="JSON" %}
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
