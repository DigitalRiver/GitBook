---
description: Understand how the Digital Rights Revocation service works.
---

# Digital rights revocation

The Digital Rights Revocation service is a real-time, request/response-based process used to revoke one external digital right. The service revokes a key that has already been delivered to the shopper. A key revocation integration sends a request to revoke or take back a key (serial number of unlock code) that was distributed when a product was purchased.

You can use the Digital Rights Revocation service to revoke a single previously-granted external digital right. If you need to revoke multiple digital rights for an order, you can send multiple revocation calls.

You can create a custom integration to revoke a key when:

* A product is returned
* An order is refunded or canceled
* There is a chargeback, fraud, or some other failure in payment or order authorization

![Digital Rights Revocation](https://files.readme.io/12b9df6-Digital\_Rights\_Revocation.png)

* **Notification**—Global Commerce generates a Revocation Service Request and sends the request to your endpoint.
* **Required response to notification**—Your endpoint must synchronously respond with a Revocation Service Response.

{% tabs %}
{% tab title="Payload" %}
{% code overflow="wrap" %}
```json
{
	"RevocationServiceRequest": {
		"orderInfo": {
			"orderID": {
				"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
				"_xsi:type": "xsd:string",
				"__text": "123456789"
			},
			"externalReferenceID": {
				"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
				"_xsi:type": "xsd:string",
				"_xsi:nil": "true"
			},
			"siteID": {
				"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
				"_xsi:type": "xsd:string",
				"__text": "siteID"
			},
			"userKey": {
				"userID": {
					"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
					"_xsi:type": "xsd:string",
					"__text": "213456789"
				},
				"externalReferenceID": {
					"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
					"_xsi:type": "xsd:string",
					"__text": "312456789"
				},
				"companyID": {
					"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
					"_xsi:type": "xsd:string",
					"__text": "412356789"
				},
				"loginID": {
					"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
					"_xsi:type": "xsd:string",
					"__text": "email@example.com"
				},
				"siteID": {
					"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
					"_xsi:type": "xsd:string",
					"__text": "siteID"
				},
				"_xmlns:ns2": "https://integration.digitalriver.com/Common/1.0",
				"_xsi:type": "ns2:UserKey"
			},
			"paymentInfo": {
				"accountID": {
					"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
					"_xsi:type": "xsd:string",
					"_xsi:nil": "true"
				},
				"authorizationID": {
					"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
					"_xsi:type": "xsd:string",
					"__text": "512346789"
				},
				"cardType": {
					"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
					"_xsi:type": "xsd:string",
					"__text": "CardType"
				},
				"customerEmail": {
					"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
					"_xsi:type": "xsd:string",
					"__text": "email2@example.com"
				},
				"cardNumber": {
					"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
					"_xsi:type": "xsd:string",
					"__text": "6123456789"
				},
				"cardExpirationMonth": {
					"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
					"_xsi:type": "xsd:string",
					"__text": "01"
				},
				"cardExpirationYear": {
					"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
					"_xsi:type": "xsd:string",
					"__text": "2080"
				},
				"customerPO": {
					"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
					"_xsi:type": "xsd:string",
					"_xsi:nil": "true"
				},
				"ccIssueCode": {
					"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
					"_xsi:type": "xsd:string",
					"_xsi:nil": "true"
				},
				"ccIssueMonth": {
					"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
					"_xsi:type": "xsd:string",
					"_xsi:nil": "true"
				},
				"ccIssueYear": {
					"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
					"_xsi:type": "xsd:string",
					"_xsi:nil": "true"
				},
				"securityIndicator": {
					"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
					"_xsi:type": "xsd:string",
					"_xsi:nil": "true"
				},
				"routingNumber": {
					"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
					"_xsi:type": "xsd:string",
					"_xsi:nil": "true"
				},
				"vatNumber": {
					"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
					"_xsi:type": "xsd:string",
					"_xsi:nil": "true"
				},
				"customerLastName": {
					"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
					"_xsi:type": "xsd:string",
					"__text": "LastName"
				},
				"customerFirstName": {
					"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
					"_xsi:type": "xsd:string",
					"__text": "FirstName"
				},
				"paymentAmount": {
					"currencyCode": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "USD"
					},
					"amount": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:decimal",
						"__text": "11.11"
					},
					"_xmlns:ns4": "https://integration.digitalriver.com/Common/1.0",
					"_xsi:type": "ns4:MoneyInfo"
				},
				"paymentMethodName": {
					"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
					"_xsi:type": "xsd:string",
					"__text": "paymentMethod"
				},
				"billingAddress": {
					"addressID": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "712345689"
					},
					"city": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "City"
					},
					"countryA2": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"_xsi:nil": "true"
					},
					"country": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "US"
					},
					"countryName": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "United States"
					},
					"line1": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "123 Example Street"
					},
					"line2": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"_xsi:nil": "true"
					},
					"line3": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"_xsi:nil": "true"
					},
					"locationCode": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"_xsi:nil": "true"
					},
					"name1": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "FirstName"
					},
					"name2": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "LastName"
					},
					"phoneNumber": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "(123) 456-7890"
					},
					"postalCode": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "12345"
					},
					"state": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"_xsi:nil": "true"
					},
					"email": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "email3@example.com"
					},
					"faxPhone": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"_xsi:nil": "true"
					},
					"companyName": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "companyName"
					},
					"phoneNumber2": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"_xsi:nil": "true"
					},
					"countyName": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"_xsi:nil": "true"
					},
					"extendedAttributes": {
						"_xsi:type": "ns5:ExtendedAttributesInfoArray"
					},
					"_xmlns:ns5": "https://integration.digitalriver.com/Common/1.0",
					"_xsi:type": "ns5:AddressInfo"
				},
				"extendedAttributes": {
					"item": {
						"name": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "extendedAttributeName"
						},
						"value": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "value"
						},
						"valueDataType": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "string"
						},
						"_xsi:type": "ns6:ExtendedAttributesInfo"
					},
					"_xmlns:ns6": "https://integration.digitalriver.com/Common/1.0",
					"_xsi:type": "ns6:ExtendedAttributesInfoArray"
				},
				"_xmlns:ns3": "https://integration.digitalriver.com/commonRequisition/1.0",
				"_xsi:type": "ns3:PaymentInformationInfo"
			},
			"extendedAttributes": {
				"item": {
					"name": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "extendedAttributeName"
					},
					"value": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "value"
					},
					"valueDataType": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "string"
					},
					"_xsi:type": "ns7:ExtendedAttributesInfo"
				},
				"_xmlns:ns7": "https://integration.digitalriver.com/Common/1.0",
				"_xsi:type": "ns7:ExtendedAttributesInfoArray"
			},
			"_xmlns:xsi": "https://www.w3.org/2001/XMLSchema-instance",
			"_xsi:type": "ns1:OrderInfo"
		},
		"lineItemInfo": {
			"lineItemID": {
				"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
				"_xsi:type": "xsd:string",
				"__text": "812345679"
			},
			"productInfo": {
				"productKey": {
					"productID": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "912345678"
					},
					"externalReferenceID": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "012345678"
					},
					"companyID": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "102345678"
					},
					"locale": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"_xsi:nil": "true"
					},
					"_xmlns:ns8": "https://integration.digitalriver.com/Common/1.0",
					"_xsi:type": "ns8:ProductKey"
				},
				"digitalRight": {
					"key": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "key"
					},
					"keyType": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "KEY_TYPE"
					},
					"lineItemQuantityID": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:int",
						"__text": "1"
					},
					"_xsi:type": "ns1:DigitalRightInfo"
				},
				"productAttributes": {
					"item": {
						"name": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "ExtendedAttributeName"
						},
						"value": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "value"
						},
						"valueDataType": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "string"
						},
						"_xsi:type": "ns9:ExtendedAttributesInfo"
					},
					"_xmlns:ns9": "https://integration.digitalriver.com/Common/1.0",
					"_xsi:type": "ns9:ExtendedAttributesInfoArray"
				},
				"_xsi:type": "ns1:ProductInfo"
			},
			"extendedAttributes": {
				"_xmlns:ns11": "https://integration.digitalriver.com/Common/1.0",
				"_xsi:type": "ns11:ExtendedAttributesInfoArray"
			},
			"_xmlns:xsi": "https://www.w3.org/2001/XMLSchema-instance",
			"_xsi:type": "ns1:LineItemInfo"
		},
		"revocationReason": {
			"_xmlns:xsi": "https://www.w3.org/2001/XMLSchema-instance",
			"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
			"_xsi:type": "xsd:string",
			"__text": "Return-Product"
		},
		"revocationInfo": {
			"disputeInfo": {
				"_xsi:type": "ns1:DisputeRevocationInfo",
				"_xsi:nil": "true"
			},
			"suppressionInfo": {
				"_xsi:type": "ns1:SuppressionRevocationInfo",
				"_xsi:nil": "true"
			},
			"returnInfo": {
				"returnID": {
					"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
					"_xsi:type": "xsd:string",
					"__text": "2013456789"
				},
				"returnLineItemID": {
					"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
					"_xsi:type": "xsd:string",
					"__text": "301245789"
				},
				"returnDate": {
					"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
					"_xsi:type": "xsd:dateTime",
					"__text": "2014-09-14T12:00:32.212Z"
				},
				"returnReason": {
					"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
					"_xsi:type": "xsd:string",
					"__text": "RETURN_REASON"
				},
				"returnTotalAmount": {
					"currencyCode": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "USD"
					},
					"amount": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:decimal",
						"__text": "11.11"
					},
					"_xmlns:ns12": "https://integration.digitalriver.com/Common/1.0",
					"_xsi:type": "ns12:MoneyInfo"
				},
				"returnSubtotalAmount": {
					"currencyCode": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "USD"
					},
					"amount": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:decimal",
						"__text": "11.11"
					},
					"_xmlns:ns13": "https://integration.digitalriver.com/Common/1.0",
					"_xsi:type": "ns13:MoneyInfo"
				},
				"returnTaxAmount": {
					"currencyCode": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "USD"
					},
					"amount": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:decimal",
						"__text": "0.00"
					},
					"_xmlns:ns14": "https://integration.digitalriver.com/Common/1.0",
					"_xsi:type": "ns14:MoneyInfo"
				},
				"returnFeesAmount": {
					"_xmlns:ns17": "https://integration.digitalriver.com/Common/1.0",
					"_xsi:type": "ns17:MoneyInfo",
					"_xsi:nil": "true"
				},
				"returnShippingAmount": {
					"currencyCode": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "USD"
					},
					"amount": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:decimal",
						"__text": "0.00"
					},
					"_xmlns:ns18": "https://integration.digitalriver.com/Common/1.0",
					"_xsi:type": "ns18:MoneyInfo"
				},
				"returnLineItemTotalAmount": {
					"currencyCode": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "USD"
					},
					"amount": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:decimal",
						"__text": "11.11"
					},
					"_xmlns:ns19": "https://integration.digitalriver.com/Common/1.0",
					"_xsi:type": "ns19:MoneyInfo"
				},
				"returnLineItemSubtotalAmount": {
					"currencyCode": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "USD"
					},
					"amount": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:decimal",
						"__text": "11.11"
					},
					"_xmlns:ns20": "https://integration.digitalriver.com/Common/1.0",
					"_xsi:type": "ns20:MoneyInfo"
				},
				"returnLineItemTaxAmount": {
					"currencyCode": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "USD"
					},
					"amount": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:decimal",
						"__text": "0.00"
					},
					"_xmlns:ns21": "https://integration.digitalriver.com/Common/1.0",
					"_xsi:type": "ns21:MoneyInfo"
				},
				"returnLineItemShippingAmount": {
					"currencyCode": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "USD"
					},
					"amount": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:decimal",
						"__text": "0.00"
					},
					"_xmlns:ns24": "https://integration.digitalriver.com/Common/1.0",
					"_xsi:type": "ns24:MoneyInfo"
				},
				"returnLineItemQuantity": {
					"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
					"_xsi:type": "xsd:int",
					"__text": "1"
				},
				"satisfaction": {
					"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
					"_xsi:type": "xsd:boolean",
					"__text": "false"
				},
				"_xsi:type": "ns1:ReturnRevocationInfo"
			},
			"_xmlns:xsi": "https://www.w3.org/2001/XMLSchema-instance",
			"_xsi:type": "ns1:RevocationInfo"
		},
		"_xmlns:ns1": "https://integration.digitalriver.com/RevocationService",
		"__prefix": "ns1"
	}
}
```
{% endcode %}
{% endtab %}

{% tab title="Successful response" %}
```json
{
	"RevocationServiceResponse": {
		"successful": "success",
		"isAutoRetriable": "false",
		"responseCode": "1234",
		"responseType": "responseType",
		"responseMessage": "SUCCESS"
	}
}
```
{% endtab %}

{% tab title="Unsuccessful response" %}
{% code overflow="wrap" %}
```json
{
	"RevocationServiceResponse": {
		"successful": "success",
		"isAutoRetriable": "false",
		"responseCode": "1234",
		"responseType": "responseType",
		"responseMessage": "SUCCESS"
	}
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Revocation reasons

### `DisputeLineitem`

The Line Item that contains the Digital Right is under dispute.

### `DisputeAmount`

A non-Line-Item-specific amount on the requisition is under dispute (for example, the client disputes $30.00 because they were unhappy with something).

### `FraudSuppression`

The requisition containing the Digital Right was suppressed.

### `ReturnProduct`

There is an issue with the product return.

### `ReturnSatisfaction`

The Line Item containing the Digital Right underwent a satisfaction refund (the product was not returned).

### `DeclinedSettlement`

The Settlement Payment Transaction was declined.

### `PreLoadCancel`

The preload Line Item was canceled and has not been released.

## Schemas

| Version     | Schema Components Table                                                                   | Raw Schema                                                                    | Sample XML                                                                            |
| ----------- | ----------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------- | ------------------------------------------------------------------------------------- |
| 6 (Current) | [View](https://drhadmin.digitalriver.com/integration/isg/schematable/RevocationService/6) | [View](https://drhadmin.digitalriver.com/integration/xsd/RevocationService/6) | [View](https://drhadmin.digitalriver.com/integration/xsd/RevocationService/6)         |
| 5           | [View](https://drhadmin.digitalriver.com/integration/isg/schematable/RevocationService/5) | [View](https://drhadmin.digitalriver.com/integration/xsd/RevocationService/5) | [View](https://drhadmin.digitalriver.com/integration/isg/example/RevocationService/5) |
| 4           | [View](https://drhadmin.digitalriver.com/integration/isg/schematable/RevocationService/4) | [View](https://drhadmin.digitalriver.com/integration/xsd/RevocationService/4) | [View](https://drhadmin.digitalriver.com/integration/isg/example/RevocationService/4) |
