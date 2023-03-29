---
description: Understand the 412 Precondition Failed error codes.
---

# 412 Precondition Failed

## `invalid-discount`

The value of the discount is invalid. The possible error descriptions are as follows:

* `The discount value is invalid. Provide a valid discount value and try again.`The discount value is invalid for one of the following reasons:
  * The value of `discount` is less than 0
  * The value of `discount` is over the maximum value of DOUBLE when `discountType` is `amountOff`.
  * The value of `discount` is greater than 100 when `discountType` is `percentOff`.

## `invalid-discount-type`

The value of the discount type is invalid. The possible error descriptions are as follows:

* `The offer discount type is invalid. Provide a valid offer discount type and try again.`The value of `discountType` shall be `amountOff` or `percentOff`.

## `invalid-product-id`

The product ID is invalid. The possible error descriptions are as follows:

* `The product ID or product external reference ID is invalid. Provide the correct product ID or product external reference ID and try again.`The product ID or product for external reference ID is invalid.

## `no-discount-or-type`

The validation failed for `discount` or `discountType`. The possible error descriptions are as follows:

* `Either the discount or discount type or both are missing. Include both the discount and discount type in the payload and try again.`Need to provide `discount` and `discountType`.
