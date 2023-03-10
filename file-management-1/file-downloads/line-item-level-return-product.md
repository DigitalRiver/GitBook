---
description: Understand the line-item level return product.
---

# Line-item level return product

{% code title="Request body" %}
```
{
	"SalesOrderActivityInfoArray": {
		"reportBeginDate": {
			"_xmlns:xsi": "https://www.w3.org/2001/XMLSchema-instance",
			"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
			"_xsi:type": "xsd:dateTime",
			"__text": "2005-12-21T06:00:00.505Z"
		},
		"reportEndDate": {
			"_xmlns:xsi": "https://www.w3.org/2001/XMLSchema-instance",
			"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
			"_xsi:type": "xsd:dateTime",
			"__text": "2005-12-21T06:00:00.505Z"
		},
		"reportRunDate": {
			"_xmlns:xsi": "https://www.w3.org/2001/XMLSchema-instance",
			"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
			"_xsi:type": "xsd:dateTime",
			"__text": "2005-12-22T10:05:21.505Z"
		},
		"salesOrderActivity": {
			"orderID": {
				"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
				"_xsi:type": "xsd:string",
				"__text": "1112223334"
			},
			"saleDate": {
				"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
				"_xsi:type": "xsd:dateTime",
				"__text": "2005-12-21T06:00:00.704Z"
			},
			"orderDate": {
				"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
				"_xsi:type": "xsd:dateTime",
				"__text": "2005-12-15T16:46:09.704Z"
			},
			"site": {
				"siteID": {
					"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
					"_xsi:type": "xsd:string",
					"__text": "testsite"
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
						"__text": "Eden Prairie"
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
						"__text": "Digital"
					},
					"name2": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "River"
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
						"_xsi:type": "ns45:ExtendedAttributesInfoArray",
						"_xsi:nil": "true"
					},
					"_xsi:type": "ns45:AddressInfo"
				},
				"siteURL": {
					"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
					"_xsi:type": "xsd:string",
					"_xsi:nil": "true"
				},
				"_xmlns:ns45": "https://integration.digitalriver.com/Common/1.0",
				"_xsi:type": "ns45:SiteInfo"
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
						"__text": "-59.49"
					},
					"_xmlns:ns47": "https://integration.digitalriver.com/Common/1.0",
					"_xsi:type": "ns47:MoneyInfo"
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
						"__text": "-59.49"
					},
					"_xmlns:ns48": "https://integration.digitalriver.com/Common/1.0",
					"_xsi:type": "ns48:MoneyInfo"
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
					"_xmlns:ns49": "https://integration.digitalriver.com/Common/1.0",
					"_xsi:type": "ns49:MoneyInfo"
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
					"_xmlns:ns50": "https://integration.digitalriver.com/Common/1.0",
					"_xsi:type": "ns50:MoneyInfo"
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
					"_xmlns:ns51": "https://integration.digitalriver.com/Common/1.0",
					"_xsi:type": "ns51:MoneyInfo"
				},
				"shippingIncentive": {
					"_xmlns:ns52": "https://integration.digitalriver.com/Common/1.0",
					"_xsi:type": "ns52:MoneyInfo",
					"_xsi:nil": "true"
				},
				"nonTaxableFees": {
					"_xmlns:ns53": "https://integration.digitalriver.com/Common/1.0",
					"_xsi:type": "ns53:MoneyInfo",
					"_xsi:nil": "true"
				},
				"taxableFees": {
					"_xmlns:ns54": "https://integration.digitalriver.com/Common/1.0",
					"_xsi:type": "ns54:MoneyInfo",
					"_xsi:nil": "true"
				},
				"taxOnTaxableFees": {
					"_xmlns:ns55": "https://integration.digitalriver.com/Common/1.0",
					"_xsi:type": "ns55:MoneyInfo",
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
					"_xmlns:ns56": "https://integration.digitalriver.com/Common/1.0",
					"_xsi:type": "ns56:MoneyInfo"
				},
				"_xmlns:ns46": "https://integration.digitalriver.com/commonRequisition/1.0",
				"_xsi:type": "ns46:OrderPriceInfo"
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
						"__text": "americanExpress"
					},
					"customerEmail": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "johndoe@yahoo.com"
					},
					"cardNumber": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"_xsi:nil": "true"
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
						"__text": "John"
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
							"__text": "-59.49"
						},
						"_xmlns:ns58": "https://integration.digitalriver.com/Common/1.0",
						"_xsi:type": "ns58:MoneyInfo"
					},
					"paymentMethodName": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"_xsi:nil": "true"
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
							"__text": "Eden Prairie"
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
							"__text": "Suite 1234"
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
							"_xsi:type": "xsd:string",
							"__text": "612-111-2222"
						},
						"postalCode": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "55441"
						},
						"state": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "MN"
						},
						"email": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "johndoe@yahoo.com"
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
							"_xsi:type": "ns59:ExtendedAttributesInfoArray",
							"_xsi:nil": "true"
						},
						"_xmlns:ns59": "https://integration.digitalriver.com/Common/1.0",
						"_xsi:type": "ns59:AddressInfo"
					},
					"_xsi:type": "ns57:PaymentInformationInfo"
				},
				"_xmlns:ns57": "https://integration.digitalriver.com/commonRequisition/1.0",
				"_xsi:type": "ns57:PaymentInformationInfoArray"
			},
			"lineItems": {
				"item": {
					"lineItemID": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "1789699700"
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
							"__text": "36454100"
						},
						"externalReferenceID": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "SSIP"
						},
						"companyID": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "test"
						},
						"locale": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"_xsi:nil": "true"
						},
						"_xmlns:ns60": "https://integration.digitalriver.com/Common/1.0",
						"_xsi:type": "ns60:ProductKey"
					},
					"productInfo": {
						"productDataID": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "198768900"
						},
						"sku": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "ETRIFF90EDL01"
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
							"__text": "Internet Security Suite"
						},
						"platform": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "N/A - not available"
						},
						"companyID": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "ca"
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
							"__text": "Computer Associates International, Inc. Master"
						},
						"extendedAttributes": {
							"item": [
								{
									"name": {
										"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
										"_xsi:type": "xsd:string"
									},
									"value": {
										"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
										"_xsi:type": "xsd:string"
									},
									"valueDataType": {
										"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
										"_xsi:type": "xsd:string",
										"__text": "string"
									},
									"_xsi:type": "ns61:ExtendedAttributesInfo"
								},
								{
									"name": {
										"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
										"_xsi:type": "xsd:string",
										"__text": "Fireclick Family"
									},
									"value": {
										"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
										"_xsi:type": "xsd:string",
										"__text": "Internet Security Suite"
									},
									"valueDataType": {
										"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
										"_xsi:type": "xsd:string",
										"__text": "string"
									},
									"_xsi:type": "ns61:ExtendedAttributesInfo"
								},
								{
									"name": {
										"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
										"_xsi:type": "xsd:string",
										"__text": "fileSize"
									},
									"value": {
										"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
										"_xsi:type": "xsd:string",
										"__text": "24800"
									},
									"valueDataType": {
										"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
										"_xsi:type": "xsd:string",
										"__text": "string"
									},
									"_xsi:type": "ns61:ExtendedAttributesInfo"
								},
								{
									"name": {
										"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
										"_xsi:type": "xsd:string",
										"__text": "longOnsiteB"
									},
									"value": {
										"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
										"_xsi:type": "xsd:string"
									},
									"valueDataType": {
										"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
										"_xsi:type": "xsd:string",
										"__text": "string"
									},
									"_xsi:type": "ns61:ExtendedAttributesInfo"
								},
								{
									"name": {
										"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
										"_xsi:type": "xsd:string",
										"__text": "numberOfIPAddresses"
									},
									"value": {
										"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
										"_xsi:type": "xsd:string",
										"__text": "100"
									},
									"valueDataType": {
										"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
										"_xsi:type": "xsd:string",
										"__text": "string"
									},
									"_xsi:type": "ns61:ExtendedAttributesInfo"
								},
								{
									"name": {
										"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
										"_xsi:type": "xsd:string",
										"__text": "catNameImage"
									},
									"value": {
										"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
										"_xsi:type": "xsd:string",
										"__text": "eISS_watermark_CL.gif"
									},
									"valueDataType": {
										"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
										"_xsi:type": "xsd:string",
										"__text": "string"
									},
									"_xsi:type": "ns61:ExtendedAttributesInfo"
								},
								{
									"name": {
										"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
										"_xsi:type": "xsd:string",
										"__text": "longOmni"
									},
									"value": {
										"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
										"_xsi:type": "xsd:string"
									},
									"valueDataType": {
										"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
										"_xsi:type": "xsd:string",
										"__text": "string"
									},
									"_xsi:type": "ns61:ExtendedAttributesInfo"
								},
								{
									"name": {
										"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
										"_xsi:type": "xsd:string",
										"__text": "Incrementor"
									},
									"value": {
										"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
										"_xsi:type": "xsd:string",
										"__text": "1"
									},
									"valueDataType": {
										"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
										"_xsi:type": "xsd:string",
										"__text": "string"
									},
									"_xsi:type": "ns61:ExtendedAttributesInfo"
								},
								{
									"name": {
										"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
										"_xsi:type": "xsd:string",
										"__text": "pdNameImage"
									},
									"value": {
										"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
										"_xsi:type": "xsd:string",
										"__text": "eISS_watermark.gif"
									},
									"valueDataType": {
										"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
										"_xsi:type": "xsd:string",
										"__text": "string"
									},
									"_xsi:type": "ns61:ExtendedAttributesInfo"
								},
								{
									"name": {
										"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
										"_xsi:type": "xsd:string",
										"__text": "pdKeyFeatures"
									},
									"value": {
										"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
										"_xsi:type": "xsd:string"
									},
									"valueDataType": {
										"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
										"_xsi:type": "xsd:string",
										"__text": "string"
									},
									"_xsi:type": "ns61:ExtendedAttributesInfo"
								},
								{
									"name": {
										"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
										"_xsi:type": "xsd:string",
										"__text": "userLicenses"
									},
									"value": {
										"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
										"_xsi:type": "xsd:string",
										"__text": "Single User"
									},
									"valueDataType": {
										"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
										"_xsi:type": "xsd:string",
										"__text": "string"
									},
									"_xsi:type": "ns61:ExtendedAttributesInfo"
								},
								{
									"name": {
										"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
										"_xsi:type": "xsd:string",
										"__text": "licenseOnly"
									},
									"value": {
										"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
										"_xsi:type": "xsd:string",
										"__text": "false"
									},
									"valueDataType": {
										"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
										"_xsi:type": "xsd:string",
										"__text": "string"
									},
									"_xsi:type": "ns61:ExtendedAttributesInfo"
								},
								{
									"name": {
										"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
										"_xsi:type": "xsd:string",
										"__text": "downloadType"
									},
									"value": {
										"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
										"_xsi:type": "xsd:string",
										"__text": "HTTP"
									},
									"valueDataType": {
										"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
										"_xsi:type": "xsd:string",
										"__text": "string"
									},
									"_xsi:type": "ns61:ExtendedAttributesInfo"
								},
								{
									"name": {
										"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
										"_xsi:type": "xsd:string",
										"__text": "fulfiller"
									},
									"value": {
										"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
										"_xsi:type": "xsd:string",
										"__text": "DSS"
									},
									"valueDataType": {
										"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
										"_xsi:type": "xsd:string",
										"__text": "string"
									},
									"_xsi:type": "ns61:ExtendedAttributesInfo"
								},
								{
									"name": {
										"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
										"_xsi:type": "xsd:string",
										"__text": "userType"
									},
									"value": {
										"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
										"_xsi:type": "xsd:string",
										"__text": "New"
									},
									"valueDataType": {
										"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
										"_xsi:type": "xsd:string",
										"__text": "string"
									},
									"_xsi:type": "ns61:ExtendedAttributesInfo"
								},
								{
									"name": {
										"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
										"_xsi:type": "xsd:string",
										"__text": "gameRating"
									},
									"value": {
										"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
										"_xsi:type": "xsd:string",
										"__text": "Teen"
									},
									"valueDataType": {
										"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
										"_xsi:type": "xsd:string",
										"__text": "string"
									},
									"_xsi:type": "ns61:ExtendedAttributesInfo"
								},
								{
									"name": {
										"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
										"_xsi:type": "xsd:string",
										"__text": "platform"
									},
									"value": {
										"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
										"_xsi:type": "xsd:string",
										"__text": "Windows 98/NT/2000/XP"
									},
									"valueDataType": {
										"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
										"_xsi:type": "xsd:string",
										"__text": "string"
									},
									"_xsi:type": "ns61:ExtendedAttributesInfo"
								},
								{
									"name": {
										"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
										"_xsi:type": "xsd:string",
										"__text": "timeFrame"
									},
									"value": {
										"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
										"_xsi:type": "xsd:string",
										"__text": "30"
									},
									"valueDataType": {
										"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
										"_xsi:type": "xsd:string",
										"__text": "string"
									},
									"_xsi:type": "ns61:ExtendedAttributesInfo"
								},
								{
									"name": {
										"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
										"_xsi:type": "xsd:string",
										"__text": "downloadAction"
									},
									"value": {
										"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
										"_xsi:type": "xsd:string",
										"__text": "GET"
									},
									"valueDataType": {
										"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
										"_xsi:type": "xsd:string",
										"__text": "string"
									},
									"_xsi:type": "ns61:ExtendedAttributesInfo"
								},
								{
									"name": {
										"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
										"_xsi:type": "xsd:string",
										"__text": "longOnsite"
									},
									"value": {
										"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
										"_xsi:type": "xsd:string"
									},
									"valueDataType": {
										"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
										"_xsi:type": "xsd:string",
										"__text": "string"
									},
									"_xsi:type": "ns61:ExtendedAttributesInfo"
								}
							],
							"_xmlns:ns61": "https://integration.digitalriver.com/Common/1.0",
							"_xsi:type": "ns61:ExtendedAttributesInfoArray"
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
								"_xsi:type": "xsd:string",
								"__text": "XXXXX-XXXXX-XXXXX-XXXXX"
							},
							"_xsi:type": "ns62:LineItemDigitalInfo"
						},
						"_xmlns:ns62": "https://integration.digitalriver.com/commonRequisition/1.0",
						"_xsi:type": "ns62:LineItemDigitalInfoArray"
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
								"__text": "Eden \nPrairie"
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
								"__text": "John"
							},
							"name2": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"__text": "Doe"
							},
							"phoneNumber": {
								"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
								"_xsi:type": "xsd:string",
								"__text": "612-111-2222"
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
								"__text": "johndoe@yahoo.com"
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
								"_xsi:type": "ns63:ExtendedAttributesInfoArray",
								"_xsi:nil": "true"
							},
							"_xmlns:ns63": "https://integration.digitalriver.com/Common/1.0",
							"_xsi:type": "ns63:AddressInfo"
						},
						"shippingMethodName": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string"
						},
						"carrierName": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "United Parcel Service"
						},
						"shipmentDate": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:date",
							"__text": "2005-12-21"
						},
						"isReship": {
							"_xmlns:soapenc": "https://schemas.xmlsoap.org/soap/encoding/",
							"_xsi:type": "soapenc:boolean",
							"_xsi:nil": "true"
						},
						"fulfillerID": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "ca"
						},
						"fulfillerName": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "Computer Associates International, Inc. Master"
						},
						"_xsi:type": "ns1:ShipmentInfo"
					},
					"returnInfo": {
						"returnType": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "LineItemLevelReturnProduct"
						},
						"returnReason": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "WRONG_PRODUCT"
						},
						"returnDate": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:date",
							"__text": "2005-12-19"
						},
						"serialNumber": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string"
						},
						"returnID": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "3095009"
						},
						"returnLineItemID": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "3829909"
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
							"_xmlns:ns64": "https://integration.digitalriver.com/Common/1.0",
							"_xsi:type": "ns64:MoneyInfo"
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
							"_xmlns:ns65": "https://integration.digitalriver.com/Common/1.0",
							"_xsi:type": "ns65:MoneyInfo"
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
							"_xmlns:ns66": "https://integration.digitalriver.com/Common/1.0",
							"_xsi:type": "ns66:MoneyInfo"
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
								"__text": "-59.49"
							},
							"_xmlns:ns67": "https://integration.digitalriver.com/Common/1.0",
							"_xsi:type": "ns67:MoneyInfo"
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
							"_xmlns:ns68": "https://integration.digitalriver.com/Common/1.0",
							"_xsi:type": "ns68:MoneyInfo"
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
							"_xmlns:ns69": "https://integration.digitalriver.com/Common/1.0",
							"_xsi:type": "ns69:MoneyInfo"
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
							"_xmlns:ns70": "https://integration.digitalriver.com/Common/1.0",
							"_xsi:type": "ns70:MoneyInfo"
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
							"_xmlns:ns71": "https://integration.digitalriver.com/Common/1.0",
							"_xsi:type": "ns71:MoneyInfo"
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
							"_xmlns:ns72": "https://integration.digitalriver.com/Common/1.0",
							"_xsi:type": "ns72:MoneyInfo"
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
							"_xmlns:ns73": "https://integration.digitalriver.com/Common/1.0",
							"_xsi:type": "ns73:MoneyInfo"
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
							"_xmlns:ns74": "https://integration.digitalriver.com/Common/1.0",
							"_xsi:type": "ns74:MoneyInfo"
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
							"_xmlns:ns76": "https://integration.digitalriver.com/Common/1.0",
							"_xsi:type": "ns76:MoneyInfo"
						},
						"calculatedTaxAmountCountry": {
							"_xmlns:ns77": "https://integration.digitalriver.com/Common/1.0",
							"_xsi:type": "ns77:MoneyInfo",
							"_xsi:nil": "true"
						},
						"calculatedTaxAmountTerritory": {
							"_xmlns:ns78": "https://integration.digitalriver.com/Common/1.0",
							"_xsi:type": "ns78:MoneyInfo",
							"_xsi:nil": "true"
						},
						"calculatedTaxAmountState": {
							"_xmlns:ns79": "https://integration.digitalriver.com/Common/1.0",
							"_xsi:type": "ns79:MoneyInfo",
							"_xsi:nil": "true"
						},
						"calculatedTaxAmountCounty": {
							"_xmlns:ns80": "https://integration.digitalriver.com/Common/1.0",
							"_xsi:type": "ns80:MoneyInfo",
							"_xsi:nil": "true"
						},
						"calculatedTaxAmountCity": {
							"_xmlns:ns81": "https://integration.digitalriver.com/Common/1.0",
							"_xsi:type": "ns81:MoneyInfo",
							"_xsi:nil": "true"
						},
						"calculatedTaxAmountSecState": {
							"_xmlns:ns82": "https://integration.digitalriver.com/Common/1.0",
							"_xsi:type": "ns82:MoneyInfo",
							"_xsi:nil": "true"
						},
						"calculatedTaxAmountSecCounty": {
							"_xmlns:ns83": "https://integration.digitalriver.com/Common/1.0",
							"_xsi:type": "ns83:MoneyInfo",
							"_xsi:nil": "true"
						},
						"calculatedTaxAmountSecCity": {
							"_xmlns:ns84": "https://integration.digitalriver.com/Common/1.0",
							"_xsi:type": "ns84:MoneyInfo",
							"_xsi:nil": "true"
						},
						"calculatedTaxAmountDistrict": {
							"_xmlns:ns85": "https://integration.digitalriver.com/Common/1.0",
							"_xsi:type": "ns85:MoneyInfo",
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
						"_xmlns:ns75": "https://integration.digitalriver.com/commonRequisition/1.0",
						"_xsi:type": "ns75:LineItemTaxListInfo"
					},
					"offerID": {
						"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string"
					},
					"extendedAttributes": {
						"item": [
							{
								"name": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:string",
									"__text": "KEYRESPRETURNCODE"
								},
								"value": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:string",
									"__text": "0"
								},
								"valueDataType": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:string",
									"__text": "string"
								},
								"_xsi:type": "ns86:ExtendedAttributesInfo"
							},
							{
								"name": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:string",
									"__text": "companyProgramID"
								},
								"value": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:string",
									"__text": "15202"
								},
								"valueDataType": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:string",
									"__text": "string"
								},
								"_xsi:type": "ns86:ExtendedAttributesInfo"
							},
							{
								"name": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:string",
									"__text": "CustomerNumber1"
								},
								"value": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:string",
									"__text": "003777B2EE"
								},
								"valueDataType": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:string",
									"__text": "string"
								},
								"_xsi:type": "ns86:ExtendedAttributesInfo"
							},
							{
								"name": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:string",
									"__text": "expirationDate"
								},
								"value": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:string",
									"__text": "12/15/2006 11:46:08 AM"
								},
								"valueDataType": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:string",
									"__text": "string"
								},
								"_xsi:type": "ns86:ExtendedAttributesInfo"
							},
							{
								"name": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:string",
									"__text": "verificationString"
								},
								"value": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:string",
									"__text": "4bf6e8fdf7d9da92e84a054b545ee359"
								},
								"valueDataType": {
									"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
									"_xsi:type": "xsd:string",
									"__text": "string"
								},
								"_xsi:type": "ns86:ExtendedAttributesInfo"
							}
						],
						"_xmlns:ns86": "https://integration.digitalriver.com/Common/1.0",
						"_xsi:type": "ns86:ExtendedAttributesInfoArray"
					},
					"_xsi:type": "ns1:LineItemInfo"
				},
				"_xsi:type": "ns1:LineItemInfoArray"
			},
			"offerID": {
				"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
				"_xsi:type": "xsd:string",
				"__text": "15111009"
			},
			"programID": {
				"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
				"_xsi:type": "xsd:string"
			},
			"customerID": {
				"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
				"_xsi:type": "xsd:string",
				"__text": "10399705709"
			},
			"loginID": {
				"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
				"_xsi:type": "xsd:string",
				"__text": "johndoe@yahoo.com"
			},
			"optIn": {
				"_xmlns:soapenc": "https://schemas.xmlsoap.org/soap/encoding/",
				"_xsi:type": "soapenc:boolean",
				"__text": "false"
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
				"item": [
					{
						"name": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "EndUserCity"
						},
						"value": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "Eden Prairie"
						},
						"valueDataType": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "string"
						},
						"_xsi:type": "ns87:ExtendedAttributesInfo"
					},
					{
						"name": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "EndUserEmail"
						},
						"value": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "johndoe@yahoo.com"
						},
						"valueDataType": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "string"
						},
						"_xsi:type": "ns87:ExtendedAttributesInfo"
					},
					{
						"name": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "EndUserAddress2"
						},
						"value": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string"
						},
						"valueDataType": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "string"
						},
						"_xsi:type": "ns87:ExtendedAttributesInfo"
					},
					{
						"name": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "EndUserCountry"
						},
						"value": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "US"
						},
						"valueDataType": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "string"
						},
						"_xsi:type": "ns87:ExtendedAttributesInfo"
					},
					{
						"name": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "EndUserPwd"
						},
						"value": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "asdf1234"
						},
						"valueDataType": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "string"
						},
						"_xsi:type": "ns87:ExtendedAttributesInfo"
					},
					{
						"name": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "TechnicianID"
						},
						"value": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "AN3693GE00"
						},
						"valueDataType": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "string"
						},
						"_xsi:type": "ns87:ExtendedAttributesInfo"
					},
					{
						"name": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "EndUserZipCode"
						},
						"value": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "77041"
						},
						"valueDataType": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "string"
						},
						"_xsi:type": "ns87:ExtendedAttributesInfo"
					},
					{
						"name": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "FranchiseID"
						},
						"value": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "GE5461GE00"
						},
						"valueDataType": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "string"
						},
						"_xsi:type": "ns87:ExtendedAttributesInfo"
					},
					{
						"name": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "EndUserFName"
						},
						"value": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "John"
						},
						"valueDataType": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "string"
						},
						"_xsi:type": "ns87:ExtendedAttributesInfo"
					},
					{
						"name": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "EndUserState"
						},
						"value": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "TX"
						},
						"valueDataType": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "string"
						},
						"_xsi:type": "ns87:ExtendedAttributesInfo"
					},
					{
						"name": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "EndUserLName"
						},
						"value": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "Doe"
						},
						"valueDataType": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "string"
						},
						"_xsi:type": "ns87:ExtendedAttributesInfo"
					},
					{
						"name": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "EndUserAddress1"
						},
						"value": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "1234 Happy Lane"
						},
						"valueDataType": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "string"
						},
						"_xsi:type": "ns87:ExtendedAttributesInfo"
					},
					{
						"name": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "EndUserCompName"
						},
						"value": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "Homeuse"
						},
						"valueDataType": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "string"
						},
						"_xsi:type": "ns87:ExtendedAttributesInfo"
					},
					{
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
						"_xsi:type": "ns87:ExtendedAttributesInfo"
					},
					{
						"name": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "EndUserPhone"
						},
						"value": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "612-111-2222"
						},
						"valueDataType": {
							"_xmlns:xsd": "https://www.w3.org/2001/XMLSchema",
							"_xsi:type": "xsd:string",
							"__text": "string"
						},
						"_xsi:type": "ns87:ExtendedAttributesInfo"
					}
				],
				"_xmlns:ns87": "https://integration.digitalriver.com/Common/1.0",
				"_xsi:type": "ns87:ExtendedAttributesInfoArray"
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
