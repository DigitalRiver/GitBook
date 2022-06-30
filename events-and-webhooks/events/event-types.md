---
description: Understand the event types supported by Digital River.
---

# Event types

In the Commerce API, there are many event types. Most integrations only need to subscribe to a relatively small number of them. You can choose what you want to monitor from the list of the event types described below. Each of these event types provides an example payload.

Every event type uses the following format: `resource.event`. This makes coding easier since you know all event types use a consistent format.&#x20;

In [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do), when you [create a webhook](../webhooks/creating-a-webhook.md) or [view the details of an existing webhook](../webhooks/searching-for-a-webhook.md), you can find the latest list of event types supported in the Commerce API.

The following topics describe the supported subscription event types.

## The delayed payment expired and reminder events

When the order has been submitted and is awaiting payment, Digital River creates a `delayed_payment.reminder` event.&#x20;

When Digital River does not receive the delayed payment, Digital River creates a `delayed_payment.expired` event. When you receive this notification, you can choose to send the notification to the customer.

The following example shows the payloads for various payment methods.

### bPay

{% code title="bPay payload example" %}
```json
"bPay": {
        "accountHolder": "",        
        "bankName": "",        
        "city": "",        
        "country": "",        
        "referenceId": "",        
        "accountNumber": "",        
        "billerId": "",        
        "customerPaymentReference": "",        
        "swiftCode": ""    
}
```
{% endcode %}

| Field                      | Description                                                                                                                                                                                                                                                                                                                  |
| -------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `accountHolder`            | The name of the account holder of the destination bank account (payment service provider).                                                                                                                                                                                                                                   |
| `bankName`                 | The name of the bank that will receive the payment.                                                                                                                                                                                                                                                                          |
| `city`                     | The city where the bank branch is located.                                                                                                                                                                                                                                                                                   |
| `country`                  | The country where the bank branch is located.                                                                                                                                                                                                                                                                                |
| `referenceId`              | <p>The unique reference identifier for the transaction. Payment Service Processors (PSP) match this identifier from the incoming payment with the Centralized Payment Gateway (CPG).<br><strong>Note</strong>: If you don't provide this identifier to the shopper, the PSP cannot match the payment to any transaction.</p> |
| `accountNumber`            | The bank account number that will receive the payment.                                                                                                                                                                                                                                                                       |
| `billerId`                 | When you display or send payment instructions by email to a shopper, the instructions should include the biller identifier.                                                                                                                                                                                                  |
| `customerPaymentReference` | When you display or send payment instructions by email to a shopper, the instructions should include the Customer Reference Number (CRN).                                                                                                                                                                                    |
| `swiftCode`                | The Society for Worldwide International Financial Telecommunications (SWIFT) code is associated with the bank.                                                                                                                                                                                                               |

#### The delayed payment reminder request

{% code title="Webhook request" %}
```json
{
  "type": "delayed_payment.reminder",
  "data": {
    "object": {
      "orderId": "25949552740199"",
      "placedOnDate": "2022-06-07T06:52:20.000Z",
      "products": [
        {
          "id": "34218800",
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
        "country": "AU",
        "countryName": "Australia",
        "phoneNumber": "555-456-7890",
        "emailAddress": "subs_test@digitalriver.com"
      },
      "shipToAddress": {
        "firstName": "Jane",
        "lastName": "Doe",
        "line1": "line1",
        "city": "Belgium",
        "postalCode": "10997",
        "country": "AU",
        "countryName": "Australia",
        "phoneNumber": "555-456-7890",
        "emailAddress": "subs_test@digitalriver.com"
      },
      "shopperId": "26467402450199",
      "locale": "en_AU",
      "siteId": "paytest",
      "orderTotal": 2.31,
      "currency": "AUD",
      "orderDiscount": 0,
      "subTotal": 2.1,
      "tax": 0.21,
      "shippingTotal": 0,
      "businessEntity": "Digital River Ireland Ltd.",
      "expirationDate": "2022-07-07T06:52:19.000Z",
      "paymentSourceType": "bPay",
      "bPay": {
        "accountHolder": "Global Collect BV",
        "bankName": "Commonwealth Bank",
        "city": "Sydney",
        "country": "Australia",
        "referenceId": "890710206589",
        "accountNumber": "062000-11002112",
        "billerId": "141606",
        "customerPaymentReference": "008907102065891",
        "swiftCode": "CTBAAU2S"
      }
    }
  },
  "clientIds": {
    "site_id": "paytest"
  },
  "searchableData": {
    "orderId": "25949552740199"
  }
```
{% endcode %}

#### The delayed payment expired request

{% code title="Webhook request" %}
```json
{
  "type": "delayed_payment.expired",
  "data": {
    "object": {
      "orderId": "25949554310199",
      "placedOnDate": "2022-06-07T06:57:31.000Z",
      "products": [
        {
          "id": "281878000",
          "displayName": "Subscription AutoRenew",
          "sku": "1234545666"
        }
      ],
      "billToAddress": {
        "firstName": "Jane",
        "lastName": "Doe",
        "line1": "line1",
        "city": "Belgium",
        "postalCode": "10997",
        "country": "AU",
        "countryName": "Australia",
        "phoneNumber": "555-456-7890",
        "emailAddress": "subs_test@digitalriver.com"
      },
      "shipToAddress": {
        "firstName": "Jane",
        "lastName": "Doe",
        "line1": "line1",
        "city": "Belgium",
        "postalCode": "10997",
        "country": "AU",
        "countryName": "Australia",
        "phoneNumber": "555-456-7890",
        "emailAddress": "subs_test@digitalriver.com"
      },
      "shopperId": "26467402970199",
      "locale": "en_AU",
      "siteId": "paytest2",
      "orderTotal": 307.67,
      "currency": "AUD",
      "orderDiscount": 0,
      "subTotal": 279.7,
      "tax": 27.97,
      "shippingTotal": 0,
      "businessEntity": "Digital River Ireland Ltd.",
      "expirationDate": "2022-07-07T06:57:29.000Z",
      "expirationDays": 30,
      "paymentSourceType": "bPay",
      "bPay": {
        "accountHolder": "Global Collect BV",
        "bankName": "Commonwealth Bank",
        "city": "Sydney",
        "country": "Australia",
        "referenceId": "890710206659",
        "accountNumber": "062000-11002112",
        "billerId": "141606",
        "customerPaymentReference": "008907102066592",
        "swiftCode": "CTBAAU2S"
      }
    }
  },
  "clientIds": {
    "site_id": "paytest2"
  },
  "searchableData": {
    "orderId": "25949554310199"
  }
}
```
{% endcode %}

### Boleto

{% code title="Boleto payload example" %}
```json
"boletoBancario": {
        "documentCode",
        "document"
}
```
{% endcode %}

| Field          | Description                                                                                              |
| -------------- | -------------------------------------------------------------------------------------------------------- |
| `documentCode` | The Boleto document code URL. This field is required for a successful request.                           |
| `document`     | The Boleto numeric identifier. The shopper can use this identifier to pay Boleto through a banking app.  |

#### The delayed payment reminder request

