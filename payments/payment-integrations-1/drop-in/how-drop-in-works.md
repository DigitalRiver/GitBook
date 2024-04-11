---
description: Learn how Drop-in payments works
---

# How Drop-in payments work

When customers initiate checkout, the client-server sends a [create checkout request](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createCheckouts) to Digital River and Digital River returns a [checkout](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts). The client-server then sends the [payment session](../../../integration-options/checkouts/creating-checkouts/payment-sessions.md) identifier to the client's front end. The client front end uses this payment session identifier, along with other configuration settings, to instantiate Drop-in payments. Once instantiated, transaction applicable payment methods are displayed in a modal window. When customers select a payment method and provide their payment details, an [`onSuccess`](drop-in-integration-guide.md#onsuccess) event is triggered and the [source](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources) identifier is sent to the client-server. The client-server uses that identifier to associate the source with [checkouts](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) and/or [customers](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Customers).

{% hint style="info" %}
To get a better understanding of how the process works, check out the [interactive Drop-in builder](https://drapi.io/drop-in-builder/).
{% endhint %}

{% embed url="https://player.vimeo.com/video/683888702?h=2b803b92e0" %}

![](<../../../.gitbook/assets/how-drop-in-works-digital-river-api (3) (2) (1) (2) (1).png>)

## Drop-in payments flows

The following table is meant to help you better understand your Drop-in payments embed options:

| Collect payment as part of a checkout flow                                                       | No  | See [Using Drop-in payments within your checkout flow](drop-in-integration-guide.md#using-drop-in-within-your-checkout-flow).                                    |
| ------------------------------------------------------------------------------------------------ | --- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Offer customers the ability to store payment methods                                             | Yes | See [Allowing the customer to save their payment credentials](drop-in-integration-guide.md#optional-allowing-the-customer-to-save-their-payment-credentials).    |
| Collect payment data from a page where customers manage or add payment methods to their accounts | Yes | See [Using Drop-in to collect payment details on a My Account page](drop-in-integration-guide.md#using-drop-in-to-collect-payment-details-on-a-my-account-page). |
