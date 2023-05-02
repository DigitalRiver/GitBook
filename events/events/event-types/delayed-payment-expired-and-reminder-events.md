---
description: Understand the delayed payment expired and reminder events.
---

# Delayed payment expired and reminder events

When the order has been submitted and is awaiting payment, Digital River creates a `delayed_payment.reminder` event.&#x20;

When Digital River does not receive the delayed payment, Digital River creates a `delayed_payment.expired` event. When you receive this notification, you can choose to send the notification to the customer.

The following example shows the payloads for various payment methods.

## Boleto

{% code title="Boleto payload example" overflow="wrap" %}
```json
"boletoBancario": {
        "documentCode",
        "document"
}
```
{% endcode %}

### `documentCode`

The Boleto document code URL. This field is required for a successful request.

### `document`

The Boleto numeric identifier. The shopper can use this identifier to pay Boleto through a banking app.&#x20;

### The delayed payment reminder request

{% code title="Webhook request" overflow="wrap" %}
```json
{
  "type": "delayed_payment.reminder",
  "data": {
    "object": {
      "orderId": "1032713644439",
      "placedOnDate": "2021-11-24T16:32:07.000Z",
      "products": [
        {
          "id": "5325101400",
          "externalReferenceId": "5325101400",
          "displayName": "Acme Security software",
          "sku": "PRW-00-001-12"
        }
      ],
      "billToAddress": {
        "firstName": "Jane",
        "lastName": "Doe",
        "line1": "line1",
        "line2": "line2",
        "city": "Sao Paulo",
        "postalCode": "09320-070",
        "state": "SP",
        "country": "BR",
        "countryName": "Brasil",
        "phoneNumber": "5552253720",
        "emailAddress": "subs_test@digitalriver.com"
      },
      "shipToAddress": {
        "firstName": "Jane",
        "lastName": "Doe",
        "line1": "line1",
        "line2": "line2",
        "city": "Sao Paulo",
        "postalCode": "09320-070",
        "state": "SP",
        "country": "BR",
        "countryName": "Brazil",
        "phoneNumber": "5552253720",
        "emailAddress": "subs_test@digitalriver.com"
      },
      "shopperId": "550619489112"",
      "locale": "pt_BR",
      "siteId": "acmeco",
      "orderTotal": 99,
      "currency": "BRL",
      "orderDiscount": 0,
      "subTotal": 86.97,
      "tax": 12.03,
      "shippingTotal": 0,
      "businessEntity": "Digital River Brazil",
      "paymentSourceType": "boletoBancario",
      "boletoBancario": {
        "documentCode": "23793381286007047838725000526100688270000009900",
        "document": "{documentUrl}"
      }
    }
  },
  "clientIds": {
    "site_id": "acmebr"
  },
  "searchableData": {
    "orderId": "1032713644439"
  }
}
```
{% endcode %}

### The delayed payment expired request

