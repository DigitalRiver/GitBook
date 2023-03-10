# Live changes

The changed attributes under the `liveChanges` object will go live immediately. You do not need to deploy these changes. You can use the following attributes to insert live changes when creating a product. After creating the product, the fields are read-only. You can apply live changes by using the `POST /v1/products/{productId}/live-changes` API. This object is available when you update a product. This object includes the following attributes:

## Live-changes resource

The following details describe the key attributes when applying live changes. For a complete list, refer to the [Update the live changes](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Manage-Product-\(Asynchronous-API\)/paths/\~1products\~1%7BbaseProductId%7D\~1variations\~1%7BvariationId%7D\~1live-changes/post) in the [Admin APIs Reference](https://www.digitalriver.com/docs/commerce-admin-api/) document.

### External reference identifier

The `externalReferenceId` is the [external reference identifier](../common-shoppers-and-admin-apis-reference/external-reference-identifier-erid.md). A unique identifier for the product from the Digital River client.

### catalogs

The `catalogs` is a collection of products for sale on your site. A catalog contains categories to organize your products.

#### Calalog identifier

A `calalogId` is the catalog identifier.

#### Categories

The `categories` is an array of products organized within within a catalog and often appear in the store to help shoppers locate products and navigate the store/site.

* **`categoryId`**: The category identifier.

#### Prices

The `prices`is an array prices for a product by currency and locale.

* **`type`**: The type of the price list. Used to classify the prices in a price list. A price list type may also indicate how the price list or pricing will be used. For example, you can create an MSRP list, a subscription renewal price list, and so on.
* **`prices`**: The `prices` is an array of prices for a product by currency and locale.
  * **`currency`**: A three-letter [ISO 4217](https://www.xe.com/iso4217.php) currency code.
  * **`locale`**: Optional. If your store supports multiple locales, your price list will contain space for you to enter pricing in currencies used by the locales supported by your store. The price you enter for a product in a currency will be used by any locale that uses the currency in which you entered the price.
  * **`configuredPrice`**: The configured price for the product.
