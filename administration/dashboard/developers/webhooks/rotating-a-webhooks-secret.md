---
description: Learn how to rotate a webhook's secret.
---

# Rotating a webhook's secret

You can rotate a webhook's secret in your [Digital River Dashboard](https://dashboard.digitalriver.com) if you think a webhook's secret is compromised. When you rotate the secret, the Dashboard blocks the old secret and generates a new one. You can choose to block the old secret immediately or allow it to expire after the specified expiration time when you rotate the secret. During that specified expiration time, both secrets work. It gives you time to make the transition from the old secret to the new secret. In either case, you can use the new secret immediately.

To rotate a webhook's secret:

1. From the **Webhooks** page on the [Dashboard](https://dashboard.digitalriver.com), click **More options** (vertical ellipses) associated with the key you want to rotate and click **Rotate**.\
   ![](<../../../../.gitbook/assets/editrotatedeletewebhook (1) (2) (1) (3).png>)
2. Choose the expiration time from the **Choose expiration** list.\
   ![](../../../../.gitbook/assets/RotateWHSigSecret.png)
3. Enter your password and click **Rotate webhook signature secret**. The Webhooks page will display signing secret and **New** next to the modified webhook.

<div align="left">

<img src="../../../../.gitbook/assets/WebhooksRotateSecret.png" alt="">

</div>