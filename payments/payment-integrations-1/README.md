---
description: Gain a better understanding of Digital River's payment solutions
---

# Payment solutions

The payment solution(s) you use depends on whether customers [purchase products and services in a checkout flow](./#payments-in-checkout-flows) or [manage their payment methods in a self-service portal](./#payment-method-management-flows).

You can [use Digital River Dashboard to enable or disable payment methods](../../administration/dashboard/settings/payment-methods/disabling-a-payment-method.md).&#x20;

## Payments in checkout flows

How you collect payment in checkout flows depends on whether you select the [Low-code checkouts](./#low-code-checkouts) or [Direct integrations](./#components-1) approach.

### Low-code checkouts

In [Low-code checkouts](./#low-code-checkouts), how you collect payment depends on whether you're using [Prebuilt Checkout](./#prebuilt-checkout) or [Components](./#components).

#### Prebuilt Checkout

Payment is collected within the [checkout modal](../../integration-options/low-code-checkouts/drop-in-checkout.md#payment) if you're using [Prebuilt Checkout](../../integration-options/low-code-checkouts/drop-in-checkout.md). Digital River then associates the resulting [source(s)](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources) with the underlying [checkout](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) and, if customers opt to save a [reusable payment method](../supported-payment-methods/) to their account, the [customer](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Customers) as well.

![Drop-in Checkout](<../../.gitbook/assets/Drop-in checkout.png>)

#### Components

If you [integrate with components](../../integration-options/low-code-checkouts/implementing-a-components-checkout.md), you can use either the [payment component](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/components/payment-component.md) or the [wallet component](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/components/wallet-component.md) to collect a customer's payment at checkout-time.&#x20;

{% tabs %}
{% tab title="Wallet component" %}
![](<../../.gitbook/assets/Wallet element.png>)
{% endtab %}

{% tab title="Payment component" %}
![](<../../.gitbook/assets/Payment element - saved payment methods (2).png>)
{% endtab %}
{% endtabs %}

### Direct Integrations <a href="#components" id="components"></a>

If you select the [Direct integrations](../../integration-options/checkouts/) option, you'll need to use [Drop-in payments](drop-in/) or [Elements](digitalriver.js/quick-start.md) to collect payment during the [checkout process](../../integration-options/checkouts/creating-checkouts/).

![Drop-in payments](<../../.gitbook/assets/Drop-in payments.png>)

In either case, you're responsible for associating a transaction's payment [source(s)](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources) with the [customer](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Customers) and/or the [checkout](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts). For more details, refer to:

* [Purchase flows](../../integration-options/checkouts/building-you-workflows/#purchase-flows) on the [Building payment workflows](../../integration-options/checkouts/building-you-workflows/) page
* [Source basics](../payment-sources/)
* [Managing sources](../payment-sources/using-the-source-identifier.md)

## Payment method management flows

If you allow registered customers to save their [payment methods](../supported-payment-methods/) for future transactions, you'll need to give them access to a self-service account management portal. A section of this portal should allow customers to add, delete, and update their payment methods.

![](<../../.gitbook/assets/Manage payment methods (1).png>)

When building these payment method management flows, you'll likely use a combination of [Drop-in payments](drop-in/) and [DigitalRiver.js with elements](digitalriver.js/quick-start.md). For more details, refer to:

* [Account management flows](../../integration-options/checkouts/building-you-workflows/#account-management-flows) on the [Building payment workflows](../../integration-options/checkouts/building-you-workflows/) page
* The [Managing sources](../payment-sources/using-the-source-identifier.md) page
