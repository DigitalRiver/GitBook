---
description: Learn more about the categories resource.
---

# Categories

## Categories query parameters

### API key

The `apiKey` is your [API key](../../resources/API-structure/api-keys.md).

### Currency

Use the `currency` query parameter when you want to see the currency associated with the category.. The currency query parameter takes precedence over the locale.&#x20;

### Expand

Use the `expand` query parameter when you want additional fields to appear in the response. The `expand` query parameter provides additional fields in the response. Expanding resources reduces the number of API calls required to accomplish a task. See [Expand query parameter](../common-shoppers-and-admin-apis-reference/fields-and-expand-query-parameters.md#expand-query-parameter) for more information.

### Fields

Use the `fields` query parameter to specify the fields that appear in the response. Filtering the fields returned in the response can conserve bandwidth and accelerate response time. See [Fields query parameter](../common-shoppers-and-admin-apis-reference/fields-and-expand-query-parameters.md#fields-query-parameter) for more information.&#x20;

### Locale

Use the `locale` query parameter when you want to see the locale associated with a category.

### Product page size

The productsPageSize query parameter specifies the maximum number of products to include for each category returned in a paginated response. The value must be a positive number greater than zero and less than 100000. The default is 10. This query parameter is only available when [getting a category by identifier](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Categories/paths/\~1v1\~1shoppers\~1me\~1categories\~1%7BcategoryId%7D/get) and [getting all categories for a specific product](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Categories/paths/\~1v1\~1shoppers\~1me\~1products\~1%7BproductId%7D\~1categories/get).

### Token

The `token` is the authorized or anonymous token for the shopper.
