---
description: Learn how Digital River reconciles conflicting offers.
---

# Reconciling conflicting offers

Commerce API reconciles conflicting offers within the same order. The following topics provide real-world examples to explain the reconciliation process.

## Running multiple offers

You can create an unlimited number of offers for a single product. However, a conflict can occur when the shopper triggers two or more offers for the same product or two or more different offers for different products. When a conflict occurs, Commerce API uses [rules and guidelines to arbitrate the offer conflicts](reconciling-conflicting-offers.md#offer-arbitration) and provide the shopper with the best discount.

## Offer arbitration

When the shopper begins checkout, the system analyzes the contents of the shopping cart. If there are two or more competing offers, the system analyzes the offers to determine the best discount and applies that discount to the shopper.&#x20;

Offers arbitration occurs each time the system recalculates the order pricing. The system applies the winning offer until arbitration occurs again. At that time, another offer may win the arbitration. The system always recalculates order pricing when one of the following events occurs:

* **Change in product quantity**—When the quantity of products in the shopping cart changes, the system reevaluates the contents to determine which offer provides the best discount. Tiered discount offers frequently use the product quantity to determine the discount.
* **Addition or removal of products**.—The product purchased by the shopper affects nearly all offers. When a shopper adds or removes products from the shopping cart, the system reevaluates the shopping cart to determine if it should apply an offer. Bundle offers typically require the shopper to purchase specific products to trigger the offer.
* **Change to shipping or billing address**—Offers can require a specific ship-to address. If the shopper changes the address, Commerce API reevaluates the order to determine if it is still eligible for the offer.&#x20;
* **Change in store locale**—You can restrict offers to specific locales. If the shopper changes the locale, Commerce API may activate or deactivate an offer for the order based on the selected locale.&#x20;
* **Change in currency**—You can restrict some offers to specific currencies. If the shopper changes the currency, the order may become ineligible for the offer based on the currency.
* **Change in shipping method**—You can set up shipping offers to require a specific shipping method. If the shopper changes the shipping method in the shopping cart, the order may become ineligible for the offer.
* **Restored shopping cart**—Commerce API uses cookies to track visitors and shopping carts. If a shopper leaves a store without completing an order, we save the contents of the shopping cart in a cookie for up to one year from the date when the shopper opened the shopping cart. When the shopper returns to the store and reopens the shopping cart, we restore the cart to the last version saved in the cookie. If Commerce API applied offers to the order, we run arbitration on the offers using current offer data and show the current discount to the shopper.

Commerce API arbitrates the offers each time it calculates the pricing in the order. As a result, the offer that Commerce API applies to the order before and after one of these events may change.&#x20;

For example, a shopper in London (`en_GB`) enters a store while using the default locale United States (`en_US`). The shopper browses the store and adds a product to the shopping cart. In the shopping cart, they see a discount of $5 off the product price of $50. The shopper changes the selected locale to the United Kingdom (`en_GB`), and the discount no longer applies to the order. In this instance, the offer is only valid for shoppers in the United States (`en_US`) locale or for orders shipped to that locale. If you set up another offer for the United Kingdom (`en_GB`), the system would apply the new offer to the order when the shopper changed the locale.

## Arbitration by discount level

Marketing offers provide discounts on one of the following levels:

* **Item Level Discount**—Discounts costs associated with a single line item (product). When the item has multiple item level discount offers, we only provide the best discount to the shopper. If there are multiple line items in the cart, every line item can have its own best item level discount offers.
* **Order Level Discount**—Discounts the total costs for an order. When the cart has multiple order level discount offers, we only provide the best discount to the shopper.
* **Order Level Shipping Discount**—Discounts shipping costs for the entire order. When the cart has multiple order-level shipping discount offers, we only provide the best discount to the shopper.
* **Product Level Shipping Discount**—Discounts shipping costs for a specific product in the order. When the product has multiple product level shipping discount offers, we only the best discount to the shopper. If there are multiple products in the cart, every product can have its own best product level shipping discount offers.
* **Product-specific Discount**—Discounts the cost for a specific product.
* **Product-specific Shipping Discount**—Discounts the shipping costs for a specific product.
* **Storewide Discount**—Discounts the cost for any product.
* **Storewide Shipping Discount**—Discounts shipping cost for any product.

The offer type determines the discount level. During offer arbitration, we only reconcile offers against other offers with the same discount level. The offers with the largest discount value per discount level win the arbitration. Under the right circumstances, the system applies up to four offer discounts to a shopper's order.

For example, if you have an order level discount offer (10% off an order totaling $100 or more) and a product level discount (5% off the product price), the system can apply both offers to the order because each offer applies a discount to a different level. The system does not run arbitration when the discount levels for the offers are different.

A "stacked" offer occurs when a shopper redeems two or more offers in the same order. In general, we provide four distinct types of discounts. A shopper can redeem a stacked offer as long as there is only one offer for each of the following discount types in the order:

For example, if you create an offer for a storewide shipping discount of 10% and an offer for a 25% product-level discount, a shopper could redeem both offers because one is a storewide shipping discount and the other is a product-specific cost discount. If both offers were product-specific shipping discounts, the shopper could only use one offer in the order. The system chooses the best deal for the shopper and applies that offer to the order.

## Other arbitration considerations

When Commerce API calculates the possible offers for the order and arbitrates the winner, other options can affect which offer the system applies to the order.

### Offer trigger

For qualifying orders, Commerce API automatically applies offers to the shopper. If you created an offer without an end date for the offer, it may conflict with new offers.

A coupon code is an offer that requires the shopper to enter a code in the shopping cart to redeem the offer for that order. If the shopper does not enter a code, the system does not apply the offer to the order. Coupon codes applied to the order remain until another offer triggers offer arbitration or a change in the shopping cart overrides the coupon code offer.

### Browser cookies

Outdated browser cookies can also affect offer arbitration. By default, all shopping carts hosted by Digital River use a cookie to track visitors and shopping cart contents. Cookies expire one year after the shopper adds the first product to the shopping cart. When a shopper returns to a store and opens the shopping cart, it may show discounts arbitrated in the previous visit.

{% hint style="success" %}
If an offer does not appear as expected, delete the browser cookies to ensure that an old cookie is not affecting the offer arbitration. Also, note that each browser uses its cookie. If you use more than one browser, you may need to delete cookies associated with each browser.
{% endhint %}

Outdated cookies can affect arbitration. Outdated cookies are common when you repeatedly test offers in a store. Users who regularly preview offers (without using the Test Live Site or Test Design Site links or functions) may see unexpected results because the system used the cookie from their previous session to arbitrate offers in the shopping cart.
