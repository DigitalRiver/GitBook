---
description: Learn more about the Product Checkout module.
---

# Product Checkout module

The `ProductCheckout` module handles syncing data to the Digital River platform during the whole checkout process.&#x20;

### Specifications

This module is responsible for calculating the tax based on shipping address if available, or billing address if the shipping address is not available.

This module contains a Drop-in integration provided by Digital River for the checkout process. This includes legal content that is fetched from Digital River.js.

Customer checkouts can process from the US or from outside the US. If you will have customers with shipping addresses to the US, add a file uploader on the **Checkout** page for uploading tax certificates. If you will have customers with shipping addresses outside of the US, add a text field for adding the tax ID for the customer.

### Pass the tax certificate

Complete the following tasks to pass the tax certificate.

1. After order placement, pass the tax certificate to Digital River for verifications. Based on the verification, buyers will be notified whether or not their tax exemption certificate is valid.
2. For the **Input field tax ID**, verify the tax ID during order placement.
3. On the `My Account` page, create a section under the **Account** page for tax certificate verification. The buyer will see their tax certificate status.&#x20;
4. Create a Drop-in payment gateway for rendering payment options on the checkout page. The buyer will select the payment options, complete the necessary fields, and process the payment.
5. After successful payment, pass all order instance data with customer data to Digital River API via the Drop-in gateway.&#x20;
6. Add a **Save payment** option for the Drop-in gateway to allow buyers to save their payment data for future purchases. Customers can process payments via **Save Cards**.&#x20;
7. Add the **Save payment** option on the **My Account** page so that customers can manage (add, update, remove, and save) their card and save payment options.

{% hint style="info" %}
Hide others' default gateway from the customer checkout end when the Digital River gateway is enabled. Show a message in **Admin Payment** tab settings that other gateways are not showing either they are enabled.
{% endhint %}

### Naming Conventions

For naming conventions:

1. On the **Checkout** page, add two fields depending on customer billing or shipping country chosen.
   * **Tax Certificate**
     * **Type**: File field
     * **Description**: Enter your tax certificate&#x20;
     * **id/key**: `dr_customer_tax_certificate`
     * **Condition**: Showing only if Shipping country is in the  US
   * **Tax ID**&#x20;
     * **Type**: number fields
     * **Description**: Enter your tax id number&#x20;
     * **id/key**: `dr_customer_tax_id_number`
     * **Condition**: Showing only if shipping country is outside of the US
2. On the **My Account** page, add a tax details section.

### Product Checkout Methods

#### Product Checkout class

The class describes the module's entry point.

| Method                  | Args, Return, and Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| ----------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| name                    | <p><strong>Args</strong>: -</p><p><strong>Return</strong>: string</p><p><strong>Description</strong>: Returns the name of the module</p>                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| \_\_construct           | <p><strong>Args</strong>: CheckoutContainer $container,<br><strong>Path</strong>: Settings $settings</p><p>/src/Modules/ProductCheckout/CheckoutContainer.php<br><br><strong>Args:</strong> TaxExemption $tax_exemption<br><strong>Path</strong>: /src/Modules/ProductCheckout/TaxExemption.php<br><br><strong>Args:</strong> CustomerMyAccount $customer_myaccount<br><strong>Path</strong>: /src/Modules/ProductCheckout/CustomerMyAccount.php<br></p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Initializes the object by passing in dependencies</p> |
| init                    | <p><strong>Args:</strong> -<br><strong>Return</strong>: void</p><p><strong>Description</strong>: Initializes the module, register necessary hooks, and call certain methods to complete the setup</p>                                                                                                                                                                                                                                                                                                                                                                              |
| render\_gateway\_class  | <p><strong>Args</strong>: array $gateways</p><p><strong>Return</strong>: array</p><p><strong>Description</strong>: Adds the DropIn class to the list of gateways</p>                                                                                                                                                                                                                                                                                                                                                                                                               |
| hide\_default\_gateways | <p><strong>Args</strong>: array $gateways</p><p><strong>Return</strong>: array</p><p><strong>Description</strong>: Remove all gateways other than Digital River if the plugin is enabled.</p>                                                                                                                                                                                                                                                                                                                                                                                      |
| show\_gateway\_message  | <p><strong>Args</strong>: -</p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Displays a message on the payment gateway settings page that if the Digital River gateway is activated, other payment methods will be hidden from checkout.</p>                                                                                                                                                                                                                                                                                                                |
| add\_to\_cart\_redirect | <p><strong>Args</strong>: String $url, int $product_id</p><p><strong>Return</strong>: String</p><p><strong>Description</strong>: Returns add to cart redirect URL</p>                                                                                                                                                                                                                                                                                                                                                                                                              |

