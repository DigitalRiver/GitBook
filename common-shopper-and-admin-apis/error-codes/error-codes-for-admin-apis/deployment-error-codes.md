---
description: Understand the deployment error codes for the Admin API.
---

# Deployment error codes

#### `AUTO_TRIAL_RENEWAL_REMINDER_MUST_BE_LESS_THAN_FREE_TRIAL_PERIOD`

The Auto Trial Renewal Reminder must be sent before the end of the Free Trial ends. Set the time interval (in days) for the Free Trial Period that is greater than the number of days for the Auto Trial Renewal Reminder (`timeIntervalForTrialReminderNotifications`) period.

* `Product 1234567800, en_US: Auto Trial Renewal Reminder (timeIntervalForTrialReminderNotifications) must less then Trial Days (freeTrialPeriod).`

#### `CANNOT_ADD_A_SUBSRIPTION_BASE_PRODUCT_TO_ANOTHER_SUBSCRIPTION_BASE_PRODUCT`

You cannot add a subscription base product to another subscription base product. You can only add variations to the subscription base product.

* For downgrade products:
  * `Product 1234567800: Cannot add the subscription base product 9876543210 to the Subscription Downgrade Products  (downgradeProducts).`
* For upgrade products:
  * `Product 1234567800: Cannot add the subscription base product 9876543210 to the Subscription Upgrade Products  (upgradeProducts).`
* For transfer product:
  * `Product 1234567800: Cannot add the subscription base product 9876543210 to the Subscription Transfer Products  (transferProduct).`

#### `CANNOT_CHANGE_NUMBER_OF_BILLING_CYCLES`

Set up the  Number of Billing Cycles (`numberOfBillingCycles`) before deploying the subscription product

* `Product 1234567800, en_US: Cannot change the Number of Billing Cycles (numberOfBillingCycles) after deployment.`

#### `CANNOT_CHANGE_PAYMENT_SCHEDULE_AFTER_DEPLOYMENT`

&#x20;Set up the Payment Schedule (`paymentSchedule`) before deploying the subscription product.

* `Product 1234567800, en_US: Cannot change the Payment Schedule (paymentSchedule) after deployment.`

#### `CANNOT_CONFIGURE_AUTO_TRIAL_RENEWAL_REMINDER_WHEN_FREE_TRIAL_IS_DISABLED`

When Free Trial is disabled, you cannot configure the Auto Trial Renewal reminder. Set Free Trial (`isFreeTrial`) to enabled), and then configure the Auto Trial Renewal Reminder (`timeIntervalForTrialReminderNotifications`).

* `Product 1234567800, en_US: Cannot configure the Auto Trial Renewal Reminder (timeIntervalForTrialReminderNotifications) when Free Trial (isFreeTrial) is disabled.`

#### `CANNOT_CONFIGURE_MANUAL_TRIAL_RENEWAL_REMINDER_WHEN_FREE_TRIAL_IS_DISABLED`

When Free Trial is disabled, you cannot configure the Manual Trial Renewal reminder. Set Free Trial (`isFreeTrial`) to enabled, and then configure a Manual Trial Renewal Reminder (`timeIntervalForTrialManualReminderNotifications`).

* `Product 1234567800, en_US: Cannot configure the Manual Trial Renewal Reminder (timeIntervalForTrialManualReminderNotifications) when Free Trial (isFreeTrial) is disabled.`

#### `CANNOT_CONFIGURE_NUMBER_OF_DAYS_FOR_RENEWAL_PERIOD_IF_PRORATE_IS_DISABLED_ON_OR_BEFORE_EXPIRATION_DATE`

Enable Prorate on or before the expiration date (`isChangeProductAsRenewal`) before you configure the number of days for Process as renewal (`numOfDaysPriorExpirationForChangeProductAsRenewal`).

* `Product 1234567800, en_US: Pricing Method: Cannot configure the number of days for Process as renewal (numOfDaysPriorExpirationForChangeProductAsRenewal) when Prorate on or before the expiration date (isChangeProductAsRenewal) is disabled`

#### `CANNOT_CONFIGURE_NUMBER_OF_DAYS_FOR_RENEWAL_PERIOD_IF_THERE_IS_NO_UPGRADE_OR_DOWNGRADE_PRODUCT`

