---
description: Understand the line-item level satisfaction refund.
---

# Line-item level satisfaction refund

{% tabs %}
{% tab title="Request body" %}
```javascript
{
	"SalesOrderActivityInfoArray": {
		"reportBeginDate": {
			"_xmlns:xsi": "http://www.w3.org/2001/XMLSchema-instance",
			"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
			"_xsi:type": "xsd:dateTime",
			"__text": "2005-12-20T06:00:00.209Z"
		},
		"reportEndDate": {
			"_xmlns:xsi": "http://www.w3.org/2001/XMLSchema-instance",
			"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
			"_xsi:type": "xsd:dateTime",
			"__text": "2005-12-20T06:00:00.209Z"
		},
		"reportRunDate": {
			"_xmlns:xsi": "http://www.w3.org/2001/XMLSchema-instance",
			"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
			"_xsi:type": "xsd:dateTime",
			"__text": "2005-12-21T10:06:11.209Z"
		},
		"salesOrderActivity": {
			"orderID": {
				"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
				"_xsi:type": "xsd:string",
				"__text": "1111222233"
			},
			"saleDate": {
				"_xsi:type": "xsd:date",
				"__text": "2006-02-10"
			},
			"site": {
				"siteID": {
					"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
					"_xsi:type": "xsd:string",
					"__text": "testsite"
				},
				"siteAddress": {
					"addressID": {
						"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"_xsi:nil": "true"
					},
					"city": {
						"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "Eden Prairie"
					},
					"countryA2": {
						"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "TW"
					},
					"country": {
						"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "TW"
					},
					"countryName": {
						"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "Taiwan"
					},
					"line1": {
						"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "1234 Happy Street"
					},
					"line2": {
						"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string"
					},
					"line3": {
						"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string"
					},
					"locationCode": {
						"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"_xsi:nil": "true"
					},
					"name1": {
						"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "Jane"
					},
					"name2": {
						"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "Doe"
					},
					"phoneNumber": {
						"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string"
					},
					"postalCode": {
						"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "55555"
					},
					"state": {
						"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "TW"
					},
					"email": {
						"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string"
					},
					"faxPhone": {
						"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string"
					},
					"companyName": {
						"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string"
					},
					"phoneNumber2": {
						"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string"
					},
					"countyName": {
						"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"_xsi:nil": "true"
					},
					"extendedAttributes": {
						"_xsi:type": "ns244:ExtendedAttributesInfoArray",
						"_xsi:nil": "true"
					},
					"_xsi:type": "ns244:AddressInfo"
				},
				"siteURL": {
					"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
					"_xsi:type": "xsd:string",
					"_xsi:nil": "true"
				},
				"_xmlns:ns244": "http://integration.digitalriver.com/Common/1.0",
				"_xsi:type": "ns244:SiteInfo"
			},
			"pricing": {
				"total": {
					"currencyCode": {
						"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "USD"
					},
					"amount": {
						"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:decimal",
						"__text": "-1.00"
					},
					"_xmlns:ns246": "http://integration.digitalriver.com/Common/1.0",
					"_xsi:type": "ns246:MoneyInfo"
				},
				"subtotal": {
					"currencyCode": {
						"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "USD"
					},
					"amount": {
						"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:decimal",
						"__text": "-1.00"
					},
					"_xmlns:ns247": "http://integration.digitalriver.com/Common/1.0",
					"_xsi:type": "ns247:MoneyInfo"
				},
				"tax": {
					"currencyCode": {
						"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "USD"
					},
					"amount": {
						"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:decimal",
						"__text": "0.00"
					},
					"_xmlns:ns248": "http://integration.digitalriver.com/Common/1.0",
					"_xsi:type": "ns248:MoneyInfo"
				},
				"shipping": {
					"currencyCode": {
						"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "USD"
					},
					"amount": {
						"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:decimal",
						"__text": "0.00"
					},
					"_xmlns:ns249": "http://integration.digitalriver.com/Common/1.0",
					"_xsi:type": "ns249:MoneyInfo"
				},
				"incentive": {
					"currencyCode": {
						"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "USD"
					},
					"amount": {
						"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:decimal",
						"__text": "0.00"
					},
					"_xmlns:ns250": "http://integration.digitalriver.com/Common/1.0",
					"_xsi:type": "ns250:MoneyInfo"
				},
				"shippingIncentive": {
					"_xmlns:ns251": "http://integration.digitalriver.com/Common/1.0",
					"_xsi:type": "ns251:MoneyInfo",
					"_xsi:nil": "true"
				},
				"nonTaxableFees": {
					"_xmlns:ns252": "http://integration.digitalriver.com/Common/1.0",
					"_xsi:type": "ns252:MoneyInfo",
					"_xsi:nil": "true"
				},
				"taxableFees": {
					"_xmlns:ns253": "http://integration.digitalriver.com/Common/1.0",
					"_xsi:type": "ns253:MoneyInfo",
					"_xsi:nil": "true"
				},
				"taxOnTaxableFees": {
					"_xmlns:ns254": "http://integration.digitalriver.com/Common/1.0",
					"_xsi:type": "ns254:MoneyInfo",
					"_xsi:nil": "true"
				},
				"exchangeRate": {
					"currencyCode": {
						"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "USD"
					},
					"amount": {
						"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:decimal",
						"__text": "1"
					},
					"_xmlns:ns255": "http://integration.digitalriver.com/Common/1.0",
					"_xsi:type": "ns255:MoneyInfo"
				},
				"_xmlns:ns245": "http://integration.digitalriver.com/commonRequisition/1.0",
				"_xsi:type": "ns245:OrderPriceInfo"
			},
			"paymentInfos": {
				"paymentInfo": {
					"authorizationID": {
						"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"_xsi:nil": "true"
					},
					"cardType": {
						"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "Visa"
					},
					"customerEmail": {
						"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "johndoe@yahoo.com"
					},
					"cardNumber": {
						"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"_xsi:nil": "true"
					},
					"cardExpirationMonth": {
						"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"_xsi:nil": "true"
					},
					"cardExpirationYear": {
						"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"_xsi:nil": "true"
					},
					"customerPO": {
						"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"_xsi:nil": "true"
					},
					"ccIssueCode": {
						"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"_xsi:nil": "true"
					},
					"ccIssueMonth": {
						"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"_xsi:nil": "true"
					},
					"ccIssueYear": {
						"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"_xsi:nil": "true"
					},
					"securityIndicator": {
						"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"_xsi:nil": "true"
					},
					"routingNumber": {
						"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"_xsi:nil": "true"
					},
					"vatNumber": {
						"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string"
					},
					"customerLastName": {
						"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "Doe"
					},
					"customerFirstName": {
						"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "John"
					},
					"paymentAmount": {
						"currencyCode": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "USD"
						},
						"amount": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:decimal",
							"__text": "-1.00"
						},
						"_xmlns:ns257": "http://integration.digitalriver.com/Common/1.0",
						"_xsi:type": "ns257:MoneyInfo"
					},
					"paymentMethodName": {
						"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "CreditCardMethod"
					},
					"billingAddress": {
						"addressID": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"_xsi:nil": "true"
						},
						"city": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "Eden Prairie"
						},
						"countryA2": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "US"
						},
						"country": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "US"
						},
						"countryName": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "United States"
						},
						"line1": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "12345 Happy Lane"
						},
						"line2": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string"
						},
						"line3": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string"
						},
						"locationCode": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"_xsi:nil": "true"
						},
						"name1": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "Jane"
						},
						"name2": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "Doe"
						},
						"phoneNumber": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "612 111-2222"
						},
						"postalCode": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "55555"
						},
						"state": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "MN"
						},
						"email": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "johndoe@yahoo.com"
						},
						"faxPhone": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string"
						},
						"companyName": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string"
						},
						"phoneNumber2": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string"
						},
						"countyName": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"_xsi:nil": "true"
						},
						"extendedAttributes": {
							"_xsi:type": "ns258:ExtendedAttributesInfoArray",
							"_xsi:nil": "true"
						},
						"_xmlns:ns258": "http://integration.digitalriver.com/Common/1.0",
						"_xsi:type": "ns258:AddressInfo"
					},
					"_xsi:type": "ns256:PaymentInformationInfo"
				},
				"_xmlns:ns256": "http://integration.digitalriver.com/commonRequisition/1.0",
				"_xsi:type": "ns256:PaymentInformationInfoArray"
			},
			"lineItems": {
				"item": {
					"lineItemID": {
						"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "1927537200"
					},
					"transactionDescription": {
						"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "RETURN_RECEIPT"
					},
					"quantity": {
						"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:integer",
						"__text": "0"
					},
					"product": {
						"productID": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "33161500"
						},
						"externalReferenceID": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string"
						},
						"companyID": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "test"
						},
						"locale": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"_xsi:nil": "true"
						},
						"_xmlns:ns259": "http://integration.digitalriver.com/Common/1.0",
						"_xsi:type": "ns259:ProductKey"
					},
					"productInfo": {
						"productDataID": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "93720900"
						},
						"sku": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "0"
						},
						"mfrPartNumber": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string"
						},
						"shipperPartNumber": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string"
						},
						"name": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "PC-cillinâ?¢ Internet Security 2005"
						},
						"platform": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "N/A - not available"
						},
						"companyID": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "test"
						},
						"year": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string"
						},
						"seats": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string"
						},
						"_xsi:type": "ns1:ProductDataInfo"
					},
					"lineItemDigitalInfoList": {
						"digitalInfo": {
							"serialNumber": {
								"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"__text": "XXXX-XXXX-XXXX-XXXX-XXXX"
							},
							"unlockCode": {
								"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string"
							},
							"_xsi:type": "ns261:LineItemDigitalInfo"
						},
						"_xmlns:ns261": "http://integration.digitalriver.com/commonRequisition/1.0",
						"_xsi:type": "ns261:LineItemDigitalInfoArray"
					},
					"shipping": {
						"shipToAddress": {
							"addressID": {
								"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"_xsi:nil": "true"
							},
							"city": {
								"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"__text": "Eden Prairie"
							},
							"countryA2": {
								"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"__text": "US"
							},
							"country": {
								"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"__text": "US"
							},
							"countryName": {
								"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"__text": "United States"
							},
							"line1": {
								"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"__text": "12345 Happy Lane"
							},
							"line2": {
								"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string"
							},
							"line3": {
								"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string"
							},
							"locationCode": {
								"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"_xsi:nil": "true"
							},
							"name1": {
								"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"__text": "Jane"
							},
							"name2": {
								"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"__text": "Doe"
							},
							"phoneNumber": {
								"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"__text": "612 111-2222"
							},
							"postalCode": {
								"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"__text": "55555"
							},
							"state": {
								"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"__text": "NY"
							},
							"email": {
								"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"__text": "johndoe@yahoo.com"
							},
							"faxPhone": {
								"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string"
							},
							"companyName": {
								"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string"
							},
							"phoneNumber2": {
								"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string"
							},
							"countyName": {
								"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"_xsi:nil": "true"
							},
							"extendedAttributes": {
								"_xsi:type": "ns262:ExtendedAttributesInfoArray",
								"_xsi:nil": "true"
							},
							"_xmlns:ns262": "http://integration.digitalriver.com/Common/1.0",
							"_xsi:type": "ns262:AddressInfo"
						},
						"shippingMethodName": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string"
						},
						"carrierName": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "FedEx"
						},
						"shipmentDate": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:date",
							"__text": "2006-02-10"
						},
						"isReship": {
							"_xmlns:soapenc": "http://schemas.xmlsoap.org/soap/encoding/",
							"_xsi:type": "soapenc:boolean",
							"_xsi:nil": "true"
						},
						"fulfillerID": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "trend"
						},
						"fulfillerName": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "Trend Micro, Inc."
						},
						"_xsi:type": "ns1:ShipmentInfo"
					},
					"returnInfo": {
						"returnType": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "LineItemLevelSatisfactionRefund"
						},
						"returnReason": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "CANT_DOWNLOAD"
						},
						"returnDate": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:date",
							"__text": "2006-02-10"
						},
						"serialNumber": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "XXXX-XXXX-XXXX-XXXX-XXXX"
						},
						"returnID": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "3564609"
						},
						"returnLineItemID": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "4399709"
						},
						"_xsi:type": "ns1:ReturnInfo"
					},
					"pricing": {
						"unitPrice": {
							"currencyCode": {
								"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"__text": "USD"
							},
							"amount": {
								"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:decimal",
								"__text": "0"
							},
							"_xmlns:ns263": "http://integration.digitalriver.com/Common/1.0",
							"_xsi:type": "ns263:MoneyInfo"
						},
						"listPrice": {
							"currencyCode": {
								"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"__text": "USD"
							},
							"amount": {
								"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:decimal",
								"__text": "0"
							},
							"_xmlns:ns264": "http://integration.digitalriver.com/Common/1.0",
							"_xsi:type": "ns264:MoneyInfo"
						},
						"pricePerQty": {
							"currencyCode": {
								"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"__text": "USD"
							},
							"amount": {
								"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:decimal",
								"__text": "0"
							},
							"_xmlns:ns265": "http://integration.digitalriver.com/Common/1.0",
							"_xsi:type": "ns265:MoneyInfo"
						},
						"saleAmount": {
							"currencyCode": {
								"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"__text": "USD"
							},
							"amount": {
								"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:decimal",
								"__text": "-1"
							},
							"_xmlns:ns266": "http://integration.digitalriver.com/Common/1.0",
							"_xsi:type": "ns266:MoneyInfo"
						},
						"shipping": {
							"currencyCode": {
								"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"__text": "USD"
							},
							"amount": {
								"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:decimal",
								"__text": "0"
							},
							"_xmlns:ns267": "http://integration.digitalriver.com/Common/1.0",
							"_xsi:type": "ns267:MoneyInfo"
						},
						"shopperShippingCostPerQty": {
							"currencyCode": {
								"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"__text": "USD"
							},
							"amount": {
								"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:decimal",
								"__text": "0"
							},
							"_xmlns:ns268": "http://integration.digitalriver.com/Common/1.0",
							"_xsi:type": "ns268:MoneyInfo"
						},
						"handling": {
							"currencyCode": {
								"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"__text": "USD"
							},
							"amount": {
								"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:decimal",
								"__text": "0"
							},
							"_xmlns:ns269": "http://integration.digitalriver.com/Common/1.0",
							"_xsi:type": "ns269:MoneyInfo"
						},
						"incentive": {
							"currencyCode": {
								"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"__text": "USD"
							},
							"amount": {
								"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:decimal",
								"__text": "0"
							},
							"_xmlns:ns270": "http://integration.digitalriver.com/Common/1.0",
							"_xsi:type": "ns270:MoneyInfo"
						},
						"reqLevelIncentivePerQuantity": {
							"currencyCode": {
								"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"__text": "USD"
							},
							"amount": {
								"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:decimal",
								"__text": "0"
							},
							"_xmlns:ns271": "http://integration.digitalriver.com/Common/1.0",
							"_xsi:type": "ns271:MoneyInfo"
						},
						"lineItemLevelIncentivePerQuantity": {
							"currencyCode": {
								"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"__text": "USD"
							},
							"amount": {
								"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:decimal",
								"__text": "0"
							},
							"_xmlns:ns272": "http://integration.digitalriver.com/Common/1.0",
							"_xsi:type": "ns272:MoneyInfo"
						},
						"taxableFeesPerQuantity": {
							"currencyCode": {
								"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"__text": "USD"
							},
							"amount": {
								"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:decimal",
								"__text": "0"
							},
							"_xmlns:ns273": "http://integration.digitalriver.com/Common/1.0",
							"_xsi:type": "ns273:MoneyInfo"
						},
						"_xsi:type": "ns1:LineItemPriceInfo"
					},
					"lineItemTaxList": {
						"typeOfTax": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"_xsi:nil": "true"
						},
						"primaryCurrencyCode": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"_xsi:nil": "true"
						},
						"federalTaxType": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"_xsi:nil": "true"
						},
						"territoryTaxType": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"_xsi:nil": "true"
						},
						"stateTaxType": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"_xsi:nil": "true"
						},
						"countyTaxType": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"_xsi:nil": "true"
						},
						"cityTaxType": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"_xsi:nil": "true"
						},
						"secondaryStateTaxType": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"_xsi:nil": "true"
						},
						"secondaryCountyTaxType": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"_xsi:nil": "true"
						},
						"secondaryCityTaxType": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"_xsi:nil": "true"
						},
						"districtTaxType": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"_xsi:nil": "true"
						},
						"zeroRateIndicator": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"_xsi:nil": "true"
						},
						"jurisdictionType": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"_xsi:nil": "true"
						},
						"countryOfJurisdictionCode": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"_xsi:nil": "true"
						},
						"territoryOfJurisdictionCode": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"_xsi:nil": "true"
						},
						"stateOfJurisdiction": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"_xsi:nil": "true"
						},
						"countyCodeOfJurisdiction": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"_xsi:nil": "true"
						},
						"countyNameOfJurisdiction": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"_xsi:nil": "true"
						},
						"cityOfJurisdiction": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"_xsi:nil": "true"
						},
						"zipCodeOfJurisdiction": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"_xsi:nil": "true"
						},
						"zipCodeExtensionOfJurisdiction": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"_xsi:nil": "true"
						},
						"geoCodeOfJurisdiction": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"_xsi:nil": "true"
						},
						"secStateOfJurisdiction": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"_xsi:nil": "true"
						},
						"secCountyCodeOfJurisdiction": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"_xsi:nil": "true"
						},
						"secCountyNameOfJurisdiction": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"_xsi:nil": "true"
						},
						"secCityOfJurisdiction": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"_xsi:nil": "true"
						},
						"secZipCodeOfJurisdiction": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"_xsi:nil": "true"
						},
						"secZipCodeExtensionOfJurisdiction": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"_xsi:nil": "true"
						},
						"secGeoCodeOfJurisdiction": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"_xsi:nil": "true"
						},
						"calculatedTaxAmountTotal": {
							"currencyCode": {
								"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"__text": "USD"
							},
							"amount": {
								"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:decimal",
								"__text": "0"
							},
							"_xmlns:ns275": "http://integration.digitalriver.com/Common/1.0",
							"_xsi:type": "ns275:MoneyInfo"
						},
						"calculatedTaxAmountCountry": {
							"_xmlns:ns276": "http://integration.digitalriver.com/Common/1.0",
							"_xsi:type": "ns276:MoneyInfo",
							"_xsi:nil": "true"
						},
						"calculatedTaxAmountTerritory": {
							"_xmlns:ns277": "http://integration.digitalriver.com/Common/1.0",
							"_xsi:type": "ns277:MoneyInfo",
							"_xsi:nil": "true"
						},
						"calculatedTaxAmountState": {
							"_xmlns:ns278": "http://integration.digitalriver.com/Common/1.0",
							"_xsi:type": "ns278:MoneyInfo",
							"_xsi:nil": "true"
						},
						"calculatedTaxAmountCounty": {
							"_xmlns:ns279": "http://integration.digitalriver.com/Common/1.0",
							"_xsi:type": "ns279:MoneyInfo",
							"_xsi:nil": "true"
						},
						"calculatedTaxAmountCity": {
							"_xmlns:ns280": "http://integration.digitalriver.com/Common/1.0",
							"_xsi:type": "ns280:MoneyInfo",
							"_xsi:nil": "true"
						},
						"calculatedTaxAmountSecState": {
							"_xmlns:ns281": "http://integration.digitalriver.com/Common/1.0",
							"_xsi:type": "ns281:MoneyInfo",
							"_xsi:nil": "true"
						},
						"calculatedTaxAmountSecCounty": {
							"_xmlns:ns282": "http://integration.digitalriver.com/Common/1.0",
							"_xsi:type": "ns282:MoneyInfo",
							"_xsi:nil": "true"
						},
						"calculatedTaxAmountSecCity": {
							"_xmlns:ns283": "http://integration.digitalriver.com/Common/1.0",
							"_xsi:type": "ns283:MoneyInfo",
							"_xsi:nil": "true"
						},
						"calculatedTaxAmountDistrict": {
							"_xmlns:ns284": "http://integration.digitalriver.com/Common/1.0",
							"_xsi:type": "ns284:MoneyInfo",
							"_xsi:nil": "true"
						},
						"sellerVatNumber": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"_xsi:nil": "true"
						},
						"buyerVatNumber": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"_xsi:nil": "true"
						},
						"commodityCode": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"_xsi:nil": "true"
						},
						"taxCompanyID": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"_xsi:nil": "true"
						},
						"stateTaxRate": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:decimal",
							"_xsi:nil": "true"
						},
						"secStateTaxRate": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:decimal",
							"_xsi:nil": "true"
						},
						"countyTaxRate": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:decimal",
							"_xsi:nil": "true"
						},
						"secCountyTaxRate": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:decimal",
							"_xsi:nil": "true"
						},
						"cityTaxRate": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:decimal",
							"_xsi:nil": "true"
						},
						"secCityTaxRate": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:decimal",
							"_xsi:nil": "true"
						},
						"countryTaxRate": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:decimal",
							"_xsi:nil": "true"
						},
						"taxDate": {
							"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:date",
							"_xsi:nil": "true"
						},
						"_xmlns:ns274": "http://integration.digitalriver.com/commonRequisition/1.0",
						"_xsi:type": "ns274:LineItemTaxListInfo"
					},
					"offerID": {
						"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "1393809"
					},
					"extendedAttributes": {
						"_xmlns:ns285": "http://integration.digitalriver.com/Common/1.0",
						"_xsi:type": "ns285:ExtendedAttributesInfoArray"
					},
					"_xsi:type": "ns1:LineItemInfo"
				},
				"_xsi:type": "ns1:LineItemInfoArray"
			},
			"offerID": {
				"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
				"_xsi:type": "xsd:string"
			},
			"programID": {
				"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
				"_xsi:type": "xsd:string"
			},
			"customerID": {
				"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
				"_xsi:type": "xsd:string",
				"__text": "11509201109"
			},
			"optIn": {
				"_xmlns:soapenc": "http://schemas.xmlsoap.org/soap/encoding/",
				"_xsi:type": "soapenc:boolean",
				"__text": "true"
			},
			"currencyCodeAlpha": {
				"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
				"_xsi:type": "xsd:string",
				"__text": "USD"
			},
			"currencyCodeNumeric": {
				"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
				"_xsi:type": "xsd:string",
				"_xsi:nil": "true"
			},
			"locale": {
				"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
				"_xsi:type": "xsd:string",
				"__text": "en_US"
			},
			"extendedAttributes": {
				"item": {
					"name": {
						"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "DPLResult"
					},
					"value": {
						"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "Accept"
					},
					"valueDataType": {
						"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "string"
					},
					"_xsi:type": "ns286:ExtendedAttributesInfo"
				},
				"_xmlns:ns286": "http://integration.digitalriver.com/Common/1.0",
				"_xsi:type": "ns286:ExtendedAttributesInfoArray"
			},
			"_xmlns:xsi": "http://www.w3.org/2001/XMLSchema-instance",
			"_xsi:type": "ns1:SalesOrderActivityInfo"
		},
		"_xmlns:ns1": "http://integration.digitalriver.com/salesOrderActivityInfoArray/1.0",
		"__prefix": "ns1"
	}
}
```
{% endtab %}
{% endtabs %}
