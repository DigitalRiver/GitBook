---
description: Learn how to create and update a regulatory fee for a product.
---

# Managing regulatory fees

Once you determine that your product has a required [regulatory fee](./), you'll need to [describe its attributes](managing-regulatory-fees.md#setting-fee-attributes) and then [create the Fee resource](managing-regulatory-fees.md#creating-a-fee).

## Setting fee attributes

{% hint style="warning" %}
In versions `2020-09-30` and earlier, you can set the `visible` boolean parameter in [create](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createFees) and [update](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/updateFees) Fee requests. In later versions, all [fees are visible](managing-regulatory-fees.md#displaying-fees) to customers.
{% endhint %}

Every Fee must have a [type](managing-regulatory-fees.md#type) and be [associated with a SKU](managing-regulatory-fees.md#sku-identifier). You also need to define its [category](managing-regulatory-fees.md#category), [value](managing-regulatory-fees.md#value), amount, currency, and [country](managing-regulatory-fees.md#country-and-subdivisions). A full list of specifications is available on the [Fees API reference page](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Fees).

### Type

You're required to provide the `type` of fee. The enumerated fee types are `battery`, `weee`, `copyright`, `e_waste`, and `packaging`.

You should use `weee` if you're creating a regulatory fee for [electronic waste](managing-regulatory-fees.md#weee) in the EU, and specify `e-waste` for similar products in the United States.

When you create a Fee for a [battery](managing-regulatory-fees.md#battery) or [WEEE](managing-regulatory-fees.md#weee), you can include a hash table that corresponds to the specified `type`. For example, a `POST/fees` request with a `type` of `battery` can contain a `battery` hash table. The child parameters of this data structure pass in more detailed information about the fee, which is used for reporting purposes.

```
curl --location --request POST 'https://api.digitalriver.com/fees' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer <API_key>' \
--data-raw '{
    "type": "battery",
    "battery":{
        "quantity": 2,
        "chemicalSystem": "Alkaline",
        "iecCode": "R20" 
    },
    ...
}'
```

#### Battery

Battery fees are designed to make entities that produce and sell batteries responsible for collecting recycling fees on depleted batteries and then remitting these fees to a recycling entity. For EU compliance purposes, Digital River requires that you specify `quantity`, `chemicalSystem`, and `iecCode`.

The `quantity` parameter indicates the number of batteries within the product.

Example `chemicalSystem` values include `Alkaline`, `Nickel Cadium`, `Lithium Ion`, and`Lithium Polymer`.

The `iecCode` is an alphanumeric value that describes the battery's electrical and physical attributes. The letters and numbers in the code indicate the number of cells, cell chemistry, shape, dimensions, the number of parallel paths in the assembled battery and any modifying letters deemed necessary. A multi-section battery (two or more voltages from the same package) has a multi-section designation. Example codes include `R20`, `4R25X`, `4LR25-2`, `6F22`, `6P222/162`, `CR17345` and `LR2616J`.

#### WEEE

Fees with a type of `weee` represent waste electrical and electronic equipment.

The `weee` hash table only contains the `weeeRegistrationID` parameter. This registration number indicates the [compliance agency](managing-regulatory-fees.md#compliance-agency). Various jurisdictions require this number to be displayed to the customer on your storefront. Additionally, products associated with a WEEE fee need to provide this identifier in the invoice.

### SKU identifier

Each Fee must be associated with a [SKU](../skus.md#skus). You do this by providing the [unique identifier of a SKU](../creating-and-updating-skus.md#unique-identifier) in a `POST/fees` or `POST/fees/{id}`. A single SKU can be associated with one or more Fees.

![](<../../.gitbook/assets/image (4) (1).png>)

### Category

The `category` parameter represents the category of the SKU as defined by regulatory law (e.g., `3. IT and Telecommunication Equipment`).

The categories are defined by and vary greatly by jurisdiction. Each product requires a category in order to facilitate compliance reporting.

Your \_\*\*\_Digital River Tax Manager can help you identify the product's category.

### Value

The `value` parameter identifies the product type as well as various product attributes (e.g., `5" Class Q900 QLED Smart 8K UHD TV`).

### Compliance Agency

The compliance agency represents the regulatory arm of the government that administers a country’s fee mandates. The compliance agency also coordinates the recycling of physical goods and maintains recycling statistics.

When a producer registers with a compliance scheme, they complete the registration process with a compliance agency.

You should supply a unique identifier for the recycling agency associated with the product's jurisdiction. This alphanumeric identifier is used for reporting purposes.

### Fee Exemption

This parameter indicates whether business to business sales are exempt from paying the fee. If the customer is exempt (assuming a valid VAT identifier is provided) then you should specify a value such as exempt. A non-exempt specification would mean the sale is not exempt from fees.

### Brand Name

The `brandName` of the product is typically the name as shown on the product itself (e.g., Jabra, Sony, AMD).

In many countries, this value is required for reporting purposes. This is true because many vendors sell products other than their own brand. As an example, Logitech sells Jaybird products.

### Weight and units

The `weightAndUnits` parameter represents both the weight of the unit, minus packaging or batteries, and the unit of measurement applied to the weight.

Weights and units are required for [WEEE](managing-regulatory-fees.md#weee), [battery](managing-regulatory-fees.md#battery), and packaging reporting.

The value must be formatted as one number representing the weight plus a white space plus the weight unit (for example, `1.73 kilogram`). Furthermore, it must conform to the following regular expression: `\d{1,16}\s.{1,64}|\d{1,16}\.\d{1,2}\s.{1,64}`.

### Country and subdivisions

For the `country`, you must provide a two-letter [Alpha-2 country code](https://www.iban.com/country-codes) as described in the [ISO 3166](https://www.iso.org/iso-3166-country-codes.html) international standard.

The optional `subdivisions`consists of an array of [ISO 3166-2 subdivision codes](https://www.iso.org/standard/63546.html).

## Creating a fee

Perform the following steps to create a regulatory fee for a product:

1. [Create the SKU](../creating-and-updating-skus.md) that requires a fee and retrieve its [unique identifier](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createSkus).
2. Consult with your Customer Success or Account Manager regarding how to configure the product's fees.
3. In a `POST/fees` request, specify the associated `skuId`, along with the other [required and optional parameters](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createFees).

The following `POST/fees` request indicates the fee pertains to [WEEE](managing-regulatory-fees.md#weee):

{% tabs %}
{% tab title="cURL" %}
```
curl --location --request POST 'https://api.digitalriver.com/fees' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer <API_key>' \
--data-raw '{
    "type": "weee",
    "skuId": "f153fa2a-f442-4822-853a-c85b12a03490",
    "category": "OLED TVs.",
    "value": "85\" Class Q900 QLED Smart 8K UHD TV.",
    "amount": 1.75,
    "currency": "USD",
    "country": "ES",
    "complianceAgency": "Test compliance agency",
    "feeExemption": "Test fee exemption",
    "brandName": "Test brand name",
    "weightAndUnits": "100 kilograms"
}'
```
{% endtab %}
{% endtabs %}

A `201 Created` response returns a [Fee object](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Fees) with a unique identifier. The Fee is associated with a SKU:

```javascript
{
    "id": "fee_1b54665d-d38b-4ad7-afbb-8014608e6031",
    "skuId": "f153fa2a-f442-4822-853a-c85b12a03490",
    "category": "OLED TVs.",
    "value": "85\" Class Q900 QLED Smart 8K UHD TV.",
    "amount": 1.75,
    "complianceAgency": "Test compliance agency",
    "feeExemption": "Test fee exemption",
    "brandName": "Test brand name",
    "weightAndUnits": "100 kilograms",
    "currency": "USD",
    "country": "ES",
    "createdTime": "2020-09-09T23:42:31Z",
    "updatedTime": "2020-09-09T23:42:31Z",
    "type": "weee",
    "liveMode": false
}
```

## Displaying fees

Some jurisdictions require fee-exclusive pricing, which means any fees attached to a product must be displayed to the customer during the checkout process.

As a result, whenever we give you back a [Checkout](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts), [Order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders), or [Invoice](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Invoices) object, Digital River provides [aggregate](../../integration-options/checkouts/creating-checkouts/accessing-regulatory-fee-information.md#determining-the-aggregated-fee-amount) and [product-level](../../integration-options/checkouts/creating-checkouts/accessing-regulatory-fee-information.md#getting-information-on-specific-fees) fee information. This allows you to provide a detailed breakdown of the product's fees to your customers.

## Deleting a fee

There are two ways a Fee can be deleted. The approach you choose depends on whether you want to delete only the Fee object or whether you want to delete both the Fee and the [SKU it is associated with](managing-regulatory-fees.md#sku-identifier).

To delete only the Fee object, use the Fees API and pass its unique identifier in a [`DELETE/fees/{id}`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/deleteFees) request. This also removes the association between the Fee and the SKU it was attached to.

Fee objects are also deleted when the SKU it is associated with is deleted. So submitting a [delete SKU request](../creating-and-updating-skus.md#deleting-a-sku) using the SKUs API deletes both the SKU and all of its associated Fees.
