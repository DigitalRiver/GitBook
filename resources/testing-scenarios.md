---
description: Learn how to use a test order to ensure your integration functions properly.
---

# Testing scenarios

This page explains how to start testing your payment integrations and provides links to the [payment methods currently supported in our test environment](testing-scenarios.md#payment-methods). When testing standard payment methods, such as [credit cards](testing-scenarios.md#credit-cards), we provide data you can use to test against success and error scenarios.

Digital River maintains the Client Test Environment (CTE) for the [Commerce API](https://docs.digitalriver.com/commerce-api/). In this environment, you'll never interact directly with the payments services. Instead, you'll be directed to a generic page that contains accept and reject options.‌

## Payment methods <a href="#payment-methods" id="payment-methods"></a>

{% tabs %}
{% tab title="Credit Cards" %}
### Success Scenarios&#x20;

If the card numbers in this section fail to produce a success scenario, try entering a different purchase amount, currency, or quantity.&#x20;

The [Get Credit Card Numbers](https://www.getcreditcardnumbers.com/) website is useful for generating valid test card numbers. The site provides numbers that validate when passed through the MOD 10 algorithm.&#x20;

#### Basic Card Numbers&#x20;

To test a successful payment, use the following credit card numbers. The expiration date must be one day in the future. Except for Visa, the security code is any random three or four-digit number.

<table data-header-hidden><thead><tr><th>Card Number</th><th width="137">Brand</th><th>Expiration Date</th><th>Security Code</th></tr></thead><tbody><tr><td>Card Number</td><td>Brand</td><td>Expiration Date</td><td>Security Code</td></tr><tr><td>3434 567890 12341</td><td>American Express</td><td>Any future date</td><td>Any four digits</td></tr><tr><td>3034 567890 1235</td><td>Diners Club</td><td>Any future date</td><td>Any three digits</td></tr><tr><td>6011 9876 9876 9876</td><td>Discover</td><td>Any future date</td><td>Any three digits</td></tr><tr><td>3528 9876 9876 9879 </td><td>JCB </td><td>Any future date</td><td>Any three digits</td></tr><tr><td>5466 1600 0000 0008</td><td>Mastercard</td><td>Any future date</td><td>Any three digits</td></tr><tr><td>6226 2200 0000 0009</td><td>UnionPay</td><td>Any future date</td><td>Any three digits</td></tr><tr><td>4444 2222 3333 1111</td><td>Visa</td><td>Any future date</td><td>123</td></tr></tbody></table>

#### 3D Secure 1 Card Numbers

You can also test how your integration handles different 3D Secure 1 authentication scenarios. To test your 3D Secure 1 integrations, use the following test data:

<table data-header-hidden><thead><tr><th>Card Number</th><th width="93">Brand</th><th>Expiration Date</th><th>Security Code</th><th>Notes</th></tr></thead><tbody><tr><td>Card Number</td><td>Brand</td><td>Expiration Date</td><td>Security Code</td><td>Notes</td></tr><tr><td>4212 3456 7890 1237</td><td>Visa</td><td>10/2030</td><td>737</td><td>When prompted to authenticate via the test page, enter <strong>user</strong> and <strong>password</strong>.</td></tr></tbody></table>

#### 3D Secure 2 Card Numbers

You can also test how your integration handles different 3D Secure 2 authentication scenarios. To test your 3D Secure 2 integrations, use the following test data:

<table data-header-hidden><thead><tr><th>Card Number</th><th width="123">Brand</th><th>Expiration Date</th><th>Security Code</th></tr></thead><tbody><tr><td>Card Number</td><td>Brand</td><td>Expiration Date</td><td>Security Code</td></tr><tr><td>3714 4963 5398 431</td><td>American Express</td><td>10/2030</td><td>7373</td></tr><tr><td>4035 5014 2814 6300</td><td>Cartes Bancaires</td><td>03/2030</td><td>737</td></tr><tr><td>3056 9309 0259 04</td><td>Diners</td><td>03/2030</td><td>737</td></tr><tr><td>6011 1111 1111 1117</td><td>Discover</td><td>03/2030</td><td>737</td></tr><tr><td>3566 1111 1111 1113</td><td>JCB</td><td>03/2030</td><td>737</td></tr><tr><td>5454 5454 5454 5454</td><td>Mastercard</td><td>03/2030</td><td>737</td></tr><tr><td>6212 3456 7890 1232</td><td>UnionPay</td><td>03/2030</td><td>737</td></tr><tr><td>4917 6100 0000 0000</td><td>Visa</td><td>03/2030</td><td>737</td></tr></tbody></table>

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

<table data-header-hidden><thead><tr><th width="135">Option</th><th>Description</th></tr></thead><tbody><tr><td>Option</td><td>Description</td></tr><tr><td>Approve</td><td><code>Source</code> moves to <code>chargeable</code> state</td></tr><tr><td>Decline</td><td><code>Source</code> remains in a <code>pending_redirect</code> state.</td></tr></tbody></table>

### Error Scenarios&#x20;

After being triggered, PayPal error scenarios provide the following unique data to the `Source` owner:&#x20;

<table data-header-hidden><thead><tr><th width="204">Scenario</th><th>Description</th></tr></thead><tbody><tr><td>Scenario</td><td>Description</td></tr><tr><td>SourceCreationFail</td><td><code>Source</code> creation fails. The <code>Source</code> state is <code>failed</code> .</td></tr><tr><td>ChargeCreationFail</td><td><code>Source</code> creation is successful but <code>Charge</code> creation fails. The <code>Charge</code> state is <code>failed</code> .</td></tr><tr><td>RefundFail</td><td><code>Source</code> and <code>Charge</code> creation is successful. Any refunds against the charge fail. <code>Refund</code> state is <code>failed</code> .</td></tr></tbody></table>
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

<table data-header-hidden><thead><tr><th width="199">Scenario</th><th>Description</th></tr></thead><tbody><tr><td>Scenario</td><td>Description</td></tr><tr><td>SourceCreationFail</td><td><code>Source</code> creation fails. The <code>Source</code> state is <code>failed</code> .</td></tr><tr><td>ChargeCreationFail</td><td><code>Source</code> creation is successful but <code>Charge</code> creation fails. The <code>Charge</code> state is <code>failed</code> .</td></tr><tr><td>RefundFail</td><td><code>Source</code> and <code>Charge</code> creation is successful. Any refunds against the charge fail. <code>Refund</code> state is <code>failed</code> .</td></tr></tbody></table>
{% endtab %}

{% tab title="Wire Transfer" %}
### Success Scenarios&#x20;

After providing success scenario test data, you'll receive a `Source` in a `pending_funds` state. The `Source` may then be used to complete your `Checkout` or `Order` .

### Error Scenarios&#x20;

After being triggered, Wire Transfer error scenarios provide the following unique data to the `Source` owner:

<table data-header-hidden><thead><tr><th width="267">Scenario</th><th>Description</th></tr></thead><tbody><tr><td>Scenario</td><td>Description</td></tr><tr><td>SourceCreationFail</td><td><code>Source</code> creation fails. The <code>Source</code> state is <code>failed</code> .</td></tr><tr><td>SourceFailWithDelay</td><td><code>Source</code> creation is successful but <code>Charge</code> creation fails. The <code>Charge</code> state is <code>failed</code> .</td></tr><tr><td>RefundFailWhileCreation</td><td><code>Source</code> and <code>Charge</code> creation is successful. Any refunds against the charge fail. The <code>Refund</code> state is <code>failed</code> .</td></tr><tr><td>RefundFailAfterPaymentInfo</td><td><code>Source</code> and <code>Charge</code> creation is successful. A refund request against the charge is successful but ultimately fails to refund.</td></tr></tbody></table>
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

<table data-header-hidden><thead><tr><th width="158">Option</th><th>Description</th></tr></thead><tbody><tr><td>Option</td><td>Description</td></tr><tr><td>Approve</td><td><code>Source</code> moves to <code>chargeable</code> state</td></tr><tr><td>Decline</td><td><code>Source</code> remains in a <code>pending_redirect</code> state.</td></tr></tbody></table>

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

<table data-header-hidden><thead><tr><th width="154">Option</th><th>Description</th></tr></thead><tbody><tr><td>Option</td><td>Description</td></tr><tr><td>Approve</td><td><code>Source</code> moves to <code>chargeable</code> state</td></tr><tr><td>Decline</td><td><code>Source</code> remains in a <code>pending_redirect</code> state.</td></tr></tbody></table>

### Error Scenarios&#x20;

After being triggered, Alipay error scenarios provide the following unique data to the `Source` owner:

<table data-header-hidden><thead><tr><th width="210">Scenario</th><th>Description</th></tr></thead><tbody><tr><td>Scenario</td><td>Description</td></tr><tr><td>authFail</td><td><code>Source</code> creation fails. The <code>Source</code> state is <code>failed</code> .</td></tr><tr><td>authFailAfterRedirect</td><td><code>Source</code> creation is successful but <code>Charge</code> creation fails. The <code>Charge</code> state is <code>failed</code> .</td></tr><tr><td>refundFail</td><td><code>Source</code> and <code>Charge</code> creation is successful. Any refunds against the charge fail. The <code>Refund</code> state is <code>failed</code> .</td></tr></tbody></table>
{% endtab %}
{% endtabs %}
