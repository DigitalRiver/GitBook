---
description: Learn how to configure the Digital River app for subscriptions.
---

# Configure subscriptions

Configuring the Digital River app for subscriptions requires you to perform a few additional steps. You must identify for each Cart Item object whether the product is a subscription with additional relevant information as described below. You should create a trigger, flow, or other mechanism to automate the population of this data as Cart Items are added to the Cart.&#x20;

Configuring the Digital River app for subscriptions requires you to perform a few additional steps. You must identify for each [Cart Item](../appendix/custom-fields-and-objects.md#cart-item-standard-object) object whether the product is a subscription with additional relevant information as described below. You should create a trigger, flow, or another mechanism to automate the population of this data as Cart Items are added to the [Cart](../appendix/custom-fields-and-objects.md#cart-standard-object).&#x20;

The Digital River app will identify whether a product is a subscription by the value in the **Recurring Line Item** field **(API name: digitalriverv3\_\_Recurring\_Line\_Item\_\_c)** which is on [Cart Item](../appendix/custom-fields-and-objects.md#cart-item-standard-object) object.&#x20;

When the **Recurring Line Item** field value is `true`, it indicates the product is a subscription. If the **Recurring Line Item** field value is `false`,  it indicates the product is not a subscription.

You will need to populate the **Recurring Line Item** field accordingly so that the app can identify whether a product is a subscription. If the field is not populated, the application will treat the product as a non-subscription. &#x20;

The application will optionally allow you to specify the subscription's `startTime` and `endTime`. The following information is included in the `subscriptionInfo` field and sent across to Digital River during the [create checkout API call](https://docs.digitalriver.com/digital-river-api/checkouts-and-orders/checkouts/creating-checkouts#creating-and-updating-the-checkout):&#x20;

* If the `startTime` and `endTime` are specified, then this information will be included in the `subscriptionInfo` **** block.
* If only the `endTime` is specified but not the `startTime`, then the app will default the `startTime` to the current date/time.
* If the `endTime` is not specified, then both the `startTime` and `endTime` are not included in the `subscriptionInfo` block.

Finally, the following optional fields are available to be populated on the Cart Item. If specified, the values will be sent to Digital River.

| Field            | Description                                                                                                                                                                                                                                                |
| ---------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `freeTrial`      | This field has a  `true` or `false` value that indicates whether a [free trial period](https://docs.digitalriver.com/digital-river-api/checkouts-and-orders/shared-properties/describing-the-items/subscription-information#free-trial) is being offered.  |
| `subscriptionId` | This field can be used to supply the client's [subscription identifier](https://docs.digitalriver.com/digital-river-api/subscriptions/subscription-information-1#subscription-identifier) (if applicable).                                                 |
