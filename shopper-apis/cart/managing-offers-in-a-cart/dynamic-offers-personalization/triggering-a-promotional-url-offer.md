---
description: Learn how to trigger a promotional URL offer.
---

# Triggering a promotional URL offer

This feature allows you to trigger a promotional URL offer type using an API call. This type of API offer mimics the triggering behavior of a promo URL offer using storefront links.

## High-level workflow

1. Apply an offer ID or ERID to a cart. This triggers Global Commerce's preconfigured offer behavior and provides the same functionality as the Promo URL for hosted storefronts.
2. The client sets up a Promotional URL-triggered offer in Global Commerce. The Cart API call triggers the offer and applies the discount with the Offer ID or ERID included in the call.
3. The system successfully applies the correct Promotional URL offer to the cart or product if the Promo URL wins among the offer arbitration.