{% code title="Webhook request" %}
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
        "countryName": "Brasil",
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

#### The delayed payment expired request

{% code title="Webhook request" %}
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

### Konbini

{% code title=" Konbini payload example" %}
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

| Field                 | Description                                         |
| --------------------- | --------------------------------------------------- |
| `storeId`             | The store identifer.                                |
| `receiptNumber`       | The Konbini receipt number.                         |
| `printableInvoiceUrl` | The URL contains the store's invoice for the order. |
| `storeName`           | The store's name.                                   |
| `localizedStoreName`  | The localized store name.                           |
| `storeLogoUrl`        | The URL for the store's logo.                       |

#### The delayed payment reminder request

{% code title="Webhook request" %}
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

#### The delayed payment expired request

{% code title="Webhook request" %}
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

### Wire Transfer

{% code title="Wire Transfer payload example" %}
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

| Field                       | Description                                                                                                                                                                                                                                                              |
| --------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `accountHolder`             | The name of the account holder of the destination bank account (payment service provider).                                                                                                                                                                               |
| `bankName`                  | The name of the bank that will receive the payment.                                                                                                                                                                                                                      |
| `city`                      | The city where the bank branch is located.                                                                                                                                                                                                                               |
| `country`                   | The country where the bank branch is located.                                                                                                                                                                                                                            |
| `referenceId`               | <p>The unique reference identifier for the transaction. The shopper should include this reference identifier when wiring funds. <br><strong>Note</strong>: If the shopper doesn't provide this unique reference identifier, the payment must be manually reconciled.</p> |
| `accountNumber`             | The bank account number that will receive the payment.                                                                                                                                                                                                                   |
| `additionalBankInformation` | Any additional information that you need to display to the shopper.                                                                                                                                                                                                      |
| `swiftCode`                 | The Society for Worldwide International Financial Telecommunications (SWIFT) code is associated with the bank. This field is only populated for EU countries.                                                                                                            |

#### The delayed payment reminder request

{% code title="Webhook request" %}
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

#### The delayed payment expired request

{% code title="Webhook request" %}
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

## The subscription action processed event

When a subscription is changed, Digital River creates the `subscription.action.processed`. This event tells you if the subscription update succeeded or failed and provides the details of the pending actions in the payload. The `actionType` identifies the action applied to the subscription.

