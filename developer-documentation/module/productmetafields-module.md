---
description: Learn more about the Product Meta Fields module.
---

# Product Meta Fields module

Digital River requires products to have certain fields that are not present in the WooCommerce product. Add these fields to the `WC_Product` by using the concept of meta fields by using the `ProductMetaFields` module.

### Add a new field to the metabox&#x20;

To add a new field to the metabox:&#x20;

1. Grab the **Field array** from the filter: `add_filter( 'digitalriver.meta_fields', 'filter_method' )`
2. Pass the array as the first argument to `filter_method()`.
3. Add or remove fields from the array and then return it.

### Product Meta Fields Methods

#### Product Meta Fields class&#x20;

This class acts as the module's entry point.

| Method                                       | Args, Returns, and Descriptions                                                                                                                                                                                                   |
| -------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| name                                         | <p><strong>Arg</strong>: -</p><p><strong>Return</strong>: string</p><p><strong>Description</strong>: Returns the name of the module</p>                                                                                           |
| \_\_construct                                | <p><strong>Arg:</strong> <code>MetaFieldsContainer</code> $container</p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Constructs the object by passing in the dependencies</p>                             |
| init                                         | <p><strong>Arg:</strong> -</p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Initializes the module, register necessary hooks, and defines the fields</p>                                                   |
| admin\_enqueue\_scripts                      | <p><strong>Arg</strong>: String $hook_suffix</p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Enqueue the scripts and stylesheets in the <code>admin_enqueue_scripts</code> hook</p>                       |
| woocommerce\_product\_data\_tabs             | <p><strong>Arg</strong>: array $product_data_tabs</p><p><strong>Return</strong>: array</p><p><strong>Description</strong>: Add a new tab to enter the Digital River product details in the product create/edit page.</p>          |
| woocommerce\_product\_data\_panels           | <p><strong>Arg</strong>: -</p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Renders HTML of Digital River tab under the WooCommerce Product Data metabox</p>                                               |
| woocommerce\_admin\_process\_product\_object | <p><strong>Arg</strong>: <code>WC_Product</code> $product</p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Saves the <code>digitalriver</code> meta values in metadata when a product is saved/created</p> |
| field                                        | <p><strong>Arg</strong>: String $key</p><p><strong>Return</strong>: Field</p><p><strong>Description</strong>: Gets a field name as an argument and returns the field object</p>                                                   |

#### Meta Fields Container class

This class acts as a Dependency Injection container for providing dependencies to classes present in the ProductMetaFields module.

| Method           | Args, Returns, and Descriptions                                                                                                                                                                                                   |
| ---------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| \_\_construct    | <p><strong>Arg</strong>: <code>PimpleContainer</code></p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Accepts a Dependency Injection container as an argument and assigns it to a container attribute</p> |
| define\_services | <p><strong>Arg</strong>: -</p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Defines all the classes present within the module</p>                                                                          |

### Field interface

The interface must be implemented by all the meta fields.

| Method    | Args, Returns, and Descriptions                                                                                                                                                   |
| --------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| meta\_key | <p><strong>Arg</strong>: -</p><p><strong>Return</strong>: string</p><p><strong>Description</strong>: Returns the meta key</p>                                                     |
| render    | <p><strong>Arg</strong>: -</p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Renders the meta field to the metabox</p>                                      |
| value     | <p><strong>Arg</strong>: int $post_id</p><p><strong>Return</strong>: mixed</p><p><strong>Description</strong>: Retrieves meta value of the post with id <code>$post_id</code></p> |
| save      | <p><strong>Arg</strong>: int $post_id, mixed $value</p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Saves the meta value to the post</p>                  |

### Field classes

This module has the following field classes:

| Field class       | Description                                                                                                                                                                                                                                                             |
| ----------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `CountryOfOrigin` | The `CountryOfOrigin` field refers to the location where the product originated. The `CountryOfOrigin` is a two-letter Alpha-2 country code as described in the ISO 3166 international standard. Here is a list of [country codes](https://www.iban.com/country-codes). |
| `ECCN`            | Exports Control Classification Number (ECCN). A list of pre-approved ECCNs is found [here](https://www.digitalriver.com/legal-other/approved-eccns/).                                                                                                                   |
| `HSCode`          | Read more [here](https://docs.digitalriver.com/digital-river-api/checkouts-and-orders/skus/common-attributes#setting-the-harmonized-system-code) about the Harmonized Commodity Description and Coding System (HS Code).                                                |
| `TaxCode`         | See a list of supported tax codes [here](https://docs.digitalriver.com/digital-river-api/checkouts-and-orders/skus/creating-and-updating-skus#setting-the-tax-code).                                                                                                    |







