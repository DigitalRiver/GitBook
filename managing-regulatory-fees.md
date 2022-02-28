---
description: Learn how to manage regulatory fees.
---

# Managing regulatory fees

The rise in the use and sale of consumer electronics (CE) has created concern over the economic and environmental impact these products have throughout their life cycle. This concern has brought about legislation and regulations in North America, Asia, and Europe to address the manufacture, use, recovery, and recycling of CE products throughout the world.

The European Commission (EC) has adopted several directives governing the fair use and end-of-life handling of Consumer Electronic products. These directives aim to control the use of hazardous substances, reduce waste from electrical and electronic equipment, and guarantee the right to duplicate copyright materials with reprography and storage devices. The EC directives have a significant and direct impact on any business that produces, sells, resells, imports, or distributes consumer electronic products within the European Union (EU). In addition, other laws apply such as the California Electronic Waste Recycling Act.

Laws regarding the recycling of hardware and consumer electronics were created as mandated by the EC directive. This directive holds producers responsible for the handling and recycling of WEEE at the end of the product’s life. To fund these obligations, producers are allowed to charge product fees at the point of sale. These fees are often presented in the shopping carts on e-commerce sites depending on the visibility requirements of each country.

In the Salesforce B2B Commerce App, the client is the source of truth for the regulatory fees. You will be responsible for:

1. Working with your regulatory support resources to determine the products and jurisdictions that require the payment of fees
2. Aligning fees to SKUs
3. Ensuring the fee is passed on the SKU object
4. Ensuring the fee amount is based on the ship-to address (jurisdiction) for the order.

This app provides support for four Product Fee types: WEEE, battery, copyright, and E-Waste fees. All the Regulatory Fee Types are created as CC Products in Salesforce and the Custom DR Field **Regulatory Fee Produc**t is set to `true` for them. Regulatory Fee Types are also excluded from the product index so that they cannot be searched in the storefront. We also have a custom object called DR Regulatory Fees (**digitalriverv2\_\_DR\_Regulatory\_Fees\_\_c**) to store the fee amount for each product based on the ship-to address state and country.

![](<.gitbook/assets/Install DR B2B API Connector103.png>)

{% hint style="info" %}
Download the **RegulatoryFeesProductSetupScript.txt** file and save it to your computer. This script creates the Regulatory Fee types as CC Products. Create Regulatory Fee products when you must collect regulatory fees in your storefront.
{% endhint %}

{% file src=".gitbook/assets/regulatoryProductScript.txt" %}
regulatoryProductScript.txt
{% endfile %}

For example, the following steps show you how to set up the E-Waste Regulatory fee for a CC Product named Splendid Sumatran Dark Roast Bean bag:

1. Go to the **DR Regulatory Fees** tab and click **New DR Regulatory Fee**. ![](<.gitbook/assets/Install DR B2B API Connector104.png>)
2. Select **EWaste** as the Regulatory Fee Type.
3. Select **Splendid Sumatran Dark Roast Bean Bag** as the CC Product. This indicates that EWaste Regulatory fees will be collected for this product whenever it is added to the cart.
4. Add the Category, Fee Amount, Currency Code, Country Code, and Subdivision (State ISO code). Enter a comma-separated list of state codes if the fee is the same for multiple states in the same country. The **Fee Id** field shows the identifier of the Fee object created by Digital River.
5. Select the **Visible** check box, if it is not already selected. This Indicates that the jurisdiction requires the fee to be included in the price displayed to the customer.\
   ![](<.gitbook/assets/Install DR B2B API Connector105.png>)
6. Click **Save**. Once the record is saved, it should set the **Sync Product to DR** flag to `true` on the CC Product **Splendid Sumatran Dark Roast Bean Bag**. \
   ![](<.gitbook/assets/Install DR B2B API Connector106.png>)
7. When the Product sync job runs next time, it will send the new regulatory fee information to Digital River so that these fees will be collected whenever this product is shipped to the state configured above. When the fee information is synced to Digital River, the Fee Id field will be populated.\
   ![](<.gitbook/assets/Install DR B2B API Connector107.png>)
8. Going forward, whenever this product is added to your cart and the ship-to address matches the configuration above, then the Regulatory Fee information will be displayed on the Order Review page as Duties. \
   ![](<.gitbook/assets/Install DR B2B API Connector108.png>)
9. The Regulatory fee amount (duties) is stamped on the Total Surcharge field on CC Cart and also on the CC Order once the order is placed.&#x20;

![](<.gitbook/assets/Install DR B2B API Connector109.png>)
