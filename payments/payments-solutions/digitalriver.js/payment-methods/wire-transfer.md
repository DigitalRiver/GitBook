---
description: >-
  Wire Transfer is an offline payment method where a consumer goes to their bank
  to send the money.
---

# Wire Transfer

When using this payment method, a customer must provide their bank with transfer information provided by the merchant to complete the payment. The transfer details consist of the account holder, bank name, city, country description, payment reference, bank account number, additional bank information, and the international bank account number (IBAN).

## Configuring Wire Transfer for DigitalRiver.js

Create a Wire Transfer payment method for your app or website in four easy steps:

* [Step 1: Build a Wire Transfer Source Request object](wire-transfer.md#step-1-build-a-wire-transfer-source-request-object)
* [Step 2: Create a Wire Transfer source using DigitalRiver.js](wire-transfer.md#step-2-create-a-wire-transfer-source-using-digitalriver-js)
* [Step 3: Use the authorized source](wire-transfer.md#step-3-use-the-authorized-source)
* [Step 4: Direct your customer to go to their banking institution](wire-transfer.md#step-4-direct-your-customer-to-go-to-their-banking-institution)

### Step 1: Build a Wire Transfer source request object

Build a Wire Transfer Source Request object. A Wire Transfer Source Request object requires the following fields.

| Field          | Value                                                      |
| -------------- | ---------------------------------------------------------- |
| `type`         | `wireTransfer`                                             |
| `sessionId`    | The payment session identifier.                            |
| `owner`        | An [Owner object](common-payment-objects.md#owner-object). |
| `wireTransfer` | A Wire Transfer object. (This is currently empty)          |

### Step 2: Create a Wire Transfer source using DigitalRiver.js

Use the DigitalRiver.js library to create and mount elements to the HTML container.

{% hint style="info" %}
The `address` object must contain postal code and state/province data that **** [adheres to a standardized format](../../../../cart/creating-or-updating-a-cart/providing-address-information.md) using the `state` attribute. Note that the `state` attribute listed below corresponds to the `countrySubdivision` attribute used when providing address information. The payment session manages the correct field name on the backend.
{% endhint %}

```javascript
var data = {
    "type": "wireTransfer",
    "sessionId": "ea03bf6f-84ef-4993-b1e7-b7d5ecf71d1f",
    "owner": {
        "firstName": "John",
        "lastName": "Doe",
        "email": "john.doe@gmail.com",
        "phoneNumber": "1555000000",
        "address": {
            "line1": "123 Main Street",
            "line2": "",
            "city": "Minnetonka",
            "state": "MN",
            "postalCode": "55343",
            "country": "US"
        }
    },
    "wireTransfer": {
    }
}

digitalriver.createSource(data).then(function(result) {
    if (result.error) {
        //handle errors
    } else {
        var source = result.source;
        //send source to back end
        sendToBackend(source);
    }
});
```

#### Wire Transfer Source response example

{% tabs %}
{% tab title="Source response" %}
```javascript
{
    "clientId": "gc",
    "channelId": "drdod15",
    "liveMode": false,
    "id": "14381d1c-8bff-4350-aeea-82b36f3a196c",
    "sessionId": "ea03bf6f-84ef-4993-b1e7-b7d5ecf71d1f",    
    "clientSecret": "14381d1c-8bff-4350-aeea-82b36f3a196c_14381d1sdfsdfc-8bff-4350-aeea-82b36f3a196c",
    "type": "wireTransfer",
    "reusable": false,
    "owner": {
        "firstName": "John",
        "lastName": "Doe",
        "email": "john.doe@gmail.com",
        "phoneNumber": "1555000000",
        "address": {
            "line1": "123 Main Street",
            "line2": "",
            "city": "Minnetonka",
            "state": "MN",
            "country": "US",
            "postalCode": "55343"
        }
    },
    "amount": "100.00",
    "currency": "USD",
    "state": "pending_funds",
    "creationIp": "209.87.178.4",
    "createdTime": "2019-05-22T01:52:40.965Z",
    "updatedTime": "2019-05-22T01:52:40.965Z",
    "flow": "receiver",
    "wireTransfer": {
        "accountHolder": "Netgiro Payments AB",
        "bankName": "ABN AMRO Bank N.V.",
        "city": "Prague",
        "country": "ES",
        "referenceId": "DR1651067521",
        "accountNumber": "0100037259",
        "additionalBankInformation": "Codigo de oficina: 0001 Codigo de entidad: 0156 Digitos de control: 09",
        "iban": "ES35 0156 0001 0901 0003 7259"
    }
}
```
{% endtab %}
{% endtabs %}

### Step 3: Use the authorized source

Once authorized, you can use the source by [attaching it to a cart](../../../sources/#attaching-a-payment-method-to-an-order-or-cart).

{% tabs %}
{% tab title="POST /v1/shoppers/me/carts/active/apply-payment-method" %}
```javascript
{
  "paymentMethod": {
    "sourceId": "e7ba0595-059c-460c-bad8-2812123b9313"
  }
}
```
{% endtab %}
{% endtabs %}

### Step 4: Direct your customer to go to their banking institution

Once the customer submits the order, the source remains in the `pending_funds` state. Direct your customer to go to their banking institution to wire the money to the account details listed in the `wireTransfer` block of your source.&#x20;

{% tabs %}
{% tab title="Source response" %}
```javascript
{
	"source": {
		"clientId": "gc",
		"channelId": "paylive",
		"liveMode": false,
		"id": "f51a7ac8-4d97-4579-bc38-1db3abe01cf5",
    "sessionId": "ea03bf6f-84ef-4993-b1e7-b7d5ecf71d1f",		
		"clientSecret": "f51a7ac8-4d97-4579-bc38-1db3abe01cf5_a654d22d-cdb3-4ad2-9f00-7b316cab6595",
		"type": "wireTransfer",
		"reusable": false,
		"owner": {
			"firstName": "John",
			"lastName": "Doe",
			"email": "john.doe@gmail.com",
			"phoneNumber": "1555000000",
			"address": {
				"line1": "123 Main Street",
				"line2": "",
				"city": "Minnetonka",
				"state": "MN",
				"country": "US",
				"postalCode": "55343"
			}
		},
		"paymentId": "b95cce28-f7bf-4818-a305-9382745d1f2b",
		"amount": "468.94",
		"currency": "USD",
		"state": "pending_funds",
		"upstreamId": "805335310080",
		"creationIp": "75.73.13.76",
		"createdTime": "2020-12-30T20:35:08.61Z",
		"updatedTime": "2020-12-30T20:35:08.746Z",
		"expirationTime": "2021-01-29T20:35:08.61Z",
		"flow": "receiver",
		"browserInfo": {
			"userAgent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/87.0.4280.88 Safari/537.36",
			"acceptHeader": "application/json, text/plain, */*",
			"language": "en-US",
			"colorDepth": 24,
			"screenHeight": 960,
			"screenWidth": 1707,
			"timeZoneOffset": 360,
			"javaEnabled": false,
			"browserIp": "75.73.13.76",
			"referrer": "https://js.digitalriverws.com/v1/components/controller/controller.html?componentId=controller-89303efc-de83-41b7-a892-c6c631c2ff49"
		},
		"wireTransfer": {
			"accountHolder": "Global Collect BV",
			"bankName": "Rabobank N.A.",
			"city": "Ontario USA",
			"country": "United States",
			"referenceId": "890703719099",
			"accountNumber": "0487369908",
			"additionalBankInformation": "ABA|122238420||Address|WESTLAKE VILLAGE, 2663 TOWNSGATE RD",
			"swiftCode": "RABOUS66XXX"
		}
	},
	"readyForStorage": false
```
{% endtab %}
{% endtabs %}

## Supported markets

For information on supported markets and currencies for Drop-in and DigitalRiver.js, go to:&#x20;

* **Payment Method Guide:** [digitalriver.com/payment-method-guide](https://www.digitalriver.com/payment-method-guide/)
* **Country Guide:** [digitalriver.com/country-guide/](https://www.digitalriver.com/country-guide/)
