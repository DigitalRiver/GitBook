---
description: Learn how to set up returns in Global Commerce.
---

# Setting up returns in Global Commerce

The following topics explain how to set up Global Commerce for the Returns API.

### API endpoints

The API consumer interacts with the API through the following endpoints:

* Production (PROD): https://api.digitalriver.com
* Client Test Environment (CTE): https://api-cte-ext.digitalriver.com

PROD and CTE require your API key and secret (if applicable).

### Setting up your site in Global Commerce

You must enable your site for self-service returns. To enable this feature, contact your Digital River Account Representative.

### Returns API and the Customer Service return functionality

The Returns API has parity with the Customer Service return functionality in Global Commerce. You can expose the Returns API to initiate a return from a non-Digital River hosted page. Once the return has been accepted, the backend processing runs as expected. The Returns API does not provide additional functionality that is not supported in Global Commerce.

{% hint style="info" %}
**Example**: If a shopper purchases multiple quantities of the same PID (product identifier) or SKU (stock keeping unit) that has a unique identifier such as an IMEI (International Mobile Equipment Identity), Global Commerce does not allow a Customer Service Representative to select which IMEI the customer can return. Therefore, this is not supported in the Returns API as downstream processing will be affected.
{% endhint %}
