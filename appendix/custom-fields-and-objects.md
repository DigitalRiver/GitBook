---
description: Learn about customer fields and objects
---

# Custom fields and objects

## Custom objects and custom fields

## Cart (Standard object)

The Cart object represents an online shopping cart in a store with the total amounts for products, shipping and handling, and taxes.

| Standard object | Custom field label        | Description                                                                                                                                                                                                                           |
| --------------- | ------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Cart            | Buyer Email               | Stores the buyer's email address.                                                                                                                                                                                                     |
| Cart            | Buyer Name                | Stores the buyer's name.                                                                                                                                                                                                              |
| Cart            | Buyer Phone               | Stores the buyer's phone number.                                                                                                                                                                                                      |
| Cart            | DR Checkout ID            | Refers to the Digital River checkout identifier.                                                                                                                                                                                      |
| Cart            | DR Checkout Type          | Identifies whether the cart is digital or non-digital.                                                                                                                                                                                |
| Cart            | DR Customer Type          | Indicates the Customer Type stamped on the order.                                                                                                                                                                                     |
| Cart            | DR Payment Session ID     | Stores Digital River's payment session identifier.                                                                                                                                                                                    |
| Cart            | DR Selling Entity         | Refers to Digital River's business selling entity.                                                                                                                                                                                    |
| Cart            | DR Tax Identifiers        | Comma-separated list of Global Tax Identifiers that are applied to this cart.                                                                                                                                                         |
| Cart            | DR Total Duty             | Indicates the total amount of duty levied by the importing country. Add this field to the page layout only if the Landed Costs feature is configured for your site.                                                                   |
| Cart            | DR Total Fees             | Regulatory Fees are collected to address the manufacture, use, recovery, and recycling of Consumer Electronics products throughout the world. Add this field to the page layout only if Regulatory Fees are collected.                |
| Cart            | DR Total IOR Tax          | Represents how much taxes the importer of record remits to the government. Add this field to the page layout only if the Landed Costs feature is configured for your site.                                                            |
| Cart            | Has Landed Cost           | When `True`, indicates the cart has Landed Cost associated with it. When `False`, indicates that the cart does not have Landed Costs. Add this field to the page layout only if the Landed Costs feature is configured for your site. |
| Cart            | Recurring Line Item Count | Indicates the number of recurring line items count in the cart.                                                                                                                                                                       |
| Cart Checkout   | DR Source ID              | Source ID attached to the checkout.                                                                                                                                                                                                   |

## Cart Item (Standard object)

The Cart Item object represents an item in a WebCart that is active in a store built with B2B Commerce on Lightning Experience. The Cart Item can be a product or charge.

| Standard object | Custom field description           | Description                                                                                                                                                                                                                           |
| --------------- | ---------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Cart Item       | DR Duty                            | Indicates the total amount of duty levied by the importing country for this Line Item. Add this field to the page layout only if the Landed Costs feature is configured for your site.                                                |
| Cart Item       | DR IOR Tax                         | Represents how much taxes the importer of record remits to the government for this Line Item. Add this field to the page layout only if the Landed Costs feature is configured for your site.                                         |
| Cart Item       | DR Regulatory Fee                  | Regulatory Fees collected to address the manufacture, use, recovery, and recycling of Consumer Electronics products throughout the world for this Line Item. Add this field to the page layout only if Regulatory Fees are collected. |
| Cart Item       | Price Includes DR Surcharge        | If `True`, indicates that the Total Price field on the Cart Item has Landed Costs and Regulatory Fees included.                                                                                                                       |
| Cart Item       | Total DR Surcharge                 | Total DR Surcharge: Landed Costs + Regulatory Fees.                                                                                                                                                                                   |
| Cart Item       | Total Price Excluding DR Surcharge | Total Price for this Cart Item before adding Landed Costs and Regulatory Fees.                                                                                                                                                        |
| Cart Item       | Recurring Line Item                | If `True`, indicates that the line item contains a subscription product.                                                                                                                                                              |
| Cart Item       | Subscription Id                    | Refers to the shopper's subscription identifier.                                                                                                                                                                                      |
| Cart Item       | Subscription Start Time            | Refers to the subscription's start date and time.                                                                                                                                                                                     |
| Cart Item       | Subscription End Time              | Refers to the subscription start time plus the subscription duration.                                                                                                                                                                 |
| Cart Item       | Free Subscription Trial            | If `True`, indidcates that the item is a free trial.                                                                                                                                                                                  |