| actionType         | Description                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| ------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `activate`         | When you [activate a shopper's subscri](https://docs.digitalriver.com/commerce-api/subscriptions/managing-subscriptions/activating-a-subscription)ption, the subscription state changes from `pendingActivation` to `Subscribed`. It also updates the subscription expiration date and all subscription-related data columns.                                                                                                                 |
| `cancel`           | When you [cancel a shopper's subscription](../../subscriptions/managing-subscriptions/cancelling-a-subscription.md), the subscription state changes to `Cancelled`.                                                                                                                                                                                                                                                                           |
| email              | <p>When you update a <a href="https://www.digitalriver.com/docs/commerce-api-reference/#operation/emailUpdater">shopper's subscription billing or shipping email address</a>, you will get a notification.<br>Billing email address: <code>subscription.billingOption.billAddress.emailAddress</code><br>Shipping email address: <code>subscription.shipToAddress.emailAddress</code></p>                                                     |
| `expiration_date`  | When you [update a shopper's subscription expiration date](https://www.digitalriver.com/docs/commerce-api-reference/#operation/updateExpirationDate), the system updates the expiration date and all subscription-related data columns.                                                                                                                                                                                                       |
| `payment_option`   | When you [update a shopper's subscription payment option](https://www.digitalriver.com/docs/commerce-api-reference/#operation/updatePaymentOption), the system associates a new billing or payment option with the subscription. When updated successfully, Retry On Account Update will trigger a billing attempt if the subscription falls under the renewal window.                                                                        |
| `payment_source`   | When you update a [shopper's subscription payment source](https://www.digitalriver.com/docs/commerce-api-reference/#operation/updatePaymentSource), the system associates the new payment source with the subscription.  If there is a billing option associated with the payment source, the system will create a new billing option for the payment source. The request payload contains the `sourceId` and `isShippingSameAsBilling` flag. |
| `perpetual_price`  | When you [modify the subscription's perpetual price](https://www.digitalriver.com/docs/commerce-api-reference/#operation/changePerpetualPrice) for a shopper, the system modifies the [price of the subscription for the remaining subscription cycle](../../subscriptions/midterm-change.md#perpetual-unit-price). The system updates the perpetual price or the hold price.                                                                 |
| `reduce`           | When you [reduce a shopper's subscription quantity or add-ons](https://www.digitalriver.com/docs/commerce-api-reference/#operation/reduceSubscription), the change is immediate.                                                                                                                                                                                                                                                              |
| `reference_id`     | When you [modify the subscription's external reference ID](../../subscriptions/managing-subscriptions/modifying-the-subscriptions-external-reference-id.md), you will receive a notification.                                                                                                                                                                                                                                                 |
| `renewal_price`    | When you [change the shopper's subscription price](../../subscriptions/managing-subscriptions/changing-the-subscription-renewal-price.md), the system updates the shopper's subscription renewal price                                                                                                                                                                                                                                        |
| `renewal_product`  | When you [change the shopper's subscription renewal produc](../../subscriptions/managing-subscriptions/changing-the-subscription-renewal-product.md)t, the system updates the shopper's subscription renewal product.                                                                                                                                                                                                                         |
| `renewal_quantity` | When you [change the shopper's subscription renewal quantity](../../subscriptions/managing-subscriptions/changing-the-subscription-renewal-quantity.md), the system updates the shopper's subscription renewal quantity.                                                                                                                                                                                                                      |
| `renewal_type`     | When you [change the shopper's subscription renewal type](../../subscriptions/managing-subscriptions/changing-the-subscription-renewal-type.md), the system updates the shopper's subscription renewal quantity.                                                                                                                                                                                                                              |
| `ship_to_address`  | When you [change the shopper's ship to address](../../subscriptions/managing-subscriptions/changing-the-subscriptions-shipping-address.md), the system either adds or updates the shopper's ship-to address.                                                                                                                                                                                                                                  |

If the subscription update event fails, Digital River will retry the subscription update event.

{% code title="Webhook request" %}
```json
{
   "type":"subscription.action.processed",
   "data":{
      "object":{
         "action":{
            "actionType":"ship_to_address",
            "actionStatus":"success"
         },
         "subscription":{
            "id":"13530199",
            "creationDate":"2022-06-01T09:14:48.000Z",
            "activationDate":"2022-06-01T05:00:00.000Z",
            "nextRenewalDate":"2022-07-01T05:00:00.000Z",
            "expirationDate":"2022-07-01T05:00:00.000Z",
            "graceDate":"2022-07-08T05:00:00.000Z",
            "currentQuantity":1,
            "renewalQuantity":1,
            "autoRenewal":true,
            "locale":"en_US",
            "state":"Subscribed",
            "duration":30,
            "frequency":30,
            "siteId":"sub2test",
            "shopper":{
               "id":"26195489030199"
            },
            "renewalPrice":{
               "unitPrice":10.99,
               "locked":false,
               "currency":"USD"
            },
            "term":{
               "termUnit":"MONTHS",
               "termLength":1
            },
            "product":{
               "id":"5363866300",
               "displayName":"Monthly auto renewal Subscription",
               "sku":"SUB_AUTORENEW"
            },
            "shipToAddress":{
               "id":"406032130199",
               "firstName":"Jane",
               "lastName":"Doe",
               "line1":"Abc",
               "city":"Pune",
               "postalCode":"324345",
               "countrySubdivision":"CA",
               "country":"AR",
               "countryName":"Argentina",
               "phoneNumber":"55534567890",
               "emailAddress":"subs_test@digitalriver.com"
            },
            "paymentOption":{
               "nickName":"Default",
               "id":"4022980199",
               "isDefault":"true",
               "type":"CreditCardMethod",
               "creditCard":{
                  "expirationMonth":"4",
                  "expirationYear":"2024",
                  "displayableNumber":"************1111",
                  "type":"visa",
                  "displayName":"Visa"
               },
               "address":{
                  "id":"406032100199",
                  "firstName":"Jane",
                  "lastName":"Doe",
                  "line1":"Abc",
                  "city":"Pune",
                  "postalCode":"324345",
                  "countrySubdivision":"CA",
                  "country":"AR",
                  "countryName":"Argentina",
                  "phoneNumber":"02134567890",
                  "emailAddress":"subs_test@digitalriver.com"
               }
            },
            "addOns":[
                
            ]
         }
      }
   },
   "clientIds":{
      "site_id":"sub2test"
   },
   "searchableData":{
      "subscriptionId":"13530199"
   }
}
```
{% endcode %}

## The subscription automatic renewal reminder event

When an existing subscription nears the end of the subscription cycle, Digital River creates an automatic renewal reminder ( `subscription.auto_reminder`).

## The subscription cancelled event

When an existing subscription has been cancelled, Digital River creates a `subscription.cancelled` event.

{% code title="Webhook request" %}
```json
{
    "type": "subscription.cancelled",
    "data": {
        "object": {
            "id": "15547380289",
            "creationDate": "2022-03-29T06:55:05.000Z",
            "activationDate": "2022-03-29T05:00:00.000Z",
            "nextRenewalDate": "2022-04-29T05:00:00.000Z",
            "expirationDate": "2022-04-29T05:00:00.000Z",
            "graceDate": "2022-05-06T05:00:00.000Z",
            "cancellationDate": "2022-03-29T05:00:00.000Z",
            "currentQuantity": 1,
            "renewalQuantity": 1,
            "autoRenewal": true,
            "locale": "en_US",
            "state": "Cancelled",
            "duration": 31,
            "frequency": 31,
            "siteId": "sub2test",
            "shopper": {
                "id": "504455390289",
                "externalReferenceId": "ZPQRTQHL16J5"
            },
            "term": {
                "termUnit": "MONTHS",
                "termLength": 1
            },
            "product": {
                "id": "5367865200",
                "displayName": "APM_2_months_auto",
                "sku": "SUBS_COMMITMENT"
            },
            "shipToAddress": {
                "id": "330005680289",
                "firstName": "Jane",
                "lastName": "Doe",
                "companyName": "DR",
                "line1": "10380 Bren Rd W",
                "line2": "Conjunto 304",
                "line3": "Conjunto 304",
                "city": "Minnetonka",
                "postalCode": "55343",
                "countrySubdivision": "MN",
                "country": "US",
                "countryName": "United States",
                "phoneNumber": "555-253-1234",
                "emailAddress": "test@digitalriver.com",
                "countyName": "Minnetonka"
            },
            "paymentOption": {
                "nickName": "VisaUNIU910",
                "id": "16070210289",
                "isDefault": "true",
                "type": "CreditCardMethod",
                "creditCard": {
                    "expirationMonth": "3",
                    "expirationYear": "2024",
                    "displayableNumber": "************1111",
                    "type": "visa",
                    "displayName": "Visa"
                },
                "address": {
                    "id": "330108580289",
                    "firstName": "Jane",
                    "lastName": "Doe",
                    "companyName": "DR",
                    "line1": "10380 Bren Rd W",
                    "line2": "Conjunto 304",
                    "line3": "Conjunto 304",
                    "city": "Minnetonka",
                    "postalCode": "55343",
                    "countrySubdivision": "MN",
                    "country": "US",
                    "countryName": "United States",
                    "phoneNumber": "555-253-1234",
                    "emailAddress": "test@digitalriver.com",
                    "countyName": "Minnetonka"
                }
            },
            "addOns": []
        }
    },
   "clientIds":{
      "site_id":"sub2test"
   },
   "searchableData":{
      "subscriptionId":"15547380289"
   }
}
```
{% endcode %}

## The subscription created event

When a customer purchase a new subscription, Digital River creates a `subscription.created` event.

During the shopping experience, a customer orders a subscription to one of your products. They may order a trial subscription or a purchased subscription.

If you [created a webhook](../webhooks/creating-a-webhook.md) using the `subscription.created` event for your application (endpoint URL), Digital River notifies your application when a successful subscription acquisition event occurs.

{% code title="Webhook request" %}
```json
{
  "type": "subscription.created",
  "data": {
    "object": {
      "id": "8457000397",
      "creationDate": "2021-07-01T05:04:47.493Z",
      "activationDate": "2021-06-30T18:30:00.000Z",
      "nextRenewalDate": "2022-06-30T18:30:00.000Z",
      "expirationDate": "2022-06-30T18:30:00.000Z",
      "graceDate": "2022-07-30T18:30:00.000Z",
      "currentQuantity": 1,
      "renewalQuantity": 1,
      "autoRenewal": true,
      "locale": "en_US",
      "state": "Subscribed",
      "duration": 365,
      "frequency": 365,
      "siteId": "sub2test",
      "shopper": {
        "id": "35504010397"
      },
      "renewalPrice": {
        "unitPrice": 95,
        "locked": false,
        "currency": "USD"
      },
      "term": {
        "termUnit": "YEARS",
        "termLength": 1
      },
      "product": {
        "id": "9964801100",
        "displayName": "Annual Auto Renewal Subscription",
        "sku": "12"
      },
      "shipToAddress": {
        "id": "76213030397",
        "firstName": "Jane",
        "lastName": "Doe",
        "companyName": "ABC",
        "line1": "Kalyani Nagar",
        "city": "Pune",
        "postalCode": "411014",
        "countrySubdivision": "AA",
        "country": "IN",
        "countryName": "India",
        "phoneNumber": "55503796942",
        "emailAddress": "subs_test@digitalriver.com"
      },
      "paymentOption": {
        "nickName": "Default",
        "id": "6631000397",
        "isDefault": "true",
        "type": "CreditCardMethod",
        "creditCard": {
          "expirationMonth": "8",
          "expirationYear": "2023",
          "displayableNumber": "************1111",
          "type": "visa",
          "displayName": "Visa"
        },
        "address": {
          "id": "66287380397",
          "firstName": "Jane",
          "lastName": "Doe",
          "companyName": "ABC",
          "line1": "Kalyani Nagar",
          "city": "Pune",
          "postalCode": "411014",
          "countrySubdivision": "AA",
          "country": "IN",
          "countryName": "India",
          "phoneNumber": "55503796942",
          "emailAddress": "subs_test@digitalriver.com"
        }
      },
      "addOns": []
    }
  },
  "clientIds": {
    "site_id": "sub2test"
  },
  "searchableData": {
    "subscriptionId": "8457000397"
  }
}
```
{% endcode %}

## The subscription credit card expired event

When the credit card is about to expire, Digital River creates a `subscription.credit_card_expired` event.

{% code title="Webhook request" %}
```json
{
   "type":"subscription.credit_card_expired",
   "data":{
      "object":{
         "id":"4200199",
         "creationDate":"2022-03-28T15:09:36.000Z",
         "activationDate":"2022-03-28T05:00:00.000Z",
         "nextRenewalDate":"2022-06-28T05:00:00.000Z",
         "expirationDate":"2022-06-28T05:00:00.000Z",
         "graceDate":"2022-07-05T05:00:00.000Z",
         "currentQuantity":1,
         "renewalQuantity":1,
         "autoRenewal":true,
         "locale":"en_US",
         "state":"Subscribed",
         "duration":92,
         "frequency":92,
         "siteId":"earth1",
         "shopper":{
            "id":"25448428670199"
         },
         "renewalPrice":{
            "unitPrice":35.99,
            "locked":true,
            "currency":"USD"
         },
         "term":{
            "termUnit":"MONTHS",
            "termLength":3
         },
         "product":{
            "id":"5619730199",
            "externalReferenceId":"",
            "displayName":"3 Month auto renew Sub - Copy",
            "sku":"SUB_ADDONS"
         },
         "shipToAddress":{
            "id":"405320220199",
            "firstName":"Digital",
            "lastName":"River QA",
            "line1":"10380 Bren Rd W",
            "city":"Minnetonka",
            "postalCode":"55343",
            "countrySubdivision":"MN",
            "country":"US",
            "countryName":"United States",
            "phoneNumber":"5555559519",
            "emailAddress":"subs_test@digitalriver.com"
         },
         "paymentOption":{
            "nickName":"Visa 1111",
            "id":"4013880199",
            "isDefault":"false",
            "type":"CreditCardMethod",
            "creditCard":{
               "expirationMonth":"4",
               "expirationYear":"2022",
               "displayableNumber":"************1111",
               "type":"visa",
               "displayName":"Visa"
            },
            "address":{
               "id":"405320210199",
               "firstName":"Jane",
               "lastName":"Doe",
               "line1":"10380 Bren Rd W",
               "city":"Minnetonka",
               "postalCode":"55343",
               "countrySubdivision":"MN",
               "country":"US",
               "countryName":"United States",
               "phoneNumber":"5555559519",
               "emailAddress":"subs_test@digitalriver.com"
            }
         },
         "addOns":[
            {
               "product":{
                  "id":"5619750199",
                  "displayName":"Subscription AddOn_1 - Copy",
                  "sku":"SUB_ADDONS"
               },
               "quantity":1,
               "renewalPrice":{
                  "unitPrice":4.0,
                  "locked":true,
                  "currency":"USD"
               }
            }
         ]
      }
   },
   "clientIds":{
      "site_id":"earth1"
   },
   "searchableData":{
      "subscriptionId":"4200199"
   }
}
```
{% endcode %}

## The subscription payment failed event

When the subscription payment attempt fails, Digital River creates a `subscription.payment_failed` event. You will receive a notification that includes the reason why the customer's transaction failed. Note that this event is only applicable to auto-renewal.

{% hint style="info" %}
PayPal and other payment methods share the same events. However, the contents of the email notification for each payment method will be different.
{% endhint %}

We include the payment method in the webhook payload for each notification.

{% code title="Webhook request" %}
```json
{
   "type":"subscription.payment_failed",
   "data":{
      "object":{
         "id":"5610199",
         "creationDate":"2022-03-28T16:29:13.000Z",
         "activationDate":"2022-03-28T05:00:00.000Z",
         "nextRenewalDate":"2022-05-28T05:00:00.000Z",
         "nextBillingDate":"2022-05-28T05:00:00.000Z",
         "expirationDate":"2022-05-28T05:00:00.000Z",
         "graceDate":"2022-06-04T05:00:00.000Z",
         "currentQuantity":1,
         "renewalQuantity":1,
         "autoRenewal":true,
         "locale":"en_US",
         "state":"PendingRenewal",
         "duration":61,
         "frequency":30,
         "currentBillingCycleNumber":2,
         "totalNumberOfBillingCycle":2,
         "siteId":"sub2test",
         "shopper":{
            "id":"25448436960199",
            "externalReferenceId":"OXELSH53JI9L"
         },
         "renewalPrice":{
            "unitPrice":9.0,
            "locked":false,
            "currency":"USD"
         },
         "term":{
            "termUnit":"MONTHS",
            "termLength":1
         },
         "product":{
            "id":"5367865200",
            "displayName":"APM_2_months_auto",
            "sku":"SUBS_COMMITMENT"
         },
         "shipToAddress":{
            "id":"405361290199",
            "firstName":"Jane",
            "lastName":"Doe",
            "companyName":"DR",
            "line1":"10380 Bren Rd W",
            "line2":"Conjunto 304",
            "line3":"Conjunto 304",
            "city":"Minnetonka",
            "postalCode":"55343",
            "countrySubdivision":"MN",
            "country":"US",
            "countryName":"United States",
            "phoneNumber":"555-253-1234",
            "emailAddress":"subs_test@digitalriver.com",
            "countyName":"Minnetonka"
         },
         "paymentOption":{
            "nickName":"VisaYVX7B2",
            "id":"4017490199",
            "isDefault":"true",
            "type":"CreditCardMethod",
            "creditCard":{
               "expirationMonth":"3",
               "expirationYear":"2024",
               "type":"visa",
               "displayName":"Visa"
            },
            "address":{
               "id":"405360070199",
               "firstName":"Jane",
               "lastName":"Doe",
               "companyName":"DR",
               "line1":"10380 Bren Rd W",
               "line2":"Conjunto 304",
               "line3":"Conjunto 304",
               "city":"Minnetonka",
               "postalCode":"55343",
               "countrySubdivision":"MN",
               "country":"US",
               "countryName":"United States",
               "phoneNumber":"555-253-1234",
               "emailAddress":"subs_test@digitalriver.com",
               "countyName":"Minnetonka"
            }
         },
         "addOns":[
             
         ]
      }
   },
   "clientIds":{
      "site_id":"sub2test"
   },
   "searchableData":{
      "subscriptionId":"5610199"
   }
}
```
{% endcode %}

## The subscription payment information changed event

When the payment information has been updated through any entry point, Digital River creates a `subscription.payment_info_changed` event.

{% code title="Webhook request" %}
```json
{
    "type": "subscription.payment_info_changed",
    "data": {
        "object": {
            "id": "12060199",
            "creationDate": "2022-05-18T16:50:53.000Z",
            "activationDate": "2022-05-18T05:00:00.000Z",
            "nextRenewalDate": "2023-05-18T05:00:00.000Z",
            "expirationDate": "2023-05-18T05:00:00.000Z",
            "graceDate": "2023-05-18T05:00:00.000Z",
            "currentQuantity": 1,
            "renewalQuantity": 1,
            "autoRenewal": false,
            "locale": "en_US",
            "state": "Subscribed",
            "duration": 365,
            "frequency": 365,
            "siteId": "sub2test",
            "shopper": {
                "id": "26092509660199"
            },
            "renewalPrice": {
                "unitPrice": 9.0,
                "locked": false,
                "currency": "USD"
            },
            "term": {
                "termUnit": "YEARS",
                "termLength": 1
            },
            "product": {
                "id": "5396391800",
                "displayName": "Annual manual renewal Subscription",
                "sku": "SUB_MANUAL_RENEW"
            },
            "shipToAddress": {
                "id": "406026490199",
                "firstName": "Jane",
                "lastName": "Doe",
                "companyName": "ABC",
                "line1": "Add1",
                "city": "Kansus",
                "postalCode": "123432",
                "countrySubdivision": "AA",
                "country": "VN",
                "countryName": "Vietnam",
                "phoneNumber": "5555673452",
                "emailAddress": "subs_test@digitalriver.com"
            },
            "paymentOption": {
                "nickName": "Default",
                "id": "4022810199",
                "isDefault": "true",
                "type": "CreditCardMethod",
                "creditCard": {
                    "expirationMonth": "3",
                    "expirationYear": "2025",
                    "displayableNumber": "************1111",
                    "type": "visa",
                    "displayName": "Visa"
                },
                "address": {
                    "id": "406026480199",
                    "firstName": "Jane",
                    "lastName": "Doe",
                    "companyName": "ABC",
                    "line1": "Add1",
                    "city": "Kansus",
                    "postalCode": "123432",
                    "countrySubdivision": "AA",
                    "country": "VN",
                    "countryName": "Vietnam",
                    "phoneNumber": "5555673452",
                    "emailAddress": "test@dr2.com"
                }
            },
            "addOns": []
        }
    },
      "clientIds":{
      "site_id":"sub2test"
   },
   "searchableData":{
      "subscriptionId":"12060199"
   }
}
```
{% endcode %}

## The subscription renewal reminder event

When a subscription reaches the [renewal notification date](../../subscriptions/subscription-lifecycle.md), Digital River creates a `subscription.renewal_reminder` event. You can use this event to remind your customer to renew their subscription.

{% hint style="info" %}
When you create a webhook using this event, it combines the auto-renewal reminder, manual renewal reminder, and the SEPA auto-renewal reminder into one event. As a result, we renamed the `subscription.auto_reminder` to `subscription.renewal_reminder`.
{% endhint %}

{% code title="Webhook request" %}
```json
{
   "type":"subscription.renewal_reminder",
   "data":{
      "object":{
         "id":"6310199",
         "creationDate":"2022-03-28T16:51:10.000Z",
         "activationDate":"2022-03-28T05:00:00.000Z",
         "nextRenewalDate":"2022-05-28T05:00:00.000Z",
         "nextBillingDate":"2022-05-28T05:00:00.000Z",
         "expirationDate":"2022-05-28T05:00:00.000Z",
         "graceDate":"2022-06-04T05:00:00.000Z",
         "currentQuantity":1,
         "renewalQuantity":1,
         "autoRenewal":false,
         "locale":"en_US",
         "state":"Subscribed",
         "duration":61,
         "frequency":30,
         "currentBillingCycleNumber":2,
         "totalNumberOfBillingCycle":2,
         "siteId":"sub2test",
         "shopper":{
            "id":"25448437760199"
         },
         "renewalPrice":{
            "unitPrice":19.0,
            "locked":true,
            "currency":"USD"
         },
         "term":{
            "termUnit":"MONTHS",
            "termLength":1
         },
         "product":{
            "id":"5403551500",
            "displayName":"APM_2_months_manual",
            "sku":"SUBS_COMMITMENT"
         },
         "shipToAddress":{
            "id":"405367800199",
            "firstName":"Jane",
            "lastName":"Doe",
            "line1":"10380 Bren Rd.",
            "city":"Minnetonka",
            "postalCode":"55343",
            "countrySubdivision":"MN",
            "country":"US",
            "countryName":"United States",
            "phoneNumber":"5555559519",
            "emailAddress":"subs_test@digitalriver.com"
         },
         "paymentOption":{
            "nickName":"Default",
            "id":"4018890199",
            "isDefault":"true",
            "type":"CreditCardMethod",
            "creditCard":{
               "expirationMonth":"6",
               "expirationYear":"2026",
               "displayableNumber":"************1111",
               "type":"visa",
               "displayName":"Visa"
            },
            "address":{
               "id":"405367320199",
               "firstName":"Digital",
               "lastName":"River QA",
               "line1":"10380 Bren Rd.",
               "city":"Minnetonka",
               "postalCode":"55343",
               "countrySubdivision":"MN",
               "country":"US",
               "countryName":"United States",
               "phoneNumber":"5555559519",
               "emailAddress":"subs_test@digitalriver.com"
            }
         },
         "addOns":[
             
         ]
      }
   },
   "clientIds":{
      "site_id":"sub2test"
   },
   "searchableData":{
      "subscriptionId":"6310199"
   }
}
```
{% endcode %}

## The subscription renewed event

When a subscription is renewed, Digital River creates a `subscription.renewed` event and notifies your application when a successful subscription renewal event occurs.

At the end of a subscription period, the shopper must renew the subscription for continued access to the product. A shopper can accomplish a renewal in two ways:

* **Automatic Renewal (Auto Renew)**–The shopper provides a payment method that the system automatically debits a specified number of days before the subscription expiration date. If the renewal fails because the billing information is not correct (for example, an expired credit card) shoppers are notified and given a chance to update their billing information. Digital River will attempt to bill a shopper for automatic renewals several times. After which Digital River will cancel the subscription and list the billing attempt as failed.
* **Manual Renewal**–The shopper receives emails at preconfigured time intervals before the expiration date that asks the shopper to complete a renewal transaction. The shopper has to renew the subscription manually. The customer can choose one of the following options to renew their product:
  * Log in to their My Account portal and renew using the features available in the self-service options.
  * Call Customer Service to renew the subscription.

In either case, the system renews the subscription when the payment is complete.

{% code title="Webhook request" %}
```json
{
  "type": "subscription.renewed",
  "data": {
    "object": {
      "id": "8457000397",
      "creationDate": "2021-07-01T05:04:27.000Z",
      "activationDate": "2021-06-30T18:30:00.000Z",
      "nextRenewalDate": "2023-06-30T18:30:00.000Z",
      "expirationDate": "2023-06-30T18:30:00.000Z",
      "graceDate": "2023-07-30T18:30:00.000Z",
      "currentQuantity": 1,
      "renewalQuantity": 1,
      "autoRenewal": true,
      "locale": "en_US",
      "state": "Subscribed",
      "duration": 365,
      "frequency": 365,
      "siteId": "sub2test",
      "shopper": {
        "id": "35504010397"
      },
      "renewalPrice": {
        "unitPrice": 95,
        "locked": false,
        "currency": "USD"
      },
      "term": {
        "termUnit": "YEARS",
        "termLength": 1
      },
      "product": {
        "id": "9964801100",
        "displayName": "Annual Auto Renewal Subscription",
        "sku": "12"
      },
      "shipToAddress": {
        "id": "76213030397",
        "firstName": "Jane",
        "lastName": "Doe",
        "companyName": "ABC",
        "line1": "Kalyani Nagar",
        "city": "Pune",
        "postalCode": "411014",
        "countrySubdivision": "AA",
        "country": "IN",
        "countryName": "India",
        "phoneNumber": "55503796942",
        "emailAddress": "subs_test@digitalriver.com"
      },
      "paymentOption": {
        "nickName": "Default",
        "id": "5551000397",
        "isDefault": "true",
        "type": "CreditCardMethod",
        "creditCard": {
          "expirationMonth": "8",
          "expirationYear": "2023",
          "displayableNumber": "************1111",
          "type": "visa",
          "displayName": "Visa"
        },
        "address": {
          "id": "66287380397",
          "firstName": "Jane",
          "lastName": "Doe",
          "companyName": "ABC",
          "line1": "Kalyani Nagar",
          "city": "Pune",
          "postalCode": "411014",
          "countrySubdivision": "AA",
          "country": "IN",
          "countryName": "India",
          "phoneNumber": "55503796942",
          "emailAddress": "subs_test@digitalriver.com"
        }
      },
      "addOns": []
    }
  },
  "clientIds": {
    "site_id": "sub2test"
  },
  "searchableData": {
    "subscriptionId": "8457000397"
  }
}
```
{% endcode %}

## The subscription updated event

When any of the following midterm change activities updates the subscription, Digital River creates a `subscription.updated` event.

### Previous attributes

Each `subscription.updated` event includes the `previousAttributes` object. The `previousAttributes` object lists the resource's attributes that changed, along with the previous values of these attributes.‌ The following example shows the previousAttributes for a change renewal type:

{% code title="previousAttributes example" %}
```json
Renewal Type Changed from Manual to Auto:
"previousAttributes": {
"autoRenewal": true
 }
 
Renewal Type Changed from Auto to Manual:
"previousAttributes": {
 "autoRenewal": false
}
```
{% endcode %}

### Change renewal price

When there is an update to the subscription's renewal price. You will receive a notification every time the subscription price has been updated regardless of the price type.

{% code title="Webhook request" %}
```json
{
    "id": "0712ca6b-b079-4dd6-b372-a117fe0a7aef",
    "type": "subscription.updated",
    "data": {
        "object": {
            "id": "4660199",
            "creationDate": "2022-05-12T11:51:56.351Z",
            "activationDate": "2022-05-12T05:00:00.000Z",
            "nextRenewalDate": "2023-05-12T05:00:00.000Z",
            "expirationDate": "2023-05-12T05:00:00.000Z",
            "graceDate": "2023-05-12T05:00:00.000Z",
            "currentQuantity": 1,
            "renewalQuantity": 1,
            "autoRenewal": true,
            "locale": "en_US",
            "state": "Subscribed",
            "duration": 365,
            "frequency": 365,
            "siteId": "sub2test",
            "shopper": {
                "id": "26007258190199",
                "externalReferenceId": "DQZYHRPJBOPE"
            },
            "renewalPrice": {
                "unitPrice": 29.99,
                "locked": true,
                "currency": "USD"
            },
            "term": {
                "termUnit": "YEARS",
                "termLength": 1
            },
            "product": {
                "id": "5336721400",
                "displayName": "Legacy_Annual_Auto_2_Has_Change",
                "sku": "Legacy_Annual_Auto_2"
            },
            "shipToAddress": {
                "id": "406030020199",
                "firstName": "Jane",
                "lastName": "Doe",
                "companyName": "DR",
                "line1": "10380 Bren Rd W",
                "line2": "Conjunto 304",
                "line3": "Conjunto 304",
                "city": "Minnetonka",
                "postalCode": "55343",
                "countrySubdivision": "MN",
                "country": "US",
                "countryName": "United States",
                "phoneNumber": "555-253-1234",
                "emailAddress": "subs_test@digitalriver.com",
                "countyName": "Minnetonka"
            },
            "paymentOption": {
                "nickName": "VisaECBJA8",
                "id": "4014370199",
                "isDefault": "true",
                "type": "CreditCardMethod",
                "creditCard": {
                    "expirationMonth": "5",
                    "expirationYear": "2024",
                    "displayableNumber": "************1111",
                    "type": "visa",
                    "displayName": "Visa"
                },
                "address": {
                    "id": "406031450199",
                    "firstName": "Jane",
                    "lastName": "Doe",
                    "companyName": "DR",
                    "line1": "10380 Bren Rd W",
                    "line2": "Conjunto 304",
                    "line3": "Conjunto 304",
                    "city": "Minnetonka",
                    "postalCode": "55343",
                    "countrySubdivision": "MN",
                    "country": "US",
                    "countryName": "United States",
                    "phoneNumber": "952-253-1234",
                    "emailAddress": "subs_test@digitalriver.com",
                    "countyName": "Minnetonka"
                }
            },
            "addOns": []
        },
        "previousAttributes": {
            "renewalPrice": {
                "locked": false,
                "unitPrice": 9.25
            }
        }
    },
    "liveMode": false,
    "createdTime": "2022-05-12T11:52:22.257527Z"
}
```
{% endcode %}

### Change renewal date

When there is an update to the subscription's renewal date. You will receive a notification any time the subscription's renewal date has changed.&#x20;

{% code title="Webhook request" %}
```json
{
  "type": "subscription.updated",
  "data": {
    "object": {
      "id": "8010199",
      "creationDate": "2022-05-24T12:48:38.000Z",
      "activationDate": "2022-05-24T05:00:00.000Z",
      "nextRenewalDate": "2022-07-01T05:00:00.000Z",
      "expirationDate": "2022-07-01T05:00:00.000Z",
      "graceDate": "2022-07-08T05:00:00.000Z",
      "currentQuantity": 1,
      "renewalQuantity": 1,
      "autoRenewal": true,
      "locale": "en_US",
      "state": "Subscribed",
      "duration": 38,
      "frequency": 31,
      "siteId": "sub2test",
      "shopper": {
        "id": "26195292440199"
      },
      "renewalPrice": {
        "unitPrice": 10.99,
        "locked": false,
        "currency": "USD"
      },
      "term": {
        "termUnit": "MONTHS",
        "termLength": 1
      },
      "product": {
        "id": "5363866300",
        "displayName": "Monthly auto renewal Subscription",
        "sku": "SUB_AUTORENEW"
      },
      "shipToAddress": {
        "id": "405935420199",
        "firstName": "Jane",
        "lastName": "Doe",
        "line1": "1030 Brent Rd",
        "city": "Pune",
        "postalCode": "411014",
        "countrySubdivision": "AK",
        "country": "IN",
        "countryName": "India",
        "phoneNumber": "55596541230",
        "emailAddress": "subs_test@digitalriver.com"
      },
      "paymentOption": {
        "nickName": "Visa 1111",
        "id": "4018780199",
        "isDefault": "false",
        "type": "CreditCardMethod",
        "creditCard": {
          "expirationMonth": "3",
          "expirationYear": "2024",
          "displayableNumber": "************1111",
          "type": "visa",
          "displayName": "Visa"
        },
        "address": {
          "id": "405935410199",
          "firstName": "Jane",
          "lastName": "Doe",
          "line1": "1030 Brent Rd",
          "city": "Pune",
          "postalCode": "411014",
          "countrySubdivision": "AK",
          "country": "IN",
          "countryName": "India",
          "phoneNumber": "07896541230",
          "emailAddress": "subs_test@digitalriver.com"
        }
      },
      "addOns": []
    },
    "previousAttributes": {
      "duration": 31,
      "nextRenewalDate": "2022-06-24T05:00:00.000Z",
      "graceDate": "2022-07-01T05:00:00.000Z",
      "expirationDate": "2022-06-24T05:00:00.000Z"
    }
  },
  "clientIds": {
    "site_id": "sub2test"
  },
  "searchableData": {
    "subscriptionId": "8010199"
  }
}
```
{% endcode %}

### Change renewal product

When there is a change to the subscribed product. For example:&#x20;

* Changing the product midterm. When there is an Immediate Midterm Change from the Preview Cart API due to either a change to the subscribed product or a change to the subscription quantity.
* Adding an addon to a base subscription or removing an addon from a base subscription.
* Product change at the end of the subscription cycle.

<mark style="color:red;">??? Is this example correct? It's not like the other examples on the Confluence page. ???</mark>

{% code title="Webhook request" %}
```json
"previousAttributes": {
  "renewalProduct" : {
    "id" : "111",
    "displayName" : "Legacy_Annual_Auto_1_Has_Change",
    "sku" : "Legacy_Annual_Auto_1"
   }
} 
```
{% endcode %}

### Change renewal type

When there is a change to the subscription renewal (manual or auto) type. Such as changing `autoRenewal` to `true` or `false`. You will receive a notification when the renewal type has changed.

{% code title="Webhook request" %}
```json
{
  "type": "subscription.updated",
  "data": {
    "object": {
      "id": "18023200289",
      "creationDate": "2022-06-07T06:39:43.000Z",
      "activationDate": "2022-06-07T05:00:00.000Z",
      "nextRenewalDate": "2023-06-07T05:00:00.000Z",
      "nextBillingDate": "2022-07-07T05:00:00.000Z",
      "expirationDate": "2023-06-07T05:00:00.000Z",
      "graceDate": "2022-07-07T05:00:00.000Z",
      "currentQuantity": 1,
      "renewalQuantity": 1,
      "autoRenewal": false,
      "locale": "en_US",
      "state": "Subscribed",
      "duration": 365,
      "frequency": 30,
      "currentBillingCycleNumber": 1,
      "totalNumberOfBillingCycle": 12,
      "siteId": "sub2test",
      "shopper": {
        "id": "507087780289",
        "externalReferenceId": "PONZUOEQZRQ5"
      },
      "renewalPrice": {
        "unitPrice": 18.1,
        "locked": true,
        "currency": "USD"
      },
      "term": {
        "termUnit": "MONTHS",
        "termLength": 1
      },
      "product": {
        "id": "5367865700",
        "displayName": "APM_12_months_auto",
        "sku": "SUBS_COMMITMENT"
      },
      "shipToAddress": {
        "id": "333129830289",
        "firstName": "Jane",
        "lastName": "Doe",
        "companyName": "DR",
        "line1": "10380 Bren Rd W",
        "line2": "Conjunto 304",
        "line3": "Conjunto 304",
        "city": "Minnetonka",
        "postalCode": "55343",
        "countrySubdivision": "MN",
        "country": "US",
        "countryName": "United States",
        "phoneNumber": "555-253-1234",
        "emailAddress": "subs_test@digitalriver.com",
        "countyName": "Minnetonka"
      },
      "paymentOption": {
        "nickName": "VisaBUSXG0",
        "id": "18557680289",
        "isDefault": "true",
        "type": "CreditCardMethod",
        "creditCard": {
          "expirationMonth": "6",
          "expirationYear": "2024",
          "displayableNumber": "************1111",
          "type": "visa",
          "displayName": "Visa"
        },
        "address": {
          "id": "333204940289",
          "firstName": "Jane",
          "lastName": "Doe",
          "companyName": "DR",
          "line1": "10380 Bren Rd W",
          "line2": "Conjunto 304",
          "line3": "Conjunto 304",
          "city": "Minnetonka",
          "postalCode": "55343",
          "countrySubdivision": "MN",
          "country": "US",
          "countryName": "United States",
          "phoneNumber": "555-253-1234",
          "emailAddress": "subs_test@digitalriver.com",
          "countyName": "Minnetonka"
        }
      },
      "addOns": []
    },
    "previousAttributes": {
      "autoRenewal": true
    }
  },
  "clientIds": {
    "site_id": "sub2test"
  },
  "searchableData": {
    "subscriptionId": "18023200289"
  }
}
```
{% endcode %}

### Change renewal quantity

When there is a change to the subscription type. Such as changing the subscribed quantity. You will receive a notification when the quantity of purchased or subscribed products has increased or decreased.

{% code title="Webhook request" %}
```json
{
  "type": "subscription.updated",
  "data": {
    "object": {
      "id": "13450199",
      "creationDate": "2022-06-01T06:10:30.000Z",
      "activationDate": "2022-06-01T05:00:00.000Z",
      "nextRenewalDate": "2022-07-01T05:00:00.000Z",
      "expirationDate": "2022-07-01T05:00:00.000Z",
      "graceDate": "2022-07-08T05:00:00.000Z",
      "currentQuantity": 3,
      "renewalQuantity": 6,
      "autoRenewal": false,
      "locale": "en_US",
      "state": "Subscribed",
      "duration": 30,
      "frequency": 30,
      "siteId": "sub2test",
      "shopper": {
        "id": "26195488930199"
      },
      "renewalPrice": {
        "unitPrice": 10.99,
        "locked": false,
        "currency": "USD"
      },
      "term": {
        "termUnit": "MONTHS",
        "termLength": 1
      },
      "product": {
        "id": "5396391700",
        "displayName": "Monthly manual renewal Subscription",
        "sku": "SUB_MANUAL_RENEW"
      },
      "shipToAddress": {
        "id": "406031020199",
        "firstName": "Jane",
        "lastName": "Doe",
        "line1": "minnesota",
        "city": "alabama",
        "postalCode": "99950",
        "countrySubdivision": "CT",
        "country": "US",
        "countryName": "United States",
        "phoneNumber": "5554567898",
        "emailAddress": "subs_test@digitalriver.com"
      },
      "paymentOption": {
        "nickName": "Visa 1111",
        "id": "4022940199",
        "isDefault": "false",
        "type": "CreditCardMethod",
        "creditCard": {
          "expirationMonth": "12",
          "expirationYear": "2036",
          "displayableNumber": "************1111",
          "type": "visa",
          "displayName": "Visa"
        },
        "address": {
          "id": "406031010199",
          "firstName": "Jane",
          "lastName": "Doe",
          "line1": "minnesota",
          "city": "alabama",
          "postalCode": "99950",
          "countrySubdivision": "CT",
          "country": "US",
          "countryName": "United States",
          "phoneNumber": "5554567898",
          "emailAddress": "subs_test@digitalriver.com"
        }
      },
      "addOns": []
    },
    "previousAttributes": {
      "renewalQuantity": 1
    }
  },
  "clientIds": {
    "site_id": "sub2test"
  },
  "searchableData": {
    "subscriptionId": "13450199"
  }
}
```
{% endcode %}

## The subscription trial converted event

When a trial has been automatically or manually converted to a paid subscription, Digital River creates the `subscription.trial_converted` event

{% code title="Webhook request" %}
```json
{
    "type": "subscription.trial_converted",
    "data": {
        "object": {
            "id": "15548700289",
            "creationDate": "2022-03-29T06:58:53.000Z",
            "activationDate": "2022-03-29T05:00:00.000Z",
            "nextRenewalDate": "2023-07-02T05:00:00.000Z",
            "expirationDate": "2023-07-02T05:00:00.000Z",
            "graceDate": "2023-07-09T05:00:00.000Z",
            "currentQuantity": 1,
            "renewalQuantity": 1,
            "autoRenewal": true,
            "locale": "en_US",
            "state": "Subscribed",
            "duration": 365,
            "frequency": 365,
            "siteId": "sub2test",
            "shopper": {
                "id": "504462170289",
                "externalReferenceId": "PBFYTT3GAYPV"
            },
            "renewalPrice": {
                "unitPrice": 15.0,
                "locked": false,
                "currency": "USD"
            },
            "term": {
                "termUnit": "YEARS",
                "termLength": 1
            },
            "product": {
                "id": "5523771400",
                "displayName": "Trial Auto Product - DO NOT EDIT OR MODIFY",
                "sku": "TRIRENREM"
            },
            "shipToAddress": {
                "id": "330009650289",
                "firstName": "Jane",
                "lastName": "Doe",
                "companyName": "DR",
                "line1": "10380 Bren Rd W",
                "line2": "Conjunto 304",
                "line3": "Conjunto 304",
                "city": "Minnetonka",
                "postalCode": "55343",
                "countrySubdivision": "MN",
                "country": "US",
                "countryName": "United States",
                "phoneNumber": "555-253-1234",
                "emailAddress": "subs_test@digitalriver.com",
                "countyName": "Minnetonka"
            },
            "paymentOption": {
                "nickName": "VisaEIB9RB",
                "id": "16063790289",
                "isDefault": "true",
                "type": "CreditCardMethod",
                "creditCard": {
                    "expirationMonth": "3",
                    "expirationYear": "2024",
                    "displayableNumber": "************1111",
                    "type": "visa",
                    "displayName": "Visa"
                },
                "address": {
                    "id": "330113400289",
                    "firstName": "Jane",
                    "lastName": "Doe",
                    "companyName": "DR",
                    "line1": "10380 Bren Rd W",
                    "line2": "Conjunto 304",
                    "line3": "Conjunto 304",
                    "city": "Minnetonka",
                    "postalCode": "55343",
                    "countrySubdivision": "MN",
                    "country": "US",
                    "countryName": "United States",
                    "phoneNumber": "555-253-1234",
                    "emailAddress": "subs_test@digitalriver.com",
                    "countyName": "Minnetonka"
                }
            },
            "addOns": []
        }
    },
    "clientIds":{
      "site_id":"sub2test"
   },
   "searchableData":{
      "subscriptionId":"15548700289"
   }
}
```
{% endcode %}

## The subscription trial renewal reminder event

A specified number of days before a free trial is converted to a paid subscription, Digital River creates the `trial_renewal_reminder` event.&#x20;

{% code title="Webhook request" %}
```json
{   
    "type": "subscription.trial_renewal_reminder",
    "data": {
        "object": {
            "id": "15548710289",
            "creationDate": "2022-03-29T07:01:38.000Z",
            "activationDate": "2022-03-29T05:00:00.000Z",
            "nextRenewalDate": "2022-05-13T05:00:00.000Z",
            "expirationDate": "2022-05-13T05:00:00.000Z",
            "graceDate": "2022-05-13T05:00:00.000Z",
            "currentQuantity": 1,
            "renewalQuantity": 1,
            "autoRenewal": true,
            "locale": "en_US",
            "state": "FreeTrial",
            "duration": 365,
            "frequency": 365,
            "siteId": "sub2test",
            "shopper": {
                "id": "504455410289",
                "externalReferenceId": "XXHMRYHHI10G4"
            },
            "renewalPrice": {
                "unitPrice": 20.0,
                "locked": true,
                "currency": "USD"
            },
            "term": {
                "termUnit": "YEARS",
                "termLength": 1
            },
            "product": {
                "id": "5582478400",
                "displayName": "New Trial Auto Product",
                "sku": "TRIRENREM"
            },
            "shipToAddress": {
                "id": "330009780289",
                "firstName": "Jane",
                "lastName": "Doe",
                "companyName": "DR",
                "line1": "10380 Bren Rd W",
                "line2": "Conjunto 304",
                "line3": "Conjunto 304",
                "city": "Minnetonka",
                "postalCode": "55343",
                "countrySubdivision": "MN",
                "country": "US",
                "countryName": "United States",
                "phoneNumber": "555-253-1234",
                "emailAddress": "subs_test@digitalriver.com",
                "countyName": "Minnetonka"
            },
            "paymentOption": {
                "nickName": "VisaPXYJ9P",
                "id": "16070220289",
                "isDefault": "true",
                "type": "CreditCardMethod",
                "creditCard": {
                    "expirationMonth": "3",
                    "expirationYear": "2024",
                    "displayableNumber": "************1111",
                    "type": "visa",
                    "displayName": "Visa"
                },
                "address": {
                    "id": "330108640289",
                    "firstName": "Jane",
                    "lastName": "Doe",
                    "companyName": "DR",
                    "line1": "10380 Bren Rd W",
                    "line2": "Conjunto 304",
                    "line3": "Conjunto 304",
                    "city": "Minnetonka",
                    "postalCode": "55343",
                    "countrySubdivision": "MN",
                    "country": "US",
                    "countryName": "United States",
                    "phoneNumber": "555-253-1234",
                    "emailAddress": "subs_test@digitalriver.com",
                    "countyName": "Minnetonka"
                }
            },
            "addOns": []
        }
    },
  "clientIds":{
      "site_id":"sub2test"
   },
   "searchableData":{
      "subscriptionId":"15548710289"
   }
}
```
{% endcode %}
