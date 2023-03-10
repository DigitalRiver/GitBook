---
description: Learn how Drop-in Payments works.
---

# How Drop-in Payments work

When the client goes to checkout, the client-server sends a [create cart request](../../../shopper-apis/cart/creating-or-updating-a-cart/#creating-a-cart) to Digital River and Digital River returns the [cart](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Carts). The client-server then sends the payment session identifier to the client's front end. The client front end uses the payment session identifier, along with other configuration settings, to instantiate Drop-in Payments. Once instantiated, transaction-applicable payment methods are displayed in a modal window. When the customer selects a payment method and provides their payment details, it triggers an `onSuccess` event and sends the source ID to the client-server. The client-server uses the identifier to associate the source with the [cart ](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Carts)or [shopper](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Shoppers).

{% hint style="info" %}
To get a better understanding of how the process works, check out the [interactive Drop-in builder](https://drapi.io/drop-in-builder/).
{% endhint %}

{% embed url="https://player.vimeo.com/video/683888702?h=2b803b92e0" %}

![](<../../../.gitbook/assets/how-drop-in-works-commerce-api (2).png>)

## Drop-in Payments flows

The following table is meant to help you better understand your Drop-in payments embed options:

| How do you want to use Drop-in?                                                                  | Do you need to store payment methods? | Instructions                                                                                                                                                              |
| ------------------------------------------------------------------------------------------------ | ------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Collect payment as part of a checkout flow                                                       | No                                    | See [Using Drop-in payments within your cart flow](drop-in-integration-guide.md#using-drop-in-payments-within-your-cart-flow).                                            |
| Offer customers the ability to store payment methods                                             | Yes                                   | See [Allowing the customer to save their payment credentials](drop-in-integration-guide.md#optional.-allowing-the-customer-to-save-their-payment-details).                |
| Collect payment data from a page where customers manage or add payment methods to their accounts | Yes                                   | See [Using Drop-in to collect payment details on a My Account page](drop-in-integration-guide.md#using-drop-in-payments-to-collect-payment-details-on-a-my-account-page). |
