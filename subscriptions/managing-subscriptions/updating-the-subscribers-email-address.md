---
description: Learn how to update the subscriber's email address.
---

# Updating the subscriber's email address

You can update a subscriber's email address so they can receive [future notifications](https://help.digitalriver.com/help/gc/Administration/Email-Notifications/Email-notifications.htm) using their preferred email address.

Digital River supports the following email types:

| email address type                                                                                                                           | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| -------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| [Shopper's email address](updating-the-subscribers-email-address.md#owners-email-address)                                                    | The email address the shopper uses to sign in to their account. You can [change the shopper's email address in the cart before placing the order](updating-the-subscribers-email-address.md#changing-the-billing-and-shipping-email-addresses-in-the-cart-before-placing-the-order).                                                                                                                                                                                                                               |
| [Requisition billing email address](updating-the-subscribers-email-address.md#requisition-billing-and-requisition-shipping-email-addresses)  | The billing email address the shopper provided when placing an order. You can [change the shopper's billing address in the cart before placing the order](updating-the-subscribers-email-address.md#changing-the-billing-and-shipping-email-addresses-in-the-cart-before-placing-the-order).                                                                                                                                                                                                                       |
| [Requisition shipping email address](updating-the-subscribers-email-address.md#requisition-billing-and-requisition-shipping-email-addresses) | The shipping email address the shopper provided when placing an order. You can [change the shopper's shipping address in the cart before placing the order](updating-the-subscribers-email-address.md#changing-the-billing-and-shipping-email-addresses-in-the-cart-before-placing-the-order).                                                                                                                                                                                                                     |
| [Subscription billing email address](updating-the-subscribers-email-address.md#subscription-billing-and-shipping-email-addresses)            | When creating a subscription, subscription-relevant information from the original acquisition, including the billing email address, is copied to the subscription. You can [update a shopper's billing email address for a specific subscription](updating-the-subscribers-email-address.md#updating-the-subscribers-email-address-for-a-specific-subscription) or [all of the shopper's subscriptions](updating-the-subscribers-email-address.md#updating-the-subscribers-email-address-for-all-subscriptions).   |
| [Subscription shipping email address](updating-the-subscribers-email-address.md#subscription-billing-and-shipping-email-addresses)           | When creating a subscription, subscription-relevant information from the original acquisition, including the shipping email address, is copied to the subscription. You can [update a shopper's shipping email address for a specific subscription](updating-the-subscribers-email-address.md#updating-the-subscribers-email-address-for-a-specific-subscription) or [all of the shopper's subscriptions](updating-the-subscribers-email-address.md#updating-the-subscribers-email-address-for-all-subscriptions). |

You can combine the notifications for a specific shopper by creating an event rule per each notification.  <mark style="color:red;"></mark>  You update email notifications using [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do).

## Email address update phases

There are three phases when you can update an email address:&#x20;

| Phase                                                                                                                                                                                  |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Create cart](../../cart/creating-or-updating-a-cart/#creating-a-cart)                                                                                                                 | <ul><li>Apply or edit the email address BEFORE placing the order. You can do this when you <a href="../../payments/sources/#attaching-a-payment-method-to-an-order-or-cart">attach a payment method to a cart</a> or <a href="../../payments/sources/#attaching-a-payment-method-to-a-customer">customer </a>and discovered the email address is not the one you expected.</li><li><a href="../../cart/creating-or-updating-a-cart/updating-the-shipping-or-billing-address.md">Change the billing and shipping email address</a> while in the cart and before submitting the order.</li></ul>                                  |
| [Submit cart](../../cart/submitting-a-cart/)                                                                                                                                           | Update the email address AFTER you [submit the order](../../cart/submitting-a-cart/) and [BEFORE ](../../private-store-1/submitting-an-order-for-a-private-store.md)you create the subscription.                                                                                                                                                                                                                                                                                                                                                                                                                                |
| [Create a subscription product](https://help.digitalriver.com/help/gc/Products/All-Products/Creating-a-product.htm) in [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do). | <p>Update an email address for a subscription.</p><ul><li>If the shopper accidentally enters the incorrect email address while placing an order, you can <a href="updating-the-subscribers-email-address.md#updating-the-subscribers-email-address-for-a-specific-subscription">update the subscriber’s email address for a specific subscription</a> or <a href="updating-the-subscribers-email-address.md#updating-the-subscribers-email-address-for-all-subscriptions">all of the subscriber's subscriptions</a>.</li><li>The subscriber can change their billing email address after creating the subscription.  </li></ul> |

![](<../../.gitbook/assets/Subscriber-email-address-sequence (1).png>)

## Changing the billing and shipping email addresses in the cart before placing the order  &#x20;

### Commerce API 

You can use one of the following calls to change the billing or shipping email address from the cart.&#x20;

* [POST /v1/shoppers/me/carts/active](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Carts/paths/\~1v1\~1shoppers\~1me\~1carts\~1active/post) to [update the billing or shipping email address in the cart](../../cart/creating-or-updating-a-cart/updating-the-shipping-or-billing-address.md).  &#x20;
* [PUT /v1/shoppers/me/carts/active/billing-address](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Billing-Address/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1billing-address/put) to override the billing email address in the cart.  &#x20;
* [PUT /v1/shoppers/me/carts/active/shipping-address](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Shipping-Address/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1shipping-address/put) to override the billing email address in the cart.  &#x20;

### Digital River-hosted storefront page 

It depends on how your cart is customized.  Contact your account representative for more information.

## Email addresses created after submitting an order

### Requisition billing and requisition shipping email addresses

When a shopper submits an order, the system creates two email addresses for the order: &#x20;

* Requisition billing email address
* Requisition shipping email address&#x20;

The requisition billing email address and requisition shipping email address are snapshots belonging to the order. The requisition billing email address is the shopper’s billing address associated with their chosen payment method. When the shopper places the order, the action disconnects the requisition billing email address from the payment method.  

#### Orders placed by Commerce API

For a physical product order, the requisition billing email address comes from the billing address associated with the shopper's payment method/payment option used to place the order. (The billing address includes the email address.) The shopper provides the requisition shipping email address, if the shopper does not specify the shipping email address, then the system copies the requisition billing email address to the requisition shipping email address. &#x20;

For a non-physical product order, the requisition shipping email address comes from the requisition billing address. (The billing address includes the email address.)  The system copies the requisition billing email address to the requisition shipping email address.  &#x20;

#### Orders placed by Digital River-hosted solution with legacy payments

When an authenticated shopper signs into your storefront and your Digital River-hosted storefront billing address page provides an Email field, the system copies the shopper’s owner email address to the requisition billing email address.  

{% hint style="success" %}
An anonymous shopper flow should provide an Email field on the storefront page where the shopper can provide their email address. &#x20;
{% endhint %}

#### Orders placed by Digital River-hosted solution with CloudPay (Checkout.js) 

A Digital River-hosted solution leverages Checkout.js to support the payment source, and Checkout.js leverages the Commerce API/apply-payment-method API to attach the source to the cart for both authenticated and anonymous shoppers. So, the system uses the requisition billing email address as the source’s billing email address in the cart.&#x20;

### Subscription billing and shipping email addresses

If the shopper submits a subscription order, the system creates two more email addresses for the subscription:  

* Subscription billing email address&#x20;
* Subscription shipping email address&#x20;

The subscription billing address is associated with the shopper's subscription and recurring payment method. You can update the [subscription email address for a shopper's specific subscription](updating-the-subscribers-email-address.md#updating-the-subscribers-email-address-for-a-specific-subscription) or [all of the shopper's subscriptions](updating-the-subscribers-email-address.md#updating-the-subscribers-email-address-for-all-subscriptions)

### Owner's email address

If the shopper is an authenticated shopper and has an account they can use to sign in, the system also associates an owner's email address with the shopper. The owner's email address applies only to the authenticated shopper and is not associated with the shopper's order or subscription.

When the authenticated user signs in to their account, they can manage their email addresses from their account and add several often-used payment methods to their account. Each payment method is associated with a billing address persisted in the shopper's address book. The billing address includes an email address, that we call the billing email address.&#x20;

## Updating the subscriber's email address for a specific subscription

A long-term subscriber sometimes needs to change their subscription email address for a specific subscription. Use the [`POST /v1/subscriptions/{subscriptionId}/email`](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Email-Updater/operation/emailUpdater) request to update a subscription customer's ship-to and bill-to email address so they can receive notifications. You need to include the email address (`emailAddress`) in the payload. The email address should use a [valid email format](https://deliverbility.com/valid-email-address-format/) and not exceed 255 characters. In the following example, the value of the `emailAddress` is `jdoe@acme.com`.&#x20;

{% tabs %}
{% tab title="cURL" %}
```javascript
curl --location --request POST 'http://{host}/v1/subscriptions/{subscriptionId}/email' \
--header 'Content-Type:  application/json' \
--header 'authorization: bearer ***\
--data-raw '{
 "emailAddress" : "jdoe@acme.com"
}'
```
{% endtab %}
{% endtabs %}

You will receive a `202 Accepted` response.

### Missing email address parameter

If the email address parameter is missing, you will see a [`400 Bad Request`](../../error-codes.md#400-bad-request) error message with a `validation-error` code.

{% tabs %}
{% tab title="JSON" %}
```javascript
{
  "errors": {
    "error": [
      {
        "code": "validation-error",
        "subcode": "required-data-missing",
        "description": "Missing required field: emailAddress"
      }
    ]
  }
}
```
{% endtab %}
{% endtabs %}

### Email address is more than 255 characters

An email address cannot exceed 255 characters. If the email address is more than 255 characters, you will see a [`400 Bad Request`](../../error-codes.md#400-bad-request) error message with an `invalid-request` code.&#x20;

```javascript
{
  "errors": {
    "error": [
      {
         "code": "invalid-request",
         "subcode": "invalid-length",
         "description": "emailAddress cannot exceed a length of 255 characters"
      }
    ]
  }
}
```

## Updating the subscriber's email address for all subscriptions

A long-term subscriber sometimes needs to change their subscription email address for all subscriptions. Use the [`POST /v1/shoppers/me?applyEmailToSubscriptions=true`](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Shoppers/paths/\~1v1\~1shoppers\~1me/post) request to update a subscription customer's ship-to and bill-to email addresses for all subscriptions so they can receive notifications. You need to include the email address (`emailAddress`). The email address should use a [valid email format](https://deliverbility.com/valid-email-address-format/) and not exceed 255 characters. In the following example, the value of the `emailAddress` is `jdoe@acme.com`.&#x20;

{% tabs %}
{% tab title="cURL" %}
```javascript
curl --location --request POST 'http://{host}/v1/shoppers/me?applyEmailToSubscriptions=true' \
--header 'Content-Type:  application/json' \
--header 'authorization: bearer ***\
--data-raw '{
 "emailAddress" : "jdoe@acme.com"
}'
```
{% endtab %}
{% endtabs %}

You will receive a `204 No Content` response.
