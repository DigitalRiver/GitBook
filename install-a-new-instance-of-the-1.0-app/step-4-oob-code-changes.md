---
description: Learn about OOB code changes.
---

# Step 4: OOB code changes

Files that are changed as a part of the Digital River payment integration, tax management, and Order Management System (OMS) will be available in the out-of-the-box (OOB) folder in the archive (custom folder). The following modified extensions will appear in the archive:&#x20;

* ``[`yacceleratorstorefront`](step-4-oob-code-changes.md#yacceleratorstorefront-files)``
* ``[`yb2bacceleratorstorefront`](step-4-oob-code-changes.md#yb2bacceleratorstorefront-files)``
* ``[`b2bacceleratoraddon`](step-4-oob-code-changes.md#undefined)``
* ``[`consignmenttrackingaddon`](step-4-oob-code-changes.md#consignmenttrackingaddon-file)``
* ``[`orderselfserviceaddon`](step-4-oob-code-changes.md#orderselfserviceaddon-files)``
* ``[`yacceleratorordermanagement`](step-4-oob-code-changes.md#ir)``

## Storefront changes

The OOB __ `yacceleratorstorefront` and `yb2bacceleratorstorefront` use the template storefront for Digital River extension development for B2C and B2B respectively. The following files are updated for tax and payment integration. If the merchant application uses any custom files, update them with the changes for Digital River from this file list:

### yacceleratorstorefront files

* `addressFormElements.tag`
* `addressFormSelector.tag`
* `billAddressFormSelector.tag`
* `billingAddressFormElements.tag`
* `orderTotals.tag`
* `orderUnconsignedEntries.tag` &#x20;
* `master.tag`
* `accountOrderDetailShippingInfo.jsp`
* `accountProfileEditPage.jsp`
* `addEditDeliveryAddressPage.jsp`
* `checkoutSummaryPage.jsp`
* `silentOrderPostPage.jsp`
* `spring-filter-config.xml`
* `base_en.properties`
* `multi-step-checkout-config.xml`
* `checkoutOrderSummary.tag`
* `accountPaymentInfoPage.jsp`
* `orderTotalsItem.tag`
* `accountOrderDetailOrderTotals.tag`
* `chooseDeliveryMethodPage.jsp`
* `guestOrderPage.jsp`
* `acc.silentorderpost.js`

### yb2bacceleratorstorefront files

* `acc.silentorderpost.js`
* `multi-step-checkout-config.xml`
* `spring-filter-config.xml`
* `addressFormElements.tag`
* `billAddressFormSelector.tag`
* `checkoutOrderSummary.tag`
* `orderTortals.tag`
* `accountOrderDetailOrderTotals.tag`
* `orderTotalsItem.tag`
* `orderUnconsignedEntries.tag`
* `master.tag`
* `accountProfileEditPage.jsp`
* `addEditDeliveryddressPage.jsp`
* `chooseDeliveryMethodPage.jsp`
* `silentOrderPostPage.jsp`
* `checkoutConfirmatinThankMessage.jsp`
* `guestOrderPage.jsp`

### b2bacceleratoraddon files

* `orderUnconsignedEntries.tag`
* `accountOrderDetailShippingInfo.jsp`
* `checkoutSummaryPage.jsp`
* `base_en`
* `multi-step-checkout-config.xml`
* `acc.paymentType.js`
* `PaymentTypeCheckoutStepController.java`

### consignmenttrackingaddon file

* `orderUnconsignedEntries.tag`

This tag, in `consignmenttrackingaddon`, `yacceleratorstorefront`,  and `yb2bacceleratorstorefront` has changed to display the status for the Digital River product. The merchant application should make the necessary changes in custom implementation for the Digital River product if changes exist.

### **orderselfserviceaddon** __ files

We changed the following files in `order-management\orderselfserviceaddon` to support Digital River product cancellation:

* `CancelOrderPageController.java`
* `extensioninfo.xml`
* `accountReturnTotals.tag`

## Order Management System (OMS) file changes

We added or modified the following files in `order-management\yacceleratorordermanagement` to support Digital River OMS:

* `extensioninfo.xml`
* `order-process-spring.xml`
* `projectdata-dynamic-business-process-order.impex`
* `projectdata-dynamic-business-process-return.impex`
* `ConfirmShipConsignmentAction.java`
* `CheckOrderAction.java`
* `CheckAuthorizeOrderPaymentAction.java`
* `SendAuthorizationFailedNotificationAction.java`
* `FulFillDigitalAction.java`
* `SourceOrderAction.java`
* `VerifyOrderCompletionAction.java`
* `ProcessOrderCancellationAction.java`
* `FraudCheckOrderAction.java`
* `SendOrderPlacedNotificationAction.java`
* `TakePaymentAction.java`
* `CaptureRefundAction.java`
* `DefaultCheckOrderService.java`
