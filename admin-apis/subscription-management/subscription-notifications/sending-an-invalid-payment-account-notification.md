---
description: Understand why a shopper's invalid payment account triggers a notification.
---

# Sending an invalid payment account notification

This notification triggers when the partnering bank returns a "Contact Customer" message for stolen or lost cards or an “Account Closed” message for deactivated accounts. See [Card Account Updater](card-account-updater.md) for more information. You need to contact the shopper to get updated information.

## Notification trigger

The following [Card Account Updater](card-account-updater.md) response codes from a reconciler job trigger this notification:

* `AccountClosed`
* `Contact`
