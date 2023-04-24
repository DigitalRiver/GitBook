---
description: Learn more about Commerce API pricing fields.
---

# Pricing

## Fields

### Line item level fields

#### Fee tax

The value for the `feeTax` field is the fee tax amount of the line item with quantity. If there is more than one fee for this product, this amount is the sum of all fee taxes regardless of whether the fees are  "Included in Price" (an invisible fee) or fee "Excluded from price" (a visible fee).

#### Import duty

The value for the `importDuty` field is the import duty amount. When a customer purchases products online, one or more of the products may not originate in the country the customer resides in, and therefore are subject to customs duty when importing products across international borders.

When goods are not shipped domestically (within the customer’s country) or within a single customs union, such as the European Union, the customer is liable to pay any inbound duties which the customer’s local customs authority deems appropriate.

#### Import tax

The value for the `importTax` field is the VAT or other sales tax assessed on the transaction.

#### List price

The value for the  `listPrice` field is the per-unit price setup in the price list for the product associated with this line item. It includes:

* The "Included in Price" fee (an invisible fee) if it's configured for the line item
* If the price list is set to tax-inclusive, this price will include tax

It does not include the following:

* The discount
* The "Excluded from price" fee (a visible fee)
* If you set the price list to tax-exclusive, this price will NOT include tax

#### List price with quantity

The value for the `listPriceWithQuantity` field is the total calculated list price for the line item with quantity. It includes:

* The "Included in Price" fee (an invisible fee) if it's configured for the line item
* If you set the price list to tax inclusive, this price will include tax

It does not include the following:

* The discount.
* The "Excluded from price" fee (a visible fee).
* If you set the price list to tax exclusive, this price will NOT include tax.
* The value for this field uses the following formula: [`listPrice`](pricing.md#list-price) × `qty`.

#### Product tax

The value for the `productTax` field is the tax amount for the product at the line-item level with quantity. When you set up a fee for the product and choose "Included in Price" (an invisible fee), the response includes the fee in the price and excludes the invisible fee tax in the `productTax`. When you set up the fee and choose "Excluded from Price” (a visible fee), the response excludes the visible fee tax from `productTax`.

#### Sale price

The value for the `salePrice` field is the per-unit price for the product associated with this line item. It includes:

* The line item level discount per unit
* The "Included in Price" fee (an invisible fee) if it's configured for the line item
* If you set the price list to tax inclusive, this price will include tax

It does not include the following:

* The order level discount
* The "Excluded from price" fee (a visible fee)
* If you set the price list to tax exclusive, this price will NOT include tax
* The value for this field uses the following formula: [`salePriceWithQuantity`](pricing.md#sale-price-with-quantity) ÷ `qty`

#### Sale price with quantity

The value for the `salePriceWithQuantity` field is the total calculated price for the line item with quantity. It includes:

* The line item level discount
* The "Included in Price" fee (an invisible fee) if it's configured for the line item
* If you set the price list to tax inclusive, this price will include tax

It does not include the following:

* The order level discount
* The "Excluded from price" fee (a visible fee)
* If you set the price list to tax exclusive, this price will NOT include tax

#### Shipping tax

The value for the `shippingTax` field is the shipping tax amount of the line item with quantity. If you ship more than one line item together, the items might share the shipping tax amount in the response for the order.

#### Tax rate

The value for the `taxRate` field is the rate available for calculating the tax for this line item.

### Order level fields

#### Discount

The value for the `discount` field is the order level discount. It includes:

* If you set the price list to tax inclusive, this price will include tax

It does not include the following:

* The line item level discount
* If you set the price list to tax exclusive, this price will NOT include tax
* If you need an overall discount for this order, you would need to sum the sum of the discount for all items.

#### Import tax and duty

The value for the `importTaxAndDuty` field is the sum of import taxes and duties for all line items.

#### Landed cost state

The value for the `landedCostState` field is the state of landed cost calculation whose enumerated values are as follows:&#x20;

* `ERROR`: Failed to calculate landed cost. This occurs when the integration service is unavailable.
* `PREPAID`: The current cart is eligible for landed cost calculation. The shopper prepays the landed cost.
* `VIEWED_NOT_ELIGIBLE` or `NOT_ELIGIBLE`: The current cart is not eligible for landed cost calculation.

#### Order total

The value for the `orderTotal` field is the final price of the order.

#### Subtotal

The value for the `subTotal` field is the order total before applying the order level discount. This is calculated based on the sum of the line-item level [`salePriceWithQuantity`](pricing.md#sales-price-with-quantity). It includes:

* The line item level discount
* The "Included in Price" fee (an invisible fee) if it's configured for the line item
* The "Excluded from price" fee (a visible fee)
* If you set the price list to tax inclusive, this price will include tax

It does not include the following:

* The order level discount
* If you set the price list to tax exclusive, this price will NOT include tax
* The value for this field is the sum of all line-item level [`salePriceWithQuantity`](pricing.md#sales-price-with-quantity) values. If there is an "Excluded from price" (a visible fee), it will be treated as a line item and included in this value.

#### Subtotal with discount

The value for the `subtotalWithDiscount` field is the subtotal applied order level discount.

* If you set the price list to tax inclusive, this price will include tax
* If you set the price list to tax exclusive, this price will NOT include tax
* The value for this field uses the following formula: [`subtotal`](pricing.md#subtotal) – [`discount`](pricing.md#discount)

#### Shipping and handling

The value for the `shippingAndHandling` field is the shipping and handling fee.

* If you set the price list to tax inclusive, this price will include tax.
* If you set the price list to tax exclusive, this price will NOT include tax.

#### Tax

The value for the `tax` field is the sum of all taxes for this order.

#### Tax-inclusive

The value for the `taxIncludedPrice` is either `true` (tax inclusive) or `false` (tax exclusive).&#x20;
