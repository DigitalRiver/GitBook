---
description: >-
  Learn how the CountrySpecs API can help you determine whether address and tax
  identifier information is required and also whether it is properly formatted.
---

# Country specs

As the [authorized reseller](../../../#working-with-digital-river) of your goods, Digital River needs specific customer data so that we can authorize payments, compute taxes, arrange fulfillments, and comply with invoicing regulations. What data is required and how it is formatted depends on the combination of the [selling entity](selling-entities.md) and country.

The [CountrySpecs API](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Country-specifications) returns schemas based on the [selling entity](selling-entities.md) and country combination you provide. You can then use these schemas to determine whether an address component or tax identifier is required and also whether it is properly formatted.

## Using the CountrySpec API

With the CountrySpecs API, you provide Digital River a [selling entity](selling-entities.md) and a country code that represents the expected billing and/or shipping address of the customer. Digital River then [returns](country-specs.md#retrieving-a-countryspec) one or more of the following schemas:

| Schema name               | Schema type                                               | Description                                                                                                                                                                                                                                                          |
| ------------------------- | --------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Billing address           | [Address](country-specs.md#address-schemas)               | This schema can be used in conjunction with the ship to address schema to process orders that contain physical goods. All data fields are optional except those required to process payments.                                                                        |
| Ship to address           | [Address](country-specs.md#address-schemas)               | This schema can be used in conjunction with the billing address schema to process orders that contain physical goods. All data fields are optional except those necessary for invoice compliance, tax computations, and shipping details.                            |
| Billing address only      | [Address](country-specs.md#address-schemas)               | This schema can be used for orders that contain only digital products since it does not validate the format of any ship to address components. All data fields are optional except those necessary for payment processing, invoice compliance, and tax computations. |
| Individual tax identifier | [Tax identifier](country-specs.md#tax-identifier-schemas) | Provides validation keywords and regular expressions to determine if tax identifiers for individuals are required and properly formatted.                                                                                                                            |
| Business tax identifier   | [Tax identifier](country-specs.md#tax-identifier-schemas) | Provides validation keywords and regular expressions to determine if tax identifiers for businesses are required and properly formatted.                                                                                                                             |

### Supported countries

When an appropriate selling entity is provided, the [Country Specs API](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Country-specifications) currently provides both address and tax identifier schemas for the United Kingdom, France, Germany, Italy, Spain, Canada, and the United States. Some countries, such as Poland and Brazil, return only tax identifiers schemas, while others do not have any available at the moment.

### Address schemas

In the various address schemas, the following keys can be used to specify an address: `name`, `organization`, `line1`, `line2`, `neighborhood`, `city`, `postalCode`, `state`, and `country`. Each key contains [certain constraining properties](country-specs.md#common-constraints).

The `required` validation keyword indicates which keys the customer must provide.

### Tax identifier schemas

In these schemas, the `taxIdentifier` key uses a [pattern validation keyword to constrain](country-specs.md#common-constraints) the format of the tax identifier.

If a tax identifier is necessary, the `required` validation keyword contains a populated array. Otherwise, the array is empty.

### Common constraints

Other than `description` , which is an annotation keyword, all of the following validation keywords may be used as constraints to ensure that [address](country-specs.md#address-schemas) or [tax identifier](country-specs.md#tax-identifier-schemas) input data is correctly formatted.

| Keyword     | Description                                                                                                      | Type        | Required | Example                       |
| ----------- | ---------------------------------------------------------------------------------------------------------------- | ----------- | -------- | ----------------------------- |
| type        | Constraint on the type of the property. Possible values are `string`, `number`, `integer`, `boolean`, or `array` | Enumeration | Yes      | integer                       |
| description | A general description of the property                                                                            | String      | No       | VAT ID for Italy (Individual) |
| minLength   | Constraint that defines the minimum length of the property                                                       | Integer     | No       | 0                             |
| maxLength   | Constraint that defines the maximum length of the property                                                       | Integer     | No       | 128                           |
| pattern     | Constraint expressed as a regular expression. This field is used for postal codes and tax identifiers.           | String      | No       | ^\[0-9]{5}(?:-\[0-9]{4})?$    |
| enum        | Constraint expressed as an enumeration. This field is used for states and countries.                             | Array       | No       | GB                            |

### Retrieving a CountrySpec

To retrieve a CountrySpec, you'll need to provide a country code and selling entity as query parameters in a `GET /country-specs` request. The `country` parameter is an [ISO 3166-1 alpha-2 country code](https://www.iban.com/country-codes) representing the expected billing or ship to address of the customer. The `sellingEntity` parameter represents the [selling entity](selling-entities.md) assigned to the order.

When you create, update, or retrieve a Checkout, a `sellingEntity` is returned in the response and contains `id` and `name` values. You should use the `id` value to set the `sellingEntity` parameter when requesting a `CountrySpec`.

{% tabs %}
{% tab title="JSON" %}
```javascript
{
    ...
    "sellingEntity": {
        "id": "DR_IRELAND-ENTITY",
        "name": "Digital River Ireland Ltd."
    },
    ...
}
```
{% endtab %}
{% endtabs %}

The following `GET` request retrieves the CountrySpec for Italy by setting the `country` to `IT` and the `sellingEntity` parameter to `DR_IRELAND-ENTITY`.

{% tabs %}
{% tab title="cURL" %}
```
curl --location --request GET 'https://api.digitalriver.com/country-specs?country=IT&sellingEntity=DR_IRELAND-ENTITY%0A' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer <API_key>' \
```
{% endtab %}
{% endtabs %}

The response returns a CountrySpec that consists of a `data` array containing schemas formatted as strings.

{% hint style="warning" %}
If either the specified `country` or `sellingEntity` are not found, the response returns an empty `data` array.
{% endhint %}

```
{
    "data": [
        {
            "country": "IT",
            "sellingEntity": "DR_IRELAND-ENTITY",
            "billingAddressSchema": "{\"$schema\":\"http://json-schema.org/draft-07/schema#\",\"title\":\"Address\",\"type\":\"object\",\"properties\":{\"name\":{\"type\":\"string\",\"description\":\"purchaser full name\",\"minLength\":0,\"maxLength\":128},\"organization\":{\"type\":\"string\",\"description\":\"purchaser company or organization\",\"minLength\":0,\"maxLength\":128},\"line1\":{\"type\":\"string\",\"description\":\"purchaser residence number and street\",\"minLength\":0,\"maxLength\":128},\"line2\":{\"type\":\"string\",\"description\":\"supplimental address information such as apartment number or suite\",\"minLength\":0,\"maxLength\":128},\"city\":{\"type\":\"string\",\"description\":\"purchaser city of residence\",\"minLength\":0,\"maxLength\":64},\"postalCode\":{\"type\":\"string\",\"description\":\"purchaser postal code\",\"pattern\":\"^\\\\d{5}$\"},\"country\":{\"type\":\"string\",\"description\":\"Address country\",\"enum\":[\"IT\"]}},\"required\":[\"country\",\"postalCode\"]}",
            "shippingAddressSchema": "{\"$schema\":\"http://json-schema.org/draft-07/schema#\",\"title\":\"Address\",\"type\":\"object\",\"properties\":{\"name\":{\"type\":\"string\",\"description\":\"purchaser full name\",\"minLength\":0,\"maxLength\":128},\"organization\":{\"type\":\"string\",\"description\":\"purchaser company or organization\",\"minLength\":0,\"maxLength\":128},\"line1\":{\"type\":\"string\",\"description\":\"purchaser residence number and street\",\"minLength\":0,\"maxLength\":128},\"line2\":{\"type\":\"string\",\"description\":\"supplimental address information such as apartment number or suite\",\"minLength\":0,\"maxLength\":128},\"city\":{\"type\":\"string\",\"description\":\"purchaser city of residence\",\"minLength\":0,\"maxLength\":64},\"postalCode\":{\"type\":\"string\",\"description\":\"purchaser postal code\",\"pattern\":\"^\\\\d{5}$\"},\"country\":{\"type\":\"string\",\"description\":\"Address country\",\"enum\":[\"IT\"]}},\"required\":[\"country\",\"city\",\"postalCode\",\"line1\"]}",
            "billingAddressOnlySchema": "{\"$schema\":\"http://json-schema.org/draft-07/schema#\",\"title\":\"Address\",\"type\":\"object\",\"properties\":{\"name\":{\"type\":\"string\",\"description\":\"purchaser full name\",\"minLength\":0,\"maxLength\":128},\"organization\":{\"type\":\"string\",\"description\":\"purchaser company or organization\",\"minLength\":0,\"maxLength\":128},\"line1\":{\"type\":\"string\",\"description\":\"purchaser residence number and street\",\"minLength\":0,\"maxLength\":128},\"line2\":{\"type\":\"string\",\"description\":\"supplimental address information such as apartment number or suite\",\"minLength\":0,\"maxLength\":128},\"city\":{\"type\":\"string\",\"description\":\"purchaser city of residence\",\"minLength\":0,\"maxLength\":64},\"postalCode\":{\"type\":\"string\",\"description\":\"purchaser postal code\",\"pattern\":\"^\\\\d{5}$\"},\"country\":{\"type\":\"string\",\"description\":\"Address country\",\"enum\":[\"IT\"]}},\"required\":[\"country\",\"postalCode\"]}",
            "individualTaxIdentifiersSchemas": [
                "{\"$schema\":\"http://json-schema.org/draft-07/schema#\",\"title\":\"it_natural\",\"description\":\"VAT ID for Italy (Individual)\",\"type\":\"object\",\"properties\":{\"taxIdentifier\":{\"type\":\"string\",\"pattern\":\"^\\\\d\\\\d\\\\d\\\\d\\\\d\\\\d\\\\d\\\\d\\\\d\\\\d\\\\d$|^IT\\\\d\\\\d\\\\d\\\\d\\\\d\\\\d\\\\d\\\\d\\\\d\\\\d\\\\d$\"}},\"required\":[]}",
                "{\"$schema\":\"http://json-schema.org/draft-07/schema#\",\"title\":\"it_cf\",\"description\":\"Italian Fiscal Code Card (Individual ID)\",\"type\":\"object\",\"properties\":{\"taxIdentifier\":{\"type\":\"string\",\"pattern\":\"^[A-Z\\\\d][A-Z\\\\d][A-Z\\\\d][A-Z\\\\d][A-Z\\\\d][A-Z\\\\d][A-Z\\\\d][A-Z\\\\d][A-Z\\\\d][A-Z\\\\d][A-Z\\\\d][A-Z\\\\d][A-Z\\\\d][A-Z\\\\d][A-Z\\\\d][A-Z\\\\d]$\"}},\"required\":[]}"
            ],
            "businessTaxIdentifiersSchemas": [
                "{\"$schema\":\"http://json-schema.org/draft-07/schema#\",\"title\":\"it\",\"description\":\"VAT ID for Italy (Business)\",\"type\":\"object\",\"properties\":{\"taxIdentifier\":{\"type\":\"string\",\"pattern\":\"^IT\\\\d\\\\d\\\\d\\\\d\\\\d\\\\d\\\\d\\\\d\\\\d\\\\d\\\\d$\"}},\"required\":[]}"
            ],
            "liveMode": false
        }
    ]
}
```

## Sample address schema

The following shows the billing address schema for products ordered in Italy (`IT`) and sold through the Digital River Ireland Ltd. entity (`DR_IRELAND-ENTITY`).

The `type` validation keyword indicates that the billing address data will be verified as a JSON object.

The keys, such as `name`, `organization`, and `line1`, all contain validation keywords, with the exception of `description`, that act as constraints.

The `minLength` and `maxLength` validation keywords, which both require an integer, define the allowable length of the `name`, `organization`, `line1`, `line2`, and `city`.

The `postalCode` key specifies a `pattern` , consisting of a regular expression, that the input data must match.

For `country`, the `enum` validation keyword constrains entries to `IT` . When a schema contains the `state` key, as is the case for addresses in the United States, multiple enumerations are available.

The `required` validation keyword indicates which keys the customer must provide. In this example, the customer must enter a valid `country` and `postalCode`.

```
"billingAddressSchema":"{
    \"$schema\":\"http://json-schema.org/draft-07/schema#\",
    \"title\":\"Address\",
    \"type\":\"object\",
    \"properties\": {
        \"name\": {
            \"type\":\"string\",
            \"description\":\"purchaser full name\",
            \"minLength\":0,
            \"maxLength\":128
        },
        \"organization\": {
            \"type\":\"string\",
            \"description\":\"purchaser company or organization\",
            \"minLength\":0,
            \"maxLength\":128
        },
        \"line1\": {
            \"type\":\"string\",
            \"description\":\"purchaser residence number and street\",
            \"minLength\":0,
            \"maxLength\":128
        },
        \"line2\": {
            \"type\":\"string\",
            \"description\":\"supplimental address information such as apartment number or suite\",
            \"minLength\":0,
            \"maxLength\":128
        },
        \"city\": {
            \"type\":\"string\",
            \"description\":\"purchaser city of residence\",
            \"minLength\":0,
            \"maxLength\":64
        },
        \"postalCode\": {
            \"type\":\"string\",
            \"description\":\"purchaser postal code\",
            \"pattern\":\"^\\\\d{5}$\"
        },
        \"country\": {
            \"type\":\"string\",
            \"description\":\"Address country\",
            \"enum\":[\"IT\"]
        }
    },
    \"required\":[\"country\",\"postalCode\"]
}"
```

## Sample tax identifier schema

The following shows the business tax identifier address schema for products ordered in Italy (`IT`) and sold through the Digital River Ireland Ltd. entity (`DR_IRELAND-ENTITY`).

The `type` validation keyword indicates that the tax identifier data will be verified as a JSON object.

The `taxIdentifier` key provides a `pattern` keyword, consisting of a regular expression, that the input data must match.

The `required` validation keyword contains an empty array, indicating that no tax identifier is required for Italian businesses to place an online order. If an identifier were required, the array would contain `\"taxIdentifier\"`.

```
"businessTaxIdentifiersSchemas": ["{
    \"$schema\":\"http://json-schema.org/draft-07/schema#\",
    \"title\":\"it\",
    \"description\":\"VAT ID for Italy (Business)\",
    \"type\":\"object\",
    \"properties\":{
        \"taxIdentifier\":{
            \"type\":\"string\",
            \"pattern\":\"^IT\\\\d\\\\d\\\\d\\\\d\\\\d\\\\d\\\\d\\\\d\\\\d\\\\d\\\\d$\"
        }
    },
    \"required\":[]
}"],
```