An upgrade or downgrade subscription product must exist before you can configure the days for Process as renewal (`numOfDaysPriorExpirationForChangeProductAsRenewal`).

* `Product 1234567800, en_US: Pricing Method: Cannot configure the days for Process as renewal (numOfDaysPriorExpirationForChangeProductAsRenewal) when there is no upgrade product or downgrade product.`

#### `CANNOT_CONFIGURE_PROCESS_AS_RENEWAL_FROM_SUBSCRIPTION_BASE_PRODUCT`

If you send an API request via API to set `isChangeProductAsRenewal` to `false` for a base product, the `isChangeProductAsRenewal` will be hidden in [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do). If you accidentally set incorrect data using an API request, you must use an API request to correct the error.

* `Product 1234567800, en_US: Pricing Method: Cannot configure the number of days for  Process as renewal (numOfDaysPriorExpirationForChangeProductAsRenewal) at the base subscription product.`

#### `CANNOT_ENABLE_TRIAL_IF_SUBSCRIPTION_ACTIVATION_DATE_IS_NOT_PURCHASE_DATE`

To enable a free trial, the activation date must be the same as the purchase date.

* `Product 1234567800, en_US: Cannot enable Trial (isFreeTrial) when the subscription activation date (autoRenewalDateBasis) is not the same as Purchase Date (PurchaseDate).`

#### `CANNOT_ENABLE_PRORATE_ON_OR_BEFORE_EXPIRATION_DATE_IF_THERE_IS_NO_UPGRADE_OR_DOWNGRADE_PRODUCT`

An upgrade or downgrade subscription product must exist before you can enable the Prorate on or before the expiration date (`isChangeProductAsRenewal`).

* `Product 1234567800, en_US: Pricing Method: Cannot enable Prorate on or before the expiration date (isChangeProductAsRenewal) when there is no upgrade product or downgrade product.`

#### `CANNOT_ENABLE_PRORATE_ON_SUBSCRIPTON_BASE_PRODUCT`

If you send an API request via API to set `isChangeProductAsRenewal` to `false` for a base product, the `isChangeProductAsRenewal` will be hidden in [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do). If you accidentally set incorrect data using an API request, you must use an API request to correct the error.

* Product 1234567800, en\_US: Pricing Method: Cannot configure the number of days for  Process as renewal (numOfDaysPriorExpirationForChangeProductAsRenewal) at the base subscription product.

#### `CANNOT_ENABLE_TRIAL_IF_SUBSCRIPTION_ACTIVATION_DATE_IS_NOT_PURCHASE_DATE`

To enable a free trial, the activation date must be the same as the purchase date.

* `Product 1234567800, en_US: Cannot enable Trial (isFreeTrial) when the subscription activation date (autoRenewalDateBasis) is not the same as Purchase Date (PurchaseDate).`

#### `CANNOT_SET_FIRST_BILLING_ATTEMPT_PRIOR_TO_EXPIRATION_WHEN_DURATION_IS_LESS_THAN_2_MONTHS`

Increase the Recurrence (`duration`) to greater than two months before setting the 1st Billing Attempt Prior to Expiration (`numOfDaysPriorExpirationForRenewalPreFirst`).

* `Product 1234567800, en_US: Cannot set 1st Billing Attempt Prior to Expiration (numOfDaysPriorExpirationForRenewalPreFirst) when Recurrence (duration) is less then 2 months.`

#### `CANNOT_SET_RETRY_INTERVAL_FOR_BILLING_ATTEMPTS_AFTER_EXPIRATION_IS_GRACE_PERIOD_IS_NONE`

When the value for Grace Period (`gracePeriod`) is `None`, you cannot configure the Retry Interval For Billing Attempts After Expiration. Set the Grace Period (`gracePeriod`) to `1 Week`, `2 Weeks`, or `1 Month`, and then configure the Retry Interval For Billing Attempts After Expiration (`postExpirationBillingAttemptIntervalInDays`)

* `Product 1234567800, en_US: Cannot set the Retry Interval For Billing Attempts After Expiration (postExpirationBillingAttemptIntervalInDays) when the Grace Period (gracePeriod) is NONE.`

#### `CANNOT_SET_SECOND_BILLING_ATTEMPT_PRIOR_TO_EXPIRATION_WHEN_DURATION_IS_LESS_THAN_1_MONTH`

