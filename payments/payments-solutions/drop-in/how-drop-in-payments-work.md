---
description: Learn how Drop-in payments works.
---

# How Drop-in payments work

When the client goes to checkout, the client-server sends a create cart request to Digital River, and Digital River returns the cart. The client-server then sends the payment session identifier to the client's front end. The client front end uses the payment session identifier and other configuration settings to instantiate Drop-in payments. Once instantiated, transaction-applicable payment methods are displayed in a modal window. When the customer selects a payment method and provides their payment details, the client front end triggers an `onSuccess` event and sends the source identifier to the client server. The client-server uses the source with the cart and shoppers.

{% hint style="info" %}
Check out the [interactive Drop-in builder](https://drapi.io/drop-in-builder/) to better understand how the process works.
{% endhint %}

{% embed url="https://player.vimeo.com/video/683888702?h=2b803b92e0" %}

<div align="left">

<img src="../../../.gitbook/assets/how-drop-in-works-commerce-api (2).png" alt="">

</div>

## Drop-in payments flows

The following table is meant to help you better understand your Drop-in payments embed options:

| How do you want to use Drop-in?                                                                  | Do you need to store payment methods? | Instructions                                                                                                                                                              |
| ------------------------------------------------------------------------------------------------ | ------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Collect payment as part of a checkout flow                                                       | No                                    | See [Using Drop-in payments within your cart flow](drop-in-integration-guide.md#using-drop-in-payments-within-your-cart-flow).                                            |
| Offer customers the ability to store payment methods                                             | Yes                                   | See [Allowing the customer to save their payment credentials](drop-in-integration-guide.md#optional.-allowing-the-customer-to-save-their-payment-details).                |
| Collect payment data from a page where customers manage or add payment methods to their accounts | Yes                                   | See [Using Drop-in to collect payment details on a My Account page](drop-in-integration-guide.md#using-drop-in-payments-to-collect-payment-details-on-a-my-account-page). |



##