{% code title="Webhook request" overflow="wrap" %}
```json
{
   "type":"delayed_payment.expired",
   "data":{
      "object":{
         "orderId":"1004717881620",
         "placedOnDate":"2022-05-31T09:14:18.000Z",
         "products":[
            {
               "id":"5530211800",
               "externalReferenceId":"900800101",
               "displayName":"PPRO E2E Digital Image",
               "sku":"900800101"
            }
         ],
         "billToAddress":{
            "firstName":"Guilherme",
            "lastName":"Miranda",
            "line1":"1000 Avenida Paulista",
            "city":"Bela Vista",
            "postalCode":"01310-100",
            "state":"SP",
            "country":"BR",
            "countryName":"Brazil",
            "phoneNumber":"5531986463859",
            "emailAddress":"guizinutesti@gmail.com"
         },
         "shipToAddress":{
            "firstName":"Guilherme",
            "lastName":"Miranda",
            "line1":"1000 Avenida Paulista",
            "city":"Bela Vista",
            "postalCode":"01310-100",
            "state":"SP",
            "country":"BR",
            "countryName":"Brazil",
            "phoneNumber":"5531986463859",
            "emailAddress":"guizinutesti@gmail.com"
         },
         "shopperId":"514650873010",
         "locale":"pt_BR",
         "siteId":"paylive",
         "orderTotal":29.94,
         "currency":"BRL",
         "orderDiscount":0.0,
         "subTotal":26.3,
         "tax":3.64,
         "shippingTotal":0.0,
         "businessEntity":"Digital River Brazil",
         "expirationDate":"2022-06-30T09:05:05.000Z",
         "expirationDays":30,
         "paymentSourceType":"boletoBancario",
         "boletoBancario":{
            "documentCode":"23793381286006844671926000526108487940000002994",
            "document":"https://meiosdepagamentobradesco.com.br/apiboleto/Bradesco?token=QjdnVkh6YUZBODhMcVJZeFUvQ2RMbVVFSHY4azhOa1JiRlRNQW9teUFkSFpaU2hLeDUxU2NqVG5taER6R3BJcQ.."
         }
      }
   },
   "clientIds":{
      "site_id":"paylive"
   },
   "searchableData":{
      "orderId":"1004717881620"
   }
}
```
{% endcode %}

## Konbini

{% code title=" Konbini payload example" overflow="wrap" %}
```json
"konbini": {
  "storeId": "010",
  "receiptNumber": "7231852091080",
  "printableInvoiceUrl": "{invoiceUrl}",
  "storeName": "Seven Eleven",
  "localizedStoreName": "セブン‐イレブン",
  "storeLogoUrl": "{storeLogoUrl}"
}
```
{% endcode %}

### `storeId`

The store identifier.

### `receiptNumber`

The Konbini receipt number.

### `printableInvoiceUrl`

The URL contains the store's invoice for the order.

### `storeName`

The store's name.

### `localizedStoreName`

The localized store name.

### `storeLogoUrl`

The URL for the store's logo.

### The delayed payment reminder request

{% code title="Webhook request" overflow="wrap" %}
```json
{
  "type": "delayed_payment.reminder",
  "data": {
    "object": {
      "orderId": "1087747290080",
      "placedOnDate": "2022-05-31T15:58:16.963Z",
      "products": [
        {
          "id": "308180500",
          "displayName": "BP Digital",
          "sku": "BP123"
        }
      ],
      "billToAddress": {
        "firstName": "Jane",
        "lastName": "Doe",
        "companyName": "DR",
        "line1": "6-chome-22 Kagurazaka",
        "line2": "Shinjuku City",
        "city": "Tokyo-to",
        "postalCode": "162-0825",
        "state": "Tokyo",
        "country": "JP",
        "countryName": "Japan",
        "phoneNumber": "555-234-56789",
        "emailAddress": "subs_test@digtialriver.com",
        "countyName": "Eastwood"
      },
      "shipToAddress": {
        "firstName": "Jane",
        "lastName": "Doe",
        "companyName": "DR",
        "line1": "6-chome-22 Kagurazaka",
        "line2": "Shinjuku City",
        "city": "Tokyo-to",
        "postalCode": "162-0825",
        "state": "Tokyo",
        "country": "JP",
        "countryName": "Japan",
        "phoneNumber": "555-234-56789",
        "emailAddress": "subs_test@digitalriver.org",
        "countyName": "Eastwood"
      },
      "shopperId": "506960950289",
      "locale": "ja_JP",
      "siteId": "paytest2",
      "orderTotal": 281,
      "currency": "JPY",
      "orderDiscount": 0,
      "subTotal": 256,
      "tax": 25,
      "shippingTotal": 0,
      "businessEntity": "Digital River Ireland Ltd.",
      "expirationDate": "2022-06-30T15:58:01.000Z",
      "paymentSourceType": "konbini",
      "konbini": {
        "storeId": "010",
        "receiptNumber": "7232251882965",
        "printableInvoiceUrl": "{printableInvoiceUrl}",
        "storeName": "Seven Eleven",
        "localizedStoreName": "セブン‐イレブン",
        "storeLogoUrl": "{storeLogoUrl}"
      }
    }
  },
  "clientIds": {
    "site_id": "paytest2"
  },
  "searchableData": {
    "orderId": "1087747290080"
  }
}
```
{% endcode %}

