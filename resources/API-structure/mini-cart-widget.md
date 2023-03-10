---
description: Understand how to use a Mini Cart widget.
---

# Mini cart widget

You can create a Mini Cart widget using javascript that runs on your website. The widget displays the contents of the cart to the shopper. You can choose to implement the Mini Cart widget with a public API key or a confidential API key. The Mini Cart widget initiates the Shopper APIs requests directly from a web browser using JSONP as the cross-domain solution. The Shopper APIs also support CORS.

The Mini Cart widget uses the following common Shopper APIs:

* `GET /oauth20/token`
* `POST v1/shoppers/me/carts/active?productId={​pid}​&quantity={​qty}`​&#x20;
* `POST v1/shoppers/me/carts/active/line-items?productId={​pid}​&quantity={​qty}`
* `GET v1/shoppers/me/carts/active`
* `POST v1/shoppers/me/carts/active/web-checkout`

##
