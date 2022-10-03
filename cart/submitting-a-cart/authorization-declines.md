---
description: >-
  Learn about the different types of authorization declines and how to handle
  them.
---

# Authorization declines

When the shopper [submits a cart](./), Digital River must request authorization from the payment provider to create a [charge ](initiating-a-charge.md)for the amount indicated. Sometimes, however, this authorization request is declined.

Digital River works with multiple credit card processors using a proprietary solution that maximizes billing success. If an authorization attempt fails with the first credit card processor, we may try billing against a different processor.

When Digital River cannot obtain a successful authorization, we return an error that indicates the reason for the decline.&#x20;

{% hint style="danger" %}
Do not share the error code with the customer. Doing so may aid parties that are attempting to care out fraudulent activities.
{% endhint %}

Some common reasons for authorization declines are incorrectly entered credit card numbers, invalid security codes, and insufficient funds. In the event of a [hard or soft](authorization-declines.md#hard-declines-vs.-soft-declines) authorization decline, you maintain responsibility for communicating with the customer, as well as following Digital River's [retry policies](authorization-declines.md#retry-policies).

There are two major types of authorization declines: hard and soft.\
\
Hard declines are permanent authorization failures.  In other words, retrying the payment source won't be successful. They are usually due to irreversible events, such as a payment method no longer being valid because the account was closed or the card was stolen. In these cases, you'll need to inform customers that they must either use a different payment method or fix any payment data that was incorrectly entered.  &#x20;

Some common reasons for authorization declines are incorrectly entered credit card numbers, invalid security codes, and insufficient funds. In the event of a [hard or soft](authorization-declines.md#hard-declines-vs.-soft-declines) authorization decline, you maintain responsibility for communicating with the customer, as well as following the Digital River [retry policies](authorization-declines.md#retry-policies).&#x20;

Soft declines, on the other hand, typically occur when the reason for the decline is temporary.  They are often due to insufficient funds or an exceeded daily limit. After a soft decline occurs, retrying the payment source may be successful. But, there are certain [retry policies](authorization-declines.md#retry-policies) you must observe when conducting these retries.

## Hard declines vs. soft declines

There are two major types of authorization declines: hard and soft.\
\
Hard declines are permanent authorization failures.  In other words, retrying the [payment source](../../payments/sources/) won't be successful. They are usually due to irreversible events, such as a payment method no longer being valid because the account was closed, or the card was stolen. In these cases, you'll need to inform customers that they must either use a different payment method or fix any payment data that was entered incorrectly.  &#x20;

Soft declines, on the other hand, typically occur when the reason for the decline is temporary. They are often due to insufficient funds or an exceeded daily limit. After a soft decline occurs, retrying the [payment source](../../payments/sources/) may be successful but there are certain [retry policies](authorization-declines.md#retry-policies) that you must observe.

## Decline codes&#x20;

For customer-initiated and merchant-initiated transactions, the following table explains whether the error code you receive indicates a [hard or soft decline](authorization-declines.md#hard-declines-vs.-soft-declines). When it's a soft decline, make sure you follow the [retry policies](authorization-declines.md#retry-policies) when submitting additional authorization requests. See the complete list of [error codes](../../error-codes.md) for more information.

### `account_closed`

* **Customer-initiated decline type**: Hard
* **Merchant-initiated decline type**: Hard

### `account_frozen`

* **Customer-initiated decline type**: Hard
* **Merchant-initiated decline type**: Hard

### `authentication_required`

* **Customer-initiated decline type**: Soft
* **Merchant-initiated decline type**: Soft

### `blacklisted_card`

* **Customer-initiated decline type**: Hard
* **Merchant-initiated decline type**: Hard

### `card_expired`

* **Customer-initiated decline type**: Hard
* **Merchant-initiated decline type**: Soft

### `card_limit_exceeded`

* **Customer-initiated decline type**: Hard
* **Merchant-initiated decline type**: Soft

### `card_not_active`

* **Customer-initiated decline type**: Hard
* **Merchant-initiated decline type**: Soft

### `card_type_block`

* **Customer-initiated decline type**: Hard
* **Merchant-initiated decline type**: Hard

### `card_velocity_exceeded`

* **Customer-initiated decline type**: Hard
* **Merchant-initiated decline type**: Soft

### `declined`

* **Customer-initiated decline type**: Hard
* **Merchant-initiated decline type**: Hard

### `declined_can_retry`

* **Customer-initiated decline type**: Soft
* **Merchant-initiated decline type**: Soft

### `do_not_honor`

* **Customer-initiated decline type**: Soft
* **Merchant-initiated decline type**: Soft

### `duplicate_transaction`

* **Customer-initiated decline type**: Hard
* **Merchant-initiated decline type**: Soft

### `fraud`

* **Customer-initiated decline type**: Hard
* **Merchant-initiated decline type**: Hard

### `fraud_block`

* **Customer-initiated decline type**: Hard
* **Merchant-initiated decline type**: Hard

### `illegal_action`

* **Customer-initiated decline type**: Hard
* **Merchant-initiated decline type**: Hard

### `insufficient_funds`

* **Customer-initiated decline type**: Hard
* **Merchant-initiated decline type**: Soft

### `invalid_address`

* **Customer-initiated decline type**: Hard
* **Merchant-initiated decline type**: Hard

### `invalid_amount`

* **Customer-initiated decline type**: Hard
* **Merchant-initiated decline type**: Hard

### `invalid_card_bin`

* **Customer-initiated decline type**: Hard
* **Merchant-initiated decline type**: Hard

### `invalid_card_number`

* **Customer-initiated decline type**: Hard
* **Merchant-initiated decline type**: Hard

### `invalid_currency`

* **Customer-initiated decline type**: Hard
* **Merchant-initiated decline type**: Soft

### `invalid_expiration_date`

* **Customer-initiated decline type**: Hard
* **Merchant-initiated decline type**: Soft

### `invalid_field_data`

* **Customer-initiated decline type**: Hard
* **Merchant-initiated decline type**: Hard

### `invalid_merchant`

* **Customer-initiated decline type**: Hard
* **Merchant-initiated decline type**: Hard

### `invalid_payment_method`

* **Customer-initiated decline type**: Hard
* **Merchant-initiated decline type**: Hard

### `invalid_pin`

* **Customer-initiated decline type**: Hard
* **Merchant-initiated decline type**: Hard

### `invalid_security_code`

* **Customer-initiated decline type**: Hard
* **Merchant-initiated decline type**: Hard

### `invalid_security_field`

* **Customer-initiated decline type**: Hard
* **Merchant-initiated decline type**: Hard

### `invalid_transaction_type`

* **Customer-initiated decline type**: Hard
* **Merchant-initiated decline type**: Hard

### `issuer_invalid_card`

* **Customer-initiated decline type**: Hard
* **Merchant-initiated decline type**: Hard

### `issuer_not_found`

* **Customer-initiated decline type**: Hard
* **Merchant-initiated decline type**: Hard

### `issuer_unavailable`

* **Customer-initiated decline type**: Soft
* **Merchant-initiated decline type**: Soft

### `limit_exceeded`

* **Customer-initiated decline type**: Hard
* **Merchant-initiated decline type**: Hard

### `lost_stolen_card`

* **Customer-initiated decline type**: Hard
* **Merchant-initiated decline type**: Hard

### `mid_limit_exceeded`

* **Customer-initiated decline type**: Hard
* **Merchant-initiated decline type**: Soft

### `new_card_issued`

* **Customer-initiated decline type**: Hard
* **Merchant-initiated decline type**: Soft

### `no_response`

* **Customer-initiated decline type**: Soft
* **Merchant-initiated decline type**: Soft

### `pin_try_exceeded`

* **Customer-initiated decline type**: Hard
* **Merchant-initiated decline type**: Soft

### `restricted_card`

* **Customer-initiated decline type**: Hard
* **Merchant-initiated decline type**: Hard

### `sca_not_completed`

* **Customer-initiated decline type**: Soft
* **Merchant-initiated decline type**: Soft

### `stop_recurring`

* **Customer-initiated decline type**: Hard
* **Merchant-initiated decline type**: Hard

### `suspected_fraud`

* **Customer-initiated decline type**: Hard
* **Merchant-initiated decline type**: Soft

### `unidentified_error`

* **Customer-initiated decline type**: Soft
* **Merchant-initiated decline type**: Soft

### `voice_authorization_required`

* **Customer-initiated decline type**: Hard
* **Merchant-initiated decline type**: Hard

## Retry policies

The following are the retry policies you must adhere to when resubmitting an authorization request:

* No more than one authorization attempt per day per subscription
* No more than four authorization attempts over a 30-day period per subscription

Additionally, we recommend that you do not schedule retries seven days apart. This prevents them from falling on the same day of the week, thereby helping you obtain a higher authorization success rate.
