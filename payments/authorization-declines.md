---
description: >-
  Learn about the different types of authorization declines and how to handle
  them.
---

# Authorization declines

At the time of [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) creation, Digital River submits a request to authorize a [charge](../order-management/orders/payment-charges/) on the transaction's [payment source](payment-sources/). Sometimes, however, this authorization request is declined.

Digital River's proprietary solution maximizes billing success with multiple credit card processors. If an authorization attempt fails with the first credit card processor, we may try billing against a different processor.

When Digital River cannot obtain a successful authorization, we return an error that indicates the reason for the decline.

{% hint style="danger" %}
Do not share the error code with the customer. Doing so may aid parties that are attempting to carry out fraudulent activities.
{% endhint %}

Some common reasons for authorization declines are incorrectly entered credit card numbers, invalid security codes, and insufficient funds. In the event of a [hard or soft](authorization-declines.md#hard-declines-vs-soft-declines) authorization decline, you maintain responsibility for communicating with the customer and following Digital River's [retry policies](authorization-declines.md#retry-policies).

## Hard declines vs. soft declines <a href="#hard-declines-vs-soft-declines" id="hard-declines-vs-soft-declines"></a>

There are two major types of authorization declines: hard and soft.

Hard declines are permanent authorization failures. In other words, retrying the [payment source](payment-sources/) won't be successful. They are usually due to irreversible events, such as a payment method no longer being valid because the account was closed or the card was stolen. In these cases, you'll need to inform customers that they must either use a different payment method or fix any payment data that was incorrectly entered.

Soft declines, on the other hand, typically occur when the reason for the decline is temporary. They are often due to insufficient funds or an exceeded daily limit. After a soft decline occurs, retrying the [payment source](payment-sources/) may be successful, but there are certain [retry policies](authorization-declines.md#retry-policies) that you must observe.

## Decline codes for merchant-initiated transactions <a href="#decline-codes" id="decline-codes"></a>

For [merchant-initiated transactions](../integration-options/checkouts/creating-checkouts/initiating-a-charge.md#merchant-initiated), the following table explains whether the error code you receive indicates a [hard or soft decline](authorization-declines.md#hard-declines-vs-soft-declines). When it's a soft decline, follow the [retry policies](authorization-declines.md#retry-policies) when submitting additional authorization requests.

{% hint style="info" %}
You can find a complete list of [error codes](https://www.digitalriver.com/docs/digital-river-api-reference/#section/Response-status-codes/Error-codes) in our [API reference documentation](https://www.digitalriver.com/docs/digital-river-api-reference/#section/Explore-Digital-River-Products).
{% endhint %}

| Error code                     | Decline type |
| ------------------------------ | ------------ |
| `account_closed`               | Hard         |
| `card_expired`                 | Soft         |
| `card_limit_exceeded`          | Soft         |
| `card_type_block`              | Hard         |
| `card_velocity_exceeded`       | Soft         |
| `declined`                     | Hard         |
| `do_not_honor`                 | Soft         |
| `fraud`                        | Hard         |
| `fraud_block`                  | Hard         |
| `insufficient_funds`           | Soft         |
| `invalid_address`              | Hard         |
| `invalid_amount`               | Hard         |
| `invalid_card_bin`             | Hard         |
| `invalid_card_number`          | Hard         |
| `invalid_currency`             | Hard         |
| `invalid_expiration_date`      | Hard         |
| `invalid_pin`                  | Hard         |
| `invalid_security_code`        | Hard         |
| `invalid_transaction_type`     | Hard         |
| `issuer_invalid_card`          | Hard         |
| `issuer_not_found`             | Hard         |
| `issuer_unavailable`           | Soft         |
| `limit_exceeded`               | Soft         |
| `lost_stolen_card`             | Hard         |
| `mid_limit_exceeded`           | Soft         |
| `no_response`                  | Soft         |
| `pin_try_exceeded`             | Soft         |
| `restricted_card`              | Hard         |
| `stop_recurring`               | Hard         |
| `voice_authorization_required` | Hard         |

## Retry policies

You must adhere to the following retry policies when resubmitting an authorization request:

* No more than one authorization attempt per day per subscription
* No more than four authorization attempts over a 30-day period per subscription

Additionally, we recommend that you do not schedule retries seven days apart. This prevents the requests from falling on the same day of the week, helping you obtain a higher authorization success rate.
