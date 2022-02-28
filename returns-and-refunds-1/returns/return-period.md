---
description: Learn about the return period.
---

# Return period

Use the following formulas to determine if the product is within the return period:

| Product Type                              | Formula                              |
| ----------------------------------------- | ------------------------------------ |
| Physical                                  | Shipped Date + Return Period         |
| Physical and Nothing Required Return Type | Order Submitted Date + Return Period |
| Digital, Download                         | Order Submitted Date + Return Period |

Where:

* **Returned Period**—The maximum number of days from the Shipped Date or Order Submitted Date when a customer can return a product. The default is 30 days. Your Digital River representative can update the Returned Period at the site level. This information is not provided in the API. The Returned Period cannot be set at the product level.
* **Shipped Date**—The date on which the product shipped.
* **Order Submitted Date**—The date on which the digital download was submitted.
