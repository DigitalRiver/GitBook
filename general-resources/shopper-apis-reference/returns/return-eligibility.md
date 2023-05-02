---
description: Learn when line items are not eligible for return.
---

# Return eligibility

Line items are not eligible for return when:&#x20;

* The site is not configured to allow self-service returns.
* The shopper previously returned the entire quantity for the line item.
* A satisfaction refund was already applied to the line item.
* A satisfaction refund was already applied to the order.
* The line item is outside the configured return window specified in the site settings by the API consumer.&#x20;
* The line item is not in a state that is compatible with a return to occur (for example, complete).
* The order is in a state that is not eligible for a return.
* The quantity the shopper wants to return is greater than the available quantity.
* The line item is a subscription type.