Increase the Recurrence (`duration`) to greater than one month before setting the 2nd Billing Attempt Prior to Expiration (`numOfDaysPriorExpirationForRenewalFirst`).

* `Product 1234567800, en_US: Cannot set 2nd Billing Attempt Prior to Expiration (numOfDaysPriorExpirationForRenewalFirst) when Recurrence (duration) is less than 1 month.`

#### `CANNOT_SET_SUBSCRIPTION_TRIAL_GRACE_PERIOD_WHEN_FREE_TRIAL_IS_DISABLED`

To set the Trial Grace Period, you must enable Free Trial (`isFreeTrial`).

* `Product 1234567800, en_US: Cannot set the Trial Grace Period (trialGracePeriod) when Free Trail (isFreeTrial) is disabled.`

#### `DRM_ON_FREE_TRIAL_CONVERSION_MUST_BE_SUPPRESSED_WHEN_FREE_TRIAL_IS_DISABLED`

Set the Free Trial Conversion for Digital Rights (`suppressDRMInTRIALConversion`) to `true` (suppress) when Free Trial (`isFreeTrial`) is disabled.

* `Product 1234567800, en_US: You must set Free Trial Conversion for Digital Rights (suppressDRMInTrialConversion) to Suppress (true) when Trial (isFreeTrial) is disabled.`

#### `INVALID_BILLING_CYCLES_NUMBER`

Specify a valid number of Billing Cycles (`numberOfBillingCycles`) between 2 and 99999999`.`

* `Product 1234567800, en_US: Number of Billing Cycles (numberOfBillingCycles) cannot` be `less than 2 or larger than 99999999.`

#### `INVALID_PARENT_VERSION_STATE_FOR_SUBSCRIPTION_PRODUCT`

The product must be in design mode if you want to add or change related products. Once you deploy the product you cannot add or change related products.

* `Product 1234567800: cannot have related products. (not in design mode)`

#### `INVALID_SUBCRIPTION_PAYMENT_SCHEDLULE`

Ensure the Payment Schedule (`paymentSchedule`) is either `matchRecurrence` or `flexibleTerm`.

* `Product 1234567800, en_US: Payment Schedule (paymentSchedule) must be either matchRecurrence or flexibleTerm.`

#### `MANUAL_TRIAL_RENEWAL_REMINDER_MUST_BE_LESS_THAN_FREE_TRIAL_PERIOD`

The Manual Trial Renewal Reminder must be sent before the end of the Free Trial ends. Set the time interval (in days) for the Free Trial Period that is greater than the number of days for the Manual Renewal Reminder (`timeIntervalForTrialManualReminderNotifications`) period.

* `Product 1234567800, en_US: Manual Trial Renewal Reminder (timeIntervalForTrialManualReminderNotifications) must less then Trial Days (freeTrialPeriod).`

#### `MAXIMUM_ORDER_QUANTITY_CANNOT_BE_LESS_THAN_MINIMUM_ORDER_QUANTITY`

The value for the maximum order quantity cannot be less than the value for the minimum order quantity.

* `Product 1234567800, en_US: the maximum quantity (maxOrderQuantity) cannot be less than the minimum quantity (minOrderQuantity).`

#### `MAXIMUM_ORDER_QUANTITY_CANNOT_BE_LESS_THAN_ZERO`

The maximum order quantity value must be 0 (zero) or greater.

* `Product 1234567800, en_US: the maximum quantity (maxOrderQuantity) cannot be less than zero.`

#### `MINIMUM_ORDER_QUANTITY_CANNOT_BE_LESS_THAN_ZERO`

The order quantity value must be 0 (zero) or greater.

* `Product 1234567800, en_US: the minimum quantity (minOrderQuantity) cannot be less than zero.`&#x20;

#### `OFI_ON_FREE_TRIAL_CONVERSION_MUST_BE_SUPPRESSED_WHEN_FREE_TRIAL_IS_DISABLED`

When a subscription product does not support Free Trial (`isFreeTrial` is disabled), you must set the Free Trial Conversion for Other Electronic Fulfillment Notice) (`suppressOFIInTrialConversion`) to `Issue New` (false).