## Cart Tax (Standard object)

The Cart Tax represents taxes for a line item in a WebCart that’s active in a store built with B2B Commerce on Lightning Experience.

| Standard object | Custom field label | Description                                                                                                                        |
| --------------- | ------------------ | ---------------------------------------------------------------------------------------------------------------------------------- |
| Card Tax        | DR Duty            | Indicates the amount of duty levied by the importing country for a Line Item.                                                      |
| Card Tax        | DR IOR Tax         | Represents how much taxes the importer of record remits to the government for a Line Item.                                         |
| Card Tax        | DR Regulatory Fee  | Regulatory Fees are collected to address the manufacture, use, recovery, and recycling of Consumer Electronics products worldwide. |

## DCM Application Log  (Custom object)

The DCM Application Log is used to store application logs.

| Custom object       | Custom field label    | Description                                                                          |
| ------------------- | --------------------- | ------------------------------------------------------------------------------------ |
| DCM Application Log | Application Name      | Stores the Application Name.                                                         |
| DCM Application Log | Class Name            | Stores the Class Name.                                                               |
| DCM Application Log | Exception Line Number | Stores the Exception Line Number in which line number error occurred.                |
| DCM Application Log | Exception Message     | Stores the Exception Message.                                                        |
| DCM Application Log | Exception Stack Trace | Stores the Exception Stack Trace.                                                    |
| DCM Application Log | Exception Type        | Stores the Exception Type, such as the list of out-of-bound and call-out exceptions. |
| DCM Application Log | Link to Record        | Stores the link to the Record ID in which an exception has occurred.                 |
| DCM Application Log | Logging Level         | Stores the Logging Level.                                                            |
| DCM Application Log | Message               | Stores an error message.                                                             |
| DCM Application Log | Method Name           | Stores the Method Name.                                                              |
| DCM Application Log | Module Name           | Stores the Module Name.                                                              |
| DCM Application Log | Record ID             | Stores the Record ID.                                                                |
| DCM Application Log | Response Status Code  | Stores the Response Status Code.                                                     |
| DCM Application Log | Running User          | Stores the Running User information.                                                 |
| DCM Application Log | Salesforce Limits     | Stores the Salesforce Limits.                                                        |
| DCM Application Log | User Role & Profile   | Stores the User Role and Profile details.                                            |

## Digital River ECCN Lookup (Custom object)

The Digital River ECCN Lookup object is used to store the ECCN value (such as DR Descriptions and DR Notes) provided by Digital River.

| Custom object             | Custom field label     | Description                                           |
| ------------------------- | ---------------------- | ----------------------------------------------------- |
| Digital River ECCN Lookup | DR Description         | Refers to the Digital River ECCN description.         |
| Digital River ECCN Lookup | DR Notes               | Refers to the Digital River ECCN notes.               |
| Digital River ECCN Lookup | DR Classification Code | Refers to the Digital River ECCN Classification Code. |

## Digital River Failed Event (Custom object)

The Digital River Failed Event contains all the Digital River webhook events that were processed by the app.

| Custom object              | Custom field label   | Description                                                                     |
| -------------------------- | -------------------- | ------------------------------------------------------------------------------- |
| Digital River Failed Event | Event Capture Reason | Stores the reason the event has been stored in Salesforce Lightning.            |
| Digital River Failed Event | Event ID             | Refers to the event's unique identifier.                                        |
| Digital River Failed Event | Event Payload        | Refers to Digital River's webhook event request payload.                        |
| Digital River Failed Event | Event Type           | Refers to Digital River's event type (for example, `order.complete`).           |
| Digital River Failed Event | Processed            | Indicates whether an event is processed successfully after the initial failure. |

## Digital River Fulfillment (Custom object)

The Digital River Fulfillment object contains information related to Digital River.

