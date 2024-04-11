---
description: Learn how to manage returns coordinated by Digital River and third-parties.
---

# Return basics

How you manage returns depends on whether [Digital River coordinates the process](./#digital-river-coordinated-returns) or whether you've [assigned a third party to manage your returns](./#third-party-coordinated-returns).

## Digital River coordinated returns

In [Digital River coordinated returns](digital-river-coordinated-returns.md), you use the [Fulfillment Returns API](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Fulfillment-Returns) to initiate the return process. Before creating a fulfillment return, you should ensure the relevant items have shipped. And before you [issue any refunds](../refunds/issuing-refunds.md), make sure you've received the return accepted event.

## Third party coordinated returns

In [third party coordinated returns](creating-a-return.md), you can use the [Returns API](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Returns) to notify Digital River of authorized and accepted returns. Once an authorized return is fully accepted, Digital River generates a refund.