* `Product 1234567800, en_US: You must set Free Trial Conversion for Electrontic Fulfillment Notice (`suppressOFIInTrialConversion`) to Issue New (false) when Trial (isFreeTrial) is disabled.`&#x20;

#### `ONLY_ONE_CHILD_SUBSCRIPTION_PRODUCT_IS_ALLOWED`

A child subscription product is already assigned to Subscription Transfer Products (`transferProduct`). You can only add one subscription child subscription product to Subscription Transfer Products (`transferProduct`).

* `Product 1234567800: Cannot add product 9876543210 to Subscription Transfer Products (transferProduct) because another product was already assigned.`

#### `PRODUCT_MUST_BE_SUBSCRIPTION_PRODUCT`

You can only add subscription products to the subscription product group.

* For downgrade products:
  * `Product 1234567800: product 9876543210 must be a subscription product to be added to Subscription Downgrade Products (downgradeProducts).`
* For upgrade products:
  * `Product 1234567800: product 9876543210 must be a subscription product to be added to Subscription Upgrade Products (upgradeProducts).`
* For transfer product:
  * `Product 1234567800: product 9876543210 must be a subscription product to be added to Subscription Transfer Products (transferProduct).`

#### `REMINDER_FOR_MANUAL_RENEWALS_MUST_BE_THE_SAME_AS_AUTOMATIC_RENEWALS_WHEN_DISTINCT_SCHEDULE_IS_DISABLED`

Ensure  the value for Reminder for Manual Renewals (`timeIntervalForManualReminderNotifications`) is the same as the Reminder for Automatic Renewals (timeIntervalForReminderNotifications) when Use a different schedule for manual renewal reminders (`isDistinctScheduleTurnedOn`) is not selected

* `Product 1234567800, en_US: Reminder for Manual Renewals (timeIntervalForManualReminderNotifications) must be the same as Reminder for Automatic Renewals (timeIntervalForReminderNotifications) if Use a different schedule for manual renewal reminders (isDistinctScheduleTurnedOn) is not selected.`

#### `SUBSCRIPTION_CHILD_PRODUCT_CANNOT_BE_A_PARENT`

You cannot add a subscription child product to itself. You can only add a child product to a base product.

* For downgrade products:
  * `Product 1234567800: Cannot add the subscription child product 9876543210 to itself using Subscription Downgrade Products  (downgradeProducts).`
* For upgrade products:
  * `Product 1234567800: Cannot add the subscription child product 9876543210 to itself using Subscription Upgrade Products  (upgradeProducts).`
* For transfer product:
  * `Product 1234567800: Cannot add the subscription child product 9876543210 to itself using Subscription Transfer Products  (transferProduct).`

#### `SUBSCRIPTION_CHILD_PRODUCT_MUST_BE_DEPLOYED`

Deploy a subscription child product before you add it to a product group.&#x20;

* For downgrade products:
  * `Product 1234567800: Cannot add the undeployed subscription child product 9876543210 to Subscription Downgrade Products (downgradeProducts).`
* For upgrade products:
  * `Product 1234567800: Cannot add the undeployed subscription child product 9876543210 to Subscription Upgrade Products (upgradeProducts).`
* For transfer product:
  * `Product 1234567800: Cannot add the undeployed subscription child product 9876543210 to Subscription Transfer Products (transferProduct).`

#### `SUBSCRIPTION_CHILD_PRODUCT_MUST_HAVE_SAME_BILLING_CYCLE`

The subscription child product must have the same payment schedule (`paymentSchedule`) as the upgrade subscription product.

* `Product 1234567800: You can only upgrade commitment subscription product 9876543210  to another product with the same commitment. That is, the payment schedule (paymentSchedule) should be the same.`

#### `SUBSCRIPTION_CHILD_PRODUCT_MUST_HAVE_SAME_DURATION`

The subscription child product must have the same Recurrence (duration) as the upgrade/downgrade product (`upgradeProducts`/`downgradeProducts`)`.`

* `Product 1234567800: You can only upgrade/downgrade (upgradeProducts/downgradeProducts) for the flexible term (flexibleTerm) commitment subscription product 9876543210 to another product that has the same Recurrence (duration).`

#### `SUBSCRIPTION_CHILD_PRODUCT_MUST_HAVE_SAME_PAYMENT_SCHEDULE`