| Custom object             | Custom field label                     | Description                                                                                                                                                                                   |
| ------------------------- | -------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Digital River Fulfillment | Digital River Fulfillment Status       | Represents the DR Order fulfillment status (for example, Open, Completed, Failed, and Reprocess).                                                                                             |
| Digital River Fulfillment | Digital River Order ID                 | Stores the Digital River order identifier.                                                                                                                                                    |
| Digital River Fulfillment | Digital River Order State              | Identifies the Digital River order state (for example, Accepted, Cancelled, and Fulfilled).                                                                                                   |
| Digital River Fulfillment | Eligible For Fulfillment               | Indicates if the order is eligible for fulfillment. This will be set to `true` when the `order.accepted` event is received by Salesforce.                                                     |
| Digital River Fulfillment | Is Fulfillment Completed               | Indicates if the fulfillment process is completed. This will be set to `true` when the `order.complete` event is received by Salesforce.                                                      |
| Digital River Fulfillment | Message                                | Text field to capture debug information.                                                                                                                                                      |
| Digital River Fulfillment | Order ID                               | Refers to the Salesforce Order ID.                                                                                                                                                            |
| Digital River Fulfillment | Retry Attempts Made                    | Number of attempts made for posting Fulfillment information to Digital River.                                                                                                                 |
| Digital River Fulfillment | Number Of Line Item Records to Process | <p>Count of child Line Item Fulfillment Records available for Fulfillment or Cancellation<br>(for example, Fulfillment Order Item Status is <code>Open</code> or <code>Reprocess</code>).</p> |

## Digital River Line Item Fulfillment (Custom object)

The Digital River Line Item Fulfillment object contains Digital River's line item fulfillment information.

| Custom object                       | Custom field label              | Description                                                                              |
| ----------------------------------- | ------------------------------- | ---------------------------------------------------------------------------------------- |
| Digital River Line Item Fulfillment | Digital River Order Fulfillment | Refers to the Order level fulfillment record.                                            |
| Digital River Line Item Fulfillment | Digital River OrderItem ID      | Refers to Digital River's Order Item Identifier.                                         |
| Digital River Line Item Fulfillment | Fulfillment OrderItem Status    | Refers to the Order Item Fulfillment notification status.                                |
| Digital River Line Item Fulfillment | Message                         | Text field to capture debug information.                                                 |
| Digital River Line Item Fulfillment | Cancel Quantity                 | Refers to the order item quantity to cancel.                                             |
| Digital River Line Item Fulfillment | Fulfill Quantity                | Refers to the order item quantity to fulfill.                                            |
| Digital River Line Item Fulfillment | DR Fulfillment request Log      | Lookup to the Digital River Fulfillment Request log record.                              |
| Digital River Line Item Fulfillment | SF Order Item                   | Lookup to the Salesforce Order Item record.                                              |
| Digital River Line Item Fulfillment | Retry Attempts Made             | Number of attempts made for posting Line Level Fulfillment information to Digital River. |

## Digital River Regulatory Fee (Custom object)

The Digital River Regulatory Fee object is used to store the Regulatory Fee record information.

| Custom object                | Custom field label | Description                                                                                      |
| ---------------------------- | ------------------ | ------------------------------------------------------------------------------------------------ |
| Digital River Regulatory Fee | Amount             | Refers to the unit amount multiplied by the line item quantity (does not include tax).           |
| Digital River Regulatory Fee | Cart Item ID       | Refers to the Salesforce Lighting Cart Item ID in which the regulatory fee record is associated. |
| Digital River Regulatory Fee | Fee ID             | Refers to Digital River's fee unique identifier.                                                 |
| Digital River Regulatory Fee | Fee Type           | Refers to the fee type. Valid values include battery, copyright, ewaste, and packaging.          |
| Digital River Regulatory Fee | Per Unit Amount    | Refers to the fee amount per unit (does not include tax).                                        |

## DR Fulfillment Request Log (Custom object)

The DR Fulfillment Request Log object is used to store the Fulfillment Request Transaction log information from the client application.

