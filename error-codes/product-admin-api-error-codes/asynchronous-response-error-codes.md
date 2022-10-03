---
description: Understand the asynchronous response error codes for the Product Admin API.
---

# Asynchronous response error codes

## `ANOTHER_REQUEST_IS_UPDATING_ERID`

Another API request is trying to update the same product. This can occur when the Enforce Unique Value is enabled for a product's external reference ID (ERID).

* `Product: The external reference ID [987654321] was requested by another API request : [abcd-1234-5678-agfe-defg]. Enter a different value and try again.`

## `ATTRIBUTE_CANNOT_BE_CHANGED_IN_PRODUCT_VARIATION`

The attribute exists in the product variation, but you cannot change it (for example, `privateStoreOnly`).

* `$Product: Cannot modify the attribute [privateStoreOnly] for a product variation.`

## `ATTRIBUTE_EXCEEDS_MAX_VALUE`

The numeric value exceeded the maximum value allowed.

* `$Product: The value [99999] of [minOrderQuantity] attribute exceeds the maximum value allowed: [999]. Decrease the value and try again.`

## `ATTRIBUTE_FAMILY_FOR_PRODUCT_VARIATION_IS_NOT_CONSISTENT_WITH_BASE_PRODUCT`

The attribute family for the product variation is not consistent with the attribute family for the base product. For example, someone set the `duration` attribute for a subscription in the product variation but did not set a corresponding `duration` attribute in the base product.

* `$Product: The attributes [duration, paymentSchedule] of [Subscription[10]] cannot be set at the variation product level only. You must set the same attributes at the base product level as well.`

## `ATTRIBUTE_FILE_DOES_NOT_EXIST`

One or more URLs for product images (details 1 \~ 5, thumbnail 1 \~ 5) are invalid, or the `custom` attribute is not an image content type. This validation only occurs when you deploy a product.

* `$Product: the file[/test.txt] for [customFile] does not exist. Try uploading the file again.`

## `ATTRIBUTE_FULFILLMENT_TYPE_NOT_ASSIGNED_TO_PRODUCT`

The attribute belongs to a specific fulfillment type that exists in the payload, but the product does not have the corresponding fulfillment type. For example, trying to set the weight for a digital product.

* `$Product: The attributes [downloadFulfillment, applicationFiles] can only be modified if fulfillment type is [Download].`
* `$Product: The attributes [weight, length] can only be modified if fulfillment type is [Physical].`

## ATTRIBUTE\_IMAGE\_DOES\_NOT\_EXIST

The product images (details 1 \~ 5, thumbnail 1 \~ 5) are either not in URL format, do not exist in [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do), or the `custom` attribute is not an image content type. This validation only occurs when you deploy a product.

* `$Product: The image [/aaa.jpg] for [productImage1] does not exist. Try uploading the image again.`

## `ATTRIBUTE_IS_REQUIRED`

The required attributes are invalid in the request  (for example, name, display name, and SKU).

* There is no localization in the payload
* There is at least one localization, but the required attributes are not in it.
* The attributes exist in all locales but values are blank

Additional information:

* `$Product: The attribute name is required and cannot be blank.`

## `ATTRIBUTE_ONLY_ALLOWED_FOR_DEFAULT_LOCALE`

The attribute exists in the non-default locale. You can only change the attribute for the default locale (for example `privateStoreOnly`).

* `$Product: The attribute [privateStoreOnly] can only be modified at default locale [en_US], not the non-default locale [ja_JP].`

## `ATTRIBUTE_VALUE_EXCEEDS_MAX_LENGTH`

The string value for the attribute exceeded the maximum number of characters allowed.

* `$Product: The length of value [11234300...] for the attribute [shortDescription] is [2001] which exceeds the maximum [2000] character length. Reduce the character length and try again.`

The attribute value will be truncated to 300 characters (if longer) and the suffix '...' will be added.

## `BASE_PRODUCT_DOES_NOT_ALLOW_DOWNGRADE`

The target product is a base product, but the payload contains as `downProducts` attribute. You cannot add the `downProducts` attribute (whether the value is empty or not) to a base product.

* `$Product: Downgrade products are not allowed for the base product. Remove the downgrade product (downProducts) from the payload for this product.`

## `BASE_PRODUCT_DOES_NOT_ALLOW_TRANSFER`

The target product is a base product, but the payload contains a `transferProduct` attribute. You cannot add the `transferProduct` attribute (whether the value is empty or not) to a base product.

* `$Product: The base product does not allow transfer products. Remove the transfer product (transferProduct) from the payload for this product.`

## `BASE_PRODUCT_DOES_NOT_ALLOW_UPGRADE`

The target product is a base product, but the payload contains an `upgradeProducts` attribute. You cannot add the `upgradeProducts` attribute (whether the value is empty or not) to a base product.

* `$Product: Upgrade products are not allowed for the base product. Remove the upgrade product (upgradeProducts) from the payload for this product.`

## `CANNOT_ADD_LOCALE`