### The delayed payment expired request

{% code title="Webhook request" overflow="wrap" %}
```json
{
  "type": "delayed_payment.expired",
  "data": {
    "object": {
      "orderId": "1087739480080",
      "placedOnDate": "2022-05-31T15:58:21.000Z",
      "products": [
        {
          "id": "82062200",
          "displayName": "Subscription 1 Week Manual Renewal",
          "sku": "123456"
        }
      ],
      "billToAddress": {
        "firstName": "Jane",
        "lastName": "Doe",
        "companyName": "DR",
        "line1": "6-chome-22 Kagurazaka",
        "line2": "Shinjuku City",
        "city": "Tokyo-to",
        "postalCode": "162-0825",
        "state": "Tokyo",
        "country": "JP",
        "countryName": "Japan",
        "phoneNumber": "811-234-56789",
        "emailAddress": "subs_test@digitalriver.com",
        "countyName": "Eastwood"
      },
      "shipToAddress": {
        "firstName": "Jane",
        "lastName": "Doe",
        "line1": "10380 Bren Rd",
        "city": "Eden Prairie",
        "postalCode": "55344",
        "state": "MN",
        "country": "US",
        "countryName": "United States",
        "emailAddress": "subs_test@digitalriver.com"
      },
      "shopperId": "506943170289",
      "locale": "ja_JP",
      "siteId": "paytest2",
      "orderTotal": 126,
      "currency": "JPY",
      "orderDiscount": 0,
      "subTotal": 126,
      "tax": 0,
      "shippingTotal": 0,
      "businessEntity": "Digital River Inc.",
      "expirationDate": "2022-06-30T15:58:07.000Z",
      "expirationDays": 30,
      "paymentSourceType": "konbini",
      "konbini": {
        "storeId": "010",
        "receiptNumber": "7232254886694",
        "printableInvoiceUrl": "[printableInvoiceUrl",
        "storeName": "Seven Eleven",
        "localizedStoreName": "セブン‐イレブン",
        "storeLogoUrl": "{storeLogoURL}"
      }
    }
  },
  "clientIds": {
    "site_id": "paytest2"
  },
  "searchableData": {
    "orderId": "1087739480080"
  }
}
```
{% endcode %}

## Wire Transfer

{% code title="Wire Transfer payload example" overflow="wrap" %}
```json
"wireTransfer": {
          "accountHolder": "Global Collect BV",
          "bankName": "Rabobank N.A.",
          "city": "Ontario USA",
          "country": "United States",
          "referenceId": "890709732999",
          "accountNumber": "0487369908",
          "additionalBankInformation": "ABA|122238420||Address|WESTLAKE VILLAGE, 2663 TOWNSGATE RD",
          "swiftCode": "RABOUS66XXX"
}
```
{% endcode %}

### `accountHolder`

The name of the account holder of the destination bank account (payment service provider).

### `bankName`

The name of the bank that will receive the payment.

### `city`

The city where the bank branch is located.

### `country`

The country where the bank branch is located.

### `referenceId`

The unique reference identifier for the transaction. The shopper should include this reference identifier when wiring funds.&#x20;

{% hint style="info" %}
**Note**: The payment must be manually reconciled if the shopper doesn't provide this unique reference identifier.
{% endhint %}

### `accountNumber`

The bank account number that will receive the payment.

### `additionalBankInformation`

Any additional information that you need to display to the shopper.

### `swiftCode`

The Society for Worldwide International Financial Telecommunications (SWIFT) code is associated with the bank. This field is only populated for EU countries.

### The delayed payment reminder request

