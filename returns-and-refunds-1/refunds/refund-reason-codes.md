---
description: Learn how to use refund reason codes.
---

# Refund reason codes

Reason codes are searchable alphanumeric strings of text that explain the reason for the refund. You can use standard Digital River reason codes or create a custom list of reason codes for this purpose and use the `reason` parameter to display this code in queries and responses.

A shopper can select a reason code that explains why they want a refund for the product. The reason codes in the request must match the reason codes configured for the API consumer’s site. The API consumer can map the description of the reason codes to the values they want to display to a shopper. API consumers can use Digital River's default reason codes or customize the reason codes to meet their specific needs. Contact your Digital River Representative if you want to customize your reason codes.

To view or configure standard Digital River reason codes and customized reason codes for your site, sign in to [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do) and follow the instructions in [How to configure reason codes](https://help.digitalriver.com/help/gc/Administration/Site/Configuring-customer-service-settings.htm#ConfigureReasonCodes) in the [Global Commerce](https://help.digitalriver.com/help/gc.htm) Help.

## Standard refund reason codes

The following refund reason codes are available by default:

| Reason Code                     | Description                                           | Required/Optional |
| ------------------------------- | ----------------------------------------------------- | ----------------- |
| FRAUD                           | Fraud                                                 | Required          |
| MISSING\_ITEMS\_FROM\_ORDER     | Missing Items From Order                              | Required          |
| NEVER\_RECEIVED                 | Never Received                                        | Required          |
| CANCELLED\_BUT\_SHIPPED         | Cancelled But Shipped                                 | Optional          |
| CANT\_DOWNLOAD                  | Cannot Download                                       | Optional          |
| CHARGEBACK\_AVOIDANCE           | DO NOT SELECT - System Initiated Chargeback Avoidance | Optional          |
| CUSTOMER\_ERROR                 | Customer Error                                        | Optional          |
| CUSTOMER\_SATISFACTION\_ISSUE   | Customer Satisfaction Issue                           | Optional          |
| DAMAGED\_PRODUCT                | Damaged Product                                       | Optional          |
| DELAYED\_SHIPPING               | Delayed Shipping                                      | Optional          |
| DUPLICATE\_ORDER                | Duplicate Order                                       | Optional          |
| FEE\_CHARGED\_INCORRECTLY       | Fee Amount Charged Incorrectly                        | Optional          |
| FEE\_EXEMPT\_CUSTOMER           | Fee Exempt Customer                                   | Optional          |
| MATCH\_PROMOTIONAL\_PRICE       | Match Promotional Price                               | Optional          |
| ORDERED\_WITHOUT\_PERMISSION    | Ordered Without Permission                            | Optional          |
| ORDER\_PROCESSING\_ERROR        | Order Processing Error                                | Optional          |
| PHONE\_ORDER\_ERROR             | Phone Order Error                                     | Optional          |
| PRODUCT\_SHOULD\_NOT\_HAVE\_FEE | Product Should Not Have a Fee                         | Optional          |
| PRODUCT\_TRIALWARE              | Trialware                                             | Optional          |
| REFUSED\_ORDER                  | Refused Order                                         | Optional          |
| TAX\_EXEMPT                     | Tax Exempt                                            | Optional          |
| UNABLE\_TO\_SHIP\_TO\_COUNTRY   | Unable To Ship To Country                             | Optional          |
| UNDELIVERABLE\_ADDRESS          | Undeliverable Address                                 | Optional          |
| VENDOR\_APPROVED\_REFUND        | Vendor Approved Refund                                | Optional          |
| WRONG\_PRODUCT                  | Wrong Product                                         | Optional          |
