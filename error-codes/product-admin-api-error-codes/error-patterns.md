---
description: >-
  Learn about the use of the product, variation, and locale patterns in Admin
  API error codes.
---

# Error patterns

On occasion, when you submit a request, you may receive one or more errors for a product or the product's locale. This topic covers the key things you need to know to determine where the error occurred.&#x20;

[Global Commerce](https://gc.digitalriver.com/gc/ent/login.do) gives you the information you need to identify which product, product variation, or locale returned an error message.&#x20;

To identify the product or product variation, the error message will contain either the `Product` or `Variation`  prefix. If the error occurs at the locale level, the error message will contain the `locale-string` prefix.&#x20;

## Update existing product&#x20;

Product errors related to existing products or product variations combine the `Product` or `Variation` prefix, external reference identifier (`ERID`), and the product identifier (`productId`). For example:

* `Product [ERID]abc-1234 [productId]1912344500, en_US:` The error belongs to a specific product (`productId`) with a specific ERID, and locale.
* `Product [ERID]abc-1234 [productId]1912344500:` The error belongs to a specific product (`productId`) with a specific ERID.
* `Product [productId]1912344500, en_US:` The error belongs to a specific product (`productId`) and locale.
* `Product [ProductId]1912344500`: The error belongs to a specific product (`productId`) and has no ERID.

## Update existing product variation

* `Variation [ERID]abc-1234 [productId]1912344500, en_US`: The error belongs to a specific product variation (`productId`) with a specific ERID, and locale.
* `Variation [ERID]abc-1234 [productId]1912344500`: The error belongs to a specific product variation (`productId`) with a specific ERID.
* `Variation [productId]1912344500, en_US`: The error belongs to a specific product variation (`productId`) and locale.
* `Variation [productId]1912344500`: The error belongs to a specific product variation (`productId`) and has no ERID.

## Create product&#x20;

* `Product abc-1234, en_US`: The error belongs to a specific locale. The ERID exists in the product payload.
* `Product abc-1234`:  The error belongs to the product. The ERID exists in the product payload.
* `Product`:  The error belongs to the product. There is no ERID in the product payload.
* `Variation abc-1234, en_US`:  The error belongs to a specific locale. The ERID exists in the product variation payload.
* `Variation abc-1234`:   The error belongs to a specific product variation. The ERID exists in the product payload.

If you don't specify the `ERID` when creating a product, the prefix uses 1st, 2nd, 3rd, and 4th to distinguish the product variations. For example:

* `1st Variation, en_US`:  The error belongs to a specific locale associated with the first product variation. There is no ERID in the product payload.
* `2nd Variation`:  The error belongs to a specific locale associated with the second product variation. There is no ERID in the product payload.

### Create a product variation for an existing base product

* `Variation, en_US`:  The error belongs to a specific locale. There is no ERID in the product payload.
* `Variation`:  The error belongs to a specific product variation. There is no ERID in the product payload.
* `Variation abc-1234, en_US`:  The error belongs to a specific locale.  There is no ERID in the product payload.
* `Variation abc-1234`:  The error belongs to a specific base product or product variation. There is no ERID in the product payload.

## Deployment errors and warnings

{% hint style="info" %}
Deployment errors and warnings do not include the `ERID` or `Variation` pattern to remain consistent with Global Commerce errors and warnings.
{% endhint %}

* `Product 12345678, en_US`: The error belongs to a specific locale for a base product or product variation.&#x20;
* `Product 12345678`: The error belongs to a specific base product or product variation.&#x20;