#### Drop-in class

This gateway class will be added to the list of supported payment gateways from the `ProductCheckout` class.

| Method           | Args, Return, and Description                                                                                                                                                                                                                     |
| ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| \_\_construct    | <p><strong>Args</strong>: -</p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Constructs the object</p>                                                                                                                     |
| init             | <p><strong>Args</strong>: -</p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Sets Payment gateway title, description, and enqueue payment scripts by calling the <code>payment_scripts()</code> method</p>                 |
| payment\_scripts | <p><strong>Args</strong>: -</p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Enqueue necessary scripts on the <code>Cart</code> and <code>Checkout</code> page only if the plugin is enabled and the API keys are set.</p> |
| payment\_fields  | <p><strong>Args</strong>: -</p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Render the payment fields</p>                                                                                                                 |
| process\_payment | <p><strong>Args</strong>: int $order_id</p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Processes the order after final payment</p>                                                                                       |

#### Tax Exemption class

This class adds `Tax exemption` fields to the `Checkout` page.

| Method                 | Args and Return                                                                                      |
| ---------------------- | ---------------------------------------------------------------------------------------------------- |
| \_\_construct          | <p><strong>Args</strong>: <code>File</code> $file_dr_handler</p><p><strong>Return</strong>: void</p> |
| init                   | <p><strong>Args</strong>: -</p><p><strong>Return</strong>: void</p>                                  |
| tax\_identifier\_types | <p><strong>Args</strong>: String $country</p><p><strong>Return</strong>: array</p>                   |
| tax\_authority\_data   | <p><strong>Args</strong>: -</p><p><strong>Return</strong>: array</p>                                 |
| assets                 | <p><strong>Args</strong>: -</p><p><strong>Return</strong>: void</p>                                  |

#### Customer My Account class

This class handles adding a new subpage to the user's **** `My Account` page where the payment sources of a user can be viewed.&#x20;

| Method                   | Args, Return, and Description                                                                                                                                                                                                                                                                                  |
| ------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| \_\_construct            | <p><strong>Args</strong>: <code>Settings</code> $settings<code>CustomerHandler</code> $customer_handler<code>TaxExemption</code> $tax_exemption<code>File</code> $file_dr_handler</p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Constructs the object by passing in dependencies</p> |
| init                     | <p><strong>Args</strong>: -</p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Registers necessary hooks</p>                                                                                                                                                                              |
| add\_myaccount\_endpoint | <p><strong>Args</strong>: -</p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Adds a new rewrite endpoint <code>/dr-payments</code></p>                                                                                                                                                  |
| add\_query\_vars         | <p><strong>Args</strong>: array</p><p><strong>Return</strong>: array</p><p><strong>Description</strong>: Adds the <code>dr-payments</code> to the list of query variables</p>                                                                                                                                  |
| myaccount\_scripts       | <p><strong>Args</strong>: -</p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Load scripts only on the <code>My Account</code> page if the plugin is enabled and API Keys are set</p>                                                                                                    |
| endpoint\_title          | <p><strong>Args</strong>: String $title</p><p><strong>Return</strong>: String</p><p><strong>Description</strong>: Sets the title for the <code>My Account</code> page and subpages</p>                                                                                                                         |
| dr\_payment\_link        | <p><strong>Args</strong>: array $menu_links</p><p><strong>Return</strong>: array</p><p><strong>Description</strong>: Adds a new link <code>'Tax and Payments'</code> to the My Account menu links (<code>$menu_links</code>) and returns the array</p>                                                         |
| dr\_payment\_content     | <p><strong>Args</strong>: -</p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Renders content callback for when the link <code>/dr-payments</code> is visited</p>                                                                                                                        |
| get\_sources             | <p><strong>Args</strong>: <code>Customer</code> $dr_customer</p><p><strong>Return</strong>: array</p><p><strong>Description</strong>: Returns an array containing the payment sources of the customer with the default source placed as the first element</p>                                                  |
| handle\_payment\_methods | <p><strong>Args</strong>: -</p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Handles payment method operations</p>                                                                                                                                                                      |
| create\_customer\_source | <p><strong>Args</strong>: -</p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Gets <code>customer_id</code> and <code>source_id</code> from the <code>$_POST</code> data and attach the source to the customer for future use</p>                                                        |

