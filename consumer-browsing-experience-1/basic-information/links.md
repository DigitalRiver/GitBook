---
description: Understand how the Shoppers resource includes links.
---

# Links

Most responses from the [Shoppers ](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Shoppers)resource include links that indicate related resources or the next action that could be performed. For example, after getting categories or products, the following URI link adds a product to the cart:

{% tabs %}
{% tab title="JSON" %}
{% code overflow="wrap" %}
```javascript
{
	"addproducttocart": {
		"_uri": "https://api.digitalriver.com/v1/shoppers/me/carts/active/line-items?productId=8350200"
	}
}
```
{% endcode %}
{% endtab %}
{% endtabs %}