{% code title="Webhook request" overflow="wrap" %}
```json
{
  "type": "delayed_payment.reminder",
  "data": {
    "object": {
      "orderId": "25949555040199",
      "placedOnDate": "2022-06-07T07:10:06.006Z",
      "products": [
        {
          "id": "12345678",
          "displayName": "Digital Product 1",
          "sku": "123123"
        }
      ],
      "billToAddress": {
        "firstName": "Jane",
        "lastName": "Doe",
        "line1": "line1",
        "city": "Belgium",
        "postalCode": "10997",
        "country": "US",
        "countryName": "United States",
        "phoneNumber": "555-456-7890",
        "emailAddress": "subs_test@digitalriver.com"
      },
      "shipToAddress": {
        "firstName": "Jane",
        "lastName": "Doe",
        "line1": "line1",
        "city": "Belgium",
        "postalCode": "10997",
        "country": "US",
        "countryName": "United States",
        "phoneNumber": "555-456-7890",
        "emailAddress": "subs_test@digitalriver.com"
      },
      "shopperId": "26467404580199",
      "locale": "en_US",
      "siteId": "paytest",
      "orderTotal": 1.62,
      "currency": "USD",
      "orderDiscount": 0,
      "subTotal": 1.5,
      "tax": 0.12,
      "shippingTotal": 0,
      "businessEntity": "DR globalTech Inc.",
      "expirationDate": "2022-07-07T07:10:04.000Z",
      "paymentSourceType": "wireTransfer",
      "wireTransfer": {
        "accountHolder": "Global Collect BV",
        "bankName": "Rabobank N.A.",
        "city": "Ontario USA",
        "country": "United States",
        "referenceId": "890710206969",
        "accountNumber": "0487369908",
        "additionalBankInformation": "ABA|122238420||Address|WESTLAKE VILLAGE, 2663 TOWNSGATE RD",
        "swiftCode": "RABOUS66XXX"
      }
    }
  },
  "clientIds": {
    "site_id": "paytest"
  },
  "searchableData": {
    "orderId": "25949555040199"
  }
}
```
{% endcode %}

### The delayed payment expired request

{% code title="Webhook request" overflow="wrap" %}
```json
{
  "type": "delayed_payment.expired",
  "data": {
    "object": {
      "orderId": "25949554420199",
      "placedOnDate": "2022-06-07T06:57:55.000Z",
      "products": [
        {
          "id": "308180500",
          "displayName": "BP Digital",
          "sku": "BP123"
        }
      ],
      "billToAddress": {
        "firstName": "Jane",
        "lastName": "Doe",
        "line1": "line1",
        "city": "Belgium",
        "postalCode": "10997",
        "country": "US",
        "countryName": "United States",
        "phoneNumber": "555-456-7890",
        "emailAddress": "subs_test@digtalriver.com"
      },
      "shipToAddress": {
        "firstName": "Jane",
        "lastName": "Doe",
        "line1": "line1",
        "city": "Belgium",
        "postalCode": "10997",
        "country": "US",
        "countryName": "United States",
        "phoneNumber": "555-456-7890",
        "emailAddress": "subs_test@digtalriver.com"
      },
      "shopperId": "26467403060199",
      "locale": "en_US",
      "siteId": "paytest2",
      "orderTotal": 1.08,
      "currency": "USD",
      "orderDiscount": 0,
      "subTotal": 1,
      "tax": 0.08,
      "shippingTotal": 0,
      "businessEntity": "Digital River Inc.",
      "expirationDate": "2022-07-07T06:57:53.000Z",
      "expirationDays": 30,
      "paymentSourceType": "wireTransfer",
      "wireTransfer": {
        "accountHolder": "Global Collect BV",
        "bankName": "Rabobank N.A.",
        "city": "Ontario USA",
        "country": "United States",
        "referenceId": "890710206719",
        "accountNumber": "0487369908",
        "additionalBankInformation": "ABA|122238420||Address|WESTLAKE VILLAGE, 2663 TOWNSGATE RD",
        "swiftCode": "RABOUS66XXX"
      }
    }
  },
  "clientIds": {
    "site_id": "paytest2"
  },
  "searchableData": {
    "orderId": "25949554420199"
  }
}
```
{% endcode %}