The subscription child product must have the same payment schedule (`paymentSchedule`) as the upgrade subscription product.

* `Product 1234567800: You can only upgrade commitment subscription product 9876543210  to another product with the same commitment. That is, the payment schedule (paymentSchedule) should be the same.`

#### `SUBSCRIPTION_CHILD_PRODUCT_SHOULD_BE_COMMITMENT_PRODUCT`

Upgrading (`upgradeProducts`) a commitment (`flexibleTerm`) subscription product to a non-commitment (`matchRecurrence`) product is not allowed.

* `Product 1234567800: You cannot upgrade (upgradeProducts) the commitment (flexibleTerm) subscription product 9876543210 to a non-commitment (matchRecurrence) product.`

#### `SUBSCRIPTION_CHILD_PRODUCT_SHOULD_BE_NON_COMMITMENT_PRODUCT`

Upgrading/downgrading (`upgradeProducts/downgradeProducts`) a non-commitment (`matchRecurrence`) subscription product to a commitment (`flexibleTerm`) product is not allowed.

* `Product 1234567800: Product 9876543210 - You cannot upgrade/downgrade (upgradeProducts/downgradeProducts) non-commitment (matchRecurrence) subscription product 9876543210 to a commitment (flexibleTerm) product.`

#### `SUBSCRIPTION_COMBINED_RENEWAL_DAYS_LESS_THAN_HALF_DURATION_INVALID`

The number of Combined Renewal days is greater than half the duration of the subscription. The value must be less than half the duration value.

* `Product 1234567800, en_US: Combined Renewals days (combinedRenewalPeriod) must be less than half the recurrence (duration) value.`

#### `SUBSCRIPTION_COMBINED_RENEWAL_DAYS_LESS_THAN_THIRTY_INVALID`

The number of Combined Renewal days for the subscription is more than 30 days. The value must be less than or equal to 30.

* `Product 1234567800, en_US: Combined Renewals days (combinedRenewalPeriod) must be less than or equal to 30 days.`

#### `SUBSCRIPTION_COMBINED_RENEWAL_DAYS_VALUE_INVALID`

The number of Combined Renewal days for the subscription is less than 0. The value must be greater than 0.

* `Product 1234567800, en_US: Combined Renewal days (combinedRenewalPeriod) cannot be less than 0.`

#### `SUBSCRIPTION_FLEXIBLE_TERM_COMBINED_RENEWALS_DISABLED`

Combined Renewal is disabled and the Combined Renewal days are set to 0 when you select the Flexible Term Payment Schedule for a subscription product.

* `Product 1234567800, en_US: Combined Renewals (isCombinedRenewal) must be disabled, and Combined Renewal days (combinedRenewalPeriod) must be 0 when you select Flexible Term Payment Schedule (flexibleTerm).`

#### `SUBSCRIPTION_FLEXIBLE_TERM_RECURRENCE_INVALID`

The Flexible Term Payment schedule (`flexibleTerm`) is not set to one month. The value must be one month.

* `Product 1234567800, en_US: Flexible Term Payment schedule (flexibleTerm) cannot set recurrence (duration) other than one month.BSCRIPTON_PRODUCT_HAS_INVALID_GROUP_STATE`

Cannot add a subscription product to a group because the subscription products group is in an invalid state.

* For downgrade products:
  * `Product 1234567800: Cannot add product 9876543210 to Subscription Downgrade Products (downgradeProducts) because the group is in an invalid state.`
* For upgrade products:
  * `Product 1234567800: Cannot add product 9876543210 to Subscription Upgrade Products (upgradeProducts) because the group is in an invalid state.`
* For transfer product:
  * `Product 1234567800: Cannot add product 9876543210 to Subscription Transfer Products`
  * `(transferProduct) because the group is in an invalid state`

#### `SUBSCRIPTION_MATCH_RECURRENCE_NUMBER_OF_BILLING_CYCLES_INVALID`

The number of billing cycles for the subscription is invalid.

* `Product 1234567800, en_US: Match Recurrence Payment Schedule (matchRecurrence) cannot set Number of Billing Cycles (numberOfBillingCycles).`

#### `SUBSCRIPTION_ONE_MONTH_GRACE_PERIOD_FOUR_DAYS_RENEWAL_INTERVAL_POST_EXP_NOT_SUPPORTED`

