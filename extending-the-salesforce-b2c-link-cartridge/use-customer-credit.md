---
description: Learn how to use the Digital River Customer Credit extension.
---

# Use Customer Credit

## Understand the Customer Credit feature

You use Digital River's customer credit feature to enable a number of different storefront customer credit functionalities such as gift certificates and rewards points.

The SFCC platform does not natively support gift cards or store credit functionality. This functionality is provided instead by 3rd party integrations. Rather than integrating directly with these 3rd party options, use the Digital River customer credit cartridge to provide several functions that make the necessary calls to Digital River to support this functionality. The back-end implementation of the customer credit functionality is provided by the `int_digitalriver_customercredit`cartridge.

You are responsible at the time of implementation to code necessary changes to the Customer Credit feature for your use case. You do this to call the functions provided by the DR cartridge that is needed to connect to your 3rd party integration.

Read the information in this section to learn how the Customer Credit cartridge supports the customer credit feature. Use the suggested customization steps to integrate the customer credit feature for enablement in specific use cases.

## Configure the Business Manager settings

In the following example of the cartridge customer credit functionality, the GIFT\_CERTIFICATE payment method and the BASIC\_CUSTOMER\_CREDIT payment processor on the SFCC side are being used.&#x20;

If you use the customer credit cartridge as demonstrated in this example, first make sure that the specified payment method and payment processor are set for the customer's site.

Use the information that follows to set up the integration of the customer credit feature with an example payment method.

{% hint style="info" %}
**Note**: If using the cartridge for integration with other customer credit use cases, make sure you apply the appropriate method/processor configuration to meet the use case.
{% endhint %}

### Configure the payment method and processor

First, use the following steps to configure the payment method and processor in the Business Manager.

In the Business Manager, go to **Merchant Tools > Ordering > Payment Processors** and ensure the BASIC\_CUSTOMER\_CREDIT payment processor is present.  If using a different payment processor, complete this step according to the use case.

![](<../.gitbook/assets/image (5).png>)

Next, go to **Merchant Tools > Ordering > Payment Methods** in the Business Manager and ensure the GIFT\_CERTIFICATE payment method is present and enabled. If using a different payment method, complete this step according to the use case. The BASIC\_CUSTOMER\_CREDIT payment processor is selected for this payment method. Select the payment processor from the previous step.

![](<../.gitbook/assets/image (25).png>)

### Use the controller endpoints

{% hint style="info" %}
**Note:** All line numbers referred to in the following code samples and example screenshots are relative.  For the location of the code changes being discussed, refer to the highlighted areas in the screenshots that are isolated with a green or red border around the code.
{% endhint %}

Digital River provides three controllers in the cartridge to integrate the backend part of the customer credit feature. These are the following:&#x20;

