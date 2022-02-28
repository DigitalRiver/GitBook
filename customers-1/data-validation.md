---
description: Understand the Data Validation service.
---

# Data validation

The Data Validation service process is a request/response-based process. The Data Validation Service provides a mechanism that allows you to attach data points on a page in a Digital River store. It also validates each data point on that page against an external endpoint provided by a third-party client.

![Data Validation Service flow](https://files.readme.io/b9b0bce-Data\_Validation\_Service.png)

## Data validation details

A successful Data Validation request results in a response that contains a non-null, non-empty element. An unsuccessful Data Validation request results in an invalid `responseCode`.

#### Note

A third-party client must define the `responseCode.`

{% tabs %}
{% tab title="Request sample" %}
```java
{
	"DataValidationRequest": {
		"dataPoints": {
			"item": [
				{
					"name": {
						"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "CustomerID"
					},
					"value": {
						"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "12345"
					},
					"valueDataType": {
						"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "string"
					},
					"_xsi:type": "ns1:DataPointInfo"
				},
				{
					"name": {
						"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "SRPID"
					},
					"value": {
						"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "67890"
					},
					"valueDataType": {
						"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "string"
					},
					"_xsi:type": "ns1:DataPointInfo"
				}
			],
			"_xmlns:xsi": "http://www.w3.org/2001/XMLSchema-instance",
			"_xsi:type": "ns1:DataPointInfos"
		},
		"extendedAttributes": {
			"_xmlns:xsi": "http://www.w3.org/2001/XMLSchema-instance",
			"_xmlns:ns2": "http://integration.digitalriver.com/Common/1.0",
			"_xsi:type": "ns2:ExtendedAttributesInfoArray",
			"_xsi:nil": "true"
		},
		"_xmlns:ns1": "http://integration.digitalriver.com/DataValidationService",
		"__prefix": "ns1"
	}
}
```
{% endtab %}

{% tab title="Successful response sample" %}
```javascript
{
	"DataValidationResponse": {
		"dataPointResponses": {
			"item": [
				{
					"name": {
						"_xmlns": "",
						"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "CustomerID"
					},
					"value": {
						"_xmlns": "",
						"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "12345"
					},
					"valueDataType": {
						"_xmlns": "",
						"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "string"
					},
					"_xsi:type": "ns1:DataPointResponseInfo"
				},
				{
					"name": {
						"_xmlns": "",
						"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "SRPID"
					},
					"value": {
						"_xmlns": "",
						"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "67890"
					},
					"valueDataType": {
						"_xmlns": "",
						"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "string"
					},
					"_xsi:type": "ns1:DataPointResponseInfo"
				}
			],
			"_xmlns": "http://integration.digitalriver.com/DataValidationService",
			"_xsi:type": "ns1:DataPointResponseInfos"
		},
		"valid": {
			"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
			"_xsi:type": "xsd:boolean",
			"__text": "true"
		},
		"_xmlns:ns1": "http://integration.digitalriver.com/DataValidationService",
		"_xmlns:xsi": "http://www.w3.org/2001/XMLSchema-instance",
		"_xsi:type": "ns1:DataValidationResponse",
		"__prefix": "ns1"
	}
}
```
{% endtab %}

{% tab title="Unsuccessful response sample" %}
```javascript
{
	"DataValidationResponse": {
		"dataPointResponses": {
			"item": [
				{
					"name": {
						"_xmlns": "",
						"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "CustomerID"
					},
					"value": {
						"_xmlns": "",
						"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "12345"
					},
					"valueDataType": {
						"_xmlns": "",
						"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "string"
					},
					"_xsi:type": "ns1:DataPointResponseInfo"
				},
				{
					"name": {
						"_xmlns": "",
						"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "SRPID"
					},
					"value": {
						"_xmlns": "",
						"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "67890"
					},
					"valueDataType": {
						"_xmlns": "",
						"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
						"_xsi:type": "xsd:string",
						"__text": "string"
					},
					"_xsi:type": "ns1:DataPointResponseInfo"
				}
			],
			"_xmlns": "http://integration.digitalriver.com/DataValidationService",
			"_xsi:type": "ns1:DataPointResponseInfos"
		},
		"valid": {
			"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
			"_xsi:type": "xsd:boolean",
			"__text": "false"
		},
		"responseCode": {
			"_xmlns:xsd": "http://www.w3.org/2001/XMLSchema",
			"_xsi:type": "xsd:string",
			"__text": "DATA_VALIDATION_INVALID"
		},
		"_xmlns:ns1": "http://integration.digitalriver.com/DataValidationService",
		"_xmlns:xsi": "http://www.w3.org/2001/XMLSchema-instance",
		"_xsi:type": "ns1:DataValidationResponse",
		"__prefix": "ns1"
	}
}
```
{% endtab %}
{% endtabs %}

## Data validation schema

| Version             | Schema Components Table                                                                       | Raw Schema                                                                        | Sample XML                                                                                |
| ------------------- | --------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------- |
| Version 1 (Current) | [View](https://drhadmin.digitalriver.com/integration/isg/schematable/DataValidationService/1) | [View](https://drhadmin.digitalriver.com/integration/xsd/DataValidationService/1) | [View](https://drhadmin.digitalriver.com/integration/isg/example/DataValidationService/1) |
