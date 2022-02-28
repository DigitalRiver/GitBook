---
description: Learn how to use modules.
---

# Modules

### Core modules

A module is a piece of program in a plugin that performs a particular task, or it can function with other modules. The WooCommerce plugin has seven core modules:&#x20;

* [`Logger`](api-logger-module.md) module
* [`OrderManagement` ](ordermanagement-module.md)module
* [`ProductCheckout`](productcheckout-module.md) module
* [`ProductMetaFields`](productmetafields-module.md) module
* [`ProductSync`](productsync-module.md) module
* [`Settings`](settings-module.md) module
* [`TaxCalculation`](taxcalculation-module.md) module

A module is a piece of program in a plugin that performs a particular task, or it can function with other modules.

### Module interface

The module interface is for any module that needs to be registered with the plugin. Custom modules need to implement this interface for registration.

{% tabs %}
{% tab title="PHP" %}
```php
interface Module {
    /**
     * Initialization of module.
     *
     * @return void
     */
    public function init(): void;

    /**
     * Return module name.
     *
     * @return string
     */
    public function name(): string;
}
```
{% endtab %}
{% endtabs %}

### **Method description**

*   **$module->name()**: This method needs to return module name.&#x20;

    The module name can be alphanumeric without spaces. Dashes and underscores are allowed.
*   **$module->init()**: Any actual work or initialization activity related to the module should go inside this method.&#x20;

    **Example**: You can add any hooks or call necessary functions/methods inside `init` to run the module. &#x20;

{% hint style="info" %}
Do not explicitly call the `init` method. The plugin calls the`init` method during module activation (under the hood).&#x20;
{% endhint %}

### **Register the custom module**

To register the custom module:

1. Create the main module class that either implements the `Module` interface or extends the `BaseModule` abstract class. Since most of the modules will only be functioning when you enable the Digital River payment gateway, it makes sense to extend the `BaseModule` class.  &#x20;
2. Add the module name by returning the `name` method to the `Plugin::$active_modules` list.
