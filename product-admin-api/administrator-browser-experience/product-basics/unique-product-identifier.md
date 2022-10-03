---
description: Understand the product identifier.
---

# Unique product identifier

## Product identifier

A product's unique identifier is represented by `id`. The product identifier value (`productID` or `PID`) is the product identifier or external reference identifier (`ERID`) associated with a product or product variaton.&#x20;

The `productId` or `PID` variable can be one of the following values:

* An [individual](product-types.md#individual-product), [base](product-types.md#base-product), or [product variation](product-types.md#product-variations) identifier
* The [external reference identifier (ERID)](unique-product-identifier.md#external-reference-identifier-erid)

A product identifier is the client's unique stock keeping unit (SKU) for a product.

## External reference identifier (ERID)

You can use an external reference ID (`externalReferenceID`) to refer to either a [product ](unique-product-identifier.md#using-an-external-reference-identifier-for-a-product)or a [customer](unique-product-identifier.md#using-an-external-reference-identifier-for-a-customer).&#x20;

### Best practices

If you want to use the [external reference identifier (ERID)](broken-reference) when creating or updating a product or product variation, we recommend that you:

* [Enable the Enforce Unique Value](unique-product-identifier.md#enabling-the-enforce-unique-value) when [configuring company settings](https://help.digitalriver.com/internal-help/gc/Administration/Company/Configuring-company-settings.htm) in Global Commerce. When the Enforce Unique Value is enabled, duplicate ERIDs are not allowed. This ensures that you won't accidentally provide an ERID that would result in duplicate products in the response if you [searched for a product by ERID](broken-reference).
* Use the `x-erid-as-pid-true` in your HTTP requests.&#x20;
* Use unique ERIDs for both the base product and its product variations. Don't use both ERIDs and product identifiers when creating a base product with product variations.

### Enabling the Enforce Unique Value

To enable the Enforce Unique Value:

1. Sign in to Global Commerce.
2. Select **Administration**, select **Company**, and then click **Configure Company Settings**. The Configure Company Settings page appears.
3. Scroll down to **Product External Reference Number** and select **Yes** next to **Enforce Unique Value**.\
   <img src="../../../.gitbook/assets/Enforce Unique Value.png" alt="Enforce Unique Value" data-size="original">
4. Click **Save**.