#### Customer Handler class

This class creates required data for a customer by using the Customer Digital River Handler class.

| Method                               | Args, Returns, and Descriptions                                                                                                                                                                                                                                                                                                                                         |
| ------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| \_\_construct                        | <p><strong>Arg</strong>: <code>TaxExemption</code> $tax_exemption, <code>Customer</code> $customer_dr_handler, <code>CheckoutUtils</code> $checkout_utils</p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Constructs the object by passing in dependencies</p>                                                                                  |
| create\_dr\_customer\_from\_postdata | <p><strong>Arg</strong>: -</p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Creates customer on Digital River from parsed post data sent by WooCommerce</p>                                                                                                                                                                                      |
| create\_dr\_customer                 | <p><strong>Arg</strong>: array $data</p><p><strong>Return</strong>: Customer</p><p><strong>Description</strong>: Creates customer on Digital River from parameters. Returns the<code>Customer</code> object and throws Exception if the data is invalid</p>                                                                                                             |
| fetch\_dr\_customer                  | <p><strong>Arg</strong>: string $id</p><p><strong>Return</strong>: Customer</p><p><strong>Description</strong>: Fetches customer from Digital River</p><p>Returns Customer object and throws Exception if the data is invalid</p>                                                                                                                                       |
| create\_dr\_customer\_source         | <p><strong>Arg</strong>: string $source_id</p><p><strong>Return</strong>: Source</p><p><strong>Description</strong>: Creates customer source on Digital River. Returns the <code>Source</code> if API is successful, throws Exception if the data is invalid</p>                                                                                                        |
| compare\_customer\_data              | <p><strong>Arg</strong>: array $data</p><p><strong>Return</strong>: <code>Customer/null</code></p><p><strong>Description</strong>: Compares customer data to check whether the customer needs an update. Returns the <code>Customer</code> object if it needs an update or is <code>null</code></p>                                                                     |
| dr\_customer\_object                 | <p><strong>Arg</strong>: String $action, <code>Customer</code> $customer</p><p><strong>Return</strong>: Customer/null</p><p><strong>Description</strong>: Gets, saves, and deletes the Digital River customer object from the <code>usermeta/wc</code> session based on the user login status. Returns retrieved <code>Customer</code> object, or <code>null</code></p> |

#### Checkout Handler class

This class creates required data for checkout by using the Checkout Digital River Handler class.

