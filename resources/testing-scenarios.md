---
description: Learn how to use test payment methods.
---

# Testing scenarios

This page explains how to get started testing your payment integrations and provides links to the [payment methods currently supported in our test environment](testing-scenarios.md#payment-methods). When testing standard payment methods, such as [credit cards](testing-scenarios.md#credit-cards), we provide data you can use to test against success and error scenarios.

Digital River maintains the Client Test Environment (CTE) for the [Commerce API](https://docs.digitalriver.com/commerce-api/). In this environment, you'll never interact directly with the payments services. Instead, you'll be directed to a generic page that contains accept and reject options.‌

## Payment methods <a href="#payment-methods" id="payment-methods"></a>

{% tabs %}
{% tab title="Credit Cards" %}
### Success Scenarios&#x20;

If the card numbers in this section fail to produce a success scenario, try entering a different purchase amount, currency, or quantity.&#x20;

The [Get Credit Card Numbers](https://www.getcreditcardnumbers.com/) website is a useful resource for generating valid test card numbers. The site provides numbers that are a possible combination of characters that validate when passed through the MOD 10 algorithm.&#x20;

#### Basic Card Numbers&#x20;

To test a successful payment, use the following credit card numbers. The expiration date must be at least one day in the future. With the exception of Visa, the security code can be any random three or four-digit number.

| Card Number          | Brand            | Expiration Date | Security Code    |
| -------------------- | ---------------- | --------------- | ---------------- |
| 3434 567890 12341    | American Express | Any future date | Any four digits  |
| 3034 567890 1235     | Diners Club      | Any future date | Any three digits |
| 6011 9876 9876 9876  | Discover         | Any future date | Any three digits |
| 3528 9876 9876 9879  | JCB              | Any future date | Any three digits |
| 5466 1600 0000 0008  | Mastercard       | Any future date | Any three digits |
| 6226 2200 0000 0009  | UnionPay         | Any future date | Any three digits |
| 4444 2222 3333 1111  | Visa             | Any future date | 123              |

#### 3D Secure 1 Card Numbers

You can also test how your integration handles different 3D Secure 1 authentication scenarios. To test your 3D Secure 1 integrations, use the following test data:

| Card Number         | Brand | Expiration Date | Security Code | Notes                                                                             |
| ------------------- | ----- | --------------- | ------------- | --------------------------------------------------------------------------------- |
| 4212 3456 7890 1237 | Visa  | 10/2030         | 737           | When prompted to authenticate via the test page, enter **user** and **password**. |

#### 3D Secure 2 Card Numbers

You can also test how your integration handles different 3D Secure 2 authentication scenarios. To test your 3D Secure 2 integrations, use the following test data:

| Card Number         | Brand            | Expiration Date | Security Code |
| ------------------- | ---------------- | --------------- | ------------- |
| 3714 4963 5398 431  | American Express | 10/2030         | 7373          |
| 4035 5014 2814 6300 | Cartes Bancaires | 03/2030         | 737           |
| 3056 9309 0259 04   | Diners           | 03/2030         | 737           |
| 6011 1111 1111 1117 | Discover         | 03/2030         | 737           |
| 3566 1111 1111 1113 | JCB              | 03/2030         | 737           |
| 5454 5454 5454 5454 | Mastercard       | 03/2030         | 737           |
| 6212 3456 7890 1232 | UnionPay         | 03/2030         | 737           |
| 4917 6100 0000 0000 | Visa             | 03/2030         | 737           |

When prompted for 3D Secure 2 text challenges, use these credentials:

| App Type | Password |
| -------- | -------- |
| Mobile   | 1234     |
| Web      | password |

### Error Scenarios

Use these test card numbers to create payments that generate specific error scenarios. The expiration date must be at least one day in the future. The security code can be any random three-digit number:

| Card Number         | Error Scenario                                                                                       |
| ------------------- | ---------------------------------------------------------------------------------------------------- |
| 4000 0000 0000 3295 | `Source` creation fails. The `Source` state is `failed`.                                             |
| 4000 0000 0000 3600 | `Source` creation is successful but `Charge` creation fails. The `Charge` state is `failed`.         |
| 4000 0000 0000 4103 | `Source` and `Charge` creation are successful, but `Capture` fails. The `Capture` state is `failed`. |
| 4000 0000 0000 4663 | `Source`, `Charge` and `Capture` are successful, but `Refund` fails. The `Refund` state is `failed`. |
| 4000 0000 0000 4442 | `Source` and `Charge` creation are successful, but `Cancel` fails. The `Cancel` state is `failed`.   |
{% endtab %}

{% tab title="PayPal" %}
### Success Scenarios&#x20;

After providing success scenario test data, you'll receive a `Source` in a `pending_redirect` state. Follow the redirect to select one of the options on the authorization page:&#x20;

| Option  | Description                                     |
| ------- | ----------------------------------------------- |
| Approve | `Source` moves to `chargeable` state            |
| Decline | `Source` remains in a `pending_redirect` state. |

### Error Scenarios&#x20;

After being triggered, PayPal error scenarios provide the following unique data to the `Source` owner:&#x20;

| Scenario           | Description                                                                                                     |
| ------------------ | --------------------------------------------------------------------------------------------------------------- |
| SourceCreationFail | `Source` creation fails. The `Source` state is `failed` .                                                       |
| ChargeCreationFail | `Source` creation is successful but `Charge` creation fails. The `Charge` state is `failed` .                   |
| RefundFail         | `Source` and `Charge` creation is successful. Any refunds against the charge fail. `Refund` state is `failed` . |
{% endtab %}

{% tab title="PayPal Credit" %}
### Success Scenarios&#x20;

After providing success scenario test data, you'll receive a `Source` in a `pending_redirect` state. Follow the redirect to select the following options on the authorization page:

| Option  | Description                                     |
| ------- | ----------------------------------------------- |
| Approve | `Source` moves to `chargeable` state            |
| Decline | `Source` remains in a `pending_redirect` state. |

### Error Scenarios&#x20;

After being triggered, PayPal credit error scenarios provide the following unique data to the `Source` owner:&#x20;

| Scenario           | Description                                                                                                     |
| ------------------ | --------------------------------------------------------------------------------------------------------------- |
| SourceCreationFail | `Source` creation fails. The `Source` state is `failed` .                                                       |
| ChargeCreationFail | `Source` creation is successful but `Charge` creation fails. The `Charge` state is `failed` .                   |
| RefundFail         | `Source` and `Charge` creation is successful. Any refunds against the charge fail. `Refund` state is `failed` . |
{% endtab %}

{% tab title="Wire Transfer" %}
### Success Scenarios&#x20;

After providing success scenario test data, you'll receive a `Source` in a `pending_funds` state. The `Source` may then be used to complete your `Checkout` or `Order` .

### Error Scenarios&#x20;

After being triggered, Wire Transfer error scenarios provide the following unique data to the `Source` owner:

| Scenario                   | Description                                                                                                                     |
| -------------------------- | ------------------------------------------------------------------------------------------------------------------------------- |
| SourceCreationFail         | `Source` creation fails. The `Source` state is `failed` .                                                                       |
| SourceFailWithDelay        | `Source` creation is successful but `Charge` creation fails. The `Charge` state is `failed` .                                   |
| RefundFailWhileCreation    | `Source` and `Charge` creation is successful. Any refunds against the charge fail. The `Refund` state is `failed` .             |
| RefundFailAfterPaymentInfo | `Source` and `Charge` creation is successful. A refund request against the charge is successful but ultimately fails to refund. |
{% endtab %}

{% tab title="SEPA Direct Debit" %}
### Success Scenarios&#x20;

After providing success scenario test data, you'll receive a `Source` in a `pending_redirect` state. Follow the redirect to select the following options on the authorization page:

| Option  | Description                                     |
| ------- | ----------------------------------------------- |
| Approve | `Source` moves to `chargeable` state            |
| Decline | `Source` remains in a `pending_redirect` state. |

### Error Scenarios&#x20;

After being triggered, SEPA Direct Debit error scenarios provide the following unique data to the `Source` owner:

| Scenario                 | Description                                                                                                              |
| ------------------------ | ------------------------------------------------------------------------------------------------------------------------ |
| SourceFail               | `Source` creation fails. The `Source` state is `failed` .                                                                |
| SourceFailAfterRedirect  | `Source` moves to `failed` state after redirecting from payment page.                                                    |
| ChargeFail               | `Source` creation is successful but `Charge` creation fails. The `Charge` state is `failed` .                            |
| ChargeFailedAfterPending | The `Charge` is initially created in a `pending` state. After a webhook call, the `Charge` is moved to a `failed` state. |
| RefundFail               | `Source` and `Charge` creation is successful. Any refunds against the charge fail and the `Refund` state is `failed` .   |
| RefundFailedAfterPending | The `Refund` is initially created in a `pending` state. After a webhook call, the `Refund` is moved to a `failed` state. |
| ChargeRemainPending      | The `Charge` remains in a `pending` state after creation.                                                                |
{% endtab %}

{% tab title="SEPA Direct Debit GB" %}
### Success Scenarios&#x20;

After providing success scenario test data, you'll receive a `source` in a `pending_redirect` state. Follow the redirect to select the following options on the authorization page:

| Option  | Description                                     |
| ------- | ----------------------------------------------- |
| Approve | `Source` moves to `chargeable` state            |
| Decline | `Source` remains in a `pending_redirect` state. |

### Error Scenarios&#x20;

After being triggered, SEPA Direct Debit GB error scenarios provide the following unique data to the `Source` owner:

| Scenario                           | Description                                                                                                              |
| ---------------------------------- | ------------------------------------------------------------------------------------------------------------------------ |
| sourceFail@email.org               | `Source` creation fails. The `Source` state is `failed` .                                                                |
| sourceFailAfterRedirect@email.org  | Source moves to a `failed` state after redirecting from the payment page.                                                |
| chargeFailedAfterWebhook@email.org | The `Charge` is initially created in a `pending` state. After a webhook call, the `Charge` is moved to a `failed` state. |
| refundFail@email.org               | `Source` and `Charge` creation is successful. Any refunds against the charge fail and the `Refund` state is `failed`     |
| refundFailedAfterWebhook@email.org | The `Refund` is initially created in a `pending` state. After a webhook call, the `Refund` is moved to a `failed` state. |
{% endtab %}

{% tab title="Alipay" %}
### Success Scenarios&#x20;

After providing success scenario test data, you'll receive a `Source` in a `pending_redirect` state. Follow the redirect to select one of the options on the authorization page:&#x20;

| Option  | Description                                     |
| ------- | ----------------------------------------------- |
| Approve | `Source` moves to `chargeable` state            |
| Decline | `Source` remains in a `pending_redirect` state. |

### Error Scenarios&#x20;

After being triggered, Alipay error scenarios provide the following unique data to the `Source` owner:

| Scenario              | Description                                                                                                         |
| --------------------- | ------------------------------------------------------------------------------------------------------------------- |
| authFail              | `Source` creation fails. The `Source` state is `failed` .                                                           |
| authFailAfterRedirect | `Source` creation is successful but `Charge` creation fails. The `Charge` state is `failed` .                       |
| refundFail            | `Source` and `Charge` creation is successful. Any refunds against the charge fail. The `Refund` state is `failed` . |
{% endtab %}
{% endtabs %}
