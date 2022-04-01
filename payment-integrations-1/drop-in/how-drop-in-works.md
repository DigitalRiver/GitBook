---
description: Learn how Drop-in works.
---

# How Drop-in works

When the client goes to checkout, the client-server sends a create cart request to Digital River and Digital River returns the cart. The client-server then sends a request to provide the payment session ID to the client's front end. The client front end instantiates Drop-in with the payment session ID and configurations, and Drop-in displays the payment methods. When the customer selects a payment method and provides their payment details, the client front end triggers an `onSuccess` event and sends the source ID to the client-server. The client-server uses the source with the cart or shopper.

![](<../../.gitbook/assets/How Drop-in Works - Commerce API.png>)

## Drop-in flows

You can choose how you want to embed Drop-in based on how you want to use it. The following table shows your options.

| How do you want to use Drop-in?                                                                                               | Do you need to store payment methods?                                              | Instructions                                                                                                                                                     | Example                                                                                                                     |
| ----------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------- |
| I want to use Drop-in to collect payment as part of my checkout flow.                                                         | I do not need to store payment methods.                                            | See [Using Drop-in within your cart flow](drop-in-integration-guide.md#using-drop-in-within-your-cart-flow).                                                     | [Drop-in for checkout flow](https://tools.drapi.io/cm/drop-in/)                                                             |
|                                                                                                                               | I want to offer my customer the ability to store payment methods.                  | See [Allowing the customer to save their payment credentials](drop-in-integration-guide.md#optional-allowing-the-customer-to-save-their-payment-details).        | [Drop-in that allows saving payment methods within a checkout flow](https://tools.drapi.io/cm/drop-in/allow-save-payment)   |
| I want to use Drop-in to collect payment data from a page where my customer manages or adds payment methods to their account. | I want to use a mode configured specifically for storing customer payment methods. | See [Using Drop-in to collect payment details on a My Account page](drop-in-integration-guide.md#using-drop-in-to-collect-payment-details-on-a-my-account-page). | [Drop-in that allows adding payment methods on a My Account page](https://tools.drapi.io/cm/drop-in/manage-payment-methods) |

##