* ``[`DigitalRiver-AddCustomerCredit`](use-customer-credit.md#digitalriver-addcustomercredit-controller)``
* ``[`DigitalRiver-RemoveCustomerCredit`](use-customer-credit.md#digitalriver-removecustomercredit-controller)``
* ``[`DigitalRiver-CustomerCredits`](use-customer-credit.md#digitalriver-customercredits-controller)``

Use these controllers to integrate customer credit functionality into your storefront. Read the next sections to understand each controller and how it is used.

### **DigitalRiver-AddCustomerCredit controller**

Use this controller to make an API call to Digital River to create a customer credit source, attach the source to the current checkout, and add a customer credit to the current basket as a GIFT\_CERTIFICATE payment method.&#x20;

Modify the code as shown in the screenshot below to create a new payment instrument for customer credit depending on your implementation of secondary payments.&#x20;

**Script path**: `int_digitalriver_customercredit/cartridge/controllers/DigitalRiver.js`

```
customerCreditPI = currentBasket.createGiftCertificatePaymentInstrument('customer_credit_code', new Money(customerCreditAmount, currentBasket.getCurrencyCode()));
```

![](<../.gitbook/assets/image (12).png>)

_Request type:_ **POST**

_Request body schema:_ `application/json`

| Parameter             | Type              | Description            |
| --------------------- | ----------------- | ---------------------- |
| customerCredit Amount | String. Required. | Customer credit value. |
| primarySourceId       | String. Optional. | Primary source ID.     |
|                       |                   |                        |

#### Request example:

```
{
    "customerCreditAmount ": 10,
    "primarySourceId": "3cfd3746d-9b3a-4cb2-bcaa-g1476348h76a"
}

```

It is expected that the `customerCreditAmount` parameter should be less than or equal to the `amountRemainingToBeContributed` value on the checkout. The value of the `customerCreditAmount` is checked to ensure that the amount matches the criteria before making a request. In the case where an amount greater is sent, a response with the error message will be received.

Pass the `primarySourceId` parameter in case the primary source is already attached to the checkout.

Prior to calling the `DigitalRiver-AddCustomerCredit` controller, make a call to the `DigitalRiver-CustomerCredits` controller and obtain `amountRemainingToBeContributed` and `primarySourceId` from the response.

#### &#x20;Successful response example:

The following is an example of a response you might receive after a successful call:

```
{
  "action": "DigitalRiver-AddCustomerCredit",
  "queryString": "",
  "locale": "en_US",
  "success": true,
  "customerCreditSources": [
    {
      "id": "9ced946c-9c5a-4bb7-bddb-e1976368b71e",
      "type": "customerCredit",
      "amount": 10,
      "owner": {
        "firstName": "My_first_name",
        "lastName": "My_last_name",
        "email": "test@test.net",
        "address": {
          "line1": "1 Wall St billing l1",
          "city": "New York",
          "postalCode": "10004",
          "state": "NY",
          "country": "US"
        }
      },
      "customerCredit": {},
      "formatted": "$10.00"
    },
    {
      "id": "3ed7a503-8f13-4a78-81f2-6ad749dd99a5",
      "type": "customerCredit",
      "amount": 5,
      "owner": {
        "firstName": "My_first_name",
        "lastName": "My_last_name",
        "email": "test@test.net",
        "address": {
          "line1": "1 Wall St billing l1",
          "city": "New York",
          "postalCode": "10004",
          "state": "NY",
          "country": "US"
        }
      },
      "customerCredit": {},
      "formatted": "$5.00"
    }

  ],
  "adjustedGrandTotal": {
    "value": 74.11,
    "formatted": "$74.11",
    "customerCreditTotal": {
      "value": 15,
      "formatted": "$15.00"
    }
  },
  "amountRemainingToBeContributed": 74.11
}
```

_Response body schema:_ `application/json`

| Parameter                      | Description                                                                                | Type    |
| ------------------------------ | ------------------------------------------------------------------------------------------ | ------- |
| success                        | Customer Credit Source created successfully.                                               | Boolean |
| customerCreditSources          | Array of Customer Credit sources that are applied to the checkout.                         | Array.  |
| **adjustedGrandTotal**         |                                                                                            | Object. |
|          _value_               | Basket total value minus customer credit value.                                            | Number. |
|          _formatted_           | Basket total value minus customer credit value in the format of the current site currency. | String. |
| **customerCreditTotal**        |                                                                                            | Object. |
|          _value_               | The sum of all Customer Credit values.                                                     | Number. |
|          _formatted_           | The sum of all Customer Credit values in the format of the current site currency.          | String. |
| amountRemainingToBeContributed | Represents the amount needed to fully fund the transaction.                                | Number. |

#### Error response examples

The following examples show error responses you may receive after an unsuccessful call.

_Invalid credit amount_ - The following is an example of an error response for an unsuccessful call involving an invalid customer credit amount.

_Status:_ Error occurred due to an invalid customer credit amount.

_Response body schema:_ `application/json`

```
{
  "action": "DigitalRiver-AddCustomerCredit",
  "queryString": "",
  "locale": "en_US",
  "error": true,
  "errorMessage": "Invalid customer credit amount"
}


```

_Credit source creation unsuccessful_ - The following example shows an error due to an unsuccessful attempt to create a Customer Credit Source.

_Status:_ An error occurred creating a Customer Credit Source. The creation is unsuccessful.&#x20;

_Response body schema:_ `application/json`

```
{
  "action": "DigitalRiver-AddCustomerCredit",
  "queryString": "",
  "locale": "en_US",
  "error": true,
  "errorMessage": “There was a problem adding customer credit source”
}
```

The following parameters describe the response schema for errors

| Parameter    | Description                                                                                                                                                                                                               | Type     |
| ------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- |
| error: true  | Customer Credit Source created successfully.                                                                                                                                                                              | Boolean. |
| errorMessage | <p>Error message.<br><br><strong>Note:</strong> The error message returned is meant for display to the shopper. A more detailed technical error message can be located in the cartridge logs in the Business Manager.</p> | String.  |

### **DigitalRiver-RemoveCustomerCredit controller**

Use this controller to delete the customer credit source from the current checkout and remove the customer credit from the current basket.

**Script path**: `int_digitalriver_customercredit\cartridge\controllers\DigitalRiver.js`

_Request type:_ **POST**

_Request body schema:_ `application/json`

| Parameter | Description                                            | Type    |
| --------- | ------------------------------------------------------ | ------- |
| sourceID  | Source ID of the customer credit source to be removed. | String. |

#### Request example:

```
{
    “sourceId”: “9ced946c-9c5a-4bb7-bddb-e1976368b71e”  
}

```

#### Successful response example:

The following example shows a response you might receive for a successful `RemoveCustomerCredit` POST call.

```
{
  "action": "DigitalRiver-RemoveCustomerCredit",
  "queryString": "",
  "locale": "en_US",
  "success": true,
  "customerCreditSources": [],
  "adjustedGrandTotal": {
    "value": 89.11,
    "formatted": "$89.11",
    "customerCreditTotal": {
      "value": 0,
      "formatted": "$0.00"
    }
  },
  "amountRemainingToBeContributed": 89.11
}
```

_Status:_ Customer Credit Source removed successfully.

_Response body schema:_ `application/json`

| Parameter                      | Description                                                                                                                                                                                                                 | Type     |
| ------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- |
| success                        | Customer Credit Source removed successfully.                                                                                                                                                                                | Boolean. |
| customerCreditSources          | <p>Array of Customer Credit sources that are applied to the checkout after the <code>sourceId</code> from the request is removed.</p><p>If no customer credit sources remain on the checkout, this array will be empty.</p> | Array.   |
| **adjustedGrandTotal**         |                                                                                                                                                                                                                             | Object   |
|         _value_                | Basket total value minus customer credit value.                                                                                                                                                                             | Number.  |
|         _formatted_            | Basket total value minus customer credit value in the format of the current site currency.                                                                                                                                  | String.  |
| **customerCreditTotal**        |                                                                                                                                                                                                                             | Object.  |
|        _value_                 | The sum of all Customer Credit values.                                                                                                                                                                                      | Number.  |
|        _formatted_             | The sum of all Customer Credit values in the format of the current site currency.                                                                                                                                           | String.  |
| amountRemainingToBeContributed | Represents the amount needed to fully fund the transaction.                                                                                                                                                                 | Number.  |

#### Error response example:

The following example shows a response if an error occurs removing a Customer Credit source.

```
{
  "action": "DigitalRiver-RemoveCustomerCredit",
  "queryString": "",
  "locale": "en_US",
  "error": true,
  "errorMessage": “There was a problem removing customer credit source”
}
```

_Status:_ Error occurred removing a Customer Credit Source.

_Response body schema:_ `application/json`

| Parameter    | Description and Type                                                                                                                                                                                                      | Type    |
| ------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------- |
| error        | Attempt to remove a Customer Credit Source is unsuccessful.                                                                                                                                                               | Boolean |
| errorMessage | <p>Error message.<br><br><strong>Note:</strong> The error message returned is meant for display to the shopper. A more detailed technical error message can be located in the cartridge logs in the Business Manager.</p> | String. |

### **DigitalRiver-CustomerCredits controller**

Use this controller to retrieve actual information about already applied customer credit sources, primary sources, and some total amounts. For example, you could use this controller to get information before adding new customer credit sources.

_Request type:_ **GET**

_Request body schema:_ `application/json`

There are no request parameters required as SFCC automatically tracks the current cart object which has all the information needed to execute the request.

**Request example:** There are no parameters for this request so an example would consist of an empty payload

#### Successful response example:

The following example shows a response you might receive for a successful CustomerCredits GET call.

```
{
  "action": "DigitalRiver-CustomerCredits",
  "queryString": "",
  "locale": "en_US",
  "success": true,
  "customerCreditSources": [
    {
      "id": "81aa2c77-4108-466d-aa0f-11bf382b861f",
      "type": "customerCredit",
      "amount": 10,
      "owner": {
        "firstName": "My_first_name",
        "lastName": "My_last_name",
        "email": "tmsdfsd@ukr.net",
        "address": {
          "line1": "1 Wall St billing l1",
          "city": "New York",
          "postalCode": "10004",
          "state": "NY",
          "country": "US"
        }
      },
      "customerCredit": {},
      "formatted": "$10.00"
    },
    {
      "id": "3ed7a503-8f13-4a78-81f2-6ad749dd99a5",
      "type": "customerCredit",
      "amount": 5,
      "owner": {
        "firstName": "My_first_name",
        "lastName": "My_last_name",
        "email": "tmsdfsd@ukr.net",
        "address": {
          "line1": "1 Wall St billing l1",
          "city": "New York",
          "postalCode": "10004",
          "state": "NY",
          "country": "US"
        }
      },
      "customerCredit": {},
      "formatted": "$5.00"
    }

  ],
  "adjustedGrandTotal": {
    "value": 54.11,
    "formatted": "$54.11",
    "customerCreditTotal": {
      "value": 15,
      "formatted": "$15.00"
    }
  },
  "primarySourceId": "83hh7c67-4207-455d-aa3a-94fo349k136s"
  "amountRemainingToBeContributed": 54.11
}
```

_Status:_ Customer Credits information has been retrieved successfully.

_Response body schema:_ `application/json`

| Parameter                         | Description                                                                                                                                                                                                  | Type     |
| --------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------- |
| success                           | Customer Credit information retrieved successfully. Boolean.                                                                                                                                                 | Boolean. |
| customerCreditSources             | Array of Customer Credit sources that are applied to the checkout.                                                                                                                                           | Array.   |
| **adjustedGrandTotal**            |                                                                                                                                                                                                              | Object.  |
|          _value_                  | Basket total value minus customer credit value.                                                                                                                                                              | Number.  |
|          _formatted_              | Basket total value minus customer credit value in the format of the current site currency.                                                                                                                   | String.  |
|           **customerCreditTotal** |                                                                                                                                                                                                              | Object   |
|                 _value_           | The sum of all Customer Credit values. Number.                                                                                                                                                               | Number.  |
|                 _formatted_       | The sum of all Customer Credit values in the format of the current site currency.                                                                                                                            | String.  |
| primarySourceId                   | <p>Unique identifier for the primary source (non-customer credit) that is already applied to the checkout. </p><p></p><p>If no primary source has been applied to the checkout this value will be empty.</p> | String.  |
| amountRemainingToBeContributed    | Represents the amount needed to fully fund the transaction.                                                                                                                                                  | Number.  |

#### Error response example:

The following example shows a response you might receive if an error occurs retrieving CustomerCredits information.

```
{
  "action": "DigitalRiver-CustomerCredits",
  "queryString": "",
  "locale": "en_US",
  "error": true,
  "errorMessage": “Failed to load customer credit sources”
}
```

_Status:_ Error occurred retrieving CustomerCredits information.

_Response body schema:_ `application/json`

| Parameter    | Description                                                                                        | Type     |
| ------------ | -------------------------------------------------------------------------------------------------- | -------- |
| error        | Attempt to retrieve CustomerCredits information and load customer credit sources was unsuccessful. | Boolean. |
| errorMessage | Error message.                                                                                     | String.  |
