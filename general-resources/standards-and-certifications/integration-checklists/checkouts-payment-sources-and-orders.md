---
description: >-
  Learn more about the standards related to processing checkouts, payment
  sources, and orders.
---

# Checkouts, payment sources, and orders

The [checklist items](checkouts-payment-sources-and-orders.md#integration-checklist) and standards in this section cover how to process [MOR/SOR](../../glossary.md#merchant-of-record-seller-of-record-mor-sor) compliant checkouts, subscriptions, payment sources, and orders.

## Integration checklist

Click any checklist item to be provided more information on how to meet the [checkouts](checkouts-payment-sources-and-orders.md#checkouts), [payment sources](checkouts-payment-sources-and-orders.md#payment-sources), and [orders](checkouts-payment-sources-and-orders.md#orders)-related integration standard.

### Checkouts

* [ ] [In `POST/checkouts` requests, does your integration provide us the required product data?](checkouts-payment-sources-and-orders.md#provide-required-product-information)
* [ ] [In `POST/checkouts` requests, does your integration provide us the required compliance product data?](checkouts-payment-sources-and-orders.md#provide-required-compliance-product-data)
* [ ] [If you're sending `productDetails` in create checkout requests, does your integration pass your system's unique product identifier as the object's `id`?](checkouts-payment-sources-and-orders.md#reference-product-identifier-in-product-details)
* [ ] [If you're sending `productDetails` in create checkout requests, does your integration reference the associated SKU group by specifying a skuGroupId?](checkouts-payment-sources-and-orders.md#reference-required-sku-group-in-product-details)
* [ ] [Do you use the `taxInclusive` flag to indicate whether the total cost of an order's items should be treated as tax inclusive or exclusive?](checkouts-payment-sources-and-orders.md#indicate-whether-taxes-are-included-in-the-retail-price)
* [ ] [Does your integration provide the customer's public IP address?](checkouts-payment-sources-and-orders.md#provide-the-customers-public-ip-address)
* [ ] [Do you use your commerce platform's unique order identifier (UUID) as the upstream identifier?](checkouts-payment-sources-and-orders.md#ensure-the-specified-upstream-identifier-matches-your-order-identifier)
* [ ] [For order's that contain physical products, do you specify `shipTo` and `shipFrom` values?](checkouts-payment-sources-and-orders.md#supply-required-shipping-address-information)
* [ ] [After Digital River responds to a create or update checkout request, does your integration use the data provided by Digital River to update the commerce system's product and shipping tax data and then ensure that the values in both systems match?](checkouts-payment-sources-and-orders.md#synchronize-checkout-data)

#### Checkouts with subscriptions

* [ ] [During subscription acquisitions, do you set the charge type to customer-initiated?](checkouts-payment-sources-and-orders.md#set-charge-type-to-customer-initiated-in-subscription-acquisitions)
* [ ] [When auto-renewing a subscription, do you set the charge type to merchant-initiated?](checkouts-payment-sources-and-orders.md#set-charge-type-to-merchant-initiated-in-subscription-auto-renewals)
* [ ] [For every subscription product or service included in a transaction, do you send subscription information?](checkouts-payment-sources-and-orders.md#send-subscription-information)
* [ ] [After the customer accepts the terms of an auto-renewing subscription, do you pass them to Digital River?](checkouts-payment-sources-and-orders.md#send-the-subscriptions-terms)
* [ ] [During the acquisition process, does your subscription management system generate a subscription identifier?](checkouts-payment-sources-and-orders.md#generate-a-subscription-identifier)
* [ ] [Do you specify a subscription's renewal method?](checkouts-payment-sources-and-orders.md#specify-a-subscriptions-renewal-method)
* [ ] [During the renewal process, do you send the same billing agreement identifier generated during the subscription's acquisition?](checkouts-payment-sources-and-orders.md#send-the-billing-agreement-identifier-in-renewals)
* [ ] [If a customer pays for a subscription with Klarna, do you provide the start and end time?](checkouts-payment-sources-and-orders.md#provide-a-start-and-end-time-for-klarna-funded-subscriptions)

### Payment sources

* [ ] [Do you use Drop-in payments to display available payment methods and create a payment source?](checkouts-payment-sources-and-orders.md#use-drop-in-to-create-payment-sources)
* [ ] [Do you provide customers the option to save payment information for future use?](checkouts-payment-sources-and-orders.md#provide-option-to-save-credit-card-for-future-use)
* [ ] [During transaction flows, if customers elect to save payment information for future purchases, do you save the source to their account?](checkouts-payment-sources-and-orders.md#save-ready-for-storage-payment-sources-to-the-customers-account)
* [ ] [Does the `onSuccess` event fired by Drop-in payments trigger a final step in your checkout process that allows the customer to review all order and tax totals before making the purchase?](checkouts-payment-sources-and-orders.md#respond-to-on-success-events-and-display-the-order-review-page)

#### Payment sources with subscriptions

* [ ] [When customers are acquiring an auto-renewing subscription, does Drop-in payments only display payment methods that support reusability?](checkouts-payment-sources-and-orders.md#display-reusable-payment-sources)
* [ ] [Do you configure Drop-in payments to display and acquire the customer's acceptance of the combined subscription and payment storage terms?](checkouts-payment-sources-and-orders.md#acquire-customers-acceptance-of-subscription-and-payment-storage-terms)
* [ ] [Do you save ready for storage payment sources to a customer's account?](checkouts-payment-sources-and-orders.md#save-ready-for-storage-source-to-customers-account)

### Orders

* [ ] [After a customer places an order on the storefront, do you pass the checkout identifier to a `POST/orders` request?](checkouts-payment-sources-and-orders.md#create-an-order-with-the-checkout-identifier)
* [ ] [Do you use the `POST/orders` response to update the storefront's UI with an order success or order failed message?](checkouts-payment-sources-and-orders.md#notify-the-customer-of-the-order-status)
* [ ] [Do you use the `POST/orders` response to set the order status in your upstream commerce platform?](checkouts-payment-sources-and-orders.md#align-order-states)
* [ ] [Do you capture the order's identifier?](checkouts-payment-sources-and-orders.md#capture-the-orders-identifier)
* [ ] [Do you capture the order's payment status?](checkouts-payment-sources-and-orders.md#capture-the-orders-payment-state)
* [ ] [Do you capture the order's fraud status?](checkouts-payment-sources-and-orders.md#capture-the-orders-fraud-state)
* [ ] [Do you listen for and handle the order accepted event?](checkouts-payment-sources-and-orders.md#listen-for-and-handle-the-order-accepted-event)
* [ ] [Do you listen for and handle order failed events?](checkouts-payment-sources-and-orders.md#consume-the-event-emitted-when-an-order-fails)

#### Orders with subscriptions

* [ ] [For auto-renewing subscriptions, do you persist the billing agreement identifier generated during the acquisition process?](checkouts-payment-sources-and-orders.md#persist-the-billing-agreement-identifier)

## Integration standards

The checkout, payment source, and order standards that apply to your integration are dependent on which of the above checklists you're using.

### Provide required product data <a href="#provide-required-product-information" id="provide-required-product-information"></a>

When [sending product data in create checkout requests](../../../integration-options/checkouts/creating-checkouts/describing-the-items/#sending-product-data) each [`items[]`](../../../integration-options/checkouts/creating-checkouts/describing-the-items/) must include a [SKU ](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SKUs)identifier or a [`productDetails`](../../../product-management/skus.md#product-details) object. Each line item in the request must also have a defined [price or aggregate price](../../../integration-options/checkouts/creating-checkouts/describing-the-items/price-of-an-item.md), as well as a [quantity](../../../integration-options/checkouts/creating-checkouts/describing-the-items/#creating-items).

### Provide required compliance product data

When [associating SKU groups with upstream product data in create checkout requests](../../../integration-options/checkouts/creating-checkouts/describing-the-items/#send-basic-data-in-product-details-and-compliance-data-in-sku-groups) each [`items[]`](../../../integration-options/checkouts/creating-checkouts/describing-the-items/) must include `productDetails` and within that object you must specify a `skuGroupId`.

### Reference product identifier in product details

If you're sending [`productDetails`](../../../product-management/using-product-details.md) in [create checkout requests](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createCheckouts), your integration should pass your system's unique product identifier as the object's `id`.

For more information, refer to the [sending product data in checkouts](../../../integration-options/checkouts/creating-checkouts/describing-the-items/#sending-product-data) section on the [Describing line items page](../../../integration-options/checkouts/creating-checkouts/describing-the-items/).

### Reference required SKU group in product details

If you're sending [`productDetails`](../../../product-management/using-product-details.md) in [create checkout requests](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createCheckouts), your integration must reference the product's associated [SKU group](../../../product-management/setting-up-sku-groups.md). You do this by specifying a `skuGroupId` in the `productDetails` object.

For more information, refer to the [sending product data in checkouts](../../../integration-options/checkouts/creating-checkouts/describing-the-items/#sending-product-data) section on the [Describing line items page](../../../integration-options/checkouts/creating-checkouts/describing-the-items/).

### Indicate whether taxes are included in the retail price

When [building a checkout](../../../integration-options/checkouts/creating-checkouts/), use the `taxInclusive` flag to indicate whether the [price of items](../../../integration-options/checkouts/creating-checkouts/describing-the-items/price-of-an-item.md) in an order should be treated as [tax inclusive or exclusive](../../../integration-options/checkouts/creating-checkouts/configuring-taxes.md#setting-tax-inclusive-prices).

### Provide the customer's public IP address

When [building a checkout](../../../integration-options/checkouts/creating-checkouts/), provide the [IP address of the browser](broken-reference) being used by the customer to place the order.

### Ensure the specified upstream identifier matches your order identifier

For tracking purposes, specify an [upstream identifier](broken-reference) during the [checkout process](../../../integration-options/checkouts/creating-checkouts/) that matches the identifier of the corresponding order in your commerce platform.

### Supply required shipping address information

Orders that contain [physical products](../../../product-management/creating-and-updating-skus.md#how-products-are-specified-as-physical-or-digital) must provide [ship from](../../../integration-options/checkouts/creating-checkouts/providing-address-information.md#ship-from-requirements) and [ship to](../../../integration-options/checkouts/creating-checkouts/providing-address-information.md#ship-to-requirements) address information.

### Synchronize checkout data

Each time you create or update a checkout, [use the response from the Checkouts API](../../../integration-options/checkouts/creating-checkouts/) to update price, fee, and tax information in the upstream commerce platform. These updates should be performed for the entire transaction and each line item in the transaction. This ensures that the values in your system stay in sync with those in our system.

Additionally, you should display these response values in your interface so customers can review tax and product totals during the checkout process.

### Set charge type to customer initiated in subscription acquisitions

Since the customer actively participates in a subscription acquisition, you should set [`chargeType`](../../../integration-options/checkouts/creating-checkouts/initiating-a-charge.md) to [`customer_initiated`](../../../integration-options/checkouts/creating-checkouts/initiating-a-charge.md#customer-initiated).

### Set charge type to merchant initiated in subscription auto-renewals

During a subscription's autorenewal, the customer is not an active participant. As a result, when [building a checkout](../../../integration-options/checkouts/creating-checkouts/) to process an autorenewal, you should set [`chargeType`](../../../integration-options/checkouts/creating-checkouts/initiating-a-charge.md) to [`merchant_initiated`](../../../integration-options/checkouts/creating-checkouts/initiating-a-charge.md#merchant-initiated).

### Send subscription information

Any transaction that includes a recurring product or service, must provide information that describes that subscription. So, when [building a checkout](../../../integration-options/checkouts/creating-checkouts/), provide these details in the [`subscriptionInfo`](../../../integration-options/checkouts/subscriptions/subscription-information-1.md#setting-subscription-information) hash table.

### Send the subscription's terms

For [auto-renewing subscriptions](../../../integration-options/checkouts/subscriptions/subscription-information-1.md#auto-renewal), you must display the subscription's terms and acquire the customer's active acceptance of them. So, before [converting a checkout to an order](../../../order-management/creating-and-updating-an-order.md#creating-an-order-with-the-checkout-identifier), pass these agreed upon terms in the checkout's [`terms`](../../../integration-options/checkouts/subscriptions/subscription-information-1.md#terms) parameter. This ensures that they are recorded in the [billing agreement](../../../integration-options/checkouts/subscriptions/subscription-information-1.md#billing-agreement-identifier).

### Generate a subscription identifier

During the acquisition process, you can optionally generate a unique subscription identifier and assign it to [`subscriptionId`](../../../integration-options/checkouts/subscriptions/subscription-information-1.md#subscription-identifier).

### Specify a subscription's renewal method

For every recurring product or service, you must use the [`autoRenewal`](../../../integration-options/checkouts/subscriptions/subscription-information-1.md#auto-renewal) parameter to tell us whether the subscription is automatically or manually renewed.

### Send the billing agreement identifier in renewals

During the renewal process, send the the [`billingAgreementId`](../../../integration-options/checkouts/subscriptions/subscription-information-1.md#billing-agreement-identifier) generated during the subscription's acquisition.

### Provide a start and end time for Klarna funded subscriptions

When acquiring or renewing a subscription with the [Klarna ](../../../payments/payment-integrations-1/digitalriver.js/payment-methods/klarna.md)payment method, you must [provide a start and end time](../../../integration-options/checkouts/subscriptions/subscription-information-1.md#start-and-end-time).

### Use Drop-in to display available payment methods and create a source <a href="#use-drop-in-to-create-payment-sources" id="use-drop-in-to-create-payment-sources"></a>

[Drop-in payments](../../../payments/payment-integrations-1/drop-in/) is our all-in-one solution for handling payments and ensuring compliance. We recommend you use this solution as a quick and easy way to start accepting payments.

During the checkout experience, you can use the [configurable Drop-in object](../../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md) to present available payment methods and then safely and securely capture a customer's payment details. The [payment source](../../../payments/payment-sources/) returned in the [`onSuccess` event](../../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md#onsuccess) can then be [attached to the checkout](../../../payments/payment-sources/using-the-source-identifier.md#attaching-sources-to-checkouts) before the customer arrives on your order review page.

### Provide option to save payment information for future use <a href="#provide-option-to-save-credit-card-for-future-use" id="provide-option-to-save-credit-card-for-future-use"></a>

During checkout flows, we recommend you provide customers the option to save their payment information for future transactions. When [building your payment workflows](../../../integration-options/checkouts/building-you-workflows/) for both [one-off](../../../integration-options/checkouts/building-you-workflows/#credit-card-details-saved-by-customer-during-checkout) and [subscription](../../../integration-options/checkouts/building-you-workflows/#customer-enters-credit-card-details-during-subscription-acquisition-checkout) purchases, you can [configure Drop-in payments to present the save payment option](../../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md#optional-allowing-the-customer-to-save-their-payment-details) to customers.

### Save ready for storage payment sources to the customer's account

In the [`onSuccess`](../../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md#onsuccess) event, if [`readyForStorage`](../../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md#optional-allowing-the-customer-to-save-their-payment-details) returns `true` or `mandate` is populated, then the customer agreed to save that transaction's payment information for future use. In response, your integration should [attach the payment source to the customer's record](../../../payments/payment-sources/using-the-source-identifier.md#attaching-sources-to-customers).

### Respond to on success event and display the order review page <a href="#respond-to-on-success-events-and-display-the-order-review-page" id="respond-to-on-success-events-and-display-the-order-review-page"></a>

Whenever [Drop-in payments](../../../payments/payment-integrations-1/drop-in/) successfully creates a [payment source](../../../payments/payment-sources/), we send you the [`onSuccess` event](../../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md#onsuccess). Once you receive this event, you should redirect the customer to the order review page. Here the customer can perform a final review of the order's details before deciding whether to make the purchase.

### Display reusable payment sources

When a customer is purchasing an auto-renewing subscription, the payment methods that [Drop-in payments](../../../payments/payment-integrations-1/drop-in/) displays must [support recurring transactions](../../../payments/payment-sources/#reusable-or-single-use). To ensure that Drop-in only displays [reusable payment methods](../../../payments/payment-integrations-1/drop-in/#supported-payment-methods), set [`autoRenewal`](../../../integration-options/checkouts/subscriptions/subscription-information-1.md#auto-renewal) to `true` in a `POST/checkouts` or `POST/checkouts/{id}` request. You then use Drop-in's configurable [`options`](../../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md#drop-in-options) to set `showTermsOfSaleDisclosure` to `true`.

### Acquire customer's acceptance of subscription and payment storage terms

When acquiring an auto-renewing subscription, customers must agree to save the transaction's payment source to their account so that it can be applied to renewals. So, you must configure [Drop-in payments](../../../payments/payment-integrations-1/drop-in/) to display the combined subscription and save payment agreement terms and then acquire the customer's active acceptance..

You do this by first setting [`autoRenewal`](../../../integration-options/checkouts/subscriptions/subscription-information-1.md#auto-renewal) to `true` in a `POST/checkouts` or `POST/checkouts/{id}` request. You then use Drop-in's configurable [`options`](../../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md#drop-in-options) to set `showTermsOfSaleDisclosure` to `true`.

### Save ready for storage source to customer's account

When the [`onSuccess`](../../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md#onsuccess) event returns a source that is [`readyForStorage`](../../../payments/payment-integrations-1/drop-in/drop-in-integration-guide.md#optional-allowing-the-customer-to-save-their-payment-details), you should save the source to the customer's account. This operation flips its `reusable` value to `true`. As a result, the source can be used in [merchant-initiated](../../../integration-options/checkouts/creating-checkouts/initiating-a-charge.md#merchant-initiated) subscription auto-renewals.

### Create an order with the checkout identifier

After you display the review order page to the customer and the customer actively accepts Digital River's [disclosure terms](../../../payments/payment-integrations-1/digitalriver.js/reference/digitalriver-object.md#digitalriver-compliance-getdetails-businessentitycode-locale) and then submits the order on the storefront, you should [convert the checkout to an order](../../../order-management/creating-and-updating-an-order.md#creating-an-order-with-the-checkout-identifier).\
\
Digital River creates an [Order](../../../order-management/orders/) based on the data in a [Checkout](../../../integration-options/checkouts/). Providing `checkoutId` in the payload of `POST/orders` acts primarily as a call to authorize payment and trigger a fraud review.

### Notify the customer of the order status

When a customer uses a [synchronous payment method](../../../payments/payment-sources/#synchronous-or-asynchronous) such as a [credit card](../../../payments/payment-sources/handling-credit-card-sources.md) to pay for a transaction, the [`POST/orders` request](../../../order-management/creating-and-updating-an-order.md#creating-an-order-with-the-checkout-identifier) almost always immediately returns either an [accepted](../../../order-management/creating-and-updating-an-order.md#accepted) or [failed](../../../order-management/creating-and-updating-an-order.md#409-conflict) order. When the order succeeds, direct the customer to the "Thank you" page. If the order fails, use the error's `message` to inform the customer of the issue through the user interface.

### Capture the order's identifier

When the [`POST/orders` response](../../../order-management/creating-and-updating-an-order.md#processing-the-post-orders-response) returns a [`201 Created`](../../../order-management/creating-and-updating-an-order.md#201-created) status code, retrieve the order's `id` from the payload, and use that value to set the corresponding attribute in the upstream commerce platform's order.

### Align order states

Use the [`POST/orders` response](../../../order-management/creating-and-updating-an-order.md#processing-the-post-orders-response) to set the status of the upstream commerce platform's order.

| `POST/orders` response                                                                     | Due to...                                                                                                                    | Ready to fulfill? |
| ------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------- | ----------------- |
| [`409 Conflict`](../../../order-management/creating-and-updating-an-order.md#409-conflict) | a [payment authorization failure](../../../order-management/creating-and-updating-an-order.md#payment-authorization-failure) | No                |
| [`409 Conflict`](../../../order-management/creating-and-updating-an-order.md#409-conflict) | a [fraud review failure](../../../order-management/creating-and-updating-an-order.md#fraud-review-failure)                   | No                |
| [`201 Created`](../../../order-management/creating-and-updating-an-order.md#201-created)   | a [pending payment](../../../order-management/creating-and-updating-an-order.md#pending-payment)                             | No                |
| [`201 Created`](../../../order-management/creating-and-updating-an-order.md#201-created)   | an [in-process secondary fraud review](../../../order-management/creating-and-updating-an-order.md#in-review)                | No                |
| [`201 Created`](../../../order-management/creating-and-updating-an-order.md#201-created)   | an [accepted order](../../../order-management/creating-and-updating-an-order.md#accepted)                                    | Yes               |

### Capture the order's payment state

When the [`POST/orders response`](../../../order-management/creating-and-updating-an-order.md#processing-the-post-orders-response) returns a [`201 Created`](../../../order-management/creating-and-updating-an-order.md#201-created) status code, retrieve [`charges[].state`](../../../order-management/orders/payment-charges/#the-charge-lifecycle) from the payload, and use that value to set the corresponding attribute in the upstream commerce platform's order.

For [`409 Conflict` errors generated by a payment authorization failure](../../../order-management/creating-and-updating-an-order.md#payment-authorization-failure), set the commerce platform's order payment status to failed.

### Capture the order's fraud state

When the [`POST/orders response`](../../../order-management/creating-and-updating-an-order.md#processing-the-post-orders-response) returns a [`201 Created`](../../../order-management/creating-and-updating-an-order.md#201-created) status code, retrieve [`fraudState`](../../../order-management/orders/the-order-lifecycle.md#fraud-review) from the payload, and use that value to set the corresponding attribute in the upstream commerce platform's order.

For [`409 Conflict` errors generated by a fraud review failure](../../../order-management/creating-and-updating-an-order.md#fraud-review-failure), set the commerce platform's order fraud status to blocked.

### Listen for and handle the order accepted event

When Digital River successfully authorizes payment and completes its fraud review, we send the [`order.accepted`](../../../order-management/creating-and-updating-an-order.md#listening-for-the-order-accepted-event) event. This event indicates that the order is ready to fulfill. Upon receipt, retrieve [`state`](../../../order-management/orders/the-order-lifecycle.md#order-states-and-events), [`fraudState`](../../../order-management/orders/the-order-lifecycle.md#fraud-review), and [`charges[].state`](../../../order-management/orders/payment-charges/#the-charge-lifecycle) from the payload, and use these values to update the corresponding attributes in the upstream commerce platform's order.

### Listen for and handle order failed events <a href="#consume-the-event-emitted-when-an-order-fails" id="consume-the-event-emitted-when-an-order-fails"></a>

An asynchronous payment authorization failure triggers an [`order.charge.failed`](../../../order-management/creating-and-updating-an-order.md#the-payment-failure-event) event. When Digital River asynchronously detects an anomaly during its [fraud review](../../../order-management/orders/the-order-lifecycle.md#fraud-review), or the customer is determined to be on the [Denied Persons List](https://www.bis.doc.gov/index.php/policy-guidance/lists-of-parties-of-concern/denied-persons-list), we send an [`order.blocked`](../../../order-management/creating-and-updating-an-order.md#the-fraud-review-failure-event) event.

Upon receipt of either event, retrieve [`state`](../../../order-management/orders/the-order-lifecycle.md#order-states-and-events), [`fraudState`](../../../order-management/orders/the-order-lifecycle.md#fraud-review), and [`charges[].state`](../../../order-management/orders/payment-charges/#the-charge-lifecycle) from the payload, and use these values to update the corresponding attributes in the upstream commerce platform's order.

### Persist the billing agreement identifier

For each subscription product or service that you create, store the [`billingAgreementId`](../../../integration-options/checkouts/subscriptions/subscription-information-1.md#billing-agreement-identifier) that Digital River generates so that it can be sent in the renewal request.

## API interfaces

| Documentation                                                                                                                                                                                                | Direct API                                                                                | PHP SDK                                                                                         |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------- |
| [Checkouts](../../../integration-options/checkouts/)                                                                                                                                                         | [Checkouts](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) | [Checkouts](https://github.com/DigitalRiver/digital-river-php/blob/main/docs/Model/Checkout.md) |
| [Sources](../../../payments/payment-sources/)                                                                                                                                                                | [Sources](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources)     | [Sources](https://github.com/DigitalRiver/digital-river-php/blob/main/docs/Model/Source.md)     |
| [Orders](../../../order-management/orders/)                                                                                                                                                                  | [Orders](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders)       | [Orders](https://github.com/DigitalRiver/digital-river-php/blob/main/docs/Model/Order.md)       |
| [DigitalRiver.js](https://github.com/DigitalRiver/GitBook/blob/Digital-River-API-latest/payments/payment-integrations-1/digitalriver.js#getting-started)                                                     |                                                                                           |                                                                                                 |
| [DigitalRiver.js Drop-in](../../../payments/payment-integrations-1/drop-in/)                                                                                                                                 |                                                                                           |                                                                                                 |
| [Events](../../../order-management/events-and-webhooks-1/events-1/): order.accepted, order.review\_opened, order.pending\_review, order.pending\_payment, order.blocked, order.charge.failed, order.complete |                                                                                           |                                                                                                 |
