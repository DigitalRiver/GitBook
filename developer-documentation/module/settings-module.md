---
description: Learn more about the Settings module.
---

# Settings module

The `Settings` module registers the plugin settings. To access the settings, select **WooCommerce**, select **Settings**, select **Payments**, then select **Digital River**.

## Settings&#x20;

The following fields are registered by the module:

| Field Name            | Description                                                                                                                                                                                   |
| --------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Enable/Disable        | Enables or disables the Digital River's payment gateway                                                                                                                                       |
| Title                 | Title for the Digital River payment gateway. This would be visible on the **Checkout** page.                                                                                                  |
| Description           | Description of the payment gateway. This would be visible on the **Checkout** page.                                                                                                           |
| Test Mode             | If active, use test credentials from Digital River.                                                                                                                                           |
| Debug Mode            | Logs API calls and exceptions. Logged information is available.                                                                                                                               |
| Automatic fulfillment | This determines whether to fulfill the orders automatically. This calls for the Digital River fulfillment API to initiate fulfillment. Currently, only third-party fulfillment is considered. |
| Test public key       | Test account's API public key                                                                                                                                                                 |
| Test confidential key | Test account's API secret key                                                                                                                                                                 |
| Live public key       | Production account's API public key                                                                                                                                                           |
| Live confidential key | Production account's API secret key                                                                                                                                                           |
| Webhook secret key    | Found in the Digital River [Dashboard's Webhook](https://docs.digitalriver.com/digital-river-api/administration/dashboard/developers/webhooks) section                                        |

### Settings Interface

The `Settings` module implements the following interface:&#x20;

```php
namespace DigitalRiver\WooCommerce\Interfaces\Modules;

/**
 * Interface Settings.
 *
 * @package DigitalRiver\WooCommerce\Modules
 */
interface Settings {

    /**
     * Registers a new settings field.
     *
     * @param SettingsFieldModel $field Setting field object.
     *
     * @return void
     */
    public function register( SettingsFieldModel $field ): void;

    /**
     * Get settings value by key.
     *
     * @param string $key Settings key.
     *
     * @return Mixed
     */
    public function get( string $key );
}
```

**Method Description**

| Method   | Args, Returns, and Descriptions                                                                                                                                                                  |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| register | <p><strong>Arg</strong>:<code>SettingsFieldModel</code></p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Registers the new settings to be added in the Settings panel</p> |
| get      | <p><strong>Arg</strong>: string $key (Field Key)</p><p><strong>Return</strong>: mixed</p><p><strong>Description</strong>: Returns the value for any registered setting</p>                       |

**Settings class**

This class takes care of accessing the setting fields and their values.

| Method                     | Args, Returns, and Descriptions                                                                                                                                                                                                                     |
| -------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| name                       | <p><strong>Arg</strong>: - </p><p><strong>Return</strong>: string</p><p><strong>Description</strong>: Returns the name of the module</p>                                                                                                            |
| init                       | <p><strong>Arg</strong>: - </p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Initializes the module</p>                                                                                                                      |
| register                   | <p><strong>Arg</strong>: <code>SettingsFieldModel</code></p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Receives a <code>SettingsFieldModel</code> object and stores it in the <code>$fields</code> private array</p>      |
| register\_settings\_fields | <p><strong>Arg</strong>: -</p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Loops through all the settings fields data, construct <code>SettingsFieldModel</code> object and call <code>register()</code> method on them</p> |
| add\_gateway\_class        | <p><strong>Arg</strong>: array</p><p><strong>Return</strong>: array</p><p><strong>Description</strong>: Adds the Digital River gateway to the list of supported payment gateways</p>                                                                |
| get\_settings              | <p><strong>Arg</strong>: -</p><p><strong>Return</strong>: array</p><p><strong>Description</strong>: Returns an array of settings fields and their details</p>                                                                                       |
| get                        | <p><strong>Arg</strong>: String</p><p><strong>Return</strong>: array</p><p><strong>Description</strong>: Gets a setting's value using the <code>Settings</code> key</p>                                                                             |

**Settings Container class**

This class defines all the services required for `Settings` module.

| Method          | Args, Returns, and Descriptions                                                                                                                                                                |
| --------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| enabled         | <p><strong>Arg</strong>: - </p><p><strong>Return</strong>: bool</p><p><strong>Description</strong>: Returns <code>true</code> if the plugin is enabled, else <code>false</code></p>            |
| logging         | <p><strong>Arg</strong>: - </p><p><strong>Return</strong>: bool</p><p><strong>Description</strong>: Returns <code>true</code> if logging is enabled, else <code>false</code></p>               |
| webhook\_secret | <p><strong>Arg</strong>: - </p><p><strong>Return</strong>: String</p><p><strong>Description</strong>: Returns the webhook secret key string</p>                                                |
| api\_keys       | <p><strong>Arg</strong>: - </p><p><strong>Return</strong>: array</p><p><strong>Description</strong>: Returns an array containing the two keys, <code>public</code> and <code>secret</code></p> |

**Settings Field Model class**

This class represents actual fields on the Settings page.

| Method           | Args, Returns, and Descriptions                                                                                                                                                                                                                                  |
| ---------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| \_\_construct    | <p><strong>Arg</strong>: array $data</p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Initializes the field and throws <code>InvalidArgumentException</code> if both <code>id</code> and <code>type</code> attributes are not present</p> |
| get\_id          | <p><strong>Arg</strong>: -</p><p><strong>Return</strong>: String</p><p><strong>Description</strong>: Returns the field <code>id</code></p>                                                                                                                       |
| get\_type        | <p><strong>Arg</strong>: -</p><p><strong>Return</strong>: String</p><p><strong>Description</strong>: Returns the field <code>type</code></p>                                                                                                                     |
| get\_title       | <p><strong>Arg</strong>: -</p><p><strong>Return</strong>: String</p><p><strong>Description</strong>: Returns the field <code>title</code></p>                                                                                                                    |
| get\_description | <p><strong>Arg</strong>: -</p><p><strong>Return</strong>: String</p><p><strong>Description</strong>: Returns the field <code>description</code></p>                                                                                                              |
| get\_desc\_tip   | <p><strong>Arg</strong>: -</p><p><strong>Return</strong>: String</p><p><strong>Description</strong>: Returns the field <code>desc_tip_</code></p>                                                                                                                |
| get\_default     | <p><strong>Arg</strong>: -</p><p><strong>Return</strong>: String</p><p><strong>Description</strong>: Returns the field <code>default</code></p>                                                                                                                  |
| get\_label       | <p><strong>Arg</strong>: -</p><p><strong>Return</strong>: String</p><p><strong>Description</strong>: Returns the field <code>label</code></p>                                                                                                                    |

**Gateway class**

This class registers the Digital River payment gateway.

| Method                                | Args, Returns, and Descriptions                                                                                                                                                                                        |
| ------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| \_\_construct                         | <p><strong>Arg</strong>: -</p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Configures the payment gateway and calls <code>init_form_fields()</code></p>                                        |
| init\_form\_fields                    | <p><strong>Arg</strong>: -</p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Calls <code>Settings::get_settings()</code> and sets the value to <code>form_fields</code> attribute</p>            |
| assets                                | <p><strong>Arg</strong>: String $pagehook</p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Loads the relevant scripts and stylesheets</p>                                                       |
| generate\_dr\_test\_config\_btn\_html | <p><strong>Arg</strong>: $key, array $value</p><p><strong>Return</strong>: String</p><p><strong>Description</strong>: Generates test connector button HTML. This function will be called by WooCommerce internally</p> |
| get\_tooltip\_html                    | <p><strong>Arg</strong>: array $data</p><p><strong>Return</strong>: String</p><p><strong>Description</strong>: Generates the tooltip HTML based on the data passed as the argument</p>                                 |
