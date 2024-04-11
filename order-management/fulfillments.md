---
description: >-
  Learn how to manage Digital River coordinated fulfillments and third-party
  coordinated fulfillments
---

# Fulfilling goods and services

Digital River offers numerous fulfillment-related APIs. The specific APIs that you use, and the sequence that you use them in, depends on whether a [third party coordinates product fulfillment](fulfillments.md#third-party-coordinated-fulfillments) or [Digital River manages the fulfillment process](fulfillments.md#digital-river-coordinated-fulfillments).

## Third-party coordinated fulfillments

If you have a third-party fulfillment system in place, meaning Digital River does not orchestrate the delivery of your goods, then the [Fulfillments API](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Fulfillments) is what you'll primarily use to handle an order's fulfillment.

For every order, by [submitting one or more `POST/fulfillments` requests](informing-digital-river-of-a-fulfillment.md), you're informing Digital River which products, and in what quantity, have been fulfilled or cancelled. Depending on the data you provide, we then attempt to [capture](../developer-resources/digital-river-api-reference/payment-charges.md#captures) or [cancel](../developer-resources/digital-river-api-reference/payment-charges.md#cancels) the appropriate [payment charge](../developer-resources/digital-river-api-reference/payment-charges.md).

For third-party coordinated fulfillments, the following diagram outlines the major steps in creating, processing, and delivering orders to customers that contain physical and digital goods.

![](<../.gitbook/assets/Fulfillment-flow (1).png>)

## Digital River managed fulfillments <a href="#digital-river-coordinated-fulfillments" id="digital-river-coordinated-fulfillments"></a>

Refer to the [Digital River coordinated fulfillments](../integration-options/checkouts/handling-digital-river-coordinated-fulfillments/) page.