| Method                                           | Args, Returns, and Descriptions                                                                                                                                                                                                                                                                                                          |
| ------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| \_\_construct                                    | <p><strong>Args</strong>:</p><p><code>CustomerHandler</code> $customer_handler, <code>TaxExemption</code> $tax_exemption, <code>Source</code> $source_dr_handler, <code>CheckoutUtils</code> $checkout_utils</p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Construct the object by passing in dependencies</p> |
| init                                             | <p><strong>Arg:</strong> -<br><strong>Return</strong>: void</p><p><strong>Description</strong>: Register necessary hooks</p>                                                                                                                                                                                                             |
| render\_checkout\_submit                         | <p><strong>Arg:</strong> -</p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Adds tax exemption fields on the checkout page</p>                                                                                                                                                                                    |
| render\_customer\_type\_option                   | <p><strong>Arg:</strong> -</p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Appends customer type option in checkout billing fields</p>                                                                                                                                                                           |
| woocommerce\_cart\_shipping\_method\_full\_label | <p><strong>Arg</strong>: string $label, <code>WC_Shipping_Rate</code> $method</p><p><strong>Return</strong>: String</p><p><strong>Description</strong>: Callback for woocommerce_cart_shipping_method_full_label filter used to display the tax information</p>                                                                          |
| update\_wc\_order\_data                          | <p><strong>Arg</strong>: <code>WC_Order</code> $order</p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Modifies WooCommerce order data and save according to Digital River checkout</p>                                                                                                                           |
| replace\_wc\_order\_details                      | <p><strong>Arg</strong>: array $total_rows, <code>WC_Order</code> $order, String $tax_display</p><p><strong>Return</strong>: array</p><p>Description: Shows Digital River checkout total on order details</p>                                                                                                                            |
| dr\_product\_subtotal                            | <p><strong>Arg</strong>: String $subtotal, Object $item, <code>WC_Order</code> $order</p><p><strong>Return</strong>: String</p><p><strong>Description</strong>: Shows the item total according to <code>digitalriver</code> checkout</p>                                                                                                 |
| validate\_order\_data                            | <p><strong>Arg</strong>: $default_value</p><p><strong>Return</strong>: mixed</p><p><strong>Description</strong>: Filters before creating Woocommerce order. Checks whether checkout object is stored in session and contains the <strong></strong> source and customer ID</p>                                                            |
| replace\_checkout\_order\_review\_template       | <p><strong>Arg</strong>: array $fragments</p><p><strong>Return</strong>: array</p><p><strong>Description</strong>: Modifies order review table HTML contents to show Digital River's calculated taxes</p>                                                                                                                                |
| assets                                           | <p><strong>Arg:</strong> -</p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Enqueues the necessary scripts and stylesheets</p>                                                                                                                                                                                    |
| process\_checkout                                | <p><strong>Arg:</strong> -</p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Processes checkout, creates customer and returns calculated tax</p>                                                                                                                                                                   |
| handle\_update\_checkout\_with\_payment\_source  | <p><strong>Arg:</strong> -</p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Handles update checkout with payment source identifier ajax request</p>                                                                                                                                                               |
| handle\_update\_source\_checkout                 | <p><strong>Arg:</strong> -</p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Updates checkout with source ID if the billing address has changed</p>                                                                                                                                                                |
| handle\_checkout\_get\_payment\_session\_id      | <p><strong>Arg:</strong> -</p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Handles get checkout payment session ID ajax request</p>                                                                                                                                                                              |
| include\_templates                               | <p><strong>Arg:</strong> -</p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Includes WordPress templates in the footer</p>                                                                                                                                                                                        |

#### Compliance class

This class responsible for displaying the legal information from Digital River on the **Cart**, **Checkout**, and **Thank You** pages in WooCommerce.

{% hint style="info" %}
&#x20;Only the `_construct` method for this class has an arg.
{% endhint %}

| Method                     | Returns and Descriptions                                                                                                                                   |
| -------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| \_\_construct              | <p><strong>Return</strong>: void</p><p><strong>Description</strong>: Construct the object by passing in dependencies</p>                                   |
| init                       | <p><strong>Return</strong>: void</p><p><strong>Description</strong>: Registers necessary hooks</p>                                                         |
| assets                     | <p><strong>Return</strong>: void</p><p><strong>Description</strong>: Loads compliance scripts and stylesheets for rendering legal content on the store</p> |
| show\_compliance           | <p><strong>Return</strong>: void</p><p><strong>Description</strong>: Renders Digital River compliance message</p>                                          |
| prepare\_checkout\_request | <p><strong>Return</strong>: array</p><p><strong>Description</strong>: Prepares request data for checkout</p>                                               |

#### Digital River Handlers/checkout class

| Method | Args, Returns, and Descriptions                                                                                                                                                                                                                                                                             |
| ------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| get    | <p><strong>Args</strong>: string $checkout_id</p><p><strong>Return</strong>: <code>Checkout</code></p><p><strong>Description</strong>: Retrieves a checkout API call to Digital River, returns the <code>Checkout</code> object on success throws Exception for invalid data, or if API throws an error</p> |
| update | <p><strong>Args</strong>: array $data</p><p><strong>Return</strong>: <code>Checkout</code></p><p><strong>Description</strong>: Updates a checkout API call to Digital River and returns <code>Checkout</code> object on success throws Exception for invalid data, or if API throws an error</p>            |
| delete | <p><strong>Args</strong>: Checkout $checkout</p><p><strong>Return</strong>: <code>Checkout</code></p><p><strong>Description</strong>: Deletes a checkout API call to Digital River and returns <code>Checkout</code> object on success throws Exception for invalid data, or if API throws an error</p>     |

#### Digital River Handlers\Customer class

