---
description: Understand the error handling and exception policy.
---

# Error handling and exception policy

## Exception handling

The Digital River Magento extension invokes an exception and logging for all 400 and 500 response statuses returned. The connector uses a try-and-catch exception policy. All 400 and 500 exceptions thrown via the DrPay extension are logged to the Magneto `system.log` in the `/var/log directory`. The application will not roll back and retry processing when an error or exception occurs unless a follow-on action is performed by the end shopper. Some system-to-system integrations that are not shopper-facing will include retry mechanisms.

All **EFS** (ElectronicFullfilmentService), **EFN** (ElectronicFulfillmentNotice), and **PON** (PostOrderNotification) failures (400s and 500s) will be retried automatically by the Magento and Digital River applications. These integrations are system-to-system and do not have a direct impact on the shopper checkout experience. 400 errors will be logged on Digital River’s application and will have operational alerts in place based on application and client thresholds. A failed EFS will have no impact on real-time and redirect payments; however, in the case of wire transfer, a failed EFS will result in a delay to shipment. A failed EFN can result in a delay in capturing the funds from the end shopper. Failed PONs will not impact the end shopper, but could delay the Magento application order status being updated. All PONs are triggered based on events initiated from the Digital River application and are intended to notify the OMS of the current order state to ensure the applications are in sync.