&#x20;This error occurs when you add more locales in the product variation than the base product. This error also occurs when you add locales that do not exist in the base product to a product variation.

* `$Product: Cannot add new locales [en_GB, jp_JP] to product variation. Add the new locales to base product.`

## `CANNOT_ADD_PRODUCT_FAMILY`&#x20;

You cannot add the product family to the current product in [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do).

{% hint style="info" %}
This is currently not testable because we don't support the product family right now. However, we may add new business logic in the future.
{% endhint %}

* `$Product: Cannot apply option [a-family[family-id]]. Remove the attributes from payload [att1, att2, att3].`

## `CANNOT_ADD_SUBSCRIPTION_ATTRIBUTES_AFTER_DEPLOYMENT`

You cannot add subscription attribute values to a non-subscription product after you deploy that individual product.

* `$Product: cannot change the product to a subscription product once deployed. Remove the subscription attributes from the payload [duration, isFreeTrial].`

## `CANNOT_ADD_SUBSCRIPTON_ATTRIBUTES_WITHOUT_USING_THE_VARYING_ATTRIBUTE`

This error occurs when you set the subscription attribute values without using the varying attribute of subscription to define the variations while creating a base product and product variation. For example, you use `Color` as a varying attribute, but you try to set `paymentSchedule` in the localized payload.

* `$Product: Cannot create a subscription product without the varying attributes [autoRenewalDateBasis, duration, isAutomatic, isDistinctScheduleTurnedOn]. Use one or more of the varying attributes to define variations.`

## `CANNOT_CHANGE_A_LIVE_CHANGE_WITH_AN_UPDATE_REQUEST`

A live change cannot exist in an update-product or update-variation request. An empty `liveChanges`object will not trigger this error. There must be at least one child field under `liveChanges`.

* For a product variation:
  * `Cannot update live changes from /products/{base_product_id}/variation/{variation_product_id}, try updating it from /products/{base_product_id}/variation/{variation_product_id}/live-changes.`
* For an individual or base product:
  * `Cannot update live changes from /products/{base_product_id}, try updating it from /products/{base_product_id}/live-changes.`

## `CANNOT_CHANGE_CATALOG_AND_CATEGORY_FOR_A_PRODUCT_VARIATION`

Cannot change the catalog or categories for a product variation in the payload.

`$Variation: Cannot add or remove catalogs or categories variation`

## CANNOT\_CHANGE\_FULFILLMENT\_TYPE\_UNTIL\_PRODUCT\_VARIATIONS\_ARE\_REMOVED

The fulfillment types in the payload are not the same as the fulfillment types in the base product when a product variation exists for the base product.

* `$Product: You cannot change the fulfillment type [Physical] before all variations are removed. Either remove it from the payload or use the existing type [Download].`

## `CANNOT_CHANGE_VARYING_ATTRIBUTE_VALUE`

You cannot use an attribute as a varying attribute and provide the same attribute in the localization payload. For example, you cannot specify the `color` attribute for the base product to define its variations and add the `color` attribute to the localization groups in the payload.

* `$Product: The attribute [platform] was used as varying attribute and cannot be updated. Remove it from attributes and try again.`

## `CANNOT_DELETE_LOCALE`

You cannot delete a default locale.

* `$Product: Cannot remove the default locale: [en_US].`

## `CANNOT_USE_A_LIVE_CHANGE_UPDATE_REQUEST_TO_UPDATE_DEPLOYMENT`

The payload contains a deployment change request for the `live-changes` folder.

*   For product variations:

    `Cannot update deployment changes from /products/{base_product_id}/variation/{variation_product_id}/live-changes, try it from /products/{base_product_id}/variation/{variation_product_id}.`
*   For individual and base products:

    `Cannot update deployment changes from /products/{base_product_id}/live-changes, try it from /products/{base_product_id}.`

## `CATALOG_DOES_NOT_BELONG_TO_COMPANY`

The given catalog exists but does not belong to the current company.

* `Product: catalog : [12345600] does not belong to company [1234].`&#x20;

## `CATALOG_NOT_FOUND`

Cannot find the catalog for the given catalog identifier.

* `$Product: Cannot find catalog for ID: [1234543200].`

## `CATEGORY_DOES_NOT_BELONG_TO_CATALOG`

The category exists but does not belong to the given catalog. Or the catalog was found, but its category ID is real.

* If the request finds the  catalog:
  * `$Product: Category : [1234543200] does not belong to catalog [12345600].`
* If the request finds the catalog and we want to check the category IDs associated with it:
  * `$Product: Cannot add the product to the category [1234543200] where the catalog does not exist.`

## `CATEGORY_NOT_FOUND`

Cannot find the category for the given catalog identifier.

* `$Product: Cannot find category for ID: [1234543200].`

## `COMPANY_NOT_FOUND`

Cannot find the specified company ID. This only occurs when the configuration in Dispatch is incorrect.

* `Cannot find company by Id: 123456`