| Method                | Args, Returns, and Descriptions                                                                                                                                                                                                                                                                                                                           |
| --------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| get                   | <p><strong>Args</strong>: string $checkout_id</p><p><strong>Return</strong>: <code>Customer</code></p><p><strong>Description</strong>: Retrieves a  customer API call to Digital River, returns <code>Customer</code> object on success throws Exception for invalid data, or if the API throws an error.</p>                                             |
| create                | <p><strong>Args</strong>: array $data</p><p><strong>Return</strong>: <code>Customer</code></p><p><strong>Description</strong>: Creates a customer API call to Digital River and returns the<code>Customer</code> object on success throws Exception for invalid data, or if the API throws an error.</p>                                                  |
| update                | <p><strong>Args</strong>: array $data</p><p><strong>Return</strong>: <code>Customer</code></p><p><strong>Description</strong>: Updates a customer API call to Digital River, returns <code>Customer</code> object on success throws Exception for invalid data or if the API throws an error</p>                                                          |
| delete                | <p><strong>Args</strong>: string $customer_id</p><p><strong>Return</strong>: <code>Customer</code></p><p><strong>Description</strong>: Deletes a customer API call to Digital River, returns the deleted <code>Customer</code> object on success throws Exception for invalid data, or if the API throws an error.</p>                                    |
| create\_source        | <p><strong>Args</strong>: string $customer_id, string $customer_id</p><p><strong>Return</strong>: <code>Source</code></p><p><strong>Description</strong>: Creates a Customer Source API call to Digital River, returns <code>Source</code> object if API is successful, throws Exception for invalid data, or if the API throws an error.</p>             |
| delete\_source        | <p><strong>Args</strong>: string $customer_id, string $customer_id</p><p><strong>Return</strong>: <code>Source</code></p><p><strong>Description</strong>: Deletes a Customer Source API call to Digital River, returns the deleted <code>Source</code> object if API is successful, throws Exception for invalid data, or if the API throws an error.</p> |
| get\_tax\_certificate | <p><strong>Args</strong>: array $data</p><p><strong>Return</strong>: <code>TaxCertificate/</code>null</p><p><strong>Description</strong>: Retrieves tax certificate data from the data array and returns new <code>TaxCertificate</code> object</p>                                                                                                       |

#### Digital River Handlers\File class

| Method             | Args, Returns, and Descriptions                                                                                                                                                                                                                                                                      |
| ------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| create             | <p><strong>Args</strong>: String $file, String $purpose</p><p><strong>Return</strong>: <code>File</code></p><p><strong>Description</strong>: Creates a <code>File</code> API call to Digital River platform and returns <code>File</code> object if API is successful or throws an Exception</p>     |
| get                | <p><strong>Args</strong>: String $file</p><p><strong>Return</strong>: <code>File</code></p><p><strong>Description</strong>: Retrieves File API call to Digital River and returns <code>File</code> object on success throws Exception for invalid data, or if the API throws an error. </p>          |
| delete             | <p><strong>Args</strong>: String $file</p><p><strong>Return</strong>: <code>File</code></p><p><strong>Description</strong>: Deletes File API call to Digital River and returns the deleted <code>File</code> object on success throws Exception for invalid data, or if the API throws an error.</p> |
| create\_file\_link | <p><strong>Args</strong>: String $file</p><p><strong>Return</strong>: <code>File</code></p><p><strong>Description</strong>: Creates file link for file object for download and view and returns a <code>FileLink</code> object if API is successful, else <code>false</code>.</p>                    |

#### Digital River Handlers\Source class

| Method | Args, Returns, and Descriptions                                                                                                                                                                                                                                                                       |
| ------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| get    | <p><strong>Args</strong>: String $source_id</p><p><strong>Return</strong>: <code>Source</code></p><p><strong>Description</strong>: Makes retrieve Source API call to Digital River and returns <code>Source</code> object on success throws Exception for invalid data or if API throws an error.</p> |

#### Checkout Container class

This class acts as a Dependency Injection container for providing dependencies to classes present in the `ProductCheckout` module.

| Method           | Args, Returns, and Descriptions                                                                                                                                                                                                    |
| ---------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| \_\_construct    | <p><strong>Args</strong>: <code>PimpleContainer</code></p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Accepts a Dependency Injection container as an argument and assigns it to a container attribute</p> |
| define\_services | <p><strong>Args</strong>: -</p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Defines all the classes present within the module</p>                                                                          |
