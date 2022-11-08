---
description: Learn how to handle various Cancel Request scenarios.
---

# Cancel Request process

The following list describes how to handle various Cancel Request scenarios.

* Process a Cancel Request after you process a Fulfillment Request and before you process a Shipment Notice.
* When a Cancel Request contains incorrect product information, and you determine that the product was discontinued or inactive when matching the product information, accept the Cancel Request by sending a Fulfillment Notice with a status of Cancelled.
* If you already shipped an order, generated a Shipped message, and sent it to Digital River, you do not need to generate and send another message to Digital River. You can ignore the Cancel Request. You received a Cancel Request because of small timing issues when processing Fulfillment Notices and generating Cancel Requests.
* If you cannot honor a Cancel Request, send the Fulfillment Notice to Digital River with a status of Shipped, as you normally would for a shipped order. In this scenario, there is no need to deny a Cancel Request; if Digital River receives a Fulfillment Notice with a status of Shipped, we assume that you were not able to cancel the order or part of the order.
* When you accept the Cancel Request, you need to remove the values from the prices you display on the packing slip. You can take the values that were in the original Fulfillment Request sent to you, and add the prices on the Cancel Request. Since the Cancel Request prices are negative, the correct values will appear on the packing slip. If you don't add the prices to the Cancel Request, the prices appear as negative values.
* Digital River could send the requests so closely together that you might process them serially in the same block. For example, Digital River could send you one Cancel Request for part of the order and then send another Cancel Request for another part of the order. If you accept one Cancel Request and not the other, the new prices in the Cancel Request would not be accurate, depending on which Cancel Request you accepted. In this situation, do not send new prices for the packing slip when you accept a Cancel Request.
