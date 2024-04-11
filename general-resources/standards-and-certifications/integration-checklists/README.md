---
description: An overview of the available integration checklists.
---

# Integration checklists

These [MOR/SOR](../../glossary.md#merchant-of-record-seller-of-record-mor-sor) integration checklists are meant to assist developers and quality assurance teams. Each checklist covers features that we either require or highly recommend you build into your tool. We also provide [sequence diagrams](./#sequence-diagram) to help you conceptualize the various interactions.

You can use these checklists and [sequence diagrams](./#sequence-diagram) while developing and testing your commerce connector.

* [ ] [Admin portal](admin-portal.md)
* [ ] [Products and SKUs](products-and-skus.md)
* [ ] [Customers and tax exemptions](customers-and-tax-exemptions.md)
* [ ] [Checkout, payment sources, and orders](checkouts-payment-sources-and-orders.md)
* [ ] [Disclosures, compliance statements, and emails](disclosures-compliance-statements-and-emails.md)
* [ ] [Fulfillments and cancellations](fulfillments-and-cancellations.md)
* [ ] [Customer portal](customer-portal.md)
* [ ] [Order refund synchronization](order-refund-synchronization.md)
* [ ] [Reversals](reversals.md)
* [ ] [Error handling](error-handling.md)

Completing these checklists helps ensure your commerce connector can pass the [tool-specific certification](../certification-process.md), and that any client sites built with the tool can successfully complete the [production checkout certification](../compliance-requirements.md#production-checkout-certification).

## Sequence diagrams <a href="#sequence-diagram" id="sequence-diagram"></a>

The following sequence diagrams depict the [core commerce flow](./#core-commerce-flow), [subscription acquisitions](./#subscription-acquisitions), [merchant-initiated auto-renewals](./#subscription-auto-renewals), key [order and fulfillment events](./#order-related-events-and-client-fulfillments), and [how customers use their account portals to create and save payment sources](./#source-creation-in-customer-portals). You can consult these sequence diagrams while working your way through the various integration checklists.

### Core commerce flow

This diagram depicts the core commerce flow and shows the basic interactions between the customer, your commerce platform, the Digital River APIs, and Digital River's Global Commerce layer. You can find the same diagram, along with accompanying text, on the [Process flow](../../../integration-options/checkouts/process-flow.md) page.

{% file src="../../../.gitbook/assets/Core Commerce.png" %}

### Core commerce flow (with submit then redirect)

This diagram depicts an end-to-end commerce flow using the submit then redirect solution. For details on how to implement it, refer to [Handling redirect payment methods](../../../integration-options/checkouts/building-you-workflows/handling-redirect-payment-methods.md).&#x20;

{% file src="../../../.gitbook/assets/Core Commerce - Submit then redirect.png" %}

### Subscription acquisitions

In this illustration, we depict the interactions that occur while using a [third-party subscription service](../../../integration-options/checkouts/subscriptions/third-party-coordinated-subscriptions.md) to build an acquisition checkout and process the orders response.

{% file src="../../../.gitbook/assets/Subscription acquisitions (1).png" %}

### Subscription auto-renewals

{% file src="../../../.gitbook/assets/Subscription auto-renewals.png" %}

This diagram depicts a standard, merchant-initiated autorenewal that uses a [third-party subscription service](../../../integration-options/checkouts/subscriptions/third-party-coordinated-subscriptions.md). In this sequence of events (other than being notified of successful and failed renewal attempts), customers don't actively interact with either the commerce platform or Digital River.

### Order-related events and client fulfillments

This visualization shows the potential webhook events that are emitted when a `POST/orders` returns a `state` of `in_review` or `pending payment`. It also demonstrates how an order in an `accepted` state drives both fulfillments and cancellations and how to handle the order complete event.

{% file src="../../../.gitbook/assets/Order and fulfillment events.png" %}

### Source creation in customer portals

In this sequence diagram, we demonstrate how customers can use their account portals to create payment sources in Drop-in that are ready for storage and how you can then save these sources to their accounts for use in future purchases. The interactions in this diagram occur outside of a standard checkout flow.

{% file src="../../../.gitbook/assets/Create sources in customer portal.png" %}