## `COMPANY_NOT_PROVIDED`

The Dispatch Key was not correctly configured. Digital River received the request, but there was no specific HTTP header that identifies the company associated with the request. The request should include either `x-companyid` or `x-siteid` in the HTTP header.&#x20;

* `The companyId is required.`

## `DEFAULT_LOCALE_IS_INCONSISTENT_WITH_BASE_PRODUCT`

&#x20;The default locales in the product variations are different from the default locales in the base product. If there is more than one default locale in both the base product and a single product variation when creating a base product and product variation, we will use an array to generate the error message.

* `$Product: Default locale [ja_JP, en_US] must be consistent with its base product [en_US, en_GB]`

## `DEFAULT_LOCALE_IS_REQUIRED`

A request to create a new product (either individual product or base product and product variation) did not include a default locale.

* `$Product: A default locale is required to create a new product.`

## `DOWNGRADE_PRODUCT_DOES_NOT_EXIST`

Could not find the downgrade product in the payload.

* `$Product: The downgrade product [1234567800] does not exist.`

## `DUPLICATE_ATTRIBUTE_IN_PAYLOAD`

There is more than one value associated with an attribute in the payload. For example,  the value for the `name` attribute is `name-1` in the storefront group and `name-2` in the export control group.

* $Product: There is a duplicate \[`sku]` attribute in the payload with values \[sku1, sku2]. Only one value is allowed.

## `DUPLICATE_DEFAULT_LOCALE`

More than one default locale exists in the base product or product variation.

* `$Product: There are more than one default locales [en_US, ca_CA] in the payload. Only one default locale is allowed.`

## `DUPLICATE_ERID_IN_COMPANY`

More than one product for a given company uses the same ERID in the payload of this request when Enforce Unique Value is enabled for a product's external reference ID.

* `$Product: The following products already use the external reference ID [987654321]: [[PID]12345678, [PID]abcdefghijk, [PID]99912345]. Choose another value and try again.`

The `$Product` prefix depends on [error patterns](error-patterns.md).

{% hint style="info" %}
We don't check duplication while enabling the feature, so it is possible that multiple products are using the same ERID after enabling the feature.
{% endhint %}

## `DUPLICATE_ERID_IN_PAYLOAD`

More than one product uses the same ERID in the payload of the request for creating a base product or product variation when Enforce Unique Value is enabled for a product's external reference ID.&#x20;

*   `$Product: The following products already use the external reference ID [987654321]: [$aProductInPayload, $aProductInPayload]. Choose another value and try again.`



    * `The prefix '$Product' depends on the variation rules.`
    * `The variable'$aProductInPayload' depends on the variation rules.`

See [Error patterns](error-patterns.md) for variation rules.

## `DUPLICATE_FULFILLMENT_TYPE`

More than one fulfillment type is assigned to the product. Only a base product that uses the fulfillment type as a varying attribute can use both types.

* `$Product: The fulfillment type is duplicated [Download, Physical]. Only one value is allowed.`

## `DUPLICATE_PRICE_IN_LIST`

Duplicate prices exist in the same price list. There can only be one instance of a price without a locale and its associated currency even if their amounts are the same, and one instance of a currency and its locale regardless of their amounts.

*   `$Product: Price [TWD 199, zh_TW] is duplicate in type [listPrice] of catalog [12345600].`

    \
    The`$Product` prefix depends on [error patterns](error-patterns.md).

{% code title="Invalid request (partial payload)" %}
```json
{
  "type": "listPrice",
  "prices": [
    {
      "currency": "USD",
      "configuredPrice": 10.5
    },
    {
      "currency": "USD",
      "configuredPrice": 10.5
    },
    {
      "currency": "CAD",
      "locale": "en_CA",
      "configuredPrice": 12.5
    },
    {
      "currency": "CAD",
      "locale": "en_CA",
      "configuredPrice": 99.5
    }
  ]
}

```
{% endcode %}

In this case,&#x20;

* The price of USD without locale appears twice, so they are invalid even if their amounts are the same.
* The price of CAD and en\_CA appears twice, so they are invalid regardless of their amounts.

{% code title="Valid request (partial payload)" %}
```json
{
  "type": "listPrice",
  "prices": [
    {
      "currency": "USD",
      "configuredPrice": 10.5
    },
    {
      "currency": "USD",
      "locale": "en_CA",
      "configuredPrice": 11.5
    },
    {
      "currency": "CAD",
      "locale": "en_CA",
      "configuredPrice": 12.5
    }
  ]
}
```
{% endcode %}

In this case, we have three prices: USD without locale, USD+en\_CA, and CAD+en\_CA. There is no duplication in this example, so this one is valid.

## `ERID_EXCEEDS_MAX_LENGTH`

The length of the ERID value in the payload exceeds the maximum number of characters allowed. The maximum number of characters is 64.

* `$Product: The external reference Id[12345678901234567890123456789012345678901234567890123456789012345] exceeds the maximum length allowed: [64], please reduce it and try again.`

## `ERID_LOCK_ERROR`

The external reference identifier (number) must be unique to your company when you [enable the Product External Reference Number](https://help.digitalriver.com/help/gc/Administration/Company/Configuring-company-settings.htm) in [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do).

![](../../.gitbook/assets/image.png)

The Commerce API can process multiple requests at the same time. This error occurs when you send multiple requests **at almost the same time** that apply the same value for the external reference number to different products. Digital River allows only one successful request (the first one) to solve this race condition issue. The remaining requests will get this error.

* `$Product: Unable to check uniqueness for external Id[987654321], cause: connection time out`&#x20;

## `EXTERNAL_FILE_DOES_NOT_EXIST`

Could not find the file specified by the file ID attribute value in the request.

* `$Product: The external file [00f1b210-98c0-4717-a5da-99ba1aa912ff] specified by attribute [productImage1] does not exist`

## `EXTERNAL_FILE_DOES_NOT_SUPPORT_SUBFOLDERS`

The value for the `[padFile]` attribute contains subfolders. The  \[padFile] attribute does not support subfolders. For example, the `[padFile]` value contains an unsupported subfolder '`fileabc/a-file-id'`.

* `$Product: The [padFile] attribute does not support subfolders, parsed folders [abc].`

## `FULFILLER_ADD_OFI_FAMILY`

Cannot add or remove the OFI family from a given product.

{% hint style="info" %}
This is currently not testable because you can add or remove an OFI family. However, we may add new business logic in the future.
{% endhint %}

`$Product: Cannot add or remove more than one fulfillment family.`

## `FULFILLER_DOES_NOT_EXIST`

The fulfiller ID specified in the payload does not exist in [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do).

* `$Product: The fulfiller [ABC] does not have the correct configuration for other fulfillment integration, available fulfillers [DEF, XYZ].`

## **`FULFILLER_IS_NOT_ENABLED`**

The fulfiller ID exists in [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do)., but the OFI integration is disabled.

* `$Product: The fulfillment integration for fulfiller [DEF] is not enabled.`

## `FULFILLMENT_TYPE_INCONSISTENT_WITH_BASE_PRODUCT`

The product variation where the fulfillment type is **not** a varying attribute and the fulfillment type for the base product is different.

* `$Product: The fulfillment type [Download] must be consistent with its varying attribute, either remove it from the payload or use the existing type [Physical].`&#x20;

In the following example, the first product variation is `Download` but its base product is `Physical`.

{% code title=" Variation" %}
```json
{
  "productType": "BASE",
  "companyId": "cast",
  "id": "1234",
  "deploymentRequiredChanges": {
    "fulfillmentTypes": [
      "Physical"
    ]
  },
  "variations": [
    {
      "productType": "VARIATION",
      "companyId": "cast",
      "id": "var1",
      "varyingAttributes": [
        {
          "attributeName": "Color",
          "attributeValue": "Red"
        }
      ],
      "deploymentRequiredChanges": {
        "fulfillmentTypes": [
          "Download"
        ]
      }
    },
    {
      "productType": "VARIATION",
      "companyId": "cast",
      "id": "var2",
      "varyingAttributes": [
        {
          "attributeName": "Color",
          "attributeValue": "Blue"
        }
      ]
    }
  ]
}
```
{% endcode %}

## `FULFILLMENT_TYPE_INCONSISTENT_WITH_VARYING_ATTRIBUTE`

A fulfillment type in the deployment required a change that is not consistent with the fulfillment type for the varying attribute associated with the product variation. Or a base product uses the fulfillment type as a varying attribute, but it is not `Download + Physical`.&#x20;

* `$Product: The fulfillment type [Download] must be consistent with its base product, either remove it from the payload or use the existing type [Physical].`

In the following example, the first product variation uses `Download` as the varying attribute, but its fulfillment type is Physical.&#x20;

{% code title="Product variation" %}
```json
{
  "productType": "BASE",
  "companyId": "cast",
  "id": "1234",
  "deploymentRequiredChanges": {
    "fulfillmentTypes": null
  },
  "variations": [
    {
      "productType": "VARIATION",
      "companyId": "cast",
      "id": "var1",
      "varyingAttributes": [
        {
          "attributeName": "fulfillmentType",
          "attributeValue": "Download"
        }
      ],
      "deploymentRequiredChanges": {
        "fulfillmentTypes": [
          "Physical"
        ]
      }
    },
    {
      "productType": "VARIATION",
      "companyId": "cast",
      "id": "var2",
      "varyingAttributes": [
        {
          "attributeName": "fulfillmentType",
          "attributeValue": "Physical"
        }
      ]
    }
  ]
}
```
{% endcode %}

In the following example, the base product does not provide the correct fulfillment types and the fulfillment type is used as the varying attribute, so you must either include both types in the base product or remove the fulfillment types from the payload.

{% code title=" Base product" %}
```json
{
  "productType": "BASE",
  "companyId": "cast",
  "id": "1234",
  "deploymentRequiredChanges": {
    "fulfillmentTypes": [
      "Physical"
    ]
  },
  "variations": [
    {
      "productType": "VARIATION",
      "companyId": "cast",
      "id": "var1",
      "varyingAttributes": [
        {
          "attributeName": "fulfillmentType",
          "attributeValue": "Download"
        }
      ]
    },
    {
      "productType": "VARIATION",
      "companyId": "cast",
      "id": "var2",
      "varyingAttributes": [
        {
          "attributeName": "fulfillmentType",
          "attributeValue": "Physical"
        }
      ]
    }
  ]
}
```
{% endcode %}

## `FULFILLMENT_TYPE_NOT_SUPPORTED`

The `Physical` fulfillment type is not currently supported.

* `$Product: The fulfillment type [Physical] is not supported.`

## `INACTIVE_PRICE_TYPE_IN_CATALOG`

The price list type exists in this catalog but is not active.

* `$Product: The price list type abcd is inactive in the catalog 12345600.`

## `INCONSISTENT_DEFAULT_LOCALE`

The locale appears more than once in the payload of a base product or product variation. However, some instances of the locale are marked as the default and others are not.

* `$Product: The value for isDefault for locale [en_US] must be consistent in the payload.`

## `INVALID_ATTRIBUTE_IMAGE_URL`

One or more URLs for product images (details 1 \~ 5, thumbnail 1 \~ 5) are invalid, or the `custom` attribute is not an image content type. This validation only occurs when you deploy a product.

* `$Product: The URL format for [//abc.ddd/a-pic] of [thumbnailImage2] is invalid. It should start with https://, http://, //. And it should end with .jpg, .gif, .png, .webp.`

## `INVALID_ATTRIBUTE_NAME`&#x20;

The specified attribute name does not exist for the current company.

* `$Product: The attributes [abc, def, 1234] is are not applicable for the current company.`

## `INVALID_ATTRIBUTE_VALUE`

The value for the attribute is invalid.

For a single value attribute:

* `$Product: The value [ABC] for the [returnMethod] attribute is invalid. The expected value is one of [LOD, Physical, or NothingRequired].`

For an attribute with multiple values:

* `$Product: The value [99, 15, 7] for the timeIntervalForCCExpirationReminderNotifications attribute is invalid. The expected values are [30, 7, 15]. Multiple values for this attribute are allowed.`

## `INVALID_ATTRIBUTE_VALUE_TYPE`

The data type for the specified attribute is invalid.

* `$Product: The type [String] for the[privateStoreOnly] attribute is invalid. The expected type is [Boolean].`

## `INVALID_EXTERNAL_FILE_NAME`

The actual file name used by the File ID is invalid. For example, the file ID '1234' exists in the headless file API, but its real file name is 'ap@image.jpg', where @ is not an allowed character.

* `$Product: The file name [b*c] in the [productImage1] attribute for external file [00f1b210-98c0-4717-a5da-99ba1aa912ff] is invalid. The filename cannot contain any spaces or special characters.`

## `INVALID_EXTERNAL_ZIP_FILE`

The file extension name is ZIP, but the file is not a valid zip file or the file is corrupt. For example, rename the file extension from TXT to ZIP and uploaded it.

* `$Product: The file specified by the {padFile] attribute for external file [00f1b210-98c0-4717-a5da-99ba1aa912ff] is not a valid zip file.`

## `INVALID_FILE_NAME_IN_EXTERNAL_ZIP_FILE`

A valid zip file contains a file with an invalid name. For example, the zip file contains a file with the name '`f~b.txt`' in a zip file called '`zipped.zip`', where \~ is not allowed.

* `$Product: The files in zip file specified by the [padFile] attribute for external file [00f1b210-98c0-4717-a5da-99ba1aa912ff] is invalid. The files in the zip file cannot contain any spaces or special characters.`

## `INVALID_FOLDER_NAME_FOR_EXTERNAL_FILE`

A subfolder in the attribute value is invalid. For example, `a!b` is not a valid folder name because it contains an "`!`".

* `$Product: The folder name [a~b] for the external file path in the [productImage1] attribute is invalid. The file path cannot contain any spaces or special characters.`

## `INVALID_FULFILLMENT_TYPE`

The fulfillment type is invalid. Only `Download` and `Physical` **** are allowed.

* `$Product: The fulfillment type [abc] is invalid. The expected types are [Download, Physical].`

## `INVALID_IMAGE_CONTENT_FOR_EXTERNAL_FILE`

The value for the `image` attribute is not a valid image type. For example, rename the TXT file extension to PNG and upload the file to the headless file API.

* `$Product: The content of image of attribute [productImage1] for external file [00f1b210-98c0-4717-a5da-99ba1aa912ff] is invalid. The supported types are [png, bmp, jpg, jpeg, gif, webp].`

## `INVALID_IMAGE_TYPE_FOR_EXTERNAL_FILE`

The extension name specified in the image attribute value is not a [supported image type](supported-image-types.md).&#x20;

* `$Product: The image type [txt] of attribute [productImage1] for external file [00f1b210-98c0-4717-a5da-99ba1aa912ff] is invalid. The supported types are [png, bmp, jpg, jpeg, gif, webp].`

## `INVALID_LIST_PRICE_LOCALE`

`The request did not provide the configuredf  priceE`–The specified locale is not supported by the Global Commerce platform. Either it does not exist or it is not supported. For example, the locale (`ab_CD`)  for the price (`USD, 123`), or empty string is not supported.

* `$Product: Locale [ab_CD] of price [USD, 123] is invalid in type [listPrice] of catalog [12345600].`

## `INVALID_LOCALE`

The locale in the payload is either invalid or not supported in [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do).

* `$Product: The locales [ab_CD, ZZZZ] are invalid.`

## `INVALID_NAME_FOR_EXTERNAL_ZIP_FILE`

The name of the zip file contains invalid characters. For example, `(` is not allowed in '`a(file.zip`'.

* `$Product: The zip file name [z+a.zip] for the [padFile] attribute for external file [00f1b210-98c0-4717-a5da-99ba1aa912ff] is invalid. The zip file name cannot contain any spaces or special characters.`

## `INVALID_PARENT_VERSION_STATE_FOR_SUBSCRIPTION_PRODUCT`

The product must be in design mode before you can change its related products. Once a product is deployed, you cannot change its related products.

* `Product 1234567800: cannot have related products. (not in design mode)`

## `INVALID_PRICE_CURRENCY`

The specified currency for the price is not supported by the Global Commerce platform. Either it does not exist or it is not supported. For example, currency ABC is not supported.

* If the request provided the locale:
  * `$Product: Currency code [ABC] of price [ABC, en_US] is invalid in type [listPrice] of catalog [12345600].`
* If the request did not provide the locale:
  * `$Product: Currency code [ABC] of price [ABC] is invalid in type [listPrice] of catalog [12345600].`

## `INVALID_VARYING_ATTRIBUTE_VALUE`

&#x20;The value provided for the varying attribute does not exist. For example, the user provided a value of `black`, but the varying attribute only supports `red`, `blue`, and `yellow`.

`Variation: Blue is an invalid color value for the varying attribute. The valid values are: [Red, Yellow, Black]`

* If the variation does not have ERID:
  * `1st Variation: [Blue] is an invalid [color[ value for the varying attribute. The valid values are: [Red, Yellow, Black]`
* If the variation has ERID:
  * `Variation erid-ABC: [Blue] is an invalid [color] value for the varying attribute. The valid values are: [Red, Yellow, Black]`

## `INVALID_VARYING_ATTRIBUTE_VALUE_TYPE`&#x20;

Cannot convert the value for the varying attribute to the expected data type. This should not occur at the API layer because we only support String and Boolean values for varying attributes, and any string can be converted to Boolean.

`Variation: Data type of value of 123 is invalid for attribute: color, expected type: Boolean`

* If the variation does not have ERID:
  * `1st Variation: data type value: [123] is an invalid for attribute: [isWireless], expected type: [Boolean].`
* If the variation has ERID:
  * `Variation erid-ABC: Data type value: [123] is an invalid for attribute: [isWireless], expected type: [Boolean].` &#x20;

{% code title="Invalid example (partial payload)" overflow="wrap" %}
```json
{
  "attributes": {
    "isWireless": "123"
  }
}
```
{% endcode %}

{% code title="Valid example (partial payload)" overflow="wrap" %}
```json
{
  "attributes": {
    "isWireless": true
  }
}
```
{% endcode %}

## `INVALID_VARYING_ATTRIBUTE_NAME`

Cannot find the specified varying attribute in Global Commerce, or the attribute type is not expected.

`Variation: Attribute: [XYZ] is invalid.`

* If the variation does not have ERID:
  * `1st Variation: Sttribute: [XYZ] is invalid.`
* If the variation has ERID:
  * `Variation erid-ABC Attribute: [XYZ] is invalid.`

{% hint style="info" %}
We don't currently provide available attribute names for this error, because there will be multiple attributes grouped in multiple product families. Organizing this information in a readable format is complex.
{% endhint %}

## `LOCALE_NOT_PROVIDED`

The required locale data is missing in the payload, URL, or other parameters. You may see the following error description:

* `A locale is required.` Provide the locale and try again.

## `MORE_THAN_ONE_DOWNGRADE_PRODUCT_EXISTS`

The downgrade product's ID refers to two or more products in [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do). This occurs when the request uses ERID as the downgrade product ID.

* `$Product: There is more than one product for the downgrade product [abc-external-reference-id], found products [Product [ERID]abc-external-reference-id [PID]1912344500, Product [ERID]abc-external-reference-id [PID]1912344600]`

## `MORE_THAN_ONE_TRANSFER_PRODUCT_EXIST`

The transfer product ID for the subscription refers to two or more products in [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do). This occurs when the request uses ERID as the transfer product ID.

* `$Product: There is more than one product for the transfer product [abc-external-reference-id], found products [Product [ERID]abc-external-reference-id [PID]1912344500, Product [ERID]abc-external-reference-id [PID]1912344600].`

## `MORE_THAN_ONE_UPGRADE_PRODUCT_EXISTS`

The ID for the upgrade product refers to two or more products in [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do). This occurs when the request uses ERID as the upgrade product ID.

* `$Product: There is more than one product for the upgrade product [abc-external-reference-id], found products [Product [ERID]abc-external-reference-id [PID]1912344500, Product [ERID]abc-external-reference-id [PID]1912344600].`

## `PRICE_CANNOT_BE_EMPTY`

The request did not provide the configured price (that is, the price is either null or does not exist in the payload).

* `$Product: A configured price is required at price [USD, en_US] in type [listPrice] of catalog [12345600].`

## `PRICE_CANNOT_BE_LESS_THAN_ZERO`

The amount of the price is less than zero (for example, -0,000004). The price cannot be a negative number.

* `$Product: Configured price cannot be less than zero for the price [USD, en_US] in price list type called [listPrice] in catalog [1234560].`

## `PRICE_CURRENCY_AND_LOCALE_NOT_CONFIGURABLE`

The currency and locale are not configurable in the given catalog when a given price list type is active. For example, you cannot add the child price list called `USD+en_GB` child price list when the price list type called `listPrice` is active.

* `$Product: Price [USD, en_GB] is invalid in the price list type [abcd] of catalog [12345600]. Try creating it in the price list before activating it.`

## `PRICE_LIST_TYPE_NOT_SUPPORTED`

The specified price list type is not supported.

* `$Product: Price list type [abcd] for catalog [12345600] is not supported.`

## `PRICE_TYPE_DOES_NOT_EXIST_IN_CATALOG`

The given catalog does not include this price type.

* `$Product: The price list type [abcd] is invalid in the catalog [12345600].`

## `PRODUCT_DOES_NOT_BELONG_TO_COMPANY`

The product exists in Digital River but does not belong to the specified company associated with the dispatch API key.

* `$Product: the product does not belong to the company: [company-id-1234].`

## `PRODUCT_ID_NOT_FOUND`

The current request type requires the product ID in the payload, URL, or other parameters. You may see the following error description:&#x20;

* `A product ID is required.` Provide the product ID and try again.

## `PRODUCT_NOT_FOUND`

The product ID for the product or product variation could not be found. You may see the following error description:&#x20;

* `Cannot find the product [produtId1].` The specified product IDs could not be found. provide the correct product ID and try again.&#x20;

## `PRODUCT_TYPE_DOES_NOT_MATCH`

The product type provided does not match the expected product type. For example:

* Add a product variation to a product variation.
* Add a product variation to an individual product.
* Delete a locale from a product variation.
* Delete a product variation that is not a product variation. It is actually a base product or individual product.
* Deploy on a product variation.
* Retire on a product variation.
* Update a product variation using the update-product URL.
* Update a product using the update-variation URL.

You may see the following error descriptions:

* `Cannot add a product variation to an individual product. Add a product variation to a base product.`
* `Cannot add a product variation to another product variation. Add the product variation to a base product.`
* `Cannot update a product variation to an individual product. Update the product variation for a base product.`
* `Cannot update a product variation to a base product. Update the product variation for a base product.`
* `Cannot delete an individual product. Delete a product variation product from a base product, or retire the individual product.`
* `Cannot delete a base product. Delete a product variation product from the base product, or retire the base product.`
* `Cannot delete a locale from a product variation. Delete the locale from a base product or an individual product.`
* `Cannot deploy the product from a product variation. Deploy the base product or an individual product.`
* `Cannot retire a product from a product variation., Retire the base product or an individual product.`
* `Cannot update a product to a product variation. Update the base product or an individual product.`
* `REQUEST_TYPE_NOT_SUPPORTED`–The request type provided is not supported. This error should not occur in the API layer. It is only used at the service level when something unexpected happened.
* `SYSTEM_ERROR`–An unexpected error occurred (for example, NPE). &#x20;

## `TRANSFER_PRODUCT_DOES_NOT_EXIST`

&#x20;Cannot find the transfer product specified in the payload.

* `$Product: The transfer product [1234567800] does not exist.`
* `$Product: The transfer product [abc-external-reference-id] does not exist.`

## `UNABLE_TO_DEPLOY_PRODUCT`

You cannot deploy a product variation.

{% hint style="info" %}
This is not testable because the request will be rejected by:  `PRODUCT_TYPE_NOT_MATCH`
{% endhint %}

* `$Product: Unable to deploy product [1234567800]. It is not a base product.`

## `UNABLE_TO_DESERIALIZE_PAYLOAD`

Cannot deserialize the payload for the expected Java object. For example, the field is not a JSON string. &#x20;

## `UNABLE_TO_RETIRE_PRODUCT`

You cannot retire a product variation.

{% hint style="info" %}
This is not testable because the request will be rejected by:  `PRODUCT_TYPE_NOT_MATCH`
{% endhint %}

* `$Product: Unable to retire product [1234567800]. It is not a base product.`

## `UNABLE_TO_SERIALIZE_PAYLOAD`

Cannot serialize the payload for the expected Jaca object. This error probably won't appear in productions since all fields are nullable, and we ignore unknown properties.

## `UNSUPPORTED_ATTRIBUTE_NAME`

The attribute exists in [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do), but the Product Admin API does not support it yet.  This only applies to attributes in the global family. A custom attribute is either invalid or valid.

* `$Product: The attributes [weight, downloadFile] are not supported.`

## `UPGRADE_PRODUCT_DOES_NOT_EXIST`

Could not find the upgrade product in the payload.

* `$Product: The upgrade product [1234567800] does not exist.`

## `VARIATION_DOES_NOT_BELONG_TO_PRODUCT_BASE`

The IDs for both the base product and Variation product exist in the URL, but they do not belong to each other. This is an error on the publisher's side.

* `Variation [12345678] does not belong to base product [87654321], try replacing the base product ID with 'product'.`

## `VARYING_ATTRIBUTE_DUPLICATE_COMBINATION`

Cannot use the same combination when adding a new variation. For example:

* Add two variations with both `color=red` and `size=small`.
* Add a variation where the same combination already exists in a given base product.

Add variations with both:

`Variation: Duplicate varying attributes [color=red, size=small]`

* If the variation does not have ERID:
  * `1st Variation: Duplicate varying attributes [color=red, size=small]`
* If the variation has ERID:
  * `Variation erid-ABC: Duplicate varying attributes [color=red, size=small]`

Add a variation where the same combination already exists in a given base product:

`Variation: Duplicate varying attributes [color=red, size=small] from the existing product variation.`

* If the variation does not have ERID:
  * `1st Variation: Duplicate varying attributes [color=red, size=small] from the existing product variation.`
* If the variation has ERID:
  * `Variation erid-ABC: Duplicate varying attributes [color=red, size=small] from the existing product variation.`

## `VARYING_ATTRIBUTE_DUPLICATE_NAME`

The same attribute appears more than once in a single variation (for example, `color=red`, `color=blue` in the same variation.)\
\
`Variation: Duplicate varying attributes: [color,size]`

* If the variation does not have ERID:
  * `1st Variation: Duplicate varying attributes: [color,size].`
* If the variation has ERID:
  * `Variation erid-ABC: Duplicate varying attributes: [color,size].`

## `VARYING_ATTRIBUTE_NAME_NOT_ELIGIBLE`

The attribute name for the varying attribute was found in Global Commerce, but cannot be used as a varying attribute.

`Variation: attribute: ABC cannot be used to define variations.`

* If the variation does not have ERID:
  * `1st Variation: Cannot use attribute [ABC] to define variations`
* If the variation has ERID:
  * `Variation erid-ABC: Cannot use attribute [ABC] to define variations`

## `VARYING_ATTRIBUTE_NOT_PROVIDED`

The user tried to add one or more product variations but did not provide the varying attribute list for all of them.

`Variation: Duplicate varying attributes cannot be empty`

* If the variation does not have ERID (external reference ID):
  * 1st Variation: Duplicate varying attributes cannot be empty
* If the variation has ERID (external reference ID):
  * Variation erid-ABC: Duplicate varying attributes cannot be empty

## `VARYING_ATTRIBUTE_NOT_SET_AT_BASE_PRODUCT`

A user tried to add a new product variation to an existing product, but there was no varying attribute defined for the base product.

`$Variation: There is no varying attribute configured for the base product. Cannot add new product variation.`

* `The prefix '$Variation' depends on the` [`variation rules`](error-patterns.md)`.`

## `VARYING_ATTRIBUTE_NOT_SUFFICIENT`

The user did not provide all of the required varying attributes when adding a product variation. For example, the user only provided color when both color and size are required.

`Variation: varying attributes are insufficient. The required attributes are [color, size], and the provided attribute) are [color, size, material].`

* If the variation does not have ERID:
  * `1st Variation: Varying attributes are insufficient. The required attributes are [color, size]. The provided attributes are [color, size, material].`
* If the variation has ERID:
  * `Variation erid-ABC: VARYING_ATTRIBUTE_NOT_SUFFICIENTarying attributes are insufficient. The required attributes are [color, size]. The provided attributes are [color, size, material].`

## `VARYING_ATTRIBUTE_NOT_USABLE_BY_COMPANY`

The attribute name for the varying attribute was found in Global Commerce, but cannot be used by the given company.

`Variation: varying attribute: TUV is not applicable at the current company`

* If the variation does not have ERID:
  * `1st Variation: Varying attribute [TUV] is not applicable at the current company.`
* If the variation has ERID:
  * `Variation erid-ABC: Varying attribute [TUV] is not applicable at the current company.`