| Custom object              | Custom field label | Description                                        |
| -------------------------- | ------------------ | -------------------------------------------------- |
| DR Fulfillment Request Log | Order ID           | Refers to the Salesforce ID.                       |
| DR Fulfillment Request Log | Order Item ID      | Refers to the Salesforce Order Item ID.            |
| DR Fulfillment Request Log | Fulfill Quantity   | Refers to the Order Item Quantity to fulfill.      |
| DR Fulfillment Request Log | Cancel Quantity    | Refers to the Order Item Quantity to cancel.       |
| DR Fulfillment Request Log | DR Order ID        | Refers to the Digital River Order identifier.      |
| DR Fulfillment Request Log | DR Order State     | Refers to the state of the Digital River order.    |
| DR Fulfillment Request Log | DR OrderItem ID    | Refers to the Digital River Order Item identifier. |

## Digital River Tax Mapping (Custom object)

The Digital River Tax Mapping object stores the tax code, product type, tax group, and tax type.

| Custom object             | Custom field label | Description                                                   |
| ------------------------- | ------------------ | ------------------------------------------------------------- |
| Digital River Tax Mapping | DR Product Type    | Indicates whether the cart's tax code is physical or digital. |
| Digital River Tax Mapping | DR Tax Code        | Refers to the Tax Group and Tax Type for the tax code.        |
| Digital River Tax Mapping | DR Tax Group       | Refers to the product's tax group.                            |
| Digital River Tax Mapping | DR Tax Type        | Refers to the product's tax type.                             |

## Digital River Transaction Payment (Custom object)

The Digital River Transaction Payment object stores transaction-related information.

| Custom object                     | Custom field label          | Description                                                                                     |
| --------------------------------- | --------------------------- | ----------------------------------------------------------------------------------------------- |
| Digital River Transaction Payment | Account                     | The user's account that created this transaction payment.                                       |
| Digital River Transaction Payment | Amount                      | Actual transaction amount.                                                                      |
| Digital River Transaction Payment | Card Number                 | Card's last four digits.                                                                        |
| Digital River Transaction Payment | Card Type                   | Card types (for example, Visa, MasterCard, and so on).                                          |
| Digital River Transaction Payment | Contact                     | The user's contact that created this transaction payment.                                       |
| Digital River Transaction Payment | Currency ISO Code           | Currency Code for this transaction (for example, USD or GBP).                                   |
| Digital River Transaction Payment | DR Transaction Payment Name | Refers to the Digital River Transaction Payment Name.                                           |
| Digital River Transaction Payment | Order                       | References the order this payment was applied to.                                               |
| Digital River Transaction Payment | Payment Instructions        | Payment instructions (for example, wire transfers).                                             |
| Digital River Transaction Payment | Payment Method              | The Payment type (for example, Credit Card, PayPal, and so on).                                 |
| Digital River Transaction Payment | Token                       | Tokenized form of the payment.                                                                  |
| Digital River Transaction Payment | Transaction Payment ID      | External ID used for data loading or other access.                                              |
| Digital River Transaction Payment | Transaction Type            | Transaction type, for example, `AUTH`, `CAPTURE`, or `AUTH+CAPTURE`. This is provider-specific. |
| Digital River Transaction Payment | User                        | The user who created this transaction payment.                                                  |

## Order (Standard object)

The Order object represents an order associated with a contract or an account.&#x20;

