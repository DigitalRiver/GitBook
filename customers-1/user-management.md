---
description: Learn how to manage users.
---

# User management

User Management provides an interface that third-party applications and processes can use to manage and retrieve Digital River-hosted user information. Use this service to add, modify, or remove a single user.

## User management details

User Management allows third-party applications to perform the following tasks:

| Task                                                                               | Request Type                    | Response Type                   |
| ---------------------------------------------------------------------------------- | ------------------------------- | ------------------------------- |
| Activate a user                                                                    | `ActivateShopperRequest`        | `ActivateShopperResponse`       |
| Inactivate a user                                                                  | `InactivateShopperRequest`      |  `InactivateShopperResponse`    |
| Reset user password                                                                |  `ResetShopperPasswordRequest`  |  `ResetShopperPasswordRequest`  |
| Retrieve user information                                                          |  `GetShopperRequest`            |  `GetShopperResponse`           |
| Add/modify users, including updating the user's default billing method             |  `AddUpdateShopperRequest`      |  `AddUpdateShopperResponse`     |
| Cancel a user's subscription                                                       |  `CancelSubscriptionRequest`    |  `CancelSubscriptionResponse`   |
| [Activate a user's subscription](user-management.md#activate-a-users-subscription) | `ActivateSubscriptionRequest`   |  `ActivateSubscriptionResponse` |
| Modify a subscription's renewal date                                               |  `ModifyRenewalDateRequest`     |  `ModifyRenewalDateResponse`    |
| Modify a subscription's renewal mechanism (manual or auto)                         |  `ModifyAutoRenewalRequest`     |  `ModifyAutoRenewalResponse`    |
| Search for a user's orders and get the order details                               |  `SearchOrderRequest`           |  `SearchOrderResponse`          |
| Cancel a user's order                                                              | `CancelOrderRequest`            |  `CancelOrderResponse`          |
| Return a user's order                                                              |  `ReturnOrderRequest`           |  `ReturnOrderResponse`          |
| Add or modify extended attributes on a user's order and line items                 |  `UpdateOrderAttributesRequest` | `UpdateOrderAttributesResponse` |

All tasks mentioned above can use user-based basic authentication. You can configure this authentication per client integration. All the complex types mentioned above inherit `CommonRequest` and `CommonResponse`.

## Activate a user's subscription

There are restrictions for an `ActivateSubscriptionRequest`. When sending an `ActivateSubscriptionRequest`, the request does not verify factors such as payment type and auto/manual. The following table lists the validations that occur during an `ActivateSubscriptionRequest`.

| Validation Task                                                                                                          | Error Information                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| ------------------------------------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| The user identified in the `shopperKey` element is valid                                                                 | <p><strong>Error Code</strong>: 200<br><strong>Message</strong>: Shopper Not Found</p>                                                                                                                                                                                                                                                                                                                                                                                              |
| The subscription identified in the 'SubscriptionID\` element is valid                                                    | <p><strong>Error Code</strong>: 710<br><strong>Message</strong>: Subscription order [888888] pending activation was not found<br><strong>Details</strong>: Where the <code>&#x3C;SubscriptionID></code> element passes the <code>888888</code> value.</p>                                                                                                                                                                                                                           |
| The specified `Subscription` belongs to the given user                                                                   | <p><strong>Error Code</strong>: 720<br><strong>Message</strong>: Subscription order [888888] does not belong to shopper [loginID =12345, externalReferenceID = 54321]<br><strong>Details</strong>: Where the<code>&#x3C;SubscriptionID></code> element passes the <code>888888</code> value. The values <code>12345</code> and <code>54321</code> are the Digital River <code>loginID</code> and <code>externalReferenceID</code> for the shopper.</p>                              |
| The specified Subscription contains a given product                                                                      | <p><strong>Error Code</strong>: 730<br><strong>Message</strong>: No subscription products found for the order [888888]<br><strong>Details</strong>: Where<code>888888</code> is the value passed in the <code>&#x3C;subscriptionProductKey></code> element</p>                                                                                                                                                                                                                      |
| The product identified in the \`' element is valid                                                                       | <p><strong>Error Code</strong>: 730<br><strong>Message</strong>: No subscription products found for the order <code>[productID=22222externalReferenceID= 33333companyID=44444locale=55555]</code><br><strong>Details</strong>: Where <code>&#x3C;subscriptionProductKey> element provides the values</code>22222<code>,</code>33333<code>,</code>44444<code>,</code>55555`.</p>                                                                                                     |
| The activation key supplied in the `<activatioKey>` element is valid for the given Subscription                          | <p><strong>Error Code</strong>: 750<br><strong>Message</strong>: Activation Key [activationKey=111] for provided productKey [productID=22222externalReferenceID=<br>33333companyID=44444locale=55555] was not found<br><strong>Details</strong>: Where <code>111</code> is the activation key supplied in the <code>&#x3C;acivtionKey></code> element and <code>22222</code>, <code>33333</code>, <code>44444</code>, <code>55555</code> are the values provided in the element</p> |
| The activation date supplied in the `<activationDate>` element is valid                                                  | <p><strong>Error Code</strong>: Not applicable<br><strong>Message</strong>: Not applicable<br><strong>Details</strong>: If invalid, the activation date will be set to the current date</p>                                                                                                                                                                                                                                                                                         |
| The activation key supplied in the `<activationKey>` element has not previously been activated                           | <p><strong>Error Code</strong>: 770<br><strong>Message</strong>: The subscription for the provided Activation Key [activationKey=111] has already been activated<br><strong>Details</strong>: Where <code>111</code> is the <code>&#x3C;activationKey></code> activation key supplied in the element</p>                                                                                                                                                                            |
| The subscription line item has not already been refunded                                                                 | <p><strong>Error Code</strong>: 780<br><strong>Message</strong>: Order [888888] has been refunded<br><strong>Details</strong>: Where <code>888888</code> is the value passed in the <code>&#x3C;SubscriptionID></code> element</p>                                                                                                                                                                                                                                                  |
| The subscription line item has not already been cancelled                                                                | <p><strong>Error Code</strong>: 790<br><strong>Message</strong>: Order [888888] was cancelled<br><strong>Details</strong>: Where <code>888888</code> is the value passed in the <code>&#x3C;SubscriptionID></code> element</p>                                                                                                                                                                                                                                                      |
| Your subscription `<SubscriptionID>` was renewed on _renewal date_ which is before so your message cannot be processed\* | <p><strong>Error Code</strong>: 851<br><strong>Message</strong>: Requested renewal date is before the subscription activation date<br><strong>Details</strong>: Not applicable</p>                                                                                                                                                                                                                                                                                                  |
| Nothing invalid                                                                                                          | <p><strong>Error Code</strong>: 0<br><strong>Message</strong>: Your request was carried out successfully.<br><strong>Details</strong>: Not applicable</p>                                                                                                                                                                                                                                                                                                                           |

{% tabs %}
{% tab title="Request sample" %}
```javascript
{
	"CancelSubscriptionRequest": {
		"shopperKey": {
			"userID": "26593336708",
			"siteID": "tmamer"
		},
		"SubscriptionID": "4343240414",
		"subscriptionProductKey": {
			"productID": "55551800",
			"companyID": "tmamer",
			"externalReferenceID": ""
		},
		"suppressCancelNotification": "false",
		"subscriptionKey": {
			"subscriptionID": "463301709"
		}
	}
}

{
	"ModifyAutoRenewalRequest": {
		"shopperKey": {
			"userID": "26593336708",
			"siteID": "tmamer"
		},
		"SubscriptionID": "4343240414",
		"subscriptionProductKey": {
			"productID": "55551800",
			"companyID": "tmamer",
			"externalReferenceID": ""
		},
		"activationKey": "22222",
		"autoRenewalAction": "Manual",
		"autoRenewalDate": "2009-08-08",
		"subscriptionKey": {
			"subscriptionID": "463301709"
		}
	}
}

{
	"ActivateSubscriptionRequest": {
		"shopperKey": {
			"userID": "26593336708",
			"siteID": "tmamer"
		},
		"SubscriptionID": "4343240414",
		"subscriptionProductKey": {
			"productID": "55551800",
			"companyID": "tmamer",
			"externalReferenceID": ""
		},
		"activationDate": "2009-02-03",
		"renewalDate": "2009-08-08",
		"subscriptionKey": {
			"subscriptionID": "463301709"
		}
	}
}
```
{% endtab %}
{% endtabs %}

## Suspending subscriptions

When you suspend a subscription, the system generates a suspension key that is unique to this subscription. (You are not responsible for providing the suspension key.)

The start date and end date must be in the `YYYY:mm:ddTHH:mm:ssZ` format.

If you want to start the suspension, do not provide the date. To change the suspension's end date to indefinite, set the `noEndDate` value to `true`.

Specify the type of suspension you want to create. If you do not provide the suspension type and provide both a suspension end date and no suspension date, this action will result in an error.

When modifying the existing suspension date for a subscription, you must supply the subscription key, the suspension type, and the new suspension date. To start the suspension immediately, provide the current date. To change the suspension's end date to indefinite, set the `noEndDate` value to `true`.

To end an existing or future suspension, you must supply the subscription key, suspension type, and the current date in the End Date field. This action removes the suspension.

The following image shows the process flow for modifying a suspension.

![Modifying a suspension](https://files.readme.io/492a5d4-User\_Management.png)

## User management schemas

| Version     | Scheme Components Table                                                                  | Raw Schema                                                                  | Sample XML    |
| ----------- | ---------------------------------------------------------------------------------------- | --------------------------------------------------------------------------- | ------------- |
| 26 (Current | [View](https://drhadmin.digitalriver.com/integration/isg/schematable/UserManagement/26)  | [View](https://drhadmin.digitalriver.com/integration/xsd/UserManagement/26) | Not available |
| 25          | [View](https://drhadmin.digitalriver.com/integration/isg/schematable/UserManagement/25)  | [View](https://drhadmin.digitalriver.com/integration/xsd/UserManagement/25) | Not available |
| 24          | [View ](https://drhadmin.digitalriver.com/integration/isg/schematable/UserManagement/24) | [View](https://drhadmin.digitalriver.com/integration/xsd/UserManagement/24) | Not available |
