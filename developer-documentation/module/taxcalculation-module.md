---
description: Learn about the Tax Calculation module.
---

# Tax Calculation module

The `TaxCalculation` module handles calculating taxes on the **Shop**, **Product**, and **Cart** pages and shows the final tax. This module shows taxes based on the WooCommerce backend settings.&#x20;

### Specifications

This module handles the tax calculation for single product and shop products.  It hides the tax class (Standard, Reduce Rate, and Zero Rate) settings in **WooCommerce Tax Settings**.&#x20;

The tax calculation is handled via the Digital River platform.&#x20;

1. Use the customer's shipping address for rendering tax rates for products on the **Shop** and **Single Product** page.&#x20;
2. Hide the tax row from the **Cart** page to finalize the tax rate review on the **Checkout** page.&#x20;
3. After all the details are on the **Checkout** page, click **Review Order** on the [Drop-in UI](https://docs.digitalriver.com/digital-river-api/payment-integrations-1/drop-in).&#x20;

Tax exclusive or inclusive from price depends on **Admin tax** settings. Use those settings to display the tax is inclusive or exclusive from the product price on the **Single product** page and **Shop** page.

### Tax Calculation Methods

#### Tax Calculation class

This class is the module's entry point.

| Method         | Args, Returns, and Descriptions                                                                                                                                                                                                                      |
| -------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| \_\_construct  | <p><strong>Arg</strong>: <code>ApiInstance</code> $api_instance, <code>OrderContainer</code> $container</p><p><strong>Return</strong>: string</p><p><strong>Description</strong>: Constructs the object by passing its dependencies</p>              |
| name           | <p><strong>Arg</strong>: -</p><p><strong>Return</strong>: string</p><p><strong>Description</strong>: Returns the name of the module</p>                                                                                                              |
| init           | <p><strong>Arg</strong>: -</p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Initializes the module, registers necessary hooks, and initializes <code>[StateManager](/src/Modules/OrderManagement/StateManager.php)</code></p> |
| calculate\_tax | <p><strong>Arg</strong>: -</p><p><strong>Return</strong>: bool</p><p><strong>Description</strong>: Returns a boolean value representing if tax needs to be calculated for the current page</p>                                                       |

#### Tax Calculation Container class

This class acts as a Dependency Injection container for providing dependencies to classes in the `OrderManagement` module.

| Method           | Args, Returns, and Descriptions                                                                                                                                                                                                   |
| ---------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| \_\_construct    | <p><strong>Arg</strong>: <code>PimpleContainer</code></p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Accepts a Dependency Injection container as an argument and assigns it to a container attribute</p> |
| define\_services | <p><strong>Arg</strong>: -</p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Defines all the classes present within the module</p>                                                                          |

#### Product class

This class relates to various products and adds a custom class to the product container and product price element.

| Method                | Args, Returns, and Descriptions                                                                                                                                                                                                                                     |
| --------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| \_\_construct         | <p><strong>Arg</strong>: <code>TaxCalculation</code></p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Accepts <code>TaxCalculation</code> dependency as an argument and assigns it to the <code>tax_handler</code> attribute</p>             |
| init                  | <p><strong>Arg</strong>: -</p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Registers necessary hooks</p>                                                                                                                                    |
| assets                | <p><strong>Arg</strong>: -</p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Enqueues necessary scripts and stylesheets</p>                                                                                                                   |
| product\_classes      | <p><strong>Arg</strong>: array $classes</p><p><strong>Return</strong>: array</p><p><strong>Description</strong>: Adds custom class to the product container</p>                                                                                                     |
| price\_html           | <p><strong>Arg</strong>: string $html, <code>WC_Product</code> $obj</p><p><strong>Return</strong>: string</p><p><strong>Description</strong>: Filters the price HTML markup</p>                                                                                     |
| maybe\_calculate\_tax | <p><strong>Arg</strong>: bool $calculate_tax</p><p><strong>Return</strong>: bool</p><p><strong>Description</strong>: If the customer is from a different country than the store, calculate taxes and return the default value for <code>$calculate_taxes</code></p> |

#### Cart Tax Calculation class

This class handles calculating taxes on the Cart page, shows the final tax, and shows taxes based on the WooCommerce backend settings.

| Method                                           | Args, Returns, and Descriptions                                                                                                                                                                                                                                      |
| ------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| init                                             | <p><strong>Arg</strong>: -</p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Initializes the module and register necessary hooks</p>                                                                                                           |
| assets                                           | <p><strong>Arg</strong>: -</p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Enqueues necessary scripts and stylesheets</p>                                                                                                                    |
| woocommerce\_cart\_subtotal                      | <p><strong>Arg</strong>: float $subtotal, $compound, $cart</p><p><strong>Return</strong>: book</p><p><strong>Descripton:</strong> -</p>                                                                                                                              |
| woocommerce\_cart\_contents\_total               | <p><strong>Arg</strong>: float $total</p><p><strong>Return</strong>: float</p><p><strong>Description</strong>: -</p>                                                                                                                                                 |
| woocommerce\_widget\_cart\_is\_hidden            | <p><strong>Arg</strong>: bool $is_hidden</p><p><strong>Return</strong>: bool</p><p><strong>Description</strong>: Creates checkout, stores it in the WooCommerce session, and returns the <code>$is_hidden</code> parameter</p>                                       |
| woocommerce\_cart\_collaterals                   | <p><strong>Arg</strong>: -</p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Loads the custom template for the cart section</p>                                                                                                                |
| wc\_get\_template                                | <p><strong>Arg</strong>: -</p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Loads the custom template for the cart section if the template name is <code>cart/cart-totals.php</code></p>                                                      |
| woocommerce\_cart\_shipping\_method\_full\_label | <p><strong>Arg</strong>: String $label, <code>WC_Shipping_Rate</code> $method</p><p><strong>Return</strong>: String</p><p><strong>Description</strong>: Loads the custom template for the cart section if the template name is <code>cart/cart-totals.php</code></p> |
| woocommerce\_cart\_item\_price                   | <p><strong>Arg</strong>: String $price, array $cart_item</p><p><strong>Return</strong>: String</p><p><strong>Description</strong>: Alters the price HTML on the <code>Cart</code> page</p>                                                                           |
| woocommerce\_cart\_item\_subtotal                | <p><strong>Arg</strong>: String $subtotal, array $cart_item</p><p><strong>Return</strong>: String</p><p><strong>Description</strong>: Alters the price HTML on the <code>Cart</code> page</p>                                                                        |
| prepare\_cart\_checkout\_request                 | <p><strong>Arg</strong>: -</p><p><strong>Return</strong>: array</p><p><strong>Description</strong>: Prepares request data for checkout</p>                                                                                                                           |
| process\_cart                                    | <p><strong>Arg</strong>: -</p><p><strong>Return</strong>: Checkout</p><p><strong>Description</strong>: Processes the <code>cart update</code> request</p>                                                                                                            |

#### Traits\Tax Calculation Utility trait

The `TaxCalculation` class uses Utility methods.

| Method                         | Args, Returns, and Descriptions                                                                                                                                                                                                                                                                                   |
| ------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| compare\_purchase\_location    | <p><strong>Arg</strong>: <code>PurchaseLocation</code> $location1, <code>PurchaseLocation</code> $location2</p><p><strong>Return</strong>: bool</p><p><strong>Description</strong>: Compares two purchase location data and returns <code>true</code> if they are <code>identical</code> or<code>false</code></p> |
| compare\_ship\_from\_addresses | <p><strong>Arg</strong>: <code>ShipFrom</code> $ship_from1, <code>ShipFrom</code> $ship_from2</p><p><strong>Return</strong>: bool</p><p><strong>Description</strong>: Compares two <code>ShipFrom</code> addresses and returns as <code>true</code> if they are identical or <code>false</code></p>               |

#### Endpoints\Product Price class

This class creates a new REST API Endpoint to fetch the product price.

| Method                  | Args, Returns, and Descriptions                                                                                                                                                                                                                                                   |
| ----------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| \_\_construct           | <p><strong>Arg</strong>: <code>TaxCalculation</code></p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Accepts <code>CheckoutService</code> and <code>Store</code> dependencies as arguments and assigns them to the <code>tax_handler</code> attribute</p> |
| init                    | <p><strong>Arg</strong>: -</p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Registers necessary hooks</p>                                                                                                                                                  |
| add\_price\_filters     | <p><strong>Arg</strong>: -</p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Registers filters related to the price</p>                                                                                                                                     |
| remove\_price\_filters  | <p><strong>Arg</strong>: -</p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Removes registered filters</p>                                                                                                                                                 |
| register                | <p><strong>Arg</strong>: -</p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Registers REST API route</p>                                                                                                                                                   |
| set\_request            | <p><strong>Arg</strong>: mixed $result, <code>WP_REST_Server</code> $server, <code>WP_REST_Request</code> $request</p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Sets request property</p>                                                              |
| fetch\_price            | <p><strong>Arg</strong>: <code>WP_REST_Request</code> $request</p><p><strong>Return</strong>: <code>WP_REST_Response/WP_Error</code></p><p><strong>Description</strong>: Callback to handle API Endpoint</p>                                                                      |
| dr\_price               | <p><strong>Arg</strong>: String $price, <code>WC_Product</code> $product</p><p><strong>Return</strong>: mixed</p><p><strong>Description</strong>: Filters the price</p>                                                                                                           |
| dr\_variation\_prices   | <p><strong>Arg</strong>: array $prices_array, <code>WC_Product</code> $product</p><p><strong>Return</strong>: array</p><p><strong>Description</strong>: Filters variation prices by calculating prices via Digital River</p>                                                      |
| add\_shipping\_choices  | <p><strong>Arg</strong>: array $data, <code>WC_Product</code> $product</p><p><strong>Return</strong>: array</p><p><strong>Description</strong>: Adds shipping choice element to data</p>                                                                                          |
| add\_purchase\_location | <p><strong>Arg</strong>: array $data</p><p><strong>Return</strong>: array</p><p><strong>Description</strong>: Adds purchase location to tax estimate data</p>                                                                                                                     |
| item                    | <p><strong>Arg</strong>: <code>WC_Product</code> $product</p><p><strong>Return</strong>: <code>SKURequestItem</code></p><p><strong>Description</strong>: Prepares a product to send in checkout request</p>                                                                       |