Digital River does not support a combination of one month Grace Period and a 4-day Retry Interval for billing attempts after expiration (`postExpirationBillingAttemptIntervalInDays`). When combining the one-month Grace Period with the Retry Interval, specify a 5-day Retry interval.

* `Product 1234567800, en_US: Digital River does not support a one-month Grace Period (gracePeriod) with 4 days Retry Interval For Billing Attempts After Expiration (postExpirationBillingAttemptIntervalInDays).`

#### `SUBSCRIPTION_ONE_MONTH_TRIAL_GRACE_PERIOD_FOUR_DAYS_TRIAL_POST_EXPIRATION_BILLING_ATTEMPT_NOT_SUPPORTED`

Digital River does not support a combination of one month Trial Grace Period and a 4-day Retry Interval for billing attempts after trial expiration (`trialPostExpirationBillingAttemptIntervalInDays`).&#x20;

* `Product 1234567800, en_US: Digital River does not support a one month Trial Grace Period (trialGracePeriod) with 4 days Retry Interval For Billing Attempts After Trial Expiration (trialPostExpirationBillingAttemptIntervalInDays).`

#### `SUBSCRIPTION_PARENT_CAN_ONLY_HAVE_ONE_TRANSFER_GROUP`

* For downgrade products:
  * `Product 1234567800: You can only create one group for Subscription Downgrade Products (downgradeProducts).`
* For upgrade products:
  * `Product 1234567800: You can only create one group for Subscription Upgrade Products (upgradeProducts).`
* For transfer product:
  * `Product 1234567800: You can only create one group for Subscription Transfer Products (transferProduct).`

#### `SUBSCRIPTION_PARENT_PRODUCT_CANNOT_BE_BASE_PRODUCT`

A base product contains multiple product variations. However, we only sell the product variations to the shopper. The base product is merely a shell so it cannot be sold, which means setting transfer/upgrade/downgrade product to a base product is meaningless.&#x20;

* `Product 1234567800: product associations are not allowed for base products.`

#### `SUBSCRIPTION_PAYMENT_SCHEDULE_AND_LOCALE_SCHEDULE_MUST_BE_THE_SAME`

Ensure the  schedules for the Payment Schedule (`paymentSchedule`) and default locale schedule are the same.

* `Product 1234567800, en_US: Payment Schedule (paymentSchedule) must be the same as the schedule for the default locale.`

#### `SUBSCRIPTION_PRODUCT_BELONGS_TO_SAME_COMPANY`

The subscription product must belong to the same company associated with the group.

* For downgrade products:
  * `Product 1234567800: Cannot add product 9876543210 to Subscription Downgrade Products (downgradeProducts) because it does not belong to the same company.`
* For upgrade products:
  * `Product 1234567800: Cannot add product 9876543210 to Subscription Upgrade Products (upgradeProducts) because it does not belong to the same company.`
* For transfer product:
  * `Product 123456 7800: Cannot add product 9876543210 to Subscription Transfer Products (transferProduct) because it does not belong to the same company.`

#### `SUBSCRIPTION_PRODUCT_CANNOT_BE_IN_BOTH_ASSOCIATION_GROUPS`&#x20;

* For downgrade products:
  * `Product 1234567800: Cannot add product 9876543210 to Subscription Downgrade Products (downgradeProducts) because it belongs to {another group (attribute name)}`
* For upgrade products:
  * `Product 1234567800: Cannot add product 9876543210 to Subscription Upgrade Products (upgradeProducts) because it belongs to {another group (attribute name)}`

#### `SUBSCRIPTION_PRODUCT_IS_ALREADY_CHILD_PRODUCT`

The subscription product already exists as a child product in the subscription products group.

* For downgrade products:
  * `Product 1234567800: Product 9876543210 has already been added to Subscription Downgrade Products (downgradeProducts).`
* For upgrade products:
  * `Product 1234567800: Product 9876543210 has already been added to Subscription Upgrade Products (upgradeProducts).`
* For transfer product:
  * `Product 1234567800: Product 9876543210 has already been added to Subscription Transfer Products (transferProduct).`
