---
description: Learn more about web checkout.
---

# Web checkout

## Web checkout query parameters

You can specify one or more query parameters separated by an ampersand (&) to filter the contents of the web checkout. The following topics describe the query parameters for [web-checkout](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Web-Checkout). For more information on how to use query parameters, see [Fields and query parameters](../common-shoppers-and-admin-apis-reference/fields-and-expand-query-parameters.md).

The following describes query parameters for [web-checkout](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Web-Checkout).

### External reference identifier (ERID)

The [`externalReferenceId`](broken-reference) is a company's internal identifier for a product.&#x20;

### Fields

Use the [`fields` query parameter](../common-shoppers-and-admin-apis-reference/fields-and-expand-query-parameters.md#fields-query-parameter) to specify the fields that appear in the response. Filtering the fields returned in the response can conserve bandwidth and accelerate response time.&#x20;

### Product identifier

A `productId` is your unique [product identifier](web-checkout.md#product-identifier) or unique stock keeping unit (SKU) for a product. A product's unique identifier is represented by an `id`.&#x20;

### Theme identifier

The `themeId` is the identifier of the theme associated with a site. The theme controls the styles of a Digital River-hosted web page.

### Token

The `token` is the authorized or anonymous token for the shopper.
