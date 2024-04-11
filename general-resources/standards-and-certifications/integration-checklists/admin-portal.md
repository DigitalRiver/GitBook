---
description: Learn more about the standards related to the admin portal.
---

# Admin portal

The [checklist items](admin-portal.md#integration-checklist) and [standards](admin-portal.md#integration-standards) in this section relate to the admin portal you must provide with your integrated tool. Using this portal, you should be able to configure the API keys for every client instance. During each [end site implementation](../certification-process.md#end-site-implementations), you use this portal to set the client-specific API keys, as well as perform other configurations.

## Integration checklist <a href="#integration-checklist" id="integration-checklist"></a>

Click any checklist item to be provided more detail on how to meet the integration standard.

* [ ] ​[Do you provide an admin portal to configure secret and public Digital River API keys?​](admin-portal.md#configuring-secret-and-public-digital-river-api-keys)
* [ ] [Do you provide an admin portal to configure a single, default ship from address?](admin-portal.md#configuring-a-single-default-ship-from-address)

## Integration standards

These integration standards relate to building an admin interface:

### Configuring public and confidential keys <a href="#configuring-secret-and-public-digital-river-api-keys" id="configuring-secret-and-public-digital-river-api-keys"></a>

You must provide a utility in your platform's admin backend portal that can assign [public and confidential API keys](../../../developer-resources/api-structure.md#public-keys). These keys then determine which Digital River account is used within the store. Each store must be given its own set of public and confidential keys.

### Configuring a single, default ship from address <a href="#configuring-a-single-default-ship-from-address" id="configuring-a-single-default-ship-from-address"></a>

You must provide a utility in your platform's admin backend portal that can assign a default [ship from address](../../../integration-options/checkouts/creating-checkouts/providing-address-information.md#ship-from-address). The default address might represent, for example, the designated warehouse of the storefront. Each client can have more than one ship from address. However, only one should be designated as the default.

Digital River uses the default address you provide to [calculate regional and localized taxes](../../../integration-options/checkouts/creating-checkouts/tax-calculations.md), [fees](../../../product-management/regulatory-fees/), and regulations during the checkout process.‌

## API interfaces <a href="#api-interfaces" id="api-interfaces"></a>

| Documentation                                                                                 | Direct API                                                                                                            | PHP SDK                                                                                                                  |
| --------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------ |
| [​Country specs​](../../../integration-options/checkouts/creating-checkouts/country-specs.md) | ​[Country specifications](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Country-specifications)​ | ​[CountrySpecification](https://github.com/DigitalRiver/digital-river-php/blob/main/docs/Model/CountrySpecification.md)​ |
