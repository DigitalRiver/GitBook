---
description: Understand the importance of providing an IP address in checkouts
---

# Providing the IP address

The  `browserIp`  you pass in [create](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts/operation/createCheckouts) or [update](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts/operation/updateCheckouts) checkout requests should represent the IP address of the browser used by the customer checking out.

By passing this data, you assist Digital River in its efforts to detect fraud and prevent [chargebacks](../../../order-management/returns-and-refunds-1/disputes-and-chargebacks.md). If you don't provide a `browserIp`, the effectiveness of our fraud prevention services are severely degraded.&#x20;
