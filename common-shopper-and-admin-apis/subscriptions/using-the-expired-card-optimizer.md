---
description: >-
  Learn how to use the Expired Card Optimizer (ECO) for a third-party
  subscription engine renewal orders.
---

# Using the Expired Card Optimizer

The Expired Card Optimizer (ECO) is a Billing Optimization feature used to optimize the subscription renewal for credit cards only. It is designed to renew orders for the Digital River subscription engine as described in [Providing subscription information](../../shopper-apis/cart/creating-or-updating-a-cart/providing-subscription-information.md). However, as described below, you can use the ECO to renew subscriptions for a third-party subscription engine (that is, a non-Digital River subscription engine).

## Renewing subscriptions that do not use the Digital River subscription engine

To use ECO to renew a subscription that does not use the Digital River subscription engine, insert both the `subscriptionInfo` and `billingOptimization` in the `lineItem` array when you create a cart using [`POST /v1/shoppers/me/carts/active`](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Third-Party-Subscription-Engine-Support/paths/\~1v1\~1shoppers\~1me\~1carts\~1active%20\(subscriptionInfo\)/post) for a third-party subscription engine.

{% hint style="warning" %}
Only provide the information used in this example to renew orders when not using the Digital River subscription engine. An expired credit card does not occur during the initial acquisition, so this information is not required during the initial acquisition.&#x20;
{% endhint %}

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```json
curl --location --request POST 'https://api.digitalriver.com/v1/shoppers/me/carts/active' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{Token}}' \
--data-raw '{
    "cart": {
        "ipAddress": "{{BrowserIP}}",
        "lineItems": {
            "lineItem": [
                {
                    "quantity": 2,
                    "product": {
                        "id": "{{productId}}"
                    }
                    "billingOptimization": {
                        "subscriptionId": "{{SubscriptionId}}",
                        "segmentId": "{{SubscriptionId}}"+"{{segmentCount}}",
                        "renewalAttemptNumber": 3
                    }
                    "subscriptionInfo": {
                        "autoRenewal": true,
                        "terms": "I agree to have the client charge all my future bills on this card",
                        "freeTrial": false,
                        "startTime": "2020-08-01T00:00:00.000Z",
                        "endTime": "2021-08-01T00:00:00.000Z",
                        "billingAgreementId": "{{BillingAgreementID}}"
                    }
                }
            ]
        },
        "chargeType": "merchant_initiated"
    }
}'
```
{% endcode %}
{% endtab %}
{% endtabs %}

| Parameter             | Definition                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| --------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `subscriptionInfo`    | The subscription information should indicate the order uses a third-party subscription engine. Note that Digital River does not validate data from non-Digital River subscription engines.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| `billingOptimization` | <p>To trigger an ECO, provide the following subscription information under <code>billingOptimization</code>: </p><ul><li><code>subscriptionId</code>–The subscription's unique identifier. The <code>subscriptionId</code> is a string of up to 32 characters.</li><li><p><code>segmentId</code>–The unique segment identifier for each renewal term must be unique across all of Digital River's client's subscriptions. The <code>segmentId</code> is a string of up to 32 characters. </p><p>The segment identifier value changes after each renewal attempt and increments upwards (for example, <code>7654321seg2</code>, <code>7654321seg3</code>). </p><p>You can format the <code>segmentId</code> as follows:</p><p><code>"segmentId": "{{subscriptionId}}"+{{segmentCount}}",</code></p><p>Where the value for <code>subscriptionId</code> is a string of up to 32 characters.</p></li><li><code>renewalAttemptNumber</code>–The number of billing attempts for the current renewal. Then the value resets to <code>1</code> after each successful renewal. At the time of the first renewal attempt, ECO generates an incremented expiration date schedule that lives in a Billing Optimization table.</li></ul> |

{% hint style="success" %}
The renewal orders for a Digital River subscription provide all the necessary information. Therefore, there is no need for you to insert this information manually.
{% endhint %}
