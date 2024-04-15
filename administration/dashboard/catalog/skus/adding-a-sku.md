---
description: Learn how to add a SKU.
---

# Adding a SKU

To add a SKU:

1. Click **SKUs** in the left navigation. The SKUs page appears.
2.  Click the **Add SKU** button at the top right of the page. The Add SKU page appears.\


    <figure><img src="../../../../.gitbook/assets/1 adding a sku.png" alt=""><figcaption></figcaption></figure>
3. Enter the required SKU information. The Metadata and Additional information sections are optional.\
   **Note:** You must provide one of the following:
   * **ECCN** and **Tax Code** (both pieces of information)
   * **SKU group**. Select one from the dropdown list.&#x20;
4. Click **Save** at the top right of the page.
5. A green **SKU added** dialog box will appear in the bottom left corner of the screen.

## Add SKU fields

### SKU information

When you add a [SKU](../../../../product-management/skus.md#skus), provide the required SKU information on the Add SKU page. The fields are defined below.

#### ID

Provides a unique identifier for a [SKU](../../../../product-management/skus.md#product-details). Retailers use a SKU to identify and track products. SKUs hold data on the most important characteristics of a product.

#### Name

Provides a unique description of that product.

#### Country of origin

Specifies the [two-letter country code](../../../../product-management/creating-and-updating-skus.md#country-of-origin) of the country where a product was manufactured. You must provide a country code that is the same as what is listed on the product's certificate of origin.

### ECCN /Tax Code OR SKU group information (required)

When you add a [SKU](../../../../product-management/skus.md#skus), provide the required pieces of [<mark style="background-color:yellow;">ECCN</mark>](../../../../product-management/creating-and-updating-skus.md#eccn) <mark style="background-color:yellow;">and</mark> [<mark style="background-color:yellow;">Tax Code</mark>](../../../../product-management/creating-and-updating-skus.md#tax-code) <mark style="background-color:yellow;">OR</mark> [<mark style="background-color:yellow;">SKU group</mark>](../../../../product-management/setting-up-sku-groups.md) information. You must provide one or the other. The fields are defined below.

#### ECCN

Specifies the product's [Export Control Classification Number ](../../../../product-management/creating-and-updating-skus.md#eccn)(ECCN).

#### Tax code

Provides [a code](../../../../product-management/creating-and-updating-skus.md#tax-code) to specify whether Digital River classifies the product as [physical or digital](adding-a-sku.md#how-products-are-specified-as-physical-or-digital). By using this code, you ensure that taxes are accurately assessed on that product.

#### SKU Group

A [SKU group](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/SkuGroups) represents a collection of products with similar compliance requirements. SKU groups store [product compliance data](adding-a-sku.md#product-compliance-data-in-sku-groups) that is used when calculating taxes, determining [landed cost](../../../../integration-options/checkouts/creating-checkouts/landed-costs.md), identifying goods at international borders, creating invoices, and numerous other downstream operations.

### Metadata (optional)

You can also provide optional [metadata](https://www.digitalriver.com/docs/digital-river-api-reference/#section/Metadata) information. Use metadata to further summarize and describe products. Use it also to classify, organize, label, and understand product data. You can use metadata to quickly sort and search data. The following section provides details on metadata information. The fields are defined below.

#### Name

Provides a descriptive name (for example, subscriberID or coupon\_Program) for the item of metadata that you are adding. You can use this information for searching and reporting purposes. The name has a 40-character limit.

#### String

Select the correct datatype of the metadata from the dropdown list. Choose either **String**, **Integer**, or **Boolean**. The default setting is String. The string has a 500-character limit.

#### Value

Provides the actual value of the metadata that will be shared. Click **Add row** to add another metadata value. Click the Trash ![](<../../../../.gitbook/assets/image (6) (2).png>)icon to delete a metadata value.

### Additional information (optional)

Besides metadata, you can also provide more optional information. The fields are defined below.

#### HS Code

Represents a SKU's [Harmonized System code](https://www.trade.gov/harmonized-system-hs-codes). The Harmonized System is a standardized numerical method used for classifying traded products. International customs authorities use the code to identify products for assessing duties and taxes and collecting statistics.

#### Weight

Specifies the [weight](../../../../product-management/creating-and-updating-skus.md#weight-and-weight-unit) of physical products in the units you have configured. If a client's physical products are being sold [cross-border](../../../../general-resources/glossary.md#cross-border), pass along the weight and unit of all of their catalog's [physical SKUs](adding-a-sku.md#how-products-are-specified-as-physical-or-digital).

#### Unit

Specifies the [weight unit](../../../../product-management/creating-and-updating-skus.md#weight-and-weight-unit) associated with a physical product. You can choose from oz, lb, g, or kg. If a client's physical products are being sold [cross-border](../../../../general-resources/glossary.md#cross-border), pass along the weight and unit of all of their catalog's [physical SKUs](adding-a-sku.md#how-products-are-specified-as-physical-or-digital).

#### Part number

Specifies a [manufacturer part number (MPN)](../../../../product-management/creating-and-updating-skus.md#manufacturer-id-and-part-number). This is a unique static code issued by manufacturers to identify a part/product. Part numbers let customers accurately identify exact parts and protect themselves from counterfeits.

#### Description

Provides a summary description of a product.

#### URL

Specifies the [address ](../../../../product-management/creating-and-updating-skus.md#image-and-url)of a resource that contains the product's description.

#### Image URL&#x20;

Specifies the URL of a resource that holds the product's [image](../../../../product-management/creating-and-updating-skus.md#image-and-url). This resource should link to one or more images you want to display to customers while they are reviewing products in a store.

#### Item breadcrumb

Specifies a path that serves as a navigational and tax classification aid for the product associated with this SKU. Create a text path to the current product in relation to the product's site structure, starting from the top level to the current product.&#x20;

The correct format for this item is `TopCategory > SubCategory1 > SubCategory2 > SubCategory3`. A space ( ) should precede and follow each angle bracket (>), for example:\
`Sports & Outdoors > Exercise & Fitness > Wearable Technology > Fitness Trackers`. Do not use a semicolon (;) character in your item. The category string has a 100-character limit. The total item breadcrumb string has a 4000-character limit.

Add multiple Item breadcrumb paths by clicking the **Add row** link underneath the Item breadcrumb field. Enter the new path and click **Save**.

[Edit ](editing-a-sku.md)the Item breadcrumb when the SKU details page is in [Edit mode](editing-a-sku.md). Click **Save**.

Delete the Item breadcrumb by clicking the Trash icon![](<../../../../.gitbook/assets/image (6) (2).png>) next to an Item breadcrumb row. Click **Save**.
