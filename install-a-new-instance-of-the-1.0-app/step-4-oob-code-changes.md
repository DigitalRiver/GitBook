---
description: Learn about OOB code changes.
---

# Step 4: OOB code changes

Files that are changed as a part of the Digital River payment integration, tax management, and Order Management System (OMS) will be available in the OOB folder in the archive (custom folder). The following modified extensions will appear in the archive:&#x20;

* `yacceleratorstorefront`
* `consignmenttrackingaddon`
* `orderselfserviceaddon`
* `yacceleratorordermanagement`

### Storefront changes

The OOB __ `yacceleratorstorefront` is the template storefront for Digital River extension development. The following files are updated for tax and payment integration. If the merchant application uses any custom files, update them with the changes for Digital River from this file list:

#### `yacceleratorstorefront` files

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

#### `consignmenttrackingaddon` file

* `orderUnconsignedEntries.tag`

This tag, in `consignmenttrackingaddon` and `yacceleratorstorefront`, has changed to display the status for the Digital River product. The merchant application should make the necessary changes in custom implementation for the Digital River product if changes exist.

#### **`orderselfserviceaddon`** __ files

The following files in the `order-management\orderselfserviceaddon` are changed for Digital River product cancellation:

* `CancelOrderPageController.java`
* `extensioninfo.xml`
* `accountReturnTotals.tag`

### Order Management System (OMS) file changes

The following files are added or modified in `order-management\yacceleratorordermanagement` for Digital River OMS support:

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
