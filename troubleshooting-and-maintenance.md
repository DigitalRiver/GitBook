---
description: >-
  Understand how to troubleshoot and maintain the Digital River Extension for
  Magento.
---

# Troubleshooting and maintenance

## Error handling&#x20;

The Digital River Extension for Magento invokes an exception for all returned **400** and **500** response statuses. If you set Enable debug logging to **Yes**, all exceptions are logged.

### Order purchase flow exception handling

#### Shopper and cart created:

* `400 invalid-request`–The DrPay extension will ensure a proper payload.
* `409 resource-already-exists`–For a guest checkout, the DrPay extension will create a new Digital River shopper each time to avoid a conﬂict. All users created will be created first in Magento and then in Digital River. If DrPay creates a user in Magento without creating a user in Digital River, an error occurs when the shopper attempts to use a stored credit card the second time through the order ﬂow. If DrPay did not use a saved cart, then Digital River will try to create the user during their next purchase.
* `500 Unable-to-place-order`–The shopper will not be able to check out and will encounter a fatal error when attempting to place their order. They will see the following error message: `Unable to Place Order`.

#### Payment authorized:

* `400 Unable to Place Order`–All payment authorization failures will display this message.
* `409 invalid_token`–If the token is invalid for any reason during the checkout, an error will occur while trying to place their order.
* `500 Unable to Place Order`–Service unavailable will result in an error message.