| Standard object | Custom field label            | Description                                                                                                                                                                                                                              |
| --------------- | ----------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Order           | DR Order ID                   | Refers to the Digital River order identifier.                                                                                                                                                                                            |
| Order           | DR Order State                | Refers to the Digital River Order State.                                                                                                                                                                                                 |
| Order           | DR Total Duty                 | Indicates the total amount of duty levied by the importing country. Add this field to the page layout only if the Landed Costs feature is configured for your site.                                                                      |
| Order           | DR Total IOR Tax              | Represents how much tax the importer of record remits to the government. Add this field to the page layout only if the Landed Costs feature is configured for your site.                                                                 |
| Order           | DR Total Regulatory Fee       | Regulatory Fees collected to address the manufacture, use, recovery, and recycling of Consumer Electronics products worldwide. Add this field to the page layout only if Regulatory Fees are collected.                                  |
| Order           | Has Landed Cost               | When `True`, indicates the Order has Landed Costs associated with it. When `False`, indicates that the Order does not have Landed Costs. Add this field to the page layout only if the Landed Costs feature is configured for your site. |
| Order           | DR Payment Status             | The state of the Digital River payment. Valid values are `Successful` and `Declined`.                                                                                                                                                    |
| Order           | DR Payment Failure Reason     | The reason for Digital River payment failure.                                                                                                                                                                                            |
| Order           | DR Selling Entity             | The Digital River Business Selling Entity.                                                                                                                                                                                               |
| Order           | Digital River Customer Type   | Indicates the Customer Type stamped on the order.                                                                                                                                                                                        |
| Order           | Digital River Fraud State     | Refers to the Digital River Fraud State.                                                                                                                                                                                                 |
| Order           | Digital River Tax Identifiers | Comma-separated list of Global Tax Identifiers that are applied to this order.                                                                                                                                                           |
| Order           | SF Order Failure Reason       | Indicates the Salesforce order failure reason.                                                                                                                                                                                           |
| Order           | Recurring Line Item Count     | Indicates the number of recurring line items in the order.                                                                                                                                                                               |

Add the **Refunds Action** button to the **Order** page layout. This will be available under **Salesforce Mobile and Lightning Experience Actions** section.

![](<../.gitbook/assets/Refunds 1.png>)

## Order Product (Standard object)

The Order Product object represents the product line items in the order.

| Standard object | Custom field label                 | Description                                                                                                                                                                                                                            |
| --------------- | ---------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Order Product   | Digital River Order Item State     | The state of the Digital River order item.                                                                                                                                                                                             |
| Order Product   | DR Duty                            | Indicates the total amount of duty levied by the importing country for this Line Item. Add this field to the page layout only if the Landed Costs feature is configured for your site.                                                 |
| Order Product   | DR IOR Tax                         | Represents how much taxes the importer of record remits to the government for this Line Item. Add this field to the page layout only if the Landed Costs feature is configured for your site.                                          |
| Order Product   | DR Order Item ID                   | The Digital River order item identifier.                                                                                                                                                                                               |
| Order Product   | DR Regulatory Fee                  | Regulatory Fees collected to address the manufacture, use, recovery, and recycling of Consumer Electronics products throughout the world for this Order Item. Add this field to the page layout only if Regulatory Fees are collected. |
| Order Product   | DR Fulfilled Quantity              | Refers to the Fulfilled Line-Item Quantity.                                                                                                                                                                                            |
| Order Product   | DR Cancelled Quantity              | Refers to the Cancelled Line-Item Quantity.                                                                                                                                                                                            |
| Order Product   | Digital River Billing Agreement Id | Refers to the Digital River Billing Agreement ID used during recurring payment processing.                                                                                                                                             |
| Order Product   | Subscription Id                    | Refers to the shopper's subscription identifier.                                                                                                                                                                                       |

## Product (Standard object)

The Product object represents a product that your organization sells. See [Step 8: Configure and synchronize the products](../integrate-the-salesforce-lightning-app/step-8-configure-and-synchronize-the-products.md) for more information.

| Standard object | Custom field label          | Description                                                                                                                     |
| --------------- | --------------------------- | ------------------------------------------------------------------------------------------------------------------------------- |
| Product         | Date Last Synced to DR      | Refers to the date when the product was last synced to Digital River.                                                           |
| Product         | DR ECCN\*                   | Refers to the ECCN code assigned to the product.                                                                                |
| Product         | DR HS Code                  | Stores the Landed cost/Harmonized System Code.                                                                                  |
| Product         | DR Part Number              | Stores the Digital River part number.                                                                                           |
| Product         | DR Product Country Origin\* | Describes the product's Country of Origin, which is a two-letter country code described in the ISO 3166 International Standard. |
| Product         | DR TAXGROUP \*              | Refers to the product's tax group.                                                                                              |
| Product         | DR TAXTYPE\*                | Refers to the product’s tax type.                                                                                               |
| Product         | Sync Product to DR          | Indicates whether a product needs to be synced to Digital River.                                                                |
