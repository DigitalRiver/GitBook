---
description: Learn how to use return reason codes.
---

# Return reason codes

Reason codes are searchable alphanumeric text strings that explain the return's reason. You can use standard Digital River reason codes or create a custom list of reason codes for this purpose and use the `reason` parameter to display this code in queries and responses.

A shopper can select a reason code explaining why they return a product. The reason codes in the request must match the codes configured for the API consumer's site. The API consumer can map the description of the reason codes to the values they want to display to a shopper. API consumers can use Digital River's default reason codes or customize them to meet their needs. Contact your Digital River Representative if you want to customize your reason codes.

To view or configure standard Digital River reason codes and customized reason codes for your site, sign in to [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do) and follow the instructions in [How to configure reason codes](https://help.digitalriver.com/help/gc/Administration/Site/Configuring-customer-service-settings.htm#ConfigureReasonCodes) in the [Global Commerce](https://help.digitalriver.com/help/gc.htm) Help.

{% hint style="info" %}
**Note**: Only Customer Service Configuration Managers can configure the reason codes.
{% endhint %}

## Standard return reason codes

The following return reason codes are available by default:

<table><thead><tr><th width="291.3333333333333">Reason Code</th><th width="265">Description</th><th>Required/Optional</th></tr></thead><tbody><tr><td>FRAUD</td><td>Fraud</td><td>Required</td></tr><tr><td>MISSING_ITEMS_FROM_ORDER</td><td>Missing Items From Order</td><td>Required</td></tr><tr><td>NEVER_RECEIVED</td><td>Never Received</td><td>Required</td></tr><tr><td>CANCELLED_BUT_SHIPPED</td><td>Cancelled But Shipped</td><td>Optional</td></tr><tr><td>CANT_DOWNLOAD</td><td>Cannot Download</td><td>Optional</td></tr><tr><td>CHARGEBACK_AVOIDANCE</td><td>DO NOT SELECT - System Initiated Chargeback Avoidance</td><td>Optional</td></tr><tr><td>CUSTOMER_ERROR</td><td>Customer Error</td><td>Optional</td></tr><tr><td>CUSTOMER_SATISFACTION_ISSUE</td><td>Customer Satisfaction Issue</td><td>Optional</td></tr><tr><td>DAMAGED_PRODUCT</td><td>Damaged Product</td><td>Optional</td></tr><tr><td>DELAYED_SHIPPING</td><td>Delayed Shipping</td><td>Optional</td></tr><tr><td>DUPLICATE_ORDER</td><td>Duplicate Order</td><td>Optional</td></tr><tr><td>FEE_CHARGED_INCORRECTLY</td><td>Fee Amount Charged Incorrectly</td><td>Optional</td></tr><tr><td>FEE_EXEMPT_CUSTOMER</td><td>Fee Exempt Customer</td><td>Optional</td></tr><tr><td>MATCH_PROMOTIONAL_PRICE</td><td>Match Promotional Price</td><td>Optional</td></tr><tr><td>ORDERED_WITHOUT_PERMISSION</td><td>Ordered Without Permission</td><td>Optional</td></tr><tr><td>ORDER_PROCESSING_ERROR</td><td>Order Processing Error</td><td>Optional</td></tr><tr><td>PHONE_ORDER_ERROR</td><td>Phone Order Error</td><td>Optional</td></tr><tr><td>PRODUCT_SHOULD_NOT_HAVE_FEE</td><td>Product Should Not Have a Fee</td><td>Optional</td></tr><tr><td>PRODUCT_TRIALWARE</td><td>Trialware</td><td>Optional</td></tr><tr><td>REFUSED_ORDER</td><td>Refused Order</td><td>Optional</td></tr><tr><td>TAX_EXEMPT</td><td>Tax Exempt</td><td>Optional</td></tr><tr><td>UNABLE_TO_SHIP_TO_COUNTRY</td><td>Unable To Ship To Country</td><td>Optional</td></tr><tr><td>UNDELIVERABLE_ADDRESS</td><td>Undeliverable Address</td><td>Optional</td></tr><tr><td>VENDOR_APPROVED_REFUND</td><td>Vendor Approved Refund</td><td>Optional</td></tr><tr><td>WRONG_PRODUCT</td><td>Wrong Product</td><td>Optional</td></tr></tbody></table>
