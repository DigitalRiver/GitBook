---
description: Learn how to handle various cancel request scenarios.
---

# Cancel request process

You received a cancel request because of small timing issues when processing fulfillment notices and generating cancel requests. The following list describes how to handle various cancel request scenarios.

* Process a cancel request after you process a fulfillment request and before you process a Shipment Notice.
* When a cancel request contains incorrect product information, and you determine that the product was discontinued or inactive when matching the product information, accept the cancel request by sending a fulfillment notice with a status of `Cancelled`.
* If you already shipped an order, generated a `Shipped` message, and sent it to Digital River, you do not need to generate and send another message to Digital River. You can ignore the cancel request.&#x20;
* If you cannot honor a cancel request, send the fulfillment notice to Digital River with a status of `Shipped`, as you normally would for a shipped order. In this scenario, there is no need to deny a cancel request; if Digital River receives a fulfillment notice with a status of `Shipped`, we assume that you were not able to cancel the order or part of the order.
* When you accept the cancel request, you need to remove the values from the prices you display on the packing slip. You can take the values that were in the original fulfillment request sent to you, and add the prices on the cancel request. Since the cancel request prices are negative, the correct values will appear on the packing slip. If you don't add the prices to the cancel request, the prices appear as negative values.
* Digital River could send the requests so closely together that you might process them serially in the same block. For example, Digital River could send you one cancel request for part of the order and then send another cancel request for another part of the order. If you accept one cancel request and not the other, the new prices in the cancel request would not be accurate, depending on which cancel request you accepted. In this situation, do not send new prices for the packing slip when you accept a cancel request.
