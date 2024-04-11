---
description: >-
  Gain a better understanding of how Global Logistics works and how your account
  can be configured to use this service
---

# Global Logistics

Global Logistics (GL) is an end-to-end delivery management solution that, in certain cases, can provide you and your customers with a guaranteed landed cost.

In the pre-launch phase, you work closely with Digital River and one of our [global logistics providers](global-logistics.md#global-logistics-providers) (GLPs) to build an integration that accepts and processes international orders.

{% hint style="info" %}
Depending on the GLP facilitating the transaction, you can also use GL to ship your goods domestically.
{% endhint %}

During checkouts, GL allows you to present customers with a menu of shipping quotes. Once the customer places an order and the goods are picked and packed at the warehouse, your [third-party logistics](../general-resources/glossary.md#third-party-logistics) provider can use GL to print shipping labels. When the products ship, you can also use GL to track their progress .

On this page, you'll find information on [how GL works](global-logistics.md#how-global-logistics-works), Digital River's [guaranteed landed cost feature](global-logistics.md#guaranteed-landed-cost), and our [GLPs](global-logistics.md#global-logistics-providers). You can also read about [the pre-deployment process](global-logistics.md#pre-deployment).

How you interact with GL during checkouts depends on your selected integration path(s). Use the following table to access the appropriate article:

| Checkout solution                                                | Article                                                                                                                              |
| ---------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| [Low-code checkouts](../integration-options/low-code-checkouts/) | [Using a shipping endpoint](../integration-options/low-code-checkouts/using-a-shipping-endpoint.md)                                  |
| [Direct Integrations](../integration-options/checkouts/)         | [Interacting with Global Logistics in checkouts](../integration-options/checkouts/interacting-with-global-logistics-in-checkouts.md) |

Once the [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) is created, you must send the ship request, get shipping labels, and track shipments. For details on handling these processes, refer to [Managing a Global Logistics order](../order-management/managing-a-global-logistics-order.md) .

## How Global Logistics works

Global Logistics (GL) can be used to request shipping quotes during checkouts.&#x20;

GL routes the request to the appropriate [global logistics provider](global-logistics.md#global-logistics-providers) (GLP) and then returns a menu of shipping quotes that can be displayed to customers.

Once customers select an option, their shipping choice is applied to the checkout. Then, assuming they selected a quote with [delivered duty paid](../integration-options/checkouts/interacting-with-global-logistics-in-checkouts.md#shipping-terms) (DDP) terms, customers can potentially be presented with a transaction's [full landed cost](../integration-options/checkouts/creating-checkouts/landed-costs.md#what-is-landed-cost).

After the order is submitted, your commerce system must send a ship request to your [third-party logistics](../general-resources/glossary.md#third-party-logistics) (3PL) provider so that they can pick and pack the goods at the warehouse. When your 3PL is ready to print a shipping label, they send a request to Digital River, which we route to the appropriate GLP.

Upon receipt of this request, the GLP generates one or more shipping labels, sends them back to Digital River, and we relay them to your 3PL.

The shipping label request also prompts the GLP to prepare an order's international shipping documentation. The GLP bundles this documentation in a pre-clearance request sent to the destination country's customs agency.

Once the shipping labels are generated, a carrier retrieves the goods from the warehouse. In the [hub and spoke logistics model](global-logistics.md#hub-and-spoke-logistics-model), the courier delivers the products to a distribution hub before moving them to an export gateway and then shipping them to the end customer's address. In the [hubless model](global-logistics.md#hubless-logistics-model), the carrier delivers the goods directly to an export gateway, where they are shipped to the final destination.

After the goods arrive in the destination country, the GLP ensures they clear customs, moves them to a distribution site and coordinates with local carriers to deliver them the "final mile" to the end customer.

Once the shipping labels are generated, you can also use GL to track an order's shipments. For each shipment, we provide information on its status at specific locations along its route.

## Guaranteed landed cost

Depending on which [GLP](global-logistics.md#global-logistics-providers) is assigned to the transaction, the Global Logistics solution can potentially give you and your customers a guaranteed [landed cost](../integration-options/checkouts/creating-checkouts/landed-costs.md#what-is-landed-cost).

With this feature, Digital River guarantees you won't be charged additional duties, fees, or import taxes beyond those in the [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders). This is true even when the actual importation costs assessed by a country's customs agency are higher than those returned by our [landed cost calculator](../integration-options/checkouts/creating-checkouts/landed-costs.md#how-landed-costs-are-calculated).

We also guarantee that customers who select a [shipping quote](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Shipping-quotes) with [delivered duty paid](../integration-options/checkouts/interacting-with-global-logistics-in-checkouts.md#shipping-terms) terms won't be required to pay any additional costs at the time of delivery. In other words, customers will have no surprise fees. Whatever they pay at the time of order placement is the final amount.

{% hint style="info" %}
Shipping is not part of a guaranteed landed cost. During checkouts, if customers select a [shipping quote](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Shipping-quotes) whose `totalAmount` is less than the actual carrier-assessed shipping costs, then Digital River is not responsible for the difference.
{% endhint %}

## Global logistics providers

In the Global Logistics solution, you partner with one or more of Digital River's global logistics providers (GLPs) .

Digital River's GLPs specialize in shipping [physical goods](../product-management/skus.md#how-products-are-classified-as-physical-or-digital) across national borders and are considered international logistics experts. They are well-versed in country-specific regulatory requirements, understand how to prepare [commercial invoices](https://en.wikipedia.org/wiki/Commercial\_invoice) that act as the basis for all other international shipping documents, and can electronically submit pre-clearance requests to most countries' customs agencies.

Digital River's GLPs also have proprietary international shipping lanes, various export gateways, numerous final mile delivery options, and multiple [logistics model](global-logistics.md#logistics-model-designation) offerings.

## Pre-deployment

In the pre-deployment phase, you collaborate with Digital River and one or more of our [global logistics providers](global-logistics.md#global-logistics-providers) (GLPs) to define your international trading patterns, configure product data, and set up your logistics.

The following sections describe the major areas of work that need to occur before deployment:

* [Defining your trading patterns](global-logistics.md#defining-trading-patterns)
* [Defining basic product data](global-logistics.md#defining-basic-product-data)
* [Defining compliance product data](global-logistics.md#defining-compliance-product-data)
* [Configuring packaging requirements](global-logistics.md#configuring-packaging)
* [Configuring carriers](global-logistics.md#configuring-carriers)
* [Logistics model designation](global-logistics.md#logistics-model-designation)
* [Preparing for returns](global-logistics.md#preparing-for-returns)

### Defining trading patterns

In the pre-deployment phase, you must define your trading patterns so that Digital River can save them to your account.&#x20;

These patterns consist of data pairs that specify where your products ship from and where customers can have them shipped to. Digital River assigns each trading pattern to a [GLP](global-logistics.md#global-logistics-providers), so we can dynamically route shipping quotes and shipping label requests to the appropriate provider.&#x20;

For each ship from country in your trading patterns, there can be one to many ship to countries. However, there can only be a single ship-from country for each ship-to country.&#x20;

### Defining basic product data

Before deployment, you must assign basic data to each [cross-border](../general-resources/glossary.md#cross-border) eligible product in your catalog. This mainly consists of defining a product's [name and description](global-logistics.md#name), [weight](global-logistics.md#weight), [URL](global-logistics.md#image-and-url), [image](global-logistics.md#image-and-url), and [country of origin](global-logistics.md#country-of-origin).

#### **Name and description** <a href="#name" id="name"></a>

All your products must be assigned a name and should ideally have a description.

#### Product weight and dunnage <a href="#weight" id="weight"></a>

For each of your [cross-border](../general-resources/glossary.md#cross-border) eligible products, you should determine its weight in grams, kilograms, ounces, or pounds and then store this value. A product's weight:

* Helps ensure that the shipping quotes returned in the checkout process are as accurate as possible. If weight is not sent in a quotes request or a value is passed that's less than a product's true weight, the shipping costs paid by the customer will likely be lower than the actual carrier-assessed costs.\
  \
  Carriers compare a package's gross weight to its dimensions and use [dimensional weight](https://en.wikipedia.org/wiki/Dimensional\_weight) pricing to calculate shipping costs. These carrier-computed costs are what you ultimately pay.
* Must be listed in the customs documentation for certain countries. When customers want to ship a product to one of these countries, Digital River needs its weight to return a landed cost. Additionally, customs officials need weight to calculate duties and import taxes.
* Should be as precise as possible. Make sure your product's weight is exclusive of packaging but inclusive of [dunnage](https://en.wikipedia.org/wiki/Dunnage). In other words, don't include the weight of the product's box but do include the weight of the protective and supporting materials that go inside the box.

#### **Image and URL**

A product's image and URL typically get added to customs documentation, which officials use to determine pre-clearance. While performing this process, these officials can use the URL to access a product description and the image to see what the product looks like.

#### **Country of origin**

A product's country of origin represents where a product was manufactured. The country value you provide Digital River must be the same as what is listed on the product's certificate of origin.&#x20;

### Defining compliance product data

Each [cross-border](../general-resources/glossary.md#cross-border) eligible product in your catalog must be associated with compliance data.

Before deployment, Digital River and your GLP work with you to define this data. Once defined, a [product's compliance data](../product-management/skus.md#basic-versus-compliance-product-data) is stored in an associated [SKU group](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SkuGroups).

The following describes some of the compliance data that must be defined during the prelaunch process:

#### Tax code

Each product must be associated with a tax code. It determines whether the product is classified as [physical or digital](../product-management/skus.md#how-products-are-classified-as-physical-or-digital). The code should be as accurate as possible to assess the correct taxes.

You'll need to provide Digital River with sufficient details about your products so that we can determine their tax codes and then add this data to the relevant SKU group.

#### Export control classification number

A product must have a [Digital River-approved Export Control Classification Number (ECCN)](https://www.digitalriver.com/legal-other/approved-eccns/). This value determines whether the product:

* Requires a US export/re-export license
* Contains any other license requirements/restrictions
* Has an end use which is prohibited by applicable export control laws

Before launching, we work with you to identify your products' ECCNs and store them in the relevant [SKU groups](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SkuGroups).

#### Harmonized system codes

You need to provide Digital River with sufficient details about your products so that we can classify their [harmonized system](https://en.wikipedia.org/wiki/Harmonized\_System) (HS) codes. This includes the six-digit universal HS code used to classify product groups at the international level and the country-specific code.

These country-specific codes almost always have more digits than the universal code. Customs officials worldwide use them to identify the duty and import tax rates that should be applied to different product groups. Digital River also needs them to generate a [landed cost](../integration-options/checkouts/creating-checkouts/landed-costs.md) calculation.

#### Dangerous goods classifications

Certain products are classified as [dangerous goods](https://en.wikipedia.org/wiki/Dangerous\_goods), considered any substance or material that poses unreasonable health, safety, or property risk when transported.

For example, some products, such as lithium batteries and (in)flammable perfumes, are susceptible to static electricity and temperature and pressure variations. These forces can cause them to leak, emit toxic fumes, ignite, or even explode. This is especially true when they are transported by air. As a result, these categories of products require special packaging, handling, and modes of transportation.

It's your responsibility to let Digital River know which of your products are classified as dangerous so that we can store this compliance data. However, in some cases, the [GLP](global-logistics.md#global-logistics-providers) might help review your product labels to determine which goods in your catalog contain ingredients that necessitate a dangerous goods classification.&#x20;

If the [GLP](global-logistics.md#global-logistics-providers) does conduct such a review, they provide Digital River with a list of these products, along with their classification values.

When a [shipping quotes request](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Shipping-quotes/operation/postShippingQuotes) is sent, Digital River determines whether any products in that request are flagged as dangerous. If this is the case, we pass this information to the GLP, and they add the appropriate surcharges, which Digital River then builds into the returned rates.

Digital River also passes this information to the GLP in the [ship label request](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Shipping-Labels) so that they can flag the entire shipment for special packaging and/or handling and encode those requirements in the label.

#### Signature requirements

You should also determine your products' signature requirements In the pre-deployment process. In other words, the products require customers to sign for them at delivery.

These are often high-value items that you don't want to be left on the customer's "doorstep" by the delivery person. Putting a signature requirement in place helps prevent theft.

### Configuring packaging

You can optionally [define and save a default package](global-logistics.md#default-box). Also, depending on the sophistication of the [warehouse management software](https://en.wikipedia.org/wiki/Warehouse\_management\_system) (WMS) you access, you may decide to [employ packing algorithms](global-logistics.md#packing-algorithms).

#### Default package <a href="#default-box" id="default-box"></a>

Our GL solution allows you to define a default box. In other words, you configure a box with a default weight, height, width, and length. Digital River then saves these values to your account.

If you configure a default box and packaging data is not sent in the shipping quotes request or shipping labels request, Global Logistics passes these saved measurements to the [GLP](global-logistics.md#global-logistics-providers).

We recommend using a default box when you know most products will be shipped in packages with uniform dimensions and a standardized weight. You can work with your [WMS](https://en.wikipedia.org/wiki/Warehouse\_management\_system) provider to identify your most frequently used box size.

#### Packing algorithms

Inefficient packing can result in higher shipping costs. This is because carriers often use [dimensional weight pricing](https://en.wikipedia.org/wiki/Dimensional\_weight), which is meant to incentivize efficient packing methods.&#x20;

If your [WMS](https://en.wikipedia.org/wiki/Warehouse\_management\_system) uses [bin packing algorithms](https://en.wikipedia.org/wiki/Bin\_packing\_problem), you can use them to potentially lower your shipping costs. These algorithms attempt to solve the problem of how to most efficiently pack multiple items of various sizes into a finite number of boxes. Based on the dimensions of a shipment's products, they return the recommended number of boxes and their optimal dimensions.

If you have access to such algorithms, work with your WMS provider to build an integration that allows you to request suggested box counts and dimensions during checkout so that they can be passed in the shipping quotes request.

### Configuring carriers

Before deployment, you work with Digital River and the GLP to set up and save your carrier options. During checkouts, when a shipping quotes request is made, the GLP uses this information to construct a list of transaction-specific shipping quotes that customers can select from.

### Logistics model designation

The [GLP](global-logistics.md#global-logistics-providers) analyzes your warehouse locations, [trading patterns](global-logistics.md#defining-trading-patterns), applicable carriers, and expected ship volumes. Based on the results of this analysis, the GLP makes a logistics model determination.

More specifically, the GLP informs you whether (1) a [hub and spoke logistics model](global-logistics.md#hub-and-spoke-logistics-model) or (2) a [hubless logistics model](global-logistics.md#hubless-logistics-model) best suits your needs. In both models, the [GLP](global-logistics.md#global-logistics-providers) acts as the [cross-border](../general-resources/glossary.md#cross-border) shipment manager.&#x20;

#### **Hub and spoke logistics model**

In the hub and spoke model, orders are picked and packed at your [3PL’s](../general-resources/glossary.md#third-party-logistics) warehouse. The 3PL then requests a shipping label for each order which will contain the final mile address (i.e., the customer’s address) which is placed on the shipment. All the shipments are then put in a container or over box and sent to the [GLP’s](global-logistics.md#global-logistics-providers) nearest hub. There the goods are processed as if they’d arrived on a pallet before being shipped to the destination country.

#### **Hubless logistics model** <a href="#hubless-logistics-model" id="hubless-logistics-model"></a>

In the hubless model, the products are picked and packed at your 3PL warehouse.

The 3PL then requests and prints a shipping label whose designated ship-to address is the final destination of the goods.

The [GLP](global-logistics.md#global-logistics-providers) then dispatches a carrier to retrieve the products from your 3PL's warehouse, moves the goods to an export gateway, and ships them to the destination country.

{% hint style="info" %}
Whichever logistics model is employed, in addition to the duties described above, the [GLP](global-logistics.md#global-logistics-providers) also:

* Prepares the import-export documentation
* Submits pre-clearance requests to the importation country's custom agency
* Ensures that the goods clear customs
* Resolves any issues should the goods get "stuck in customs"
* Coordinates with local carriers to ensure that the products are transported the "final mile" to the customer's designated ship-to address
{% endhint %}

### Preparing for returns

In the pre-deployment phase, you work with Digital River and a [GLP](global-logistics.md#global-logistics-providers) to design a reverse logistics flow that aligns with your business objectives and return policies. Since international returns are complex, there are various ways to process reversals.

At a minimum, however, you should:

* [Determine how to communicate return information](global-logistics.md#communicate-return-information)
* [Identify re-importation restrictions](global-logistics.md#determine-re-importation-restrictions)
* [Compare product value and return costs](global-logistics.md#compare-product-value-and-return-costs)
* [Set up a product disposition agreement](global-logistics.md#set-up-a-product-disposition-agreement)
* [Devise a refund policy](global-logistics.md#determine-refund-policies)

#### Communicate return information

Throughout the order flow, make sure you provide customers with consistent and detailed return instructions.

For each of your [approved ship-to countries](global-logistics.md#defining-trading-patterns), the [GLP](global-logistics.md#global-logistics-providers) supplies you with an address where customers must send returned products. The GLP can give you these return addresses prior to deployment and/or at runtime.

{% hint style="info" %}
At runtime, the GLP sends Digital River an order-specific return address during [shipping label generation](../order-management/managing-a-global-logistics-order.md#managing-shipping-labels). We then transmit this return-to address to you in both the [shipping label response](../order-management/managing-a-global-logistics-order.md#the-shipping-label-response) and the [logistics return response](../order-management/managing-a-global-logistics-order.md#the-logistics-return-response).
{% endhint %}

We recommend carefully considering how you want to provide customers with this address (along with other return instructions). For example, you could provide this information in shipment notification emails, order invoices, and/or on a customer's order management page.

#### Determine re-importation restrictions

Before accepting international orders, you'll work with the [GLP](global-logistics.md#global-logistics-providers) to review your catalog and identify goods that may be subject to strict re-importation restrictions. With such product types, returns are often not feasible.

Health and beauty products frequently fall into this category. For example, due to tampering concerns, some exported cosmetics and supplements are either not allowed back into the United States or, if they are, require [Food and Drug Administration](https://www.fda.gov) approval.

#### Compare product value and return costs

International shipping is expensive. Sometimes, the expense of returning a product to its origin warehouse is greater than its manufacturing cost or purchase value. As a result, you may decide to destroy or liquidate such goods rather than facilitate their return. We recommend you work with the [GLP](global-logistics.md#global-logistics-providers) to identify these product types and, once identified, develop an appropriate [disposition plan](global-logistics.md#set-up-a-product-disposition-agreement) for them.

You should also remember that a product may be subject to import duties on its return journey. For example, if a product with a declared value of $1500 is exported and then returned to its warehouse, it could be assessed for re-importation duties because it exceeds the [de minimis value](https://www.trade.gov/de-minimis-value) in many countries.

#### Set up a product disposition agreement

You'll need to work with the [GLP](global-logistics.md#global-logistics-providers) to establish a disposition agreement for each product type. The terms of this agreement stipulate under what conditions the GLP should either:

* **Destroy the product product** assess you a fee for doing so, and then generate a certificate of physical destruction.
* **Liquidate the product** by selling it at a predetermined price and then shipping it to an agreed-upon location.
* **Return the product** to one of your 3PL's warehouses so that it can be put back into inventory.

You can also establish price thresholds with GLPs which they then use to determine what type of disposition to perform. For example, an agreement may specify that the GLP should destroy any products worth less than $100, liquidate products that have a value between $100 and $200, and return any higher-valued items.

#### Determine refund policies

Importation countries collect duties and taxes before permitting a shipment to clear customs. Once collected, most countries don't refund these costs simply because customers experienced a 'change of heart' or decided the merchandise is 'not as described'.

So, before checking out customers, you should identify the conditions that prompt you to issue refunds on duties and import taxes.

The [Refunds API](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Refunds) allows you to customize refunds you issue customers. For example, at the order level, we support full and partial refunds on duties and import taxes. And at the item level, you can configure duty refunds in the same way.

For details, refer to the [Issuing refunds](../order-management/returns-and-refunds-1/refunds/issuing-refunds.md) page.

If you refund duties and import taxes, remember that you're responsible for seeking reimbursement from the applicable agency in the importation country.

One option might be to devise your returns policy so duty paid is refunded on defective and damaged products but not for 'change-of-heart' returns. You could also adopt a similar policy for refunding shipping costs. Alternatively, you might decide to refund only product costs in all scenarios.

## Next steps

To learn more about how you interact with Global Logistics during checkouts, use the following table to access the appropriate article:&#x20;

| Checkout solution                                                | Article                                                                                                                              |
| ---------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| [Low-code checkouts](../integration-options/low-code-checkouts/) | [Using a shipping endpoint](../integration-options/low-code-checkouts/using-a-shipping-endpoint.md)                                  |
| [Direct Integrations](../integration-options/checkouts/)         | [Interacting with Global Logistics in checkouts](../integration-options/checkouts/interacting-with-global-logistics-in-checkouts.md) |
