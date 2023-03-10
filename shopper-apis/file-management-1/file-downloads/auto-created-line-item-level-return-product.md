---
description: Understand the auto-created line-item level return product.
---

# Auto-created line-item level return product



{% code title="Request body" overflow="wrap" %}
```json
{
	"SalesOrderActivityInfoArray": {
		"reportBeginDate": {
			"_xmlns:xsi": "https://www.w3.org/2001/XMLSchema-instance",
			"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
			"_xsi:type": "xsd:dateTime",
			"__text": "2005-12-20T06:00:00.209Z"
		},
		"reportEndDate": {
			"_xmlns:xsi": "https://www.w3.org/2001/XMLSchema-instance",
			"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
			"_xsi:type": "xsd:dateTime",
			"__text": "2005-12-20T06:00:00.209Z"
		},
		"reportRunDate": {
			"_xmlns:xsi": "https://www.w3.org/2001/XMLSchema-instance",
			"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
			"_xsi:type": "xsd:dateTime",
			"__text": "2005-12-21T10:06:11.209Z"
		},
		"salesOrderActivity": {
			"orderID": {
				"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
				"_xsi:type": "xsd:string",
				"__text": "3950971700"
			},
			"saleDate": {
				"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
				"_xsi:type": "xsd:dateTime",
				"__text": "2006-01-31T06:00:00.328Z"
			},
			"orderDate": {
				"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
				"_xsi:type": "xsd:dateTime",
				"__text": "2005-12-04T15:07:41.328Z"
			},
			"site": {
				"siteID": {
					"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
					"_xsi:type": "xsd:string",
					"__text": "adventur"
				},
				"siteAddress": {
					"addressID": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"_xsi:nil": "true"
					},
					"city": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "Culver City"
					},
					"countryA2": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "US"
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
						"__text": "1234 Happy Lane"
					},
					"line2": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "Suite 200"
					},
					"line3": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string"
					},
					"locationCode": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"_xsi:nil": "true"
					},
					"name1": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "John"
					},
					"name2": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "Doe"
					},
					"phoneNumber": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string"
					},
					"postalCode": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "55555"
					},
					"state": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "MN"
					},
					"email": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string"
					},
					"faxPhone": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string"
					},
					"companyName": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string"
					},
					"phoneNumber2": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string"
					},
					"countyName": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"_xsi:nil": "true"
					},
					"extendedAttributes": {
						"_xsi:type": "ns142:ExtendedAttributesInfoArray",
						"_xsi:nil": "true"
					},
					"_xsi:type": "ns142:AddressInfo"
				},
				"siteURL": {
					"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
					"_xsi:type": "xsd:string",
					"_xsi:nil": "true"
				},
				"_xmlns:ns142": "https://integration.digitalriver.com/Common/1.0",
				"_xsi:type": "ns142:SiteInfo"
			},
			"pricing": {
				"total": {
					"currencyCode": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "USD"
					},
					"amount": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:decimal",
						"__text": "-23.99"
					},
					"_xmlns:ns144": "https://integration.digitalriver.com/Common/1.0",
					"_xsi:type": "ns144:MoneyInfo"
				},
				"subtotal": {
					"currencyCode": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "USD"
					},
					"amount": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:decimal",
						"__text": "-23.99"
					},
					"_xmlns:ns145": "https://integration.digitalriver.com/Common/1.0",
					"_xsi:type": "ns145:MoneyInfo"
				},
				"tax": {
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
					"_xmlns:ns146": "https://integration.digitalriver.com/Common/1.0",
					"_xsi:type": "ns146:MoneyInfo"
				},
				"shipping": {
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
					"_xmlns:ns147": "https://integration.digitalriver.com/Common/1.0",
					"_xsi:type": "ns147:MoneyInfo"
				},
				"incentive": {
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
					"_xmlns:ns148": "https://integration.digitalriver.com/Common/1.0",
					"_xsi:type": "ns148:MoneyInfo"
				},
				"shippingIncentive": {
					"_xmlns:ns149": "https://integration.digitalriver.com/Common/1.0",
					"_xsi:type": "ns149:MoneyInfo",
					"_xsi:nil": "true"
				},
				"nonTaxableFees": {
					"_xmlns:ns150": "https://integration.digitalriver.com/Common/1.0",
					"_xsi:type": "ns150:MoneyInfo",
					"_xsi:nil": "true"
				},
				"taxableFees": {
					"_xmlns:ns151": "https://integration.digitalriver.com/Common/1.0",
					"_xsi:type": "ns151:MoneyInfo",
					"_xsi:nil": "true"
				},
				"taxOnTaxableFees": {
					"_xmlns:ns152": "https://integration.digitalriver.com/Common/1.0",
					"_xsi:type": "ns152:MoneyInfo",
					"_xsi:nil": "true"
				},
				"exchangeRate": {
					"currencyCode": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "USD"
					},
					"amount": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:decimal",
						"__text": "1"
					},
					"_xmlns:ns153": "https://integration.digitalriver.com/Common/1.0",
					"_xsi:type": "ns153:MoneyInfo"
				},
				"_xmlns:ns143": "https://integration.digitalriver.com/commonRequisition/1.0",
				"_xsi:type": "ns143:OrderPriceInfo"
			},
			"paymentInfos": {
				"paymentInfo": {
					"authorizationID": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"_xsi:nil": "true"
					},
					"cardType": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "visa"
					},
					"customerEmail": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "johndoe@msn.com"
					},
					"cardExpirationMonth": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"_xsi:nil": "true"
					},
					"cardExpirationYear": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"_xsi:nil": "true"
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
						"_xsi:type": "xsd:string"
					},
					"customerLastName": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "Doe"
					},
					"customerFirstName": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "John G"
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
							"__text": "-23.99"
						},
						"_xmlns:ns155": "https://integration.digitalriver.com/Common/1.0",
						"_xsi:type": "ns155:MoneyInfo"
					},
					"paymentMethodName": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "CreditCardMethod"
					},
					"billingAddress": {
						"addressID": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"_xsi:nil": "true"
						},
						"city": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "Silver Springs"
						},
						"countryA2": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "US"
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
							"__text": "1234 Happy Street"
						},
						"line2": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string"
						},
						"line3": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string"
						},
						"locationCode": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"_xsi:nil": "true"
						},
						"name1": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "John G"
						},
						"name2": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "Doe"
						},
						"phoneNumber": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "111-222-3333"
						},
						"postalCode": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "55555"
						},
						"state": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "MN"
						},
						"email": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "johndoe@msn.com"
						},
						"faxPhone": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string"
						},
						"companyName": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string"
						},
						"phoneNumber2": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string"
						},
						"countyName": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"_xsi:nil": "true"
						},
						"extendedAttributes": {
							"_xsi:type": "ns156:ExtendedAttributesInfoArray",
							"_xsi:nil": "true"
						},
						"_xmlns:ns156": "https://integration.digitalriver.com/Common/1.0",
						"_xsi:type": "ns156:AddressInfo"
					},
					"_xsi:type": "ns154:PaymentInformationInfo",
					"__text": "xsi:nil=\"true\"/>"
				},
				"_xmlns:ns154": "https://integration.digitalriver.com/commonRequisition/1.0",
				"_xsi:type": "ns154:PaymentInformationInfoArray"
			},
			"lineItems": {
				"item": [
					{
						"lineItemID": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "1748693400"
						},
						"transactionDescription": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "RETURN_RECEIPT"
						},
						"quantity": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:integer",
							"__text": "1"
						},
						"product": {
							"productID": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"__text": "38434700"
							},
							"externalReferenceID": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string"
							},
							"companyID": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"__text": "adventur"
							},
							"locale": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"_xsi:nil": "true"
							},
							"_xmlns:ns157": "https://integration.digitalriver.com/Common/1.0",
							"_xsi:type": "ns157:ProductKey"
						},
						"productInfo": {
							"productDataID": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"__text": "144838500"
							},
							"sku": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"__text": "20038"
							},
							"mfrPartNumber": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string"
							},
							"shipperPartNumber": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string"
							},
							"name": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"__text": "Math Blaster Master the Basics"
							},
							"platform": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"__text": "N/A - not available"
							},
							"companyID": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"__text": "adventur"
							},
							"year": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string"
							},
							"seats": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string"
							},
							"productOwningCompanyName": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"__text": "Knowledge Adventure"
							},
							"extendedAttributes": {
								"item": [
									{
										"name": {
											"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
											"_xsi:type": "xsd:string",
											"__text": "platform"
										},
										"value": {
											"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
											"_xsi:type": "xsd:string",
											"__text": "Windows"
										},
										"valueDataType": {
											"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
											"_xsi:type": "xsd:string",
											"__text": "string"
										},
										"_xsi:type": "ns158:ExtendedAttributesInfo"
									},
									{
										"name": {
											"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
											"_xsi:type": "xsd:string",
											"__text": "upc"
										},
										"value": {
											"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
											"_xsi:type": "xsd:string",
											"__text": "876930005435"
										},
										"valueDataType": {
											"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
											"_xsi:type": "xsd:string",
											"__text": "string"
										},
										"_xsi:type": "ns158:ExtendedAttributesInfo"
									},
									{
										"name": {
											"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
											"_xsi:type": "xsd:string",
											"__text": "weight"
										},
										"value": {
											"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
											"_xsi:type": "xsd:string",
											"__text": "0.5 lb"
										},
										"valueDataType": {
											"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
											"_xsi:type": "xsd:string",
											"__text": "string"
										},
										"_xsi:type": "ns158:ExtendedAttributesInfo"
									}
								],
								"_xmlns:ns158": "https://integration.digitalriver.com/Common/1.0",
								"_xsi:type": "ns158:ExtendedAttributesInfoArray"
							},
							"_xsi:type": "ns1:ProductDataInfo"
						},
						"lineItemDigitalInfoList": {
							"digitalInfo": {
								"serialNumber": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:string"
								},
								"unlockCode": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:string"
								},
								"_xsi:type": "ns159:LineItemDigitalInfo"
							},
							"_xmlns:ns159": "https://integration.digitalriver.com/commonRequisition/1.0",
							"_xsi:type": "ns159:LineItemDigitalInfoArray"
						},
						"shipping": {
							"shipToAddress": {
								"addressID": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:string",
									"_xsi:nil": "true"
								},
								"city": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:string",
									"__text": "Silver Springs"
								},
								"countryA2": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:string",
									"__text": "US"
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
									"__text": "1044 Se 178th Ct"
								},
								"line2": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:string"
								},
								"line3": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:string"
								},
								"locationCode": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:string",
									"_xsi:nil": "true"
								},
								"name1": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:string",
									"__text": "John G"
								},
								"name2": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:string",
									"__text": "Doe"
								},
								"phoneNumber": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:string",
									"__text": "111-222-3333"
								},
								"postalCode": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:string",
									"__text": "55555"
								},
								"state": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:string",
									"__text": "MN"
								},
								"email": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:string",
									"__text": "johndoe@msn.com"
								},
								"faxPhone": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:string"
								},
								"companyName": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:string"
								},
								"phoneNumber2": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:string"
								},
								"countyName": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:string",
									"_xsi:nil": "true"
								},
								"extendedAttributes": {
									"_xsi:type": "ns160:ExtendedAttributesInfoArray",
									"_xsi:nil": "true"
								},
								"_xmlns:ns160": "https://integration.digitalriver.com/Common/1.0",
								"_xsi:type": "ns160:AddressInfo"
							},
							"shippingMethodName": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"__text": "UPS - Ground"
							},
							"carrierName": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"__text": "United Parcel Service"
							},
							"shipmentDate": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:date",
								"__text": "2006-01-31"
							},
							"isReship": {
								"_xmlns:soapenc": "https://schemas.xmlsoap.org/soap/encoding/",
								"_xsi:type": "soapenc:boolean",
								"_xsi:nil": "true"
							},
							"fulfillerID": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"__text": "dss"
							},
							"fulfillerName": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"__text": "DSS"
							},
							"_xsi:type": "ns1:ShipmentInfo"
						},
						"returnInfo": {
							"returnType": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"__text": "*AutoCreatedLineItemLevelReturnProduct*"
							},
							"returnReason": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string"
							},
							"returnDate": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:date",
								"__text": "2006-01-31"
							},
							"serialNumber": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string"
							},
							"returnID": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"__text": "3463709"
							},
							"returnLineItemID": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"__text": "4275309"
							},
							"_xsi:type": "ns1:ReturnInfo"
						},
						"pricing": {
							"unitPrice": {
								"currencyCode": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:string",
									"__text": "USD"
								},
								"amount": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:decimal",
									"__text": "0"
								},
								"_xmlns:ns161": "https://integration.digitalriver.com/Common/1.0",
								"_xsi:type": "ns161:MoneyInfo"
							},
							"listPrice": {
								"currencyCode": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:string",
									"__text": "USD"
								},
								"amount": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:decimal",
									"__text": "0"
								},
								"_xmlns:ns162": "https://integration.digitalriver.com/Common/1.0",
								"_xsi:type": "ns162:MoneyInfo"
							},
							"pricePerQty": {
								"currencyCode": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:string",
									"__text": "USD"
								},
								"amount": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:decimal",
									"__text": "0"
								},
								"_xmlns:ns163": "https://integration.digitalriver.com/Common/1.0",
								"_xsi:type": "ns163:MoneyInfo"
							},
							"saleAmount": {
								"currencyCode": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:string",
									"__text": "USD"
								},
								"amount": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:decimal",
									"__text": "0"
								},
								"_xmlns:ns164": "https://integration.digitalriver.com/Common/1.0",
								"_xsi:type": "ns164:MoneyInfo"
							},
							"shipping": {
								"currencyCode": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:string",
									"__text": "USD"
								},
								"amount": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:decimal",
									"__text": "0"
								},
								"_xmlns:ns165": "https://integration.digitalriver.com/Common/1.0",
								"_xsi:type": "ns165:MoneyInfo"
							},
							"shopperShippingCostPerQty": {
								"currencyCode": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:string",
									"__text": "USD"
								},
								"amount": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:decimal",
									"__text": "0"
								},
								"_xmlns:ns166": "https://integration.digitalriver.com/Common/1.0",
								"_xsi:type": "ns166:MoneyInfo"
							},
							"handling": {
								"currencyCode": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:string",
									"__text": "USD"
								},
								"amount": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:decimal",
									"__text": "0"
								},
								"_xmlns:ns167": "https://integration.digitalriver.com/Common/1.0",
								"_xsi:type": "ns167:MoneyInfo"
							},
							"incentive": {
								"currencyCode": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:string",
									"__text": "USD"
								},
								"amount": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:decimal",
									"__text": "0"
								},
								"_xmlns:ns168": "https://integration.digitalriver.com/Common/1.0",
								"_xsi:type": "ns168:MoneyInfo"
							},
							"reqLevelIncentivePerQuantity": {
								"currencyCode": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:string",
									"__text": "USD"
								},
								"amount": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:decimal",
									"__text": "0"
								},
								"_xmlns:ns169": "https://integration.digitalriver.com/Common/1.0",
								"_xsi:type": "ns169:MoneyInfo"
							},
							"lineItemLevelIncentivePerQuantity": {
								"currencyCode": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:string",
									"__text": "USD"
								},
								"amount": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:decimal",
									"__text": "0"
								},
								"_xmlns:ns170": "https://integration.digitalriver.com/Common/1.0",
								"_xsi:type": "ns170:MoneyInfo"
							},
							"taxableFeesPerQuantity": {
								"currencyCode": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:string",
									"__text": "USD"
								},
								"amount": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:decimal",
									"__text": "0"
								},
								"_xmlns:ns171": "https://integration.digitalriver.com/Common/1.0",
								"_xsi:type": "ns171:MoneyInfo"
							},
							"_xsi:type": "ns1:LineItemPriceInfo"
						},
						"lineItemTaxList": {
							"typeOfTax": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"_xsi:nil": "true"
							},
							"primaryCurrencyCode": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"_xsi:nil": "true"
							},
							"federalTaxType": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"_xsi:nil": "true"
							},
							"territoryTaxType": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"_xsi:nil": "true"
							},
							"stateTaxType": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"_xsi:nil": "true"
							},
							"countyTaxType": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"_xsi:nil": "true"
							},
							"cityTaxType": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"_xsi:nil": "true"
							},
							"secondaryStateTaxType": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"_xsi:nil": "true"
							},
							"secondaryCountyTaxType": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"_xsi:nil": "true"
							},
							"secondaryCityTaxType": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"_xsi:nil": "true"
							},
							"districtTaxType": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"_xsi:nil": "true"
							},
							"zeroRateIndicator": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"_xsi:nil": "true"
							},
							"jurisdictionType": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"_xsi:nil": "true"
							},
							"countryOfJurisdictionCode": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"_xsi:nil": "true"
							},
							"territoryOfJurisdictionCode": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"_xsi:nil": "true"
							},
							"stateOfJurisdiction": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"_xsi:nil": "true"
							},
							"countyCodeOfJurisdiction": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"_xsi:nil": "true"
							},
							"countyNameOfJurisdiction": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"_xsi:nil": "true"
							},
							"cityOfJurisdiction": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"_xsi:nil": "true"
							},
							"zipCodeOfJurisdiction": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"_xsi:nil": "true"
							},
							"zipCodeExtensionOfJurisdiction": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"_xsi:nil": "true"
							},
							"geoCodeOfJurisdiction": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"_xsi:nil": "true"
							},
							"secStateOfJurisdiction": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"_xsi:nil": "true"
							},
							"secCountyCodeOfJurisdiction": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"_xsi:nil": "true"
							},
							"secCountyNameOfJurisdiction": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"_xsi:nil": "true"
							},
							"secCityOfJurisdiction": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"_xsi:nil": "true"
							},
							"secZipCodeOfJurisdiction": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"_xsi:nil": "true"
							},
							"secZipCodeExtensionOfJurisdiction": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"_xsi:nil": "true"
							},
							"secGeoCodeOfJurisdiction": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"_xsi:nil": "true"
							},
							"calculatedTaxAmountTotal": {
								"currencyCode": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:string",
									"__text": "USD"
								},
								"amount": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:decimal",
									"__text": "0"
								},
								"_xmlns:ns173": "https://integration.digitalriver.com/Common/1.0",
								"_xsi:type": "ns173:MoneyInfo"
							},
							"calculatedTaxAmountCountry": {
								"_xmlns:ns174": "https://integration.digitalriver.com/Common/1.0",
								"_xsi:type": "ns174:MoneyInfo",
								"_xsi:nil": "true"
							},
							"calculatedTaxAmountTerritory": {
								"_xmlns:ns175": "https://integration.digitalriver.com/Common/1.0",
								"_xsi:type": "ns175:MoneyInfo",
								"_xsi:nil": "true"
							},
							"calculatedTaxAmountState": {
								"_xmlns:ns176": "https://integration.digitalriver.com/Common/1.0",
								"_xsi:type": "ns176:MoneyInfo",
								"_xsi:nil": "true"
							},
							"calculatedTaxAmountCounty": {
								"_xmlns:ns177": "https://integration.digitalriver.com/Common/1.0",
								"_xsi:type": "ns177:MoneyInfo",
								"_xsi:nil": "true"
							},
							"calculatedTaxAmountCity": {
								"_xmlns:ns178": "https://integration.digitalriver.com/Common/1.0",
								"_xsi:type": "ns178:MoneyInfo",
								"_xsi:nil": "true"
							},
							"calculatedTaxAmountSecState": {
								"_xmlns:ns179": "https://integration.digitalriver.com/Common/1.0",
								"_xsi:type": "ns179:MoneyInfo",
								"_xsi:nil": "true"
							},
							"calculatedTaxAmountSecCounty": {
								"_xmlns:ns180": "https://integration.digitalriver.com/Common/1.0",
								"_xsi:type": "ns180:MoneyInfo",
								"_xsi:nil": "true"
							},
							"calculatedTaxAmountSecCity": {
								"_xmlns:ns181": "https://integration.digitalriver.com/Common/1.0",
								"_xsi:type": "ns181:MoneyInfo",
								"_xsi:nil": "true"
							},
							"calculatedTaxAmountDistrict": {
								"_xmlns:ns182": "https://integration.digitalriver.com/Common/1.0",
								"_xsi:type": "ns182:MoneyInfo",
								"_xsi:nil": "true"
							},
							"sellerVatNumber": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"_xsi:nil": "true"
							},
							"buyerVatNumber": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"_xsi:nil": "true"
							},
							"commodityCode": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"_xsi:nil": "true"
							},
							"taxCompanyID": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"_xsi:nil": "true"
							},
							"stateTaxRate": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:decimal",
								"_xsi:nil": "true"
							},
							"secStateTaxRate": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:decimal",
								"_xsi:nil": "true"
							},
							"countyTaxRate": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:decimal",
								"_xsi:nil": "true"
							},
							"secCountyTaxRate": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:decimal",
								"_xsi:nil": "true"
							},
							"cityTaxRate": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:decimal",
								"_xsi:nil": "true"
							},
							"secCityTaxRate": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:decimal",
								"_xsi:nil": "true"
							},
							"countryTaxRate": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:decimal",
								"_xsi:nil": "true"
							},
							"taxDate": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:date",
								"_xsi:nil": "true"
							},
							"_xmlns:ns172": "https://integration.digitalriver.com/commonRequisition/1.0",
							"_xsi:type": "ns172:LineItemTaxListInfo"
						},
						"offerID": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "15762509"
						},
						"extendedAttributes": {
							"_xmlns:ns183": "https://integration.digitalriver.com/Common/1.0",
							"_xsi:type": "ns183:ExtendedAttributesInfoArray"
						},
						"_xsi:type": "ns1:LineItemInfo"
					},
					{
						"lineItemID": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "1748688900"
						},
						"transactionDescription": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "RETURN_RECEIPT"
						},
						"quantity": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:integer",
							"__text": "1"
						},
						"product": {
							"productID": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"__text": "38432800"
							},
							"externalReferenceID": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string"
							},
							"companyID": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"__text": "adventur"
							},
							"locale": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"_xsi:nil": "true"
							},
							"_xmlns:ns184": "https://integration.digitalriver.com/Common/1.0",
							"_xsi:type": "ns184:ProductKey"
						},
						"productInfo": {
							"productDataID": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"__text": "144396900"
							},
							"sku": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"__text": "72046"
							},
							"mfrPartNumber": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string"
							},
							"shipperPartNumber": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string"
							},
							"name": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"__text": "JumpStart Advanced 1st Grade"
							},
							"platform": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"__text": "N/A - not available"
							},
							"companyID": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"__text": "adventur"
							},
							"year": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string"
							},
							"seats": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string"
							},
							"productOwningCompanyName": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"__text": "Knowledge Adventure"
							},
							"extendedAttributes": {
								"item": [
									{
										"name": {
											"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
											"_xsi:type": "xsd:string",
											"__text": "platform"
										},
										"value": {
											"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
											"_xsi:type": "xsd:string",
											"__text": "Macintosh/Windows"
										},
										"valueDataType": {
											"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
											"_xsi:type": "xsd:string",
											"__text": "string"
										},
										"_xsi:type": "ns185:ExtendedAttributesInfo"
									},
									{
										"name": {
											"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
											"_xsi:type": "xsd:string",
											"__text": "upc"
										},
										"value": {
											"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
											"_xsi:type": "xsd:string",
											"__text": "876930000140"
										},
										"valueDataType": {
											"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
											"_xsi:type": "xsd:string",
											"__text": "string"
										},
										"_xsi:type": "ns185:ExtendedAttributesInfo"
									},
									{
										"name": {
											"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
											"_xsi:type": "xsd:string",
											"__text": "weight"
										},
										"value": {
											"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
											"_xsi:type": "xsd:string",
											"__text": "0.59 lb"
										},
										"valueDataType": {
											"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
											"_xsi:type": "xsd:string",
											"__text": "string"
										},
										"_xsi:type": "ns185:ExtendedAttributesInfo"
									}
								],
								"_xmlns:ns185": "https://integration.digitalriver.com/Common/1.0",
								"_xsi:type": "ns185:ExtendedAttributesInfoArray"
							},
							"_xsi:type": "ns1:ProductDataInfo"
						},
						"lineItemDigitalInfoList": {
							"digitalInfo": {
								"serialNumber": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:string"
								},
								"unlockCode": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:string"
								},
								"_xsi:type": "ns186:LineItemDigitalInfo"
							},
							"_xmlns:ns186": "https://integration.digitalriver.com/commonRequisition/1.0",
							"_xsi:type": "ns186:LineItemDigitalInfoArray"
						},
						"shipping": {
							"shipToAddress": {
								"addressID": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:string",
									"_xsi:nil": "true"
								},
								"city": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:string",
									"__text": "Silver Springs"
								},
								"countryA2": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:string",
									"__text": "US"
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
									"__text": "1044 Se 178th Ct"
								},
								"line2": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:string"
								},
								"line3": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:string"
								},
								"locationCode": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:string",
									"_xsi:nil": "true"
								},
								"name1": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:string",
									"__text": "John G"
								},
								"name2": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:string",
									"__text": "Doe"
								},
								"phoneNumber": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:string",
									"__text": "111-222-3333"
								},
								"postalCode": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:string",
									"__text": "34488-5744"
								},
								"state": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:string",
									"__text": "MN"
								},
								"email": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:string",
									"__text": "Johndoe@msn.com"
								},
								"faxPhone": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:string"
								},
								"companyName": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:string"
								},
								"phoneNumber2": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:string"
								},
								"countyName": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:string",
									"_xsi:nil": "true"
								},
								"extendedAttributes": {
									"_xsi:type": "ns187:ExtendedAttributesInfoArray",
									"_xsi:nil": "true"
								},
								"_xmlns:ns187": "https://integration.digitalriver.com/Common/1.0",
								"_xsi:type": "ns187:AddressInfo"
							},
							"shippingMethodName": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"__text": "UPS - Ground"
							},
							"carrierName": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"__text": "United Parcel Service"
							},
							"shipmentDate": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:date",
								"__text": "2006-01-31"
							},
							"isReship": {
								"_xmlns:soapenc": "https://schemas.xmlsoap.org/soap/encoding/",
								"_xsi:type": "soapenc:boolean",
								"_xsi:nil": "true"
							},
							"fulfillerID": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"__text": "dss"
							},
							"fulfillerName": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"__text": "DSS"
							},
							"_xsi:type": "ns1:ShipmentInfo"
						},
						"returnInfo": {
							"returnType": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"__text": "AutoCreatedLineItemLevelReturnProduct"
							},
							"returnReason": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string"
							},
							"returnDate": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:date",
								"__text": "2006-01-31"
							},
							"serialNumber": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string"
							},
							"returnID": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"__text": "3463709"
							},
							"returnLineItemID": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"__text": "4275209"
							},
							"_xsi:type": "ns1:ReturnInfo"
						},
						"pricing": {
							"unitPrice": {
								"currencyCode": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:string",
									"__text": "USD"
								},
								"amount": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:decimal",
									"__text": "0"
								},
								"_xmlns:ns188": "https://integration.digitalriver.com/Common/1.0",
								"_xsi:type": "ns188:MoneyInfo"
							},
							"listPrice": {
								"currencyCode": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:string",
									"__text": "USD"
								},
								"amount": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:decimal",
									"__text": "0"
								},
								"_xmlns:ns189": "https://integration.digitalriver.com/Common/1.0",
								"_xsi:type": "ns189:MoneyInfo"
							},
							"pricePerQty": {
								"currencyCode": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:string",
									"__text": "USD"
								},
								"amount": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:decimal",
									"__text": "0"
								},
								"_xmlns:ns190": "https://integration.digitalriver.com/Common/1.0",
								"_xsi:type": "ns190:MoneyInfo"
							},
							"saleAmount": {
								"currencyCode": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:string",
									"__text": "USD"
								},
								"amount": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:decimal",
									"__text": "-23.99"
								},
								"_xmlns:ns191": "https://integration.digitalriver.com/Common/1.0",
								"_xsi:type": "ns191:MoneyInfo"
							},
							"shipping": {
								"currencyCode": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:string",
									"__text": "USD"
								},
								"amount": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:decimal",
									"__text": "0"
								},
								"_xmlns:ns192": "https://integration.digitalriver.com/Common/1.0",
								"_xsi:type": "ns192:MoneyInfo"
							},
							"shopperShippingCostPerQty": {
								"currencyCode": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:string",
									"__text": "USD"
								},
								"amount": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:decimal",
									"__text": "0"
								},
								"_xmlns:ns193": "https://integration.digitalriver.com/Common/1.0",
								"_xsi:type": "ns193:MoneyInfo"
							},
							"handling": {
								"currencyCode": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:string",
									"__text": "USD"
								},
								"amount": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:decimal",
									"__text": "0"
								},
								"_xmlns:ns194": "https://integration.digitalriver.com/Common/1.0",
								"_xsi:type": "ns194:MoneyInfo"
							},
							"incentive": {
								"currencyCode": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:string",
									"__text": "USD"
								},
								"amount": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:decimal",
									"__text": "0"
								},
								"_xmlns:ns195": "https://integration.digitalriver.com/Common/1.0",
								"_xsi:type": "ns195:MoneyInfo"
							},
							"reqLevelIncentivePerQuantity": {
								"currencyCode": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:string",
									"__text": "USD"
								},
								"amount": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:decimal",
									"__text": "0"
								},
								"_xmlns:ns196": "https://integration.digitalriver.com/Common/1.0",
								"_xsi:type": "ns196:MoneyInfo"
							},
							"lineItemLevelIncentivePerQuantity": {
								"currencyCode": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:string",
									"__text": "USD"
								},
								"amount": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:decimal",
									"__text": "0"
								},
								"_xmlns:ns197": "https://integration.digitalriver.com/Common/1.0",
								"_xsi:type": "ns197:MoneyInfo"
							},
							"taxableFeesPerQuantity": {
								"currencyCode": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:string",
									"__text": "USD"
								},
								"amount": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:decimal",
									"__text": "0"
								},
								"_xmlns:ns198": "https://integration.digitalriver.com/Common/1.0",
								"_xsi:type": "ns198:MoneyInfo"
							},
							"_xsi:type": "ns1:LineItemPriceInfo"
						},
						"lineItemTaxList": {
							"typeOfTax": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"_xsi:nil": "true"
							},
							"primaryCurrencyCode": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"_xsi:nil": "true"
							},
							"federalTaxType": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"_xsi:nil": "true"
							},
							"territoryTaxType": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"_xsi:nil": "true"
							},
							"stateTaxType": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"_xsi:nil": "true"
							},
							"countyTaxType": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"_xsi:nil": "true"
							},
							"cityTaxType": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"_xsi:nil": "true"
							},
							"secondaryStateTaxType": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"_xsi:nil": "true"
							},
							"secondaryCountyTaxType": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"_xsi:nil": "true"
							},
							"secondaryCityTaxType": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"_xsi:nil": "true"
							},
							"districtTaxType": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"_xsi:nil": "true"
							},
							"zeroRateIndicator": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"_xsi:nil": "true"
							},
							"jurisdictionType": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"_xsi:nil": "true"
							},
							"countryOfJurisdictionCode": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"_xsi:nil": "true"
							},
							"territoryOfJurisdictionCode": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"_xsi:nil": "true"
							},
							"stateOfJurisdiction": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"_xsi:nil": "true"
							},
							"countyCodeOfJurisdiction": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"_xsi:nil": "true"
							},
							"countyNameOfJurisdiction": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"_xsi:nil": "true"
							},
							"cityOfJurisdiction": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"_xsi:nil": "true"
							},
							"zipCodeOfJurisdiction": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"_xsi:nil": "true"
							},
							"zipCodeExtensionOfJurisdiction": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"_xsi:nil": "true"
							},
							"geoCodeOfJurisdiction": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"_xsi:nil": "true"
							},
							"secStateOfJurisdiction": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"_xsi:nil": "true"
							},
							"secCountyCodeOfJurisdiction": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"_xsi:nil": "true"
							},
							"secCountyNameOfJurisdiction": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"_xsi:nil": "true"
							},
							"secCityOfJurisdiction": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"_xsi:nil": "true"
							},
							"secZipCodeOfJurisdiction": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"_xsi:nil": "true"
							},
							"secZipCodeExtensionOfJurisdiction": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"_xsi:nil": "true"
							},
							"secGeoCodeOfJurisdiction": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"_xsi:nil": "true"
							},
							"calculatedTaxAmountTotal": {
								"currencyCode": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:string",
									"__text": "USD"
								},
								"amount": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:decimal",
									"__text": "0"
								},
								"_xmlns:ns200": "https://integration.digitalriver.com/Common/1.0",
								"_xsi:type": "ns200:MoneyInfo"
							},
							"calculatedTaxAmountCountry": {
								"_xmlns:ns201": "https://integration.digitalriver.com/Common/1.0",
								"_xsi:type": "ns201:MoneyInfo",
								"_xsi:nil": "true"
							},
							"calculatedTaxAmountTerritory": {
								"_xmlns:ns202": "https://integration.digitalriver.com/Common/1.0",
								"_xsi:type": "ns202:MoneyInfo",
								"_xsi:nil": "true"
							},
							"calculatedTaxAmountState": {
								"_xmlns:ns203": "https://integration.digitalriver.com/Common/1.0",
								"_xsi:type": "ns203:MoneyInfo",
								"_xsi:nil": "true"
							},
							"calculatedTaxAmountCounty": {
								"_xmlns:ns204": "https://integration.digitalriver.com/Common/1.0",
								"_xsi:type": "ns204:MoneyInfo",
								"_xsi:nil": "true"
							},
							"calculatedTaxAmountCity": {
								"_xmlns:ns205": "https://integration.digitalriver.com/Common/1.0",
								"_xsi:type": "ns205:MoneyInfo",
								"_xsi:nil": "true"
							},
							"calculatedTaxAmountSecState": {
								"_xmlns:ns206": "https://integration.digitalriver.com/Common/1.0",
								"_xsi:type": "ns206:MoneyInfo",
								"_xsi:nil": "true"
							},
							"calculatedTaxAmountSecCounty": {
								"_xmlns:ns207": "https://integration.digitalriver.com/Common/1.0",
								"_xsi:type": "ns207:MoneyInfo",
								"_xsi:nil": "true"
							},
							"calculatedTaxAmountSecCity": {
								"_xmlns:ns208": "https://integration.digitalriver.com/Common/1.0",
								"_xsi:type": "ns208:MoneyInfo",
								"_xsi:nil": "true"
							},
							"calculatedTaxAmountDistrict": {
								"_xmlns:ns209": "https://integration.digitalriver.com/Common/1.0",
								"_xsi:type": "ns209:MoneyInfo",
								"_xsi:nil": "true"
							},
							"sellerVatNumber": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"_xsi:nil": "true"
							},
							"buyerVatNumber": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"_xsi:nil": "true"
							},
							"commodityCode": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"_xsi:nil": "true"
							},
							"taxCompanyID": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"_xsi:nil": "true"
							},
							"stateTaxRate": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:decimal",
								"_xsi:nil": "true"
							},
							"secStateTaxRate": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:decimal",
								"_xsi:nil": "true"
							},
							"countyTaxRate": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:decimal",
								"_xsi:nil": "true"
							},
							"secCountyTaxRate": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:decimal",
								"_xsi:nil": "true"
							},
							"cityTaxRate": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:decimal",
								"_xsi:nil": "true"
							},
							"secCityTaxRate": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:decimal",
								"_xsi:nil": "true"
							},
							"countryTaxRate": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:decimal",
								"_xsi:nil": "true"
							},
							"taxDate": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:date",
								"_xsi:nil": "true"
							},
							"_xmlns:ns199": "https://integration.digitalriver.com/commonRequisition/1.0",
							"_xsi:type": "ns199:LineItemTaxListInfo"
						},
						"offerID": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "15762509"
						},
						"extendedAttributes": {
							"_xmlns:ns210": "https://integration.digitalriver.com/Common/1.0",
							"_xsi:type": "ns210:ExtendedAttributesInfoArray"
						},
						"_xsi:type": "ns1:LineItemInfo"
					}
				],
				"_xsi:type": "ns1:LineItemInfoArray"
			},
			"offerID": {
				"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
				"_xsi:type": "xsd:string"
			},
			"programID": {
				"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
				"_xsi:type": "xsd:string"
			},
			"customerID": {
				"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
				"_xsi:type": "xsd:string",
				"__text": "11122233344"
			},
			"loginID": {
				"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
				"_xsi:type": "xsd:string",
				"__text": "johndoe@msn.com"
			},
			"optIn": {
				"_xmlns:soapenc": "https://schemas.xmlsoap.org/soap/encoding/",
				"_xsi:type": "soapenc:boolean",
				"__text": "true"
			},
			"currencyCodeAlpha": {
				"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
				"_xsi:type": "xsd:string",
				"__text": "USD"
			},
			"currencyCodeNumeric": {
				"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
				"_xsi:type": "xsd:string",
				"_xsi:nil": "true"
			},
			"locale": {
				"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
				"_xsi:type": "xsd:string",
				"__text": "en_US"
			},
			"extendedAttributes": {
				"item": {
					"name": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "DPLResult"
					},
					"value": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "Accept"
					},
					"valueDataType": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "string"
					},
					"_xsi:type": "ns211:ExtendedAttributesInfo"
				},
				"_xmlns:ns211": "https://integration.digitalriver.com/Common/1.0",
				"_xsi:type": "ns211:ExtendedAttributesInfoArray"
			},
			"_xmlns:xsi": "https://www.w3.org/2001/XMLSchema-instance",
			"_xsi:type": "ns1:SalesOrderActivityInfo"
		},
		"_xmlns:ns1": "https://integration.digitalriver.com/salesOrderActivityInfoArray/1.0",
		"__prefix": "ns1"
	}
}
```
{% endcode %}
