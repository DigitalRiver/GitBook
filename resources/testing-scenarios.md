---
description: Learn how to test payment methods.
---

# Testing scenarios

This page explains how to [start testing](testing-scenarios.md#getting-started) your payment integrations and provides links to the [payment methods currently supported in our test environment](testing-scenarios.md#payment-methods). When testing standard payment methods, such as [cards (credit and debit)](testing-scenarios.md#testing-standard-payment-methods), we provide data you can use to test against success and error scenarios. We also provide information on testing [redirect](testing-scenarios.md#testing-redirect-payment-methods) and [receiver](testing-scenarios.md#testing-receiver-payment-methods)-type payment methods.

## Getting started

When evaluating your integration, always use your [test API keys](API-structure/api-keys.md). This prevents you from interacting directly with payment services and ensures that the test data you enter does not create an actual charge or result in the transfer of funds.

Use your confidential (secret) test API key when conducting testing in the Digital River API. Use your public test API key to create test payment sources in DigitalRiver.js.

Your testing approach depends on whether the payment method has an [authentication flow](../payments/sources/#authentication-flow) of standard, redirect, or receiver. If you don't know the flow of the payment method you'd like to test, you can find it on the [Supported payment methods](../payments/supported-payment-methods/) page.

## Supported payment methods in a test environment

The Commerce APIs support a wide range of payment methods. Not all of them, however, are currently supported in our testing environment. You can find the test environment status for each payment method on the Supported payment methods page.

## Testing standard payment methods

The payment methods with a `standard` [authentication flow](../payments/sources/#authentication-flow) that Digital River currently supports in our testing environment are Apple Pay, Credit Cards, and Google Pay.&#x20;

Before accepting live payments, you can use the card numbers in this section to test against [success](testing-scenarios.md#success-scenarios-2) and [error](testing-scenarios.md#error-scenarios-2) scenarios. These numbers are only valid in our testing environment. They do not create a real charge or result in a transfer of funds.

To conduct the testing, [create a source](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Source/operation/createSources), and use the appropriate data to set the parameters of the `creditCard` hash table.

#### Success Scenarios&#x20;

To test a successful payment, use the following **basic credit card numbers**. The expiration date must be at least one day in the future. Except for Visa, the security code can be any random three or four-digit number.

| Card Number          | Brand            | Expiration Date | Security Code    |
| -------------------- | ---------------- | --------------- | ---------------- |
| 3434 567890 12341    | American Express | Any future date | Any four digits  |
| 3034 567890 1235     | Diners Club      | Any future date | Any three digits |
| 6011 9876 9876 9876  | Discover         | Any future date | Any three digits |
| 3528 9876 9876 9879  | JCB              | Any future date | Any three digits |
| 5466 1600 0000 0008  | Mastercard       | Any future date | Any three digits |
| 6226 2200 0000 0009  | UnionPay         | Any future date | Any three digits |
| 4444 2222 3333 1111  | Visa             | Any future date | 123              |

You can also test how your integration handles different 3D Secure 2 authentication scenarios. To test your 3D Secure 2 integrations, use the following test data:

| Card Number         | Brand      | Expiration Date | Security Code |
| ------------------- | ---------- | --------------- | ------------- |
| 5454 5454 5454 5454 | Mastercard | 03/2030         | 737           |
| 4917 6100 0000 0000 | Visa       | 10/2030         | 737           |

When prompted for 3D Secure 2 text challenges, use these credentials:

| App Type | Password |
| -------- | -------- |
| Mobile   | 1234     |
| Web      | password |

#### Error Scenarios

Use these test card numbers to create payments that generate specific error scenarios. The expiration date must be at least one day in the future. The security code can be any random three-digit number:

| Card Number         | Error Scenario                                                                                             |
| ------------------- | ---------------------------------------------------------------------------------------------------------- |
| 4000 0000 0000 3295 | A Source is not created. The `state` of the Source is `failed`.                                            |
| 4000 0000 0000 3600 | A Source is successfully created but the Charge fails. The `state` of the Charge is `failed`.              |
| 4000 0000 0000 4103 | Both a Source and Charge are successfully created, but the Capture fails. The Capture `state` is `failed`. |
| 4000 0000 0000 4663 | Source, Charge, and Capture are successful, but `Refund` fails. The `Refund state` is `failed`.            |
| 4000 0000 0000 4442 | Both a Source and Charge are successfully created, but the Cancel fails. The Cancel `state` is `failed`.   |

## Testing redirect payment methods

The following are the payment methods with a `redirect` [authentication flow](../payments/sources/#authentication-flow) that Digital River currently supports in our testing environment: Afterpay, Alipay (domestic), Alipay+ (cross-border), Amazon Pay, Bancontact, BLIK, Boleto, CCAvenue, Clearpay, iDEAL, Klarna, Online Banking (FPX), Online Banking (IBP), Online Banking (Korea Bank Transfer), PayCo, PayPal, PayPal Billing, PayPal Credit, PayPal Py in 3, PayPal Pay in 4, PayPal RatenZahlung, SEPA Direct Debit, and TreviPay.

### Success scenarios

Use the [create source method](../shopper-apis/cart/payment-sessions.md#creating-a-source-with-payment-sessions) to provide success scenario test data for redirect payment sources. Once you've done this, you should receive a Source in a `pending_redirect` state.

You'll then be directed to our generic authorization page that contains accept and reject options. Follow the redirect and select one of the following options:

| Option  | Expected result                                   |
| ------- | ------------------------------------------------- |
| Approve | The Source moves to a `chargeable` state          |
| Decline | The Source remains in a `pending_redirect` state. |

### Error scenarios

First, select one of the following payment methods for redirect sources. Then identify the error scenario you would like to test against. Finally, when [creating an authority](broken-reference) set the `lastName` parameter in the [Owner object](broken-reference) to the value you expect to trigger the scenario.

{% tabs %}
{% tab title="PayPal" %}
This tab's testing information applies to PayPal, PayPal Billing Agreement, and PayPal Credit.

| Scenario             | Description                                                                                                     |
| -------------------- | --------------------------------------------------------------------------------------------------------------- |
| `lastName` parameter | Expected result                                                                                                 |
| SourceCreationFail   | `Source` creation fails. The `Source` state is `failed` .                                                       |
| ChargeCreationFail   | `Source` creation is successful but `Charge` creation fails. The `Charge` state is `failed` .                   |
| RefundFail           | `Source` and `Charge` creation is successful. Any refunds against the charge fail. `Refund` state is `failed` . |
{% endtab %}

{% tab title="SEPA Direct Debit" %}
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

{% tab title="Klarna Credit" %}
| Scenario             | Description                                                                                       |
| -------------------- | ------------------------------------------------------------------------------------------------- |
| `lastName` parameter | Expected result                                                                                   |
| Expected result      | A Source is not created. The `state` of the Source is `failed`.                                   |
| ChargeCreationFail   | A Source is successfully created, but the Charge fails. The `state` of the Charge is `failed`.    |
| RefundFail           | successfully created, but refunds against the Charge fail. The `state` of the Refund is `failed`. |
{% endtab %}

{% tab title="Alipay" %}
### Error Scenarios&#x20;

After being triggered, Alipay error scenarios provide the following unique data to the `Source` owner:

| Scenario              | Description                                                                                                                        |
| --------------------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| `lastName` parameter  | Expected result                                                                                                                    |
| authFail              | A Source is not created. The `state` of the Source is `failed`.                                                                    |
| authFailAfterRedirect | A Source is successfully created but the Charge fails. The `state` of the Charge is `failed`.                                      |
| refundFail            | Both a Source and the Charge are successfully created, but refunds against the Charge fail. The `state` of the Refund is `failed`. |
{% endtab %}
{% endtabs %}

## Testing receiver payment methods

Wire Transfer is currently the only payment method with a `receiver` [authentication flow ](broken-reference)that Digital River [supports in our testing environment](testing-scenarios.md#supported-payment-methods-in-test-environment).

{% hint style="warning" %}
You should coordinate with your support team when testing wire transfers. They can provide instructions on how to move your orders into a completed state.
{% endhint %}

### Success scenarios

Use the [create source method](broken-reference) for receiver-type payment methods to provide success scenario test data. Once you've done this, you should receive a Source in a `pending_funds` state. You can then use the Source to complete your Checkout or Order.

### Error scenarios

First, identify the error scenario you would like to test against from the following table. Then when [creating a source](broken-reference), set the `lastName` parameter in the [Owner object](broken-reference) to the value you expect to trigger the scenario.

| Scenario                   | Description                                                                                                                                  |
| -------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------- |
| `lastName` parameter       | Expected result                                                                                                                              |
| SourceCreationFail         | A Source is not created. The `state` of the Source is `failed`.                                                                              |
| SourceFailWithDelay        | A Source is successfully created but the Charge fails. The `state` of the Charge is `failed`.                                                |
| RefundFailWhileCreation    | Both a Source and the Charge are successfully created but refunds against the Charge fail. The `state` of the Refund is `failed`.            |
| RefundFailAfterPaymentInfo | Both a Source and the Charge are successfully created, and a Refund request against the Charge is successful but ultimately fails to refund. |

## Testing the CCAvenue payment method

You can test your payment integration in the CCAvenue sandbox. When evaluating your integration, always use your [test API keys](API-structure/api-keys.md). This prevents you from interacting directly with payment services and ensures that the test data you enter does not create an actual charge or result in the transfer of funds.

Use your confidential (secret) test API key when conducting testing in the Digital River API. Use your public test API key to create test payment sources in DigitalRiver.js.

Your testing approach depends on whether the payment method has an [authentication flow](../payments/sources/#authentication-flow) of redirect. If you don't know the flow of the payment method you'd like to test, you can find it on the [Supported payment methods](../payments/supported-payment-methods/) page.

Use the following payment information when running a test.

| Payment option | Payment information                     | Notes                                                                                                                                                                                                                                                                                                                                      |
| -------------- | --------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Credit Card    | 4111111111111111 / 123                  | The expiration date must be at lease one day in the future.                                                                                                                                                                                                                                                                                |
| Net Banking    | AvenueTest                              |                                                                                                                                                                                                                                                                                                                                            |
| UPI            | select BHIM (first button) / 123456@upi | Wait for the countdown. Unified Payment Interface (UPI) identifier can be any six-digit number and @upi—for example, 123456@upi and 458093@upi. You can use every UPI identifier multiple times per day. However, when testing, you should either (1) clear the cookies or (2) use an incognito window every time after placing the order. |
| Wallet         | AvenueTest                              |                                                                                                                                                                                                                                                                                                                                            |

### Success and error scenarios

To test for successful or failed payment scenarios, use any card number under [Testing CCAvenue](../payments/payments-solutions/digitalriver.js/payment-methods/configuring-ccavenue.md#testing-ccavenue).  Visit the Bank Response Page via the following URL [https://test.ccavenue.com/bnk/servlet/processCCardReq?gtwID=AVN\&requestType=PAYMENT](https://test.ccavenue.com/bnk/servlet/processCCardReq?gtwID=AVN\&requestType=PAYMENT) to specify the card's behavior. Before running the test scenario, complete the necessary fields and set the **Transaction Status** to **Y** for a success scenario and **N** for an error scenario.

<div align="left">

<figure><img src="../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

</div>
