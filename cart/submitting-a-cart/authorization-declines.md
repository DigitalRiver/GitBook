# Authorization declines

Authorization declines occur when Digital River submits a request to authorize a charge on your customer's [payment source](../sources/) but the request is denied. &#x20;

Digital River works with multiple credit card processors using a proprietary solution that maximizes billing success. If an authorization attempt fails with the first credit card processor, Digital River may try billing against a different processor.

When Digital River cannot obtain a successful authorization, the error `code` returned in the response will indicate the reason for the decline.  Some common reasons for authorization declines are incorrectly entered credit card numbers, invalid security codes, and insufficient funds.&#x20;

In the event of an authorization decline, you maintain responsibility for communicating with the customer, as well as following the Digital River [retry policies](authorization-declines.md#retry-policies).&#x20;

{% hint style="danger" %}
The error code and description returned in the response should never be shared with the customer. Doing so may aid parties that are attempting to carry out fraudulent activities.
{% endhint %}

## Hard declines vs. soft declines

There are two major types of authorization declines: hard and soft.\
\
Hard declines are permanent authorization failures.  In other words, retrying the payment method won't be successful. They are usually due to irreversible events, such as a payment method no longer being valid because the account was closed or the card was stolen. In these cases, you'll need to inform customers that they must either use a different payment method or fix any payment data that was incorrectly entered.  &#x20;

Soft declines, on the other hand, typically occur when the reason for the decline is temporary.  They are often due to insufficient funds or an exceeded daily limit. For [merchant initiated transactions](initiating-a-charge.md#merchant-initiated), after a soft decline occurs, retrying the payment source may be successful. But, there are [certain policies](authorization-declines.md#retry-policies) you must observe when conducting these retries.

{% hint style="danger" %}
The authorization decline (hard or soft) and description returned in the response should never be shared with the customer. Doing so may aid parties that are attempting to carry out fraudulent activities.
{% endhint %}

## Decline codes

The following table explains whether the error `code` you receive in response to a request to authorize a charge indicates a [hard or soft decline](authorization-declines.md#hard-declines-vs-soft-declines).&#x20;

{% hint style="info" %}
You can find a complete list of Commerce API error codes [here](../../error-codes.md).
{% endhint %}

For soft declines, make sure you follow the [retry policies](authorization-declines.md#retry-policies) when submitting additional authorization requests.

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

The following are the retry policies you must adhere to when resubmitting an authorization request:

* No more than one authorization attempt per day per subscription
* No more than four authorization attempts over a 30 day period per subscription

Additionally, we recommend that you do not schedule retries seven days apart. This prevents them from falling on the same day of the week, thereby helping you obtain a higher authorization success rate.
