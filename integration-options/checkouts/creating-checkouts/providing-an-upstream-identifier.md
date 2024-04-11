---
description: Understand the purpose of specifying an upstream identifier.
---

# Providing an upstream identifier

The `upstreamId` can be any identifier that you want to associate with a [Checkout](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts), [Invoice](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Invoices), or [Order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders). Unlike metadata, you can use this value as a query parameter in `GET` requests.

For tracking purposes, we recommend you provide the universally unique identifier (UUID) that clients use to identify the corresponding order in their system.
