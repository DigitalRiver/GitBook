---
description: Learn how to redirect to a Digital River-hosted cart.
---

# Redirecting to a Digital River-hosted cart

To overcome the PCI liability, you can use the [`GET /v1/shoppers/me/carts/active/web-checkout`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Web-Checkout/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1web-checkout/get) resource to transfer a customer to your Digital River-hosted checkout pages. This endpoint returns a 302 redirect with the appropriate location of the shopping cart.

{% hint style="danger" %}
**Required**: A session-aware token is required to ensure continuity between the API cart and the Digital River-hosted checkout.
{% endhint %}

Upon successful redirection, the customer will complete their order on your Digital River-hosted checkout pages.
