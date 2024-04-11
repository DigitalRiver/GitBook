---
description: Gain a better understanding of how to test your payments integration
---

# Testing scenarios

To confirm that the payment methods in your integration work as expected, you can simulate transactions without transferring any money.

On this page you'll find information on:

* [How to get started with payments testing  ](testing-scenarios.md#getting-started)
* [Which payment methods are supported in our test environment](testing-scenarios.md#supported-payment-methods-in-a-test-environment)
* How to test [standard](testing-scenarios.md#testing-standard-payment-methods), [redirect](testing-scenarios.md#testing-redirect-payment-methods), and [receiver](testing-scenarios.md#testing-receiver-payment-methods) payment methods
* [Production testing best practices](testing-scenarios.md#production-testing-best-practices)

{% hint style="success" %}
For details on evaluating VAT implementations, refer to the [test tax identifiers](../integration-options/checkouts/creating-checkouts/tax-identifiers.md#test-tax-identifiers) section on the [Tax identifiers](../integration-options/checkouts/creating-checkouts/tax-identifiers.md) page.
{% endhint %}

## Getting started

Always use your [test API keys](api-structure.md#test-and-production-environments) to evaluate your integration. This prevents direct interactions with payment services and ensures that input data doesn't result in the creation of an actual [charge](digital-river-api-reference/payment-charges.md) or the transfer of funds.

When testing in the Digital River APIs, use your [confidential (secret) test key](api-structure.md#confidential-keys) and your [public test key](api-structure.md#public-keys) to create [payment sources ](../payments/payment-sources/)in [DigitalRiver.js](reference/) and [DigitalRiverCheckout.js](digitalrivercheckout.js-reference/).

How you test a payment method depends on whether its resulting [source](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources) has an [authentication flow](../payments/payment-sources/#authentication-flow) of [standard](testing-scenarios.md#testing-standard-payment-methods), [redirect](testing-scenarios.md#testing-redirect-payment-methods), or [receiver](testing-scenarios.md#testing-receiver-payment-methods). You can find it on the Supported payment methods page if you don't know this.

## Payment methods supported in the test environment <a href="#supported-payment-methods-in-a-test-environment" id="supported-payment-methods-in-a-test-environment"></a>

Digital River supports a wide range of payment methods. However, not all of them are currently supported in our [test environment](api-structure.md#test-and-production-environments). To determine the test environment status of each, refer to [Supported payment methods](../payments/supported-payment-methods/).

## Testing standard payment methods

In this section, you'll find information on testing payment methods whose resulting [source](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources) has a [standard authentication flow](../payments/payment-sources/#authentication-flow).&#x20;

### Credit cards

The following card numbers are only valid for testing. They do not create a real [charge](digital-river-api-reference/payment-charges.md) or result in a transfer of funds.

#### Success scenarios

To test a successful payment, use the following credit card numbers. For each, the expiration date must be at least one day. Except for Visa and American Express, the security code can be any random three-digit number.&#x20;

| Card number         | Brand            | Expiration date | Security code    |
| ------------------- | ---------------- | --------------- | ---------------- |
| 3434 567890 12341   | American Express | Any future date | Any four digits  |
| 3034 567890 1235    | Diners Club      | Any future date | Any three digits |
| 6011 9876 9876 9876 | Discover         | Any future date | Any three digits |
| 3528 9876 9876 9879 | JCB              | Any future date | Any three digits |
| 5466 1600 0000 0008 | Mastercard       | Any future date | Any three digits |
| 6226 2200 0000 0009 | UnionPay         | Any future date | Any three digits |
| 4444 2222 3333 1111 | Visa             | Any future date | 123              |

Use the following data to test how your integration handles different 3D Secure 2 authentication scenarios.

| Card number         | Brand      | Expiration date | Security code |
| ------------------- | ---------- | --------------- | ------------- |
| 5454 5454 5454 5454 | Mastercard | 03/2030         | 737           |
| 4917 6100 0000 0000 | Visa       | 03/2030         | 737           |

When prompted for 3D Secure 2 text challenges, use these credentials:

| App type | Password |
| -------- | -------- |
| Mobile   | 1234     |
| Web      | password |

#### Error scenarios

Use these card numbers to test specific error scenarios. For each card:

* The expiration date must be at least one day in the future
* The security code can be any random three-digit number.

| Card Number         | Expected result                                                                                                                                               |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 4000 0000 0000 3295 | A Source is not created. The `state` of the Source is `failed`.                                                                                               |
| 4000 0000 0000 3600 | A Source is successfully created but the Charge fails. The `state` of the Charge is `failed`.                                                                 |
| 4000 0000 0000 4103 | Both a Source and Charge are successfully created , but the Capture fails. The Capture `state` is `failed`.                                                   |
| 4000 0000 0000 4111 | A Source, Charge, and Capture are successfully created, but the Refund fails. The Refund`state` is `failed`.                                                  |
| 4000 0000 0000 4442 | Both a Source and Charge are successfully created , but the Cancel fails. The Cancel `state` is `failed`.                                                     |
| 4485 9517 8852 1565 | Both a Source and Charge are successfully created, but the Capture is created in a `pending` state. After a delay, the Capture `state` updates to `failed`.   |
| 4556 6025 6424 0839 | A Source, Charge, and Capture are successfully created, but the Refund is created in a`pending` state. After a delay, the Refund `state` updates to `failed.` |
| 4024 0071 2057 9635 | Both a Source and Charge are successfully created, but the Capture is created in a`pending` state. The Capture `state` remains `pending`.                     |
| 4000 0000 0000 0028 | Both a Source and Charge are successfully created, but the Capture is created in a`pending` state. The Capture `state` remains `pending`.                     |

### Google Pay testing

Before you test Google Pay, you need to:

* Have a [Google Account](https://support.google.com/accounts/answer/27441?hl=en).
* Join the [Google Pay API Test Cards Allowlist](https://groups.google.com/g/googlepay-test-mode-stub-data) group. Once you've joined, a[ test card suite](https://developers.google.com/pay/api/android/guides/resources/test-card-suite) is enabled in your Google account.

Any credit card in this suite can create a [source](../payments/payment-sources/), [charge](digital-river-api-reference/payment-charges.md), [capture](digital-river-api-reference/payment-charges.md#captures), and [refund](../order-management/returns-and-refunds-1/refunds/).&#x20;

However, the customer's last name must be a specific value to evaluate whether your application properly handles failures and [Strong Customer Authentication](../payments/psd2-and-sca/). Use the table below to determine the scenario you want to test and the value that triggers the behavior.

{% hint style="warning" %}
Digital River's [low-code checkout solutions](../integration-options/low-code-checkouts/) don't currently support testing Google Pay failures and SCA.
{% endhint %}

| Scenario                                                                                                                                                                                                                                                                                                                                           | Last name   |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------- |
| The [source ](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources)is created but its `state` is `failed`                                                                                                                                                                                                                    | SourceFail  |
| The [source](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources) is successfully created but the [charge's](digital-river-api-reference/payment-charges.md) `state` is `failed`                                                                                                                                            | ChargeFail  |
| Both the [source](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources) and [charge](digital-river-api-reference/payment-charges.md) are successfully created but the [capture's](digital-river-api-reference/payment-charges.md#captures) `state` is `failed`                                                               | CaptureFail |
| The [source](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources) and [charge](digital-river-api-reference/payment-charges.md) are successfully created by the [cancel's](digital-river-api-reference/payment-charges.md#cancels) `state` is `failed`                                                                       | CancelFail  |
| The [source](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources), [charge](digital-river-api-reference/payment-charges.md), and [capture](digital-river-api-reference/payment-charges.md#captures) are successfully created but the [refund's](digital-river-api-reference/payment-charges.md#refunds) `state` is `failed` | RefundFail  |
| The [source](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources) is successfully created and the user is challenged                                                                                                                                                                                                        | SCATest     |
| The [source](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources) is successfully created and the user is challenged but the [charge's](digital-river-api-reference/payment-charges.md) `state` is `failed`                                                                                                                 | SCATestFail |

## Testing redirect payment methods

You can use the information in this section to test [success](testing-scenarios.md#success-scenarios-1) and [error](testing-scenarios.md#error-scenarios) scenarios on payment methods whose resulting [source](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources) has a [`redirect` authentication flow](../payments/payment-sources/#authentication-flow).&#x20;

### Success scenarios

Use the [create source method](../payments/payment-sources/using-the-source-identifier.md#creating-payment-sources) to provide success scenario test data for redirect payment sources. Once you've done this, you should receive a Source in a `pending_redirect` state.

You'll then be directed to our generic authorization page that contains accept and reject options. Follow the redirect and select one of the following options:

| Option  | Expected result                                   |
| ------- | ------------------------------------------------- |
| Approve | The Source moves to a `chargeable` state          |
| Decline | The Source remains in a `pending_redirect` state. |

### Error scenarios

First, select one of the following payment methods for redirect sources. Then identify the error scenario you would like to test against. Finally, when [creating a source](../payments/payment-sources/using-the-source-identifier.md#creating-payment-sources), set the `lastName` parameter in the [Owner object](../payments/payment-integrations-1/digitalriver.js/payment-methods/common-payment-objects.md#owner-object) to the value you expect to trigger the scenario.

{% tabs %}
{% tab title="PayPal" %}
This tab's testing information applies to PayPal, PayPal Billing Agreement, and PayPal Credit.

| `lastName` parameter | Expected result                                                                                                                   |
| -------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| SourceCreationFail   | A Source is not created. The `state` of the Source is `failed`.                                                                   |
| ChargeCreationFail   | A Source is successfully created but the Charge fails. The `state` of the Charge is `failed`.                                     |
| RefundFail           | Both a Source and the Charge are successfully created but refunds against the Charge fail. The `state` of the Refund is `failed`. |
{% endtab %}

{% tab title="SEPA Direct Debit" %}
| `lastName` parameter     | Expected result                                                                                                                   |
| ------------------------ | --------------------------------------------------------------------------------------------------------------------------------- |
| SourceFail               | A Source is not created. The `state` of the Source is `failed`.                                                                   |
| SourceFailAfterRedirect  | The Source moves to a `state` of `failed` after redirecting from payment page.                                                    |
| ChargeFail               | A Source is successfully created but the Charge fails. The `state` of the Charge is `failed`.                                     |
| ChargeFailedAfterPending | The Charge is initially created in a `pending` state. After a webhook call, the Charge is moved to a `failed` state.              |
| RefundFail               | Both a Source and the Charge are successfully created but refunds against the Charge fail. The `state` of the Refund is `failed`. |
| RefundFailedAfterPending | The Refund is initially created in a `pending` state. After a webhook call, the Refund is moved to a `failed` state.              |
| ChargeRemainPending      | After a Charge is created, it remains in a `state` of `pending`.                                                                  |
{% endtab %}

{% tab title="Klarna Credit" %}
| `lastName` parameter | Expected result                                                                                                                   |
| -------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| SourceCreationFail   | A Source is not created. The `state` of the Source is `failed`.                                                                   |
| ChargeCreationFail   | A Source is successfully created but the Charge fails. The `state` of the Charge is `failed`.                                     |
| RefundFail           | Both a Source and the Charge are successfully created but refunds against the Charge fail. The `state` of the Refund is `failed`. |
{% endtab %}

{% tab title="Alipay" %}
| `lastName` parameter  | Expected result                                                                                                                   |
| --------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| authFail              | A Source is not created. The `state` of the Source is `failed`..                                                                  |
| authFailAfterRedirect | A Source is successfully created but the Charge fails. The `state` of the Charge is `failed`.                                     |
| refundFail            | Both a Source and the Charge are successfully created but refunds against the Charge fail. The `state` of the Refund is `failed`. |
{% endtab %}
{% endtabs %}

## Testing receiver payment methods

You can use the information in this section to test [success](testing-scenarios.md#success-scenarios-1) and [error](testing-scenarios.md#error-scenarios) scenarios on payment methods whose resulting [source](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources) has a [receiver authentication flow](../payments/payment-sources/#authentication-flow).&#x20;

{% hint style="warning" %}
Work with your support team when testing wire transfers. They can provide instructions on how to move your orders into a completed state.
{% endhint %}

### Success scenarios

Use the [create source method](../payments/payment-sources/using-the-source-identifier.md#creating-payment-sources) for receiver-type payment methods to provide success scenario test data. Once you've done this, you should receive a Source in a `pending_funds` state. You can then use the Source to complete your Checkout or Order.

### Error scenarios

First, identify the error scenario you would like to test against from the following table. Then when [creating a source](../payments/payment-sources/using-the-source-identifier.md#creating-payment-sources), set the `lastName` parameter in the [Owner object](../payments/payment-integrations-1/digitalriver.js/payment-methods/common-payment-objects.md#owner-object) to the value you expect to trigger the scenario.

| Scenario                   | Description                                                                                                                                 |
| -------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| `lastName` parameter       | Expected result                                                                                                                             |
| SourceCreationFail         | A Source is not created. The `state` of the Source is `failed`.                                                                             |
| SourceFailWithDelay        | A Source is successfully created but the Charge fails. The `state` of the Charge is `failed`.                                               |
| RefundFailWhileCreation    | Both a Source and the Charge are successfully created but refunds against the Charge fail. The `state` of the Refund is `failed`.           |
| RefundFailAfterPaymentInfo | Both a Source and the Charge are successfully created and a Refund request against the Charge is successful but ultimately fails to refund. |

## Testing the CCAvenue payment method

Use the following when testing in the CCAvenue sandbox:

| Payment option | Payment information                     | Notes                                                                                                                                                                                                                                                                                                                                      |
| -------------- | --------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Credit Card    | 4111111111111111 / 123                  | The expiration date must be at lease one day in the future.                                                                                                                                                                                                                                                                                |
| Net Banking    | AvenueTest                              |                                                                                                                                                                                                                                                                                                                                            |
| UPI            | select BHIM (first button) / 123456@upi | Wait for the countdown. Unified Payment Interface (UPI) identifier can be any six-digit number and @upi—for example, 123456@upi and 458093@upi. You can use every UPI identifier multiple times per day. However, when testing, you should either (1) clear the cookies or (2) use an incognito window every time after placing the order. |
| Wallet         | AvenueTest                              |                                                                                                                                                                                                                                                                                                                                            |

### Success and error scenarios

To test for successful or failed payment scenarios, use any card number available under [Testing CCAvenue](../payments/payment-integrations-1/digitalriver.js/payment-methods/configuring-ccavenue.md#testing-ccavenue). Visit the Bank Response Page via the following URL [https://test.ccavenue.com/bnk/servlet/processCCardReq?gtwID=AVN\&requestType=PAYMENT](https://test.ccavenue.com/bnk/servlet/processCCardReq?gtwID=AVN\&requestType=PAYMENT) to specify the card's behavior. Before running the test scenario, complete the necessary fields and set the **Transaction Status** to **Y** for a success scenario and **N** for an error scenario.

<div align="left">

<figure><img src="../.gitbook/assets/CCAvenue bank response page.png" alt=""><figcaption></figcaption></figure>

</div>

## Production testing best practices

To conduct end-to-end testing of your financial systems before going live, you'll need to use our [production environment](api-structure.md#test-and-production-environments). This is because Digital River's financial APIs, which can be used to access [sales transactions](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sales-transactions), [sales summaries](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sales-summaries), and [payouts](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Payouts), aren't supported in [test mode](best-practices.md#test-mode). As a result, you can't [configure a webhook](../order-management/events-and-webhooks-1/webhooks/) in this mode to listen for [events](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events) with a [`type`](../order-management/events-and-webhooks-1/events-1/#event-types) of `sales_transaction.created` and `payout.created`.

Here are some guidelines to follow when testing in production:

* Keep the volume of transactions and their monetary value to a minimum to avoid heavy impacts on your financial reporting.
* Pass "real" data (i.e., actual card numbers, names, emails, and addresses).&#x20;

{% hint style="danger" %}
Don't use the test data contained in this article. Doing so might negatively affect your authorization rates, trigger manual reviews of transactions by Digital River, and result in fraud blocks being placed on the [order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) `email` address.
{% endhint %}

* Ensure that your transactions are flowing through the proper fraud system. There's no way for you to configure the JavaScript libraries or APIs to control this flow. So, before doing live testing, notify your Digital River representatives and they'll work with our fraud team to get everything set up correctly.&#x20;
* Provide your Digital River representative with any data you'd like positive or negative listed. For example, you can provide us email addresses that represent "good" customers. We'll then add those emails to a positive list. When orders with those values enter our fraud system, we'll let them pass through without any checks. Alternatively, you might want orders with certain IP addresses to be held for fraud review or rejected outright. If that's the case, you can give us with a list of those addresses and we'll add them to a negative list.&#x20;

