---
description: Understand the credit card error and declined messages.
---

# Credit card error and declined messages

A transaction error for a payment method such as a credit card saved in the payment source may contain additional information as shown in the following [declined message](../../shopper-apis/cart/submitting-a-cart/authorization-declines.md) (`declinedMessage`) example:

{% code overflow="wrap" %}
```json
"errors": {
    "error": [
        {
            "relation": "https://developers.digitalriver.com/v1/shoppers/SubmitCartResource",
            "code": "declined",
            "subcode": "fraud_block",
            "description": "The transaction has been identified by Digital River as fraudulent.",
            "declinedMessage": {
                "merchantDeclinedType": "Hard",
                "customerDeclinedType": "Hard",
                "code": "7011"
            }
        }
    ]
}
```
{% endcode %}

## Credit card error codes

The error codes for transactions using a credit card saved in the payment source are described below.

### `declined`

The `declined` error code has the following subcodes:

* `account_frozen`–The account is frozen.
* `account_closed`–The account is closed.
* `authentication_required`–The transaction requires authentication.
* `blacklisted_card`–The credit card is blacklisted.
* `card_limit_exceeded`–The transaction exceeds the card limit amount.
* `card_not_active`–The card is not active yet.
* `card_type_block`–The merchant has blocked this card type.
* `card_velocity_exceeded`–The transaction exceeds the velocity amount.
* `declined`–The card has been declined for an unknown reason.
* `declined_can_retry`–The card has been declined for an unknown reason.
* `do_not_honor`–The card issuing bank has declined this payment.
* `duplicate_transaction`–The transaction is a duplicate.
* `fraud`–The transaction has been identified by the issuing bank as fraudulent.
* `fraud`–The transaction has been identified as fraudulent.
* `fraud_block`–The transaction has been identified by Digital River as fraudulent.
* `illegal_action`–The transaction has been identified as illegal.
* `insufficient_funds`–The card has insufficient funds to complete the purchase
* `invalid_amount`–The amount is not accepted by the card network.
* `invalid_currency`–The currency is not supported.
* `invalid_field_data`–The transaction contains invalid data.
* `invalid_merchant`–The merchant is invalid for this type of transaction.
* `invalid_payment_method`–The payment method used is invalid.
* `invalid_security_field`–The transaction contains invalid data.
* `invalid_transaction_type`–The transaction type is invalid.
* `issuer_unavailable`–The card does not exist with the issuer.
* `limit_exceeded`–The transaction amount exceeds your assigned limit.
* `lost_stolen_card`–The issuing bank has marked this card as lost or stolen.
* `mid_limit_exceeded`–The transaction amount exceeds the limit assigned for this MID.
* `new_card_issued`–New account information is available.
* `no_response`–The payment processor did not respond.
* `pin_try_exceeded`–The bank's allowable number of PIN tries has been exceeded.
* `restricted_card`–The use of this card has been restricted by the card network.
* `sca_not_completed`–The payment authorization was not initiated as the shopper did not successfully complete the authentication process.
* `stop_recurring`–Stop all billing as this account is closed.
* `suspected_fraud`–The issuer has identified this transaction potentially as fraudulent.
* `unidentified_error`–The card has been declined for an unknown reason.

### `declined - contact bank`

The `declined - contact bank` error code has the following subcodes:

* `voice_authorization_required`–Voice authorization is required by the issuer.

### `invalid`

The `invalid` error code has the following subcodes:

* `issuer_invalid_card`–The card does not exist with the issuer.

### `invalid card`

The `invalid card` error code has the following subcodes:

* `card_expired`–The card is expired.
* `invalid_address`–The address does not match the card network's records.
* `invalid_card_number`–The card number entered is invalid.
* `invalid_card_bin`–The card bin is invalid.
* `invalid_expiration_date`–The card is expired or the expiration date is invalid.
* `invalid_pin`–The PIN provided is invalid or incorrect.
* `invalid_security_code`–The security code provided is invalid or incorrect.
* `issuer_not_found`–The card issuer does not exist.

## Declined messages

### `declinedMessage`&#x20;

A `declinedMessage` includes the following information:

* `code`–This code helps to categorize failure reasons for the declined message that look different but point to the same issue.
* `merchantDeclinedType`–This field indicates the authentication decline type of transaction initiated by the merchant.
* `customerDeclinedType`–This field indicates the authentication decline type of transaction initiated by the shopper.
