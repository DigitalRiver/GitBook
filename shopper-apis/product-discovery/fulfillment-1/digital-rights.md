---
description: Understand how Digital Rights work.
---

# Digital rights

Digital Rights refer to the rights or permissions granted to a shopper by the publisher or manufacturer to use or access a software application, game, system, and so forth. Digital Rights protect the sale and distribution of copyrighted works. Use Digital Rights to enable and manage the serial numbers and unlock codes that control access to software and other digital products.

The types of custom integrations for Digital Rights are as follows:

* Key Request
* Key Revocation

Digital Rights is an outbound event.

You can create keys and then associate them with products to deliver and manage Digital Rights. You can create as many keys as needed to satisfy your Digital Rights requirements.

When a shopper buys a product that has Digital rights, they get a key (serial number or unlock code) that they can use to access the product.

## Response details for a successful scenario

A successful Digital Rights request results in a response that contains a non-null, non-empty `<key>` element.

Note that the `<item>` element is unbounded. That means you can send multiple keys in response (in response to the `<quantity>` element in this `<getKeyRequest>`).

In a successful scenario such as this, the `<returnCode>`, `<isAutoRetryiable>`, and `<returnMessage>` elements are ignored. These elements come into play in an unsuccessful scenario.

## Response details for an unsuccessful scenario

An unsuccessful response occurs when the `<key>` element is missing or empty. In this situation, Digital River will try to fix the issue causing the non-successful response by using the `<returnCode>`, `<isAutoRetriable>`, and `<returnMessage>` elements and try again.

If the `<isAutoRetriable>` flag is set to false, the `<returnCode>` element must contain a non-0 response. Also, the `<returnMessage>` element should explain what the value in `<returnCode>` means and contain an explanation of what is wrong with the request and, if possible, how to fix it.

When an unsuccessful Digital Rights response occurs:

* The consumer is not charged for the line item until the consumer receives a serial number, unlock code, or download URL.
* The line item goes into a "failed digital rights" state. When this happens, the line item appears on the globalCommerce Integration Exception screen.
* Using the details provided in the `<returnMessage>` element, you can use the globalCommerce Integration Exception screen to fix the issue and resubmit the line item.

If the `<isAutoRetriable>` element is set to true, Digital River automatically retries the request every hour for 21 days. If there is no action after 21 days, the system "forgets" the order.

When you receive an unsuccessful response or experience communication issues (such as failed transports), the shopping process behaves as follows:

* The consumer does not receive the Digital Right (serial number, unlock code, or download URL). Instead, the consumer is instructed to wait for an email that will contain the Digital Right.
* When the Digital Right is fulfilled, the consumer will receive the email.
* The consumer is charged until the Digital Right is fulfilled.