* `subscription_product_belongs_to_same_company`–The subscription child product must have the same Number of Billing Cycles (`numberOfBillingCycles`) as the upgrade subscription product.
  * Product 1234567800: You can only upgrade commitment subscription product 9876543210 to another product with the same commitment. That is, the Number of Billing Cycles (`numberOfBillingCycles`) should be the same.

#### `SUBSCRIPTION_PRODUCT_IS_RETIRED`

You can only add deployed products t a group.

* For downgrade products:
  * `Product 1234567800: Cannot add a retired product 9876543210 to Subscription Downgrade Products (downgradeProducts).`
* For upgrade products:
  * `Product 1234567800: Cannot add retired product 9876543210 to Subscription Upgrade Products (upgradeProducts).`

#### `SUBSCRIPTION_PRODUCT_MUST_BE_VARIATION`

You can only add subscription product variations that are in the Design state to a group

* For downgrade products:
  * `Product 1234567800: Product 9876543210 is not allowed. You can only add products in the Design state that are variations of the current product to Subscription Downgrade Products (downgradeProducts).`
* For upgrade products:
  * `Product 1234567800: Product 9876543210 is not allowed. You can only add products in the Design stat that are variations of the current product to Subscription Upgrade Products (upgradeProducts).`

#### `SUBSCRIPTION_PRODUCT_NOT_ORDERABLE`

Cannot add the subscription product to the subscription products group because it is not orderable.

* For downgrade products:
  * `Product 1234567800: Cannot add product 9876543210 to Subscription Downgrade Products (downgradeProducts) because it is not orderable.`
* For upgrade products:
  * `Product 1234567800: Cannot add product 9876543210 to Subscription Upgrade Products (upgradeProducts) because it is not orderable.`
* For transfer product:
  * `Product 1234567800: Cannot add product 9876543210 to Subscription Transfer Products (transferProduct) because it is not orderable.`

#### `SUBSCRIPTION_PRODUCT_NOT_VIEWABLE`

You can only add visible subscription products to a group.

* For downgrade products:
  * `Product 1234567800: Cannot add product 9876543210 to Subscription Downgrade Products (downgradeProducts) because it is not visible.`
* For upgrade products:
  * `Product 1234567800: Cannot add product 9876543210 to Subscription Upgrade Products (upgradeProducts) because it is not visible.`
* For transfer product:
  * `Product 1234567800: Cannot add product 9876543210 to Subscription Transfer Products (transferProduct) because it is not visible.`

#### `SUBSCRIPTION_RENEWAL_BASIS_INVALID`

You can only specify the Activation Date (`ActivationDate`) or Purchase Date (`PurchaseDate`) as the subscription activation date.

* `Product 1234567800: Subscription activation date (autoRenewalDateBasis) can only be Activation Date (ActivationDate) or Purchase Date (PurchaseDate).`

#### `SUBSCRIPTION_TRIAL_DAYS_VALUE_INVALID`

The number of days for the subscription's free trial period (`freeTrialPeriod`) is less than 1 or greater than 1095 in the payload. The value cannot be less than 1 or larger than 1095.

* `Product 1234567800, en_US: Trial Days (freeTrialPeriod) cannot be less than 1 or larger than 1095.`
* `subscription_trial_grace_period_set_for_non_free_trial`–To set the Trial Grace Period, you must enable Free Trial (isFreeTrial).
  * `Product 1234567800, en_US: Cannot set the Trial Grace Period (trialGracePeriod) when Free Trail (isFreeTrial) is disabled.`&#x20;

#### `SUBSCRIPTION_TRIAL_POST_EXPIRATION_BILLING_ATTEMPT_INTERVAL_IN_DAYS_SET_FOR_NON_FREE_TRIAL`

`You cannot` configure `trailPostExpirationBillingAttemptIntervalInDays` if the product is not a free trial product.

* `Product 1234567800, en_US: Cannot set the Retry Interval for Billing Attempt After Trial Expiration (trialPostExpirationBillingAttemptIntervalInDays) when Trial (isFreeTrial) is disabled.`

#### `SUBSCRIPTION_UPGRADE_AS_RENEWAL_DAYS_MINIMAL_VALUE_INVALID`

The value for Process as renewal days must be a positive number.

* `Product 1234567800, en_US: Pricing Method: the days of Process as renewal (numOfDaysPriorExpirationForChangeProductAsRenewal) must be positive number.`
