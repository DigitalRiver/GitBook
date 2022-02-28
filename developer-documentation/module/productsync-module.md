---
description: Learn more about the Product Sync module.
---

# Product Sync module

This module syncs the product information to Digital River when any product is created, updated, or deleted. Products can be manually synced from the Admin dashboard via `Tools -> Available Tools`

## Specifications

This module will leverage SKU API provided by Digital River.

Whenever a product in WooCommerce is created, updated, or deleted, this module will call the Digital River SKU API and update the SKU information.

SKU API will also need the ECCN, HS Code, Country of origin, and Tax code. These fields will be added and provided by `ProductMetaFields` module.&#x20;

The `ProductSync` module does not manage the addition and validation of required meta fields. That process is managed in the `ProductMetaFields` module.

### Modify the SKU Request object&#x20;

To modify the `SKURequest` object before sync:

1. Grab the `SKURequest` object from the filter: `add_filter( 'digitalriver.pre_sync_sku_request', 'filter_method' )`
2. The `SKURequest` object will be passed as the first argument to `filter_method()`.
3. Make any changes to the object and then return the object.

### Replace the Sync Handler with a custom class

To replace the `SyncHandler` with a custom class:

1. Grab the `SyncHandler` object from the filter: `add_filter( 'digitalriver.sync_handler', 'filter_method' )`
2. The `SKURequest` object will be passed as the first argument to `filter_method()`.
3. Swap out the object if necessary and then return the object.&#x20;

## Product Sync Methods

#### Product Sync class

This class describes the module's entry point.

| Method           | Args, Returns, and Descriptions                                                                                                                                                                                     |
| ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| name             | <p><strong>Arg</strong>: -</p><p><strong>Return</strong>: string</p><p><strong>Description</strong>: Returns the name of the module</p>                                                                             |
| init             | <p><strong>Arg</strong>: -</p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Initializes the module and register necessary hooks</p>                                                          |
| assets           | <p><strong>Arg</strong>: String $page_hook</p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Enqueues the scripts and stylesheets in the <code>tools.php</code></p>                           |
| sync             | <p><strong>Arg</strong>: int $post_id</p><p><strong>Return</strong>: bool</p><p><strong>Description</strong>: Syncs the  product to Digital River and return the status of the sync</p>                             |
| delete           | <p><strong>Arg</strong>: int $post_id</p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Deletes the product from Digital River using <code>ProductSyncHandler</code></p>                      |
| get              | <p><strong>Arg</strong>: int $post_id</p><p><strong>Return</strong>: SKU</p><p><strong>Description</strong>: Fetches the product from <code>digitalriver</code> using <code>ProductSyncHandler</code></p>           |
| sync\_status     | <p><strong>Arg</strong>: -</p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Gets the sync status of the product. Product ID should always be the parent product ID.</p>                      |
| sync\_variations | <p><strong>Arg</strong>: <code>WC_Product</code> $product</p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Syncs all variations for variable product</p>                                     |
| sync\_tool\_box  | <p><strong>Arg</strong>: -</p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Displays the manual product sync toolbox</p>                                                                     |
| sync\_handler    | <p><strong>Arg</strong>: -</p><p><strong>Return</strong>: ProductSyncHandler</p><p><strong>Description</strong>: Returns an instance of the <code>ProductSyncHandler</code> from the <code>SyncContainer</code></p> |

#### Sync Container class

This class defines all the services required for this module.

| Method           | Args, Returns, and Descriptions                                                                                                                                                                                                   |
| ---------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| \_\_construct    | <p><strong>Arg</strong>: <code>PimpleContainer</code></p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Accepts a Dependency Injection container as an argument and assigns it to a container attribute</p> |
| define\_services | <p><strong>Arg</strong>: -</p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Defines all the classes present within the module</p>                                                                          |

#### Sync Meta Box class

This class adds the metabox to the **Product Edit** screen and contains a button to trigger the product sync action.

| Method   | Args, Returns, and Descriptions                                                                                                                                                            |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| init     | <p><strong>Arg</strong>: -</p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Initializes the object and registers the necessary hooks for displaying the metabox</p> |
| assets   | <p><strong>Arg</strong>: String $page_hook</p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Enqueues the scripts and stylesheets in the <code>tools.php</code></p>  |
| add      | <p><strong>Arg</strong>: -</p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Adds the metabox to the product edit page and triggers the render callback</p>          |
| callback | <p><strong>Arg</strong>: -</p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Displays the metabox contents with the render callback</p>                              |

#### Sync Handler class

This class handles the actual sync process between WooCommerce and Digital River.

| Method       | Args, Returns, and Descriptions                                                                                                                                                                                                                                                                                                                      |
| ------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| init         | <p><strong>Arg</strong>: <code>ApiInstance</code> $api_instance, <code>SkuRequest</code> $sku_request, <code>MetaFields</code> $meta_handler</p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Constructs the object by passing its dependencies</p>                                                                           |
| upsert       | <p><strong>Arg</strong>: -</p><p><strong>Return</strong>: bool</p><p><strong>Description</strong>: Uses the <code>ApiInstance</code> to insert or update the <code>$product</code> to Digital River. Returns the status of the sync operation.</p>                                                                                                   |
| delete       | <p><strong>Arg</strong>: -</p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Uses the <code>ApiInstance</code> to delete the <code>$product</code> from Digital River</p>                                                                                                                                                      |
| get          | <p><strong>Arg</strong>: -</p><p><strong>Return</strong>: SKU</p><p><strong>Description</strong>: Uses the <code>ApiInstance</code> to get the SKU from Digital River</p>                                                                                                                                                                            |
| product      | <p><strong>Arg</strong>: <code>WC_Product</code>$product</p><p><strong>Return</strong>: <code>ProductSyncHandler</code></p><p><strong>Description</strong>: Sets the product to sync and returns the SyncHandler object and is useful for chaining methods</p>                                                                                       |
| sku\_request | <p><strong>Arg</strong>: -</p><p><strong>Return</strong>: SKURequest/null</p><p><strong>Description</strong>: Prepares the <code>SKURequest</code> model and sets necessary fields (ECCN, Tax code, Country of origin, HS Code) from the <code>$product</code> meta fields and returns the request. Returns <code>null</code> if data is invalid</p> |

#### Endpoint/Sync class

This class exposes the `/digitalriver/v1/sync` endpoint and syncs products to Digital River when a request is sent to that endpoint.

| Method         | Args, Returns, and Descriptions                                                                                                                                                                                      |
| -------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| \_\_construct  | <p><strong>Arg</strong>: <code>ProductSync</code> $sync_obj<code>Cursor</code> $cursor</p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Constructs the object by passing its dependencies</p> |
| init           | <p><strong>Arg</strong>: -</p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Makes a call to the <code>register()</code>  method on <code>rest_api_init</code></p>                             |
| register       | <p><strong>Arg</strong>: -</p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Registers the <code>/digitalriver/v1/sync</code> endpoint and defines the callback</p>                            |
| sync\_products | <p><strong>Arg</strong>: <code>WP_REST_Request</code></p><p><strong>Return</strong>: <code>WP_REST_Response</code></p><p><strong>Description</strong>: Initiates the product sync with the REST route callback</p>   |