{% tabs %}
{% tab title="Payload" %}
{% code overflow="wrap" %}
```json
{
	"GetKeyRequest": {
		"orderID": {
			"_xmlns:xsi": "https://www.w3.org/2001/XMLSchema-instance",
			"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
			"_xsi:type": "xsd:string",
			"__text": "123456789"
		},
		"submissionDate": {
			"_xmlns:xsi": "http://www.w3.org/2001/XMLSchema-instance",
			"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
			"_xsi:type": "xsd:dateTime",
			"__text": "2014-09-24T15:50:12.252Z"
		},
		"orderExternalReferenceID": {
			"_xmlns:xsi": "http://www.w3.org/2001/XMLSchema-instance",
			"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
			"_xsi:type": "xsd:string",
			"_xsi:nil": "true"
		},
		"orderLineItemID": {
			"_xmlns:xsi": "http://www.w3.org/2001/XMLSchema-instance",
			"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
			"_xsi:type": "xsd:string",
			"__text": "213456789"
		},
		"quantity": {
			"_xmlns:xsi": "http://www.w3.org/2001/XMLSchema-instance",
			"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
			"_xsi:type": "xsd:int",
			"__text": "1"
		},
		"preOrder": {
			"_xmlns:xsi": "http://www.w3.org/2001/XMLSchema-instance",
			"_xmlns:soapenc": "http://schemas.xmlsoap.org/soap/encoding/",
			"_xsi:type": "soapenc:boolean",
			"__text": "false"
		},
		"productKey": {
			"productID": {
				"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
				"_xsi:type": "xsd:string",
				"__text": "312456789"
			},
			"externalReferenceID": {
				"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
				"_xsi:type": "xsd:string",
				"__text": "4123456789"
			},
			"companyID": {
				"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
				"_xsi:type": "xsd:string",
				"__text": "companyID"
			},
			"locale": {
				"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
				"_xsi:type": "xsd:string",
				"__text": "en_US"
			},
			"_xmlns:xsi": "http://www.w3.org/2001/XMLSchema-instance",
			"_xmlns:ns2": "http://integration.digitalriver.com/Common/1.0",
			"_xsi:type": "ns2:ProductKey"
		},
		"userKey": {
			"userID": {
				"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
				"_xsi:type": "xsd:string",
				"__text": "512346789"
			},
			"externalReferenceID": "2269079261",
			"companyID": {
				"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
				"_xsi:type": "xsd:string",
				"__text": "companyID"
			},
			"loginID": {
				"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
				"_xsi:type": "xsd:string",
				"__text": "test@example.com"
			},
			"siteID": {
				"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
				"_xsi:type": "xsd:string",
				"__text": "siteID"
			},
			"_xmlns:xsi": "http://www.w3.org/2001/XMLSchema-instance",
			"_xmlns:ns3": "http://integration.digitalriver.com/Common/1.0",
			"_xsi:type": "ns3:UserKey"
		},
		"billingAddress": {
			"addressID": {
				"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
				"_xsi:type": "xsd:string",
				"__text": "612345789"
			},
			"city": {
				"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
				"_xsi:type": "xsd:string",
				"__text": "City"
			},
			"countryA2": {
				"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
				"_xsi:type": "xsd:string",
				"_xsi:nil": "true"
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
				"__text": "123 Example Street"
			},
			"line2": {
				"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
				"_xsi:type": "xsd:string",
				"_xsi:nil": "true"
			},
			"line3": {
				"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
				"_xsi:type": "xsd:string",
				"_xsi:nil": "true"
			},
			"locationCode": {
				"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
				"_xsi:type": "xsd:string",
				"_xsi:nil": "true"
			},
			"name1": {
				"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
				"_xsi:type": "xsd:string",
				"__text": "FirstName"
			},
			"name2": {
				"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
				"_xsi:type": "xsd:string",
				"__text": "LastName"
			},
			"phoneNumber": {
				"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
				"_xsi:type": "xsd:string",
				"__text": "(123) 456-7890"
			},
			"postalCode": {
				"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
				"_xsi:type": "xsd:string",
				"__text": "12345"
			},
			"state": {
				"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
				"_xsi:type": "xsd:string",
				"__text": "MN"
			},
			"email": {
				"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
				"_xsi:type": "xsd:string",
				"__text": "test2@email.com"
			},
			"faxPhone": {
				"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
				"_xsi:type": "xsd:string",
				"_xsi:nil": "true"
			},
			"companyName": {
				"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
				"_xsi:type": "xsd:string",
				"__text": "Company Name"
			},
			"phoneNumber2": {
				"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
				"_xsi:type": "xsd:string",
				"_xsi:nil": "true"
			},
			"countyName": {
				"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
				"_xsi:type": "xsd:string",
				"_xsi:nil": "true"
			},
			"extendedAttributes": {
				"item": {
					"name": {
						"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "ExtendedAttributeName"
					},
					"value": {
						"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "value"
					},
					"valueDataType": {
						"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "string"
					},
					"_xsi:type": "ns4:ExtendedAttributesInfo"
				},
				"_xsi:type": "ns4:ExtendedAttributesInfoArray"
			},
			"_xmlns:xsi": "http://www.w3.org/2001/XMLSchema-instance",
			"_xmlns:ns4": "http://integration.digitalriver.com/Common/1.0",
			"_xsi:type": "ns4:AddressInfo"
		},
		"shippingAddress": {
			"addressID": {
				"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
				"_xsi:type": "xsd:string",
				"__text": "612345789"
			},
			"city": {
				"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
				"_xsi:type": "xsd:string",
				"__text": "City"
			},
			"countryA2": {
				"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
				"_xsi:type": "xsd:string",
				"_xsi:nil": "true"
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
				"__text": "123 Example Street"
			},
			"line2": {
				"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
				"_xsi:type": "xsd:string",
				"_xsi:nil": "true"
			},
			"line3": {
				"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
				"_xsi:type": "xsd:string",
				"_xsi:nil": "true"
			},
			"locationCode": {
				"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
				"_xsi:type": "xsd:string",
				"_xsi:nil": "true"
			},
			"name1": {
				"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
				"_xsi:type": "xsd:string",
				"__text": "FirstName"
			},
			"name2": {
				"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
				"_xsi:type": "xsd:string",
				"__text": "LastName"
			},
			"phoneNumber": {
				"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
				"_xsi:type": "xsd:string",
				"__text": "(123) 456-7890"
			},
			"postalCode": {
				"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
				"_xsi:type": "xsd:string",
				"__text": "12345"
			},
			"state": {
				"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
				"_xsi:type": "xsd:string",
				"__text": "MN"
			},
			"email": {
				"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
				"_xsi:type": "xsd:string",
				"__text": "test2@email.com"
			},
			"faxPhone": {
				"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
				"_xsi:type": "xsd:string",
				"_xsi:nil": "true"
			},
			"companyName": {
				"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
				"_xsi:type": "xsd:string",
				"__text": "Company Name"
			},
			"phoneNumber2": {
				"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
				"_xsi:type": "xsd:string",
				"_xsi:nil": "true"
			},
			"countyName": {
				"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
				"_xsi:type": "xsd:string",
				"_xsi:nil": "true"
			},
			"extendedAttributes": {
				"_xsi:type": "ns5:ExtendedAttributesInfoArray"
			},
			"_xmlns:xsi": "http://www.w3.org/2001/XMLSchema-instance",
			"_xmlns:ns5": "http://integration.digitalriver.com/Common/1.0",
			"_xsi:type": "ns5:AddressInfo"
		},
		"extendedAttributes": {
			"item": {
				"name": {
					"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
					"_xsi:type": "xsd:string",
					"__text": "ExtendedAttributeName"
				},
				"value": {
					"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
					"_xsi:type": "xsd:string",
					"__text": "value"
				},
				"valueDataType": {
					"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
					"_xsi:type": "xsd:string",
					"__text": "string"
				},
				"_xsi:type": "ns6:ExtendedAttributesInfo"
			},
			"_xmlns:xsi": "http://www.w3.org/2001/XMLSchema-instance",
			"_xmlns:ns6": "http://integration.digitalriver.com/Common/1.0",
			"_xsi:type": "ns6:ExtendedAttributesInfoArray"
		},
		"orderPricing": {
			"total": {
				"currencyCode": {
					"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
					"_xsi:type": "xsd:string",
					"__text": "USD"
				},
				"amount": {
					"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
					"_xsi:type": "xsd:decimal",
					"__text": "11.11"
				},
				"_xmlns:ns8": "http://integration.digitalriver.com/Common/1.0",
				"_xsi:type": "ns8:MoneyInfo"
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
					"__text": "11.11"
				},
				"_xmlns:ns9": "http://integration.digitalriver.com/Common/1.0",
				"_xsi:type": "ns9:MoneyInfo"
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
				"_xmlns:ns10": "http://integration.digitalriver.com/Common/1.0",
				"_xsi:type": "ns10:MoneyInfo"
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
				"_xmlns:ns13": "http://integration.digitalriver.com/Common/1.0",
				"_xsi:type": "ns13:MoneyInfo"
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
				"_xmlns:ns14": "http://integration.digitalriver.com/Common/1.0",
				"_xsi:type": "ns14:MoneyInfo"
			},
			"shippingIncentive": {
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
				"_xmlns:ns15": "http://integration.digitalriver.com/Common/1.0",
				"_xsi:type": "ns15:MoneyInfo"
			},
			"nonTaxableFees": {
				"_xmlns:ns16": "http://integration.digitalriver.com/Common/1.0",
				"_xsi:type": "ns16:MoneyInfo",
				"_xsi:nil": "true"
			},
			"taxableFees": {
				"_xmlns:ns17": "http://integration.digitalriver.com/Common/1.0",
				"_xsi:type": "ns17:MoneyInfo",
				"_xsi:nil": "true"
			},
			"taxOnTaxableFees": {
				"_xmlns:ns18": "http://integration.digitalriver.com/Common/1.0",
				"_xsi:type": "ns18:MoneyInfo",
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
				"_xmlns:ns19": "http://integration.digitalriver.com/Common/1.0",
				"_xsi:type": "ns19:MoneyInfo"
			},
			"_xmlns:xsi": "http://www.w3.org/2001/XMLSchema-instance",
			"_xmlns:ns7": "http://integration.digitalriver.com/commonRequisition/1.0",
			"_xsi:type": "ns7:OrderPriceInfo"
		},
		"lineItemPricing": {
			"unitPrice": {
				"currencyCode": {
					"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
					"_xsi:type": "xsd:string",
					"__text": "USD"
				},
				"amount": {
					"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
					"_xsi:type": "xsd:decimal",
					"__text": "11.11"
				},
				"_xmlns:ns21": "http://integration.digitalriver.com/Common/1.0",
				"_xsi:type": "ns21:MoneyInfo"
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
					"__text": "11.11"
				},
				"_xmlns:ns22": "http://integration.digitalriver.com/Common/1.0",
				"_xsi:type": "ns22:MoneyInfo"
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
					"__text": "11.11"
				},
				"_xmlns:ns24": "http://integration.digitalriver.com/Common/1.0",
				"_xsi:type": "ns24:MoneyInfo"
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
				"_xmlns:ns25": "http://integration.digitalriver.com/Common/1.0",
				"_xsi:type": "ns25:MoneyInfo"
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
				"_xmlns:ns28": "http://integration.digitalriver.com/Common/1.0",
				"_xsi:type": "ns28:MoneyInfo"
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
					"__text": "0.00"
				},
				"_xmlns:ns29": "http://integration.digitalriver.com/Common/1.0",
				"_xsi:type": "ns29:MoneyInfo"
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
				"_xmlns:ns30": "http://integration.digitalriver.com/Common/1.0",
				"_xsi:type": "ns30:MoneyInfo"
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
					"__text": "0.00"
				},
				"_xmlns:ns31": "http://integration.digitalriver.com/Common/1.0",
				"_xsi:type": "ns31:MoneyInfo"
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
					"__text": "0.00"
				},
				"_xmlns:ns32": "http://integration.digitalriver.com/Common/1.0",
				"_xsi:type": "ns32:MoneyInfo"
			},
			"taxableFees": {
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
				"_xmlns:ns33": "http://integration.digitalriver.com/Common/1.0",
				"_xsi:type": "ns33:MoneyInfo"
			},
			"taxOnTaxableFees": {
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
				"_xmlns:ns34": "http://integration.digitalriver.com/Common/1.0",
				"_xsi:type": "ns34:MoneyInfo"
			},
			"nonTaxableFees": {
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
				"_xmlns:ns35": "http://integration.digitalriver.com/Common/1.0",
				"_xsi:type": "ns35:MoneyInfo"
			},
			"recurringFee": {
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
				"_xmlns:ns36": "http://integration.digitalriver.com/Common/1.0",
				"_xsi:type": "ns36:MoneyInfo"
			},
			"shippingBeforeDiscount": {
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
				"_xmlns:ns37": "http://integration.digitalriver.com/Common/1.0",
				"_xsi:type": "ns37:MoneyInfo"
			},
			"_xmlns:xsi": "http://www.w3.org/2001/XMLSchema-instance",
			"_xmlns:ns20": "http://integration.digitalriver.com/commonRequisition/1.0",
			"_xsi:type": "ns20:LineItemPriceInfo"
		},
		"productAttributes": {
			"item": {
				"name": {
					"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
					"_xsi:type": "xsd:string",
					"__text": "ExtendedAttributeName"
				},
				"value": {
					"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
					"_xsi:type": "xsd:string",
					"__text": "value"
				},
				"valueDataType": {
					"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
					"_xsi:type": "xsd:string",
					"__text": "string"
				},
				"_xsi:type": "ns38:ExtendedAttributesInfo"
			},
			"_xmlns:xsi": "http://www.w3.org/2001/XMLSchema-instance",
			"_xmlns:ns38": "http://integration.digitalriver.com/Common/1.0",
			"_xsi:type": "ns38:ExtendedAttributesInfoArray"
		},
		"_xmlns:ns1": "http://integration.digitalriver.com/DigitalRight/1.0",
		"__prefix": "ns1"
	}
}
```
{% endcode %}
{% endtab %}

