---
description: Learn how to apply landed cost with tax-included pretty price.
---

# Tax-included pretty price

Tax-included pretty price is a feature that allows you to display a price that appeals to your shoppers. This guide shows you how to enable the tax-included pretty price with landed cost.

See[ Best practice flows by payment type](../../../../payments/sources/using-the-source-identifier.md#best-practice-flows-by-payment-type) for more information.

## Prerequisites

{% hint style="info" %}
The tax-included pretty price is based on the [landed cost](./) feature. Customer Success must enable landed cost and tax-included pretty price to use this feature. Contact your Customer Success Manager for assistance.
{% endhint %}

To enable a tax-included pretty price, you need to:

1. Work with your Customer Success Manager to enable landed cost.
2. Work with your Customer Success Manager to enable landed cost with a tax-included pretty price.
3. [Create a price list](tax-included-pretty-price.md#creating-a-price-list-with-a-pretty-price) and enable Prices Include Value Added Tax (VAT).
4. [Set the shipping cost to tax-inclusive](tax-included-pretty-price.md#setting-the-shipping-cost-to-tax-inclusive).

## Creating a price list with a tax-included pretty price

Price lists allow you to define how to convert product prices from the default currency to other currencies for different locales. Create a price list with Prices Include Value Added Tax (VAT) enabled to enable the tax-included pretty price.

1. Sign in to [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do).
2. If your company has more than one site, select the site from the **Sites** field. Global Commerce automatically populates the **Site** field if your company has only one site.\
   &#x20;<img src="../../../../.gitbook/assets/sites.png" alt="" data-size="original">&#x20;
3.  Select **Catalog**, select **Pricing & Plans**, and then choose one of the following options:

    * Click **Create Price List**.
    * Click **Manage Price Lists** and then click **Create Price List**.&#x20;

    The Create Price List page appears.&#x20;

    <div align="left">

    <figure><img src="../../../../.gitbook/assets/Create Price List.png" alt=""><figcaption></figcaption></figure>

    </div>
4. Complete the fields, and select the **Prices Include Value Added Tax (VAT)** checkbox to enable tax-inclusive pricing. See [Create Price List](https://help.digitalriver.com/help/gc/Products/Price-Lists/Creating-a-price-list.htm?Highlight=Price%20List#CreatePriceListAttributes) attributes for more information.
5.  Click **Save**. The Price List Details page appears.

    <div align="left">

    <figure><img src="../../../../.gitbook/assets/Price List Details.png" alt=""><figcaption></figcaption></figure>

    </div>
6. Complete the fields on the Price List Details page. See the [Price List Details attributes](https://help.digitalriver.com/help/gc/Catalog/Pricing-and-Plans/Managing-price-list-details.htm#PriceListDetailsAttributes) for more information.
7. Scroll down and click **Done**.

## Setting the shipping cost to tax-inclusive

The Features tab on the Configure Site Settings page allows you to enable or disable features that appear in your store. For landed cost and landed cost with a tax-included pretty price, shipping costs should be tax-inclusive.

1.  From [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do), select **Administration**, select **Site**, then click **Configure Site Settings**. The Configure Site Settings page appears.

    <figure><img src="../../../../.gitbook/assets/Configure Site Settings.png" alt=""><figcaption></figcaption></figure>
2.  To set the shipping cost to tax exclusive, click the **Features** tab, scroll down to **Input Tax-Inclusive Shipping Cost**, and set the toggle for **Input Tax-Inclusive Shipping** to **ON**. Digital River will send the tax-inclusive shipping costs to the shipping carrier for the landed cost calculation. This ensures the shopper is not double-taxed by the shipping carrier.\
    \
    **Note**: If you need to support shipping a product to another locale within a country (non-cross border), and the locale supports the landed cost solution, contact your Customer Success Manager.

    <div align="left">

    <figure><img src="../../../../.gitbook/assets/Input Tax-Inclusive Shipping Cost enabled.png" alt=""><figcaption></figcaption></figure>

    </div>
3. Click **Apply**.

## Landed cost without a tax-inclusive pretty price

When you disable the tax-inclusive pretty price, the landed cost solution can only accept the Tax Exclusive Product Price. You need to manually calculate a tax-exclusive price, and then add the tax-exclusive price to the price list. If the tax-inclusive price is $1599, you can back-calculate the product price to $1279.2 without taxes. Digital River rounds the price to $1279 if a locale does not accept decimals.

Product pricing setup:

* Physical product price (tax exclusive): $1279
* Shipping cost (tax exclusive): $0 (free shipping)
* Estimated tax rate configured by Digital River: 25%

In the following table, you can see the final price (`orderTotal`) is $1598.75. While it's not a pretty price, it's close to the expected $1599.

<table><thead><tr><th width="134"></th><th>Cart without address input</th><th>Cart with address / submit cart</th></tr></thead><tbody><tr><td>Physical line item</td><td><p><code>listPrice: 1279</code></p><p><code>salePrice: 1279</code></p><p><code>productTax: 319.75</code> </p><p><code>shippingTax: 0</code></p><p><code>feeTax: 0</code></p><p><code>taxRate: 0.25</code> </p><p><code>importTax: 0</code></p><p><code>importDuty: 0</code></p></td><td><p><code>listPrice: 1279</code></p><p><code>salePrice: 1279</code></p><p><code>productTax: 0</code></p><p><code>shippingTax: 0</code>  </p><p><code>feeTax: 0</code></p><p><code>taxRate: 0</code></p><p><code>importTax: 319.75</code> </p><p><code>importDuty: 0</code></p></td></tr><tr><td>Order level</td><td><p><code>subtotal: 1598.75</code></p><p><code>discount: 0</code></p><p><code>shippingAndHandling: 0</code></p><p><code>importTaxAndDuty: 0</code></p><p><code>tax: 319.75</code> </p><p><code>orderTotal: 1598.75</code> </p></td><td><p><code>subtotal: 1598.75</code></p><p><code>discount: 0</code></p><p><code>shippingAndHandling: 119</code></p><p><code>importTaxAndDuty: 319.75</code></p><p><code>tax: 0</code> </p><p><code>orderTotal: 1598.75</code> </p></td></tr><tr><td>Tax inclusive flag</td><td><code>taxinclusive: false</code></td><td><code>taxInclusive: false</code></td></tr></tbody></table>

## Landed cost with a tax-inclusive pretty price

Product pricing setup:

* Physical product price (tax inclusive): $1599
* Shipping cost (tax exclusive): $0 (free shipping)
* Estimated tax rate configured by Digital River: 25%

In the following table, you can see the tax-inclusive pretty price in the final price where the `orderTotal` is $1599.&#x20;

|                    | Cart without address input                                                                                                                                                                                                                                                    | Cart with address / submit cart                                                                                                                                                                                                                                             |
| ------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Physical line item | <p><code>listPrice: 1599</code></p><p><code>salePrice: 1599</code></p><p><code>productTax: 319.8</code> </p><p><code>shippingTax: 0</code></p><p><code>feeTax: 0</code></p><p><code>taxRate: 0.25</code></p><p><code>importTax: 0</code></p><p><code>importDuty: 0</code></p> | <p><code>listPrice: 1599</code></p><p><code>salePrice: 1599</code></p><p><code>productTax: 0</code></p><p><code>shippingTax: 0</code>  </p><p><code>feeTax: 0</code></p><p><code>taxRate: 0</code></p><p><code>importTax: 319.8</code></p><p><code>importDuty: 0</code></p> |
| Order level        | <p><code>subtotal: 1599</code></p><p><code>discount: 0</code></p><p><code>shippingAndHandling: 0</code></p><p><code>importTaxAndDuty: 0</code></p><p><code>tax: 319.8</code> </p><p><code>orderTotal: 1599</code> </p>                                                        | <p><code>subtotal: 1599</code></p><p><code>discount: 0</code></p><p><code>shippingAndHandling: 119</code></p><p><code>importTaxAndDuty: 319.8</code> </p><p><code>tax: 0</code> </p><p><code>orderTotal: 1599</code></p>                                                    |
| Tax inclusive flag | `taxInclusive: true`                                                                                                                                                                                                                                                          | `taxInclusive: true`                                                                                                                                                                                                                                                        |

See [Pricing fields](../../../../general-resources/shopper-apis-reference/carts/#pricing-fields) for more information.

## Tax-inclusive pretty price in the shopper's checkout flow

### Cart&#x20;

The callouts in the following list show the API response payloads corresponding with the tax-inclusive pretty price values that appear on the Cart page.

<div align="left">

<figure><img src="../../../../.gitbook/assets/Cart with pretty pricing.png" alt=""><figcaption></figcaption></figure>

</div>

1. The total calculated price for the line item with quantity ([`listPriceWithQuantity`](../../../../general-resources/shopper-apis-reference/carts/pricing.md#list-price-with-quantity)). You can find it here in the response:\
   \
   `"lineItems": {`\
   `...`\
   &#x20; `"lineItem": {`\
   &#x20;     `"pricing": {` \
   `...` \
   &#x20;      `"listPriceWithQuantity": {` \
   &#x20;        `"currency": "USD",` \
   &#x20;        `"value": 3016.00` \
   `...`\
   &#x20;      `},` \
   `...`\
   &#x20;   `}`\
   `...`\
   &#x20; `}`\
   `...`\
   `}`
2. The  total calculated price for the line item with quantity ([`salePriceWithQuantity`](../../../../general-resources/shopper-apis-reference/carts/pricing.md#sale-price-with-quantity)). You can find it here in the response:\
   \
   `"lineItems": {`\
   `...`\
   &#x20; `"lineItem": {`\
   &#x20;     `"pricing": {` \
   `...` \
   &#x20;      `"salePriceWithQuantity": {` \
   &#x20;        `"currency": "USD",` \
   &#x20;        `"value": 2413.00`\
   `...`\
   &#x20;      `},` \
   `...`\
   &#x20;   `}`\
   `...`\
   &#x20; `}`\
   `...`\
   `}`
3. The shipping and handling fee of the order ([`shippindAndHandling`](../../../../general-resources/shopper-apis-reference/carts/pricing.md#shipping-and-handling)). You can find it here in the response:\
   \
   `"pricing": {` \
   `...` \
   &#x20;  `"shippingAndHandling": {` \
   &#x20;    `"currency": "USD",` \
   &#x20;    `"value": 171.00` \
   &#x20;  `},` \
   `...`\
   `}`
4. The final price of the order ([`orderTotal`](../../../../general-resources/shopper-apis-reference/carts/pricing.md#order-total)). You can find it here in the response:\
   \
   `"pricing": {` \
   `...` \
   &#x20;  `"orderTotal": {` \
   &#x20;    `"currency": "USD",` \
   &#x20;    `"value": 2513.00` \
   &#x20;  `},` \
   `...`\
   `}`

See [Pricing fields](../../../../general-resources/shopper-apis-reference/carts/#pricing-fields) for more information.

### Order review

The callouts in the following list show the API response payloads corresponding with the tax-inclusive pretty price values that appear on the Order Review page.

<div align="left">

<figure><img src="../../../../.gitbook/assets/Order review pretty pricing.png" alt=""><figcaption></figcaption></figure>

</div>

1. The final price of the order ([`orderTotal`](../../../../general-resources/shopper-apis-reference/carts/pricing.md#order-total)). You can find it here in the response:\
   \
   `pricing` > `orderTotal`\
   `"pricing": {` \
   `...` \
   &#x20;  `"orderTotal": {` \
   &#x20;    `"currency": "USD",` \
   &#x20;    `"value": 2684.00`\
   &#x20;  `},` \
   `...`\
   `}`
2. The import taxes and duties of the order, which is the sum of import taxes and duties for all the line items ([`importTaxAndDuty`](../../../../general-resources/shopper-apis-reference/carts/pricing.md#import-tax-and-duty)). Make sure the value for [`landedCostState`](../../../../general-resources/shopper-apis-reference/carts/pricing.md#landed-cost-state) is `PREPAID`. You can find it here in the response:\
   \
   `pricing` > `orderTotal`\
   `"pricing": {` \
   `...` \
   &#x20;  `"importTaxAndDuty": {` \
   &#x20;    `"currency": "USD",` \
   &#x20;    `"value": 152.00`\
   &#x20;  `},` \
   `...`\
   `}`

See [Pricing fields](../../../../general-resources/shopper-apis-reference/carts/#pricing-fields) for more information.

### Thank you

The callouts in the following list show the API response payloads that correspond with the tax-inclusive pretty price values that appear on the Thank You page.

<div align="left">

<figure><img src="../../../../.gitbook/assets/Thank you pretty pricing (1).png" alt=""><figcaption></figcaption></figure>

</div>

1. The final price of the order ([`orderTotal`](../../../../general-resources/shopper-apis-reference/carts/pricing.md#order-total)). You can find it here in the response:\
   \
   `"pricing": {` \
   `...` \
   &#x20;  `"orderTotal": {` \
   &#x20;    `"currency": "USD",` \
   &#x20;    `"value": 2684.00`\
   &#x20;  `},` \
   `...`\
   `}`&#x20;

See [Pricing fields](../../../../general-resources/shopper-apis-reference/carts/#pricing-fields) for more information.

### Invoice

The callouts in the following list show the API response payloads corresponding with the tax-inclusive pretty price values that appear on the Invoice.

<div align="left">

<figure><img src="../../../../.gitbook/assets/Invoice pretty pricing (1).png" alt=""><figcaption></figcaption></figure>

</div>

1. The  total calculated price for the line item with quantity ([`salePriceWithQuantity`](../../../../general-resources/shopper-apis-reference/carts/pricing.md#sale-price-with-quantity)). You can find it here in the response:\
   \
   `"lineItems": {`\
   `...`\
   &#x20; `"lineItem": {`\
   &#x20;     `"pricing": {` \
   `...` \
   &#x20;      `"salePriceWithQuantity": {` \
   &#x20;        `"currency": "USD",` \
   &#x20;        `"value": 2413.00`\
   `...`\
   &#x20;      `},` \
   `...`\
   &#x20;   `}`\
   `...`\
   &#x20; `}`\
   `...`\
   `}`
2. The shipping and handling fee ([`shippindAndHandling`](../../../../general-resources/shopper-apis-reference/carts/pricing.md#shipping-and-handling)). You can find it here in the response:\
   \
   `"pricing": {` \
   `...` \
   &#x20;  `"shippingAndHandling": {` \
   &#x20;    `"currency": "USD",` \
   &#x20;    `"value": 171.00` \
   &#x20;  `},` \
   `...`\
   `}`
3. The final price of the order ([`orderTotal`](../../../../general-resources/shopper-apis-reference/carts/pricing.md#order-total)). You can find it here in the response:\
   \
   `"pricing": {` \
   `...` \
   &#x20;  `"orderTotal": {` \
   &#x20;    `"currency": "USD",` \
   &#x20;    `"value": 2513.00` \
   &#x20;  `},` \
   `...`\
   `}`
4.  The order-level import taxes and duties ([`importTaxAndDuty`](../../../../general-resources/shopper-apis-reference/carts/pricing.md#import-tax-and-duty)) is the sum of **all** line items' import taxes ([`importTax`](../../../../general-resources/shopper-apis-reference/carts/pricing.md#import-duty)) and import duties ([`importDuty`](../../../../general-resources/shopper-apis-reference/carts/pricing.md#import-duty)). For example:

    * `importDutyTax`: 75
    * `lineItem`: A
      * `importTax`: 15
      * `importDuty`: 10
    * `lineItem`: B
      * `importTax`: 30
      * `importDuty`: 20

    Make sure the value for [`landedCostState`](../../../../general-resources/shopper-apis-reference/carts/pricing.md#landed-cost-state) is `PREPAID`. You can find it here in the response:\
    \
    `"pricing": {` \
    `...` \
    &#x20;  `"importTaxAndDuty": {` \
    &#x20;    `"currency": "USD",` \
    &#x20;    `"value": 75.00`\
    &#x20;  `},` \
    `...` \
    &#x20;  `"importTax": {` \
    &#x20;    `"currency": "USD",` \
    &#x20;    `"value": 15.00`\
    &#x20;  `},` \
    `...   "importDuty": {` \
    &#x20;    `"currency": "USD",` \
    &#x20;    `"value": 10.00`\
    &#x20;  `},` \
    `...`\
    &#x20;  `"importTax": {` \
    &#x20;    `"currency": "USD",` \
    &#x20;    `"value": 30.00`\
    &#x20;  `},` \
    `...   "importDuty": {` \
    &#x20;    `"currency": "USD",` \
    &#x20;    `"value": 20.00`\
    &#x20;  `},` \
    `...`\
    `}`

See [Pricing fields](../../../../general-resources/shopper-apis-reference/carts/#pricing-fields) for more information.

### Additional pricing information

The callouts in the following list show the API response payloads corresponding with the tax-inclusive pretty price values that appear on the Invoice as additional pricing information.

<figure><img src="../../../../.gitbook/assets/Invoice 2 pretty pricing with additional information.png" alt=""><figcaption></figcaption></figure>

1. The  total calculated price for the line item with quantity ([`salePriceWithQuantity`](../../../../general-resources/shopper-apis-reference/carts/pricing.md#sale-price-with-quantity)). You can find it here in the response:\
   \
   `"lineItems": {`\
   `...`\
   &#x20; `"lineItem": {`\
   &#x20;     `"pricing": {` \
   `...` \
   &#x20;      `"salePriceWithQuantity": {` \
   &#x20;        `"currency": "USD",` \
   &#x20;        `"value": 2261.00`\
   `...`\
   &#x20;      `},` \
   `...`\
   &#x20;   `}`\
   `...`\
   &#x20; `}`\
   `...`\
   `}`
2. The tax amount for the product ([`productTax`](../../../../general-resources/shopper-apis-reference/carts/pricing.md#product-tax)) at the line-item level with quantity. You can find it here in the response:\
   \
   `"lineItems": {`\
   `...`\
   &#x20; `"lineItem": {`\
   `...`\
   &#x20;  `"id="488822300023",`\
   `...`\
   &#x20;     `"pricing": {` \
   `...` \
   &#x20;      `"productTax": {` \
   &#x20;        `"currency": "USD",` \
   &#x20;        `"value": 0.00`\
   `...`\
   &#x20;      `},` \
   `...`\
   &#x20;   `}`\
   `...`\
   &#x20; `}`\
   &#x20; `"lineItem": {`\
   `...`\
   &#x20;  `"id="488822300024",`\
   `...`\
   &#x20;     `"pricing": {` \
   `...` \
   &#x20;      `"productTax": {` \
   &#x20;        `"currency": "USD",` \
   &#x20;        `"value": 5.00`\
   `...`\
   &#x20;      `},` \
   `...`\
   &#x20;   `}`\
   `...`\
   &#x20; `}`\
   `...`\
   `}`
3. The sum of the import tax ([`importTax`](../../../../general-resources/shopper-apis-reference/carts/pricing.md#import-duty)) and import duty ([`importDuty`](../../../../general-resources/shopper-apis-reference/carts/pricing.md#import-duty)). (Make sure the value for [`landedCostState`](../../../../general-resources/shopper-apis-reference/carts/pricing.md#landed-cost-state) is `PREPAID`.) You can find it here in the response:\
   \
   `"lineItems": {`\
   `...`\
   &#x20; `"lineItem": {`\
   `...`\
   &#x20;  `"id="488822300023",`\
   `...`\
   &#x20;     `"pricing": {` \
   `...` \
   &#x20;    `"importTax": {` \
   &#x20;      `"currency": "USD",` \
   &#x20;      `"value": 103.00`\
   &#x20;    `},` \
   `...`\
   &#x20;    `"importDuty": {` \
   &#x20;      `"currency": "USD",` \
   &#x20;      `"value": 49.00`\
   &#x20;    `},` \
   `...`\
   &#x20; `}`\
   &#x20; `"lineItem": {`\
   `...`\
   &#x20;  `"id="488822300024",`\
   `...`\
   &#x20;     `"pricing": {` \
   `...` \
   &#x20;    `"importTax": {` \
   &#x20;      `"currency": "USD",` \
   &#x20;      `"value": 0.00`\
   &#x20;    `},` \
   `...`\
   &#x20;    `"importDuty": {` \
   &#x20;      `"currency": "USD",` \
   &#x20;      `"value": 0.00`\
   &#x20;    `},` \
   `...`\
   &#x20; `}`\
   `...`\
   `}`
4. The sale price with quantity ([`salePriceWithQuantity`](../../../../general-resources/shopper-apis-reference/carts/pricing.md#sale-price-with-quantity)) excluding the import tax ([`importTax`](../../../../general-resources/shopper-apis-reference/carts/pricing.md#import-tax)) and import duty ([`importDuty`](../../../../general-resources/shopper-apis-reference/carts/pricing.md#import-duty)).\
   \
   `"lineItems": {`\
   `...`\
   &#x20; `"lineItem": {`\
   `...`\
   &#x20;  `"id="488822300023",`\
   `...`\
   &#x20;     `"pricing": {` \
   `...` \
   &#x20;    `"salePriceWithQuantity": {` \
   &#x20;      `"currency": "USD",` \
   &#x20;      `"value": 2413.00`\
   &#x20;    `},` \
   `...`\
   &#x20; `}`\
   &#x20; `"lineItem": {`\
   `...`\
   &#x20;  `"id="488822300024",`\
   `...`\
   &#x20;     `"pricing": {` \
   `...` \
   &#x20;    `"salePriceWithQuantity": {` \
   &#x20;      `"currency": "USD",` \
   &#x20;      `"value": 100.00`\
   &#x20;    `},` \
   `...`\
   &#x20; `}`\
   `...`\
   `}`\

5. The shipping and handling fee ([`shippindAndHandling`](../../../../general-resources/shopper-apis-reference/carts/pricing.md#shipping-and-handling)). You can find it here in the response:\
   \
   `"pricing": {` \
   `...` \
   &#x20;  `"shippingAndHandling": {` \
   &#x20;    `"currency": "USD",` \
   &#x20;    `"value": 171.00` \
   &#x20;  `},` \
   `...`\
   `}`
6. The sum of import taxes and duties for all the line items ([`importTaxAndDuty`](../../../../general-resources/shopper-apis-reference/carts/pricing.md#import-tax-and-duty)). Make sure the value for [`landedCostState`](../../../../general-resources/shopper-apis-reference/carts/pricing.md#landed-cost-state) is `PREPAID`. You can find it here in the response:\
   \
   `"pricing": {` \
   `...` \
   &#x20;  `"importTaxAndDuty": {` \
   &#x20;    `"currency": "USD",` \
   &#x20;    `"value": 152.00`\
   &#x20;  `},` \
   `...`\
   `}`
7. The sum of all taxes ([`tax`](../../../../general-resources/shopper-apis-reference/carts/pricing.md#tax)) for the order. You can find it here in the response:\
   \
   `"pricing": {` \
   `...` \
   &#x20;  `"tax": {` \
   &#x20;    `"currency": "USD",` \
   &#x20;    `"value": 5.00`\
   &#x20;  `},` \
   `...`\
   `}`
8. The final price of the order ([`orderTotal`](../../../../general-resources/shopper-apis-reference/carts/pricing.md#order-total)). You can find it here in the response:\
   \
   `"pricing": {` \
   `...` \
   &#x20;  `"orderTotal": {` \
   &#x20;    `"currency": "USD",` \
   &#x20;    `"value": 2684.00` \
   &#x20;  `},` \
   `...`\
   `}`

See [Pricing fields](../../../../general-resources/shopper-apis-reference/carts/#pricing-fields) for more information.
