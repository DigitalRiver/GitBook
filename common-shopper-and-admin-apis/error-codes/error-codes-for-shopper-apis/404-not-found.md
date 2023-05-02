---
description: 404 Not Found Understand the 404 Not Found error codes.
---

# 404 Not Found

## `duplicate_offer_identifier`

The system gets duplicated offer identifiers (offer ID or offer external reference ID) from the request. The possible error descriptions are as follows:

* `Use either offer ID or offer external reference ID in the Applied Offers payload and try again.`\
  Provide either the offer ID or the offer external reference ID. You cannot provide both.

## `duplicate_product_identifier`

The system gets duplicated product identifiers (product ID or product external reference ID) from the request. The possible error descriptions are as follows:

*   `Use either product ID or product external reference ID in the Applied Offers payload and try again.`

    Provide either the product ID or the product external reference ID. You cannot provide both.

## `invalid-offer-id`

The offer ID for the request is invalid. The possible error descriptions are as follows:

* `The offer ID: {offerID} for the request is invalid. Provide a valid offer ID or Offer external reference ID and try again.`The offer ID for the request is invalid.
* `The offer external reference ID: {offerId} for the request is invalid. Provide a valid offer ID or Offer external reference ID and try again.` The external reference ID for the request is invalid.

## `no-offer-identifier`

The system cannot get an offer identifier (offer ID or offer external reference Id) from the request. The possible error descriptions are as follows:

* `The offer ID or offer external reference ID is missing. Provide the offer ID or external reference ID and try again.`Provide the offer ID or external reference ID.
* `Use either offer ID or offer external reference ID in the Applied Offers payload and try again.`Provide either the offer ID or the external reference ID. You cannot provide both.

## `no-product-identifier`

The system cannot get the product identifier (product ID or external reference ID) from the request. The possible error descriptions are as follows:

* `The product ID or product external reference ID is missing. Provide the product ID or external reference ID and try again.`Provide the product ID or product external reference ID.

## `resource-not-found`

Could not find a \[resourceName] resource with an internal ID \[resourceId]. The possible error descriptions are as follows:

* `A Cart identifier for the provided value of \"298407701971\" is not valid.` The cart identifier (`cartId`) is not valid. Provide the correct value for the `cartId` and try again.
*   `Could not find a Line Item with an id of {line item id}`

    The system could not find the line item for the provided ID.
*   `Could not find an Order with an id of {orderId}`

    The system could not find the order for the provided ID.
* `Invalid site for specified company`\
  The company of the site with the provided header `siteId` and the one with the provided header `companyId` are different, but they should be the same.
* `offer-not-found`\
  The specified offer identifier (`offerId`) was not applied to the cart.