{% tab title="Successful response" %}
{% code overflow="wrap" %}
```json
{
	"getKeyResponse": {
		"key": {
			"item": {
				"key": "ABC123",
				"keyType": "SERIAL_NUMBER"
			}
		}
	}
}
```
{% endcode %}
{% endtab %}

{% tab title="Unsuccessful response" %}
{% code overflow="wrap" %}
```json
{
	"getKeyResponse": {
		"returnCode": "1",
		"isAutoRetriable": "false",
		"returnMessage": "Unrecognized orderExternalReferenceID - \nplease supply correct value"
	}
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Key request

The Digital Right process is a request/response-based process used for retrieving external digital rights. The process requests a serial number or an unlock code when a purchase occurs. A key request integration sends a request for a key (serial number of unlock code) when a shopper purchases a product set up to use the integration.

![Get key request](https://files.readme.io/48e67d5-Digital\_Rights.png)

* **Notification**—Global Commerce generates a Get Key Request and sends the request to your endpoint.
* **Required Response to Notification**—Your endpoint must synchronously respond with a Get Key Response.

## Schemas

| Version      | Schema Component Table                                                                | Raw Schema                                                                | Sample XML                                                                        |
| ------------ | ------------------------------------------------------------------------------------- | ------------------------------------------------------------------------- | --------------------------------------------------------------------------------- |
| 10 (Current) | [View](https://drhadmin.digitalriver.com/integration/isg/schematable/DigitalRight/10) | [View](https://drhadmin.digitalriver.com/integration/xsd/DigitalRight/10) | [View](https://drhadmin.digitalriver.com/integration/isg/example/DigitalRight/10) |
| 9            | [View](https://drhadmin.digitalriver.com/integration/isg/schematable/DigitalRight/9)  | [View](https://drhadmin.digitalriver.com/integration/xsd/DigitalRight/9)  | [View](https://drhadmin.digitalriver.com/integration/isg/example/DigitalRight/9)  |
| 8            | [View](https://drhadmin.digitalriver.com/integration/isg/schematable/DigitalRight/8)  | [View](https://drhadmin.digitalriver.com/integration/xsd/DigitalRight/8)  | [View](https://drhadmin.digitalriver.com/integration/isg/example/DigitalRight/8)  |
