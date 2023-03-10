---
description: Understand how a midterm change works.
---

# Midterm change

A midterm change occurs when a customer requests a change to their subscription before their next renewal. A Call Center agent can use this opportunity to dissuade the customer from cancelling their subscription, encourage their customer to increase the quantity of their subscription, upgrade their subscription, purchase an add-on to their subscription, or sell another promotion.&#x20;

The Call Center agent must identify the type of midterm change. The Call Center agent can offer a [perpetual unit price](selling-subscriptions-without-add-ons/#perpetual-unit-price) or offer a [one-time price override](selling-subscriptions-without-add-ons/#prorated-subscription-price) to persuade the customer not to cancel their subscription. They can also offer to [reduce the subscription quantity](selling-subscriptions-without-add-ons/#reduced-subscription-quantity).

## Perpetual unit price

Call Center agents can use the perpetual unit price (`perpetualUnitPrice`) attribute to [assign a perpetual price to a subscription](selling-subscriptions-without-add-ons/assigning-a-perpetual-unit-price.md). A perpetual unit price remains the same each time the customer renews the monthly or annual subscription until they change their subscription by adding or subtracting quantity or add-ons. You essentially honor the deal until something changes. The customer can be an individual or business subscription entity.&#x20;

For example, a Call Center agent [creates a cart with a perpetual price](selling-subscriptions-without-add-ons/assigning-a-perpetual-unit-price.md#creating-a-cart-with-a-perpetual-unit-price). The catalog price for the subscription product is $20.00. When the agent sets the perpetual unit price to $15.00, the perpetual unit price does not change until the deal changes. When the deal changes, the price per unit can change (in this instance, it could change to $18.00).

Use the [Perpetual Price resource](selling-subscriptions-without-add-ons/assigning-a-perpetual-unit-price.md#assigning-a-perpetual-unit-price-to-a-subscription) and [Cart ](selling-subscriptions-without-add-ons/assigning-a-perpetual-unit-price.md#creating-a-cart-with-a-perpetual-unit-price)resources to assign the perpetual price.&#x20;

## Prorated subscription price

Call Center agents can use the prorated unit price (`proratedUnitPrice`) to [apply a midterm change with price override](selling-subscriptions-without-add-ons/applying-a-midterm-change-with-price-override.md) to the unit price listed in the product catalog during a midterm subscription change request based on a customer's request. The customer may request an increase in the product quantity, a product upgrade, or a product add-on.

Use the [Preview ](selling-subscriptions-without-add-ons/applying-a-midterm-change-with-price-override.md#apply-a-unit-prorated-price-using-the-preview-resource)and [Preview-cart](selling-subscriptions-without-add-ons/applying-a-midterm-change-with-price-override.md#apply-a-unit-prorated-price-using-the-preview-cart-resource) resources to override a unit price, increase the base product quantity, upgrade the base product, increase the add-on product, or add a new add-on via a midterm change. The [Preview-cart](selling-subscriptions-without-add-ons/applying-a-midterm-change-with-price-override.md#apply-a-unit-prorated-price-using-the-preview-cart-resource) resource creates a cart behind the scene that shows the customer how much the cost will change. The preview cart includes the credit, subtotal, total tax, and the total amount due to be paid if the preview changes result in an amount due. It also includes a link to the cart with the rest of the payload. The [Preview](selling-subscriptions-without-add-ons/applying-a-midterm-change-with-price-override.md#apply-a-unit-prorated-price-using-the-preview-resource) resource does not return the cart details if created in the response. Use the [Preview](selling-subscriptions-without-add-ons/applying-a-midterm-change-with-price-override.md#apply-a-unit-prorated-price-using-the-preview-resource) resource if you want to create a cart by subsequently calling another resource. The [Preview ](selling-subscriptions-without-add-ons/applying-a-midterm-change-with-price-override.md#apply-a-unit-prorated-price-using-the-preview-cart-resource)and [Preview-cart](selling-subscriptions-without-add-ons/applying-a-midterm-change-with-price-override.md#apply-a-unit-prorated-price-using-the-preview-cart-resource) resources allow you to chose when and how to initiate a cart.

Once the shopper submits or confirms the immediate midterm change, any subsequent lifecycle operation (auto or manual renewal, product or quantity change, cancel, and so on) on the subscription will take into account the changed configuration of the subscription and add-ons.‌

For example, a customer currently has a subscription quantity of four and wants to increase the quantity to 10. They originally agreed to a unit price of $20.00 for a total of $80.00. The Call Center agent offers a prorated unit price of $15.00 for an additional six subscriptions for a total of $90.00 as an incentive for the subscription duration. The next time the customer renews their subscription, the unit price will be $20 for a total of $200.00.

## Reduced subscription quantity

You can also use the [Reduce](selling-subscriptions-without-add-ons/reducing-the-quantity-of-a-subscription.md) resource to [decrease the base product quantity](selling-subscriptions-without-add-ons/reducing-the-quantity-of-a-subscription.md), decrease the product add-on quantity (`quantity`), or remove a product add-on from a subscription. Use the [Reduce](selling-subscriptions-without-add-ons/reducing-the-quantity-of-a-subscription.md) resource if a [Preview](selling-subscriptions-without-add-ons/applying-a-midterm-change-with-price-override.md#apply-a-unit-prorated-price-using-the-preview-cart-resource) resource call does not create a cart that decreases a product quantity or removes a product add-on. Invoking the [Reduce](selling-subscriptions-without-add-ons/reducing-the-quantity-of-a-subscription.md) resource will update the desired configuration in the database tables.‌

For example, an agent can reduce a quantity of 10 subscriptions to 6 subscriptions at the customer's request.
