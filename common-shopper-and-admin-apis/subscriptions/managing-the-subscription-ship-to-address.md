---
description: Learn how to change the subscription's shipping address.
---

# Managing the subscription ship to address

The following [`POST /v1/subscriptions/{subscriptionId}/ship-to-address`](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Address/operation/modifyShippingAddress) request changes the subscription's shipping address. You need to provide the subscription identifier (`subscriptionId`) and provide the updated [address information](../../shopper-apis/cart/creating-or-updating-a-cart/providing-address-information.md#basic-address-information). See the [ship-to-address](../../general-resources/common-shoppers-and-admin-apis-reference/subscriptions/#ship-to-address-resource) resource for more information.

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```javascript
curl --location --request POST 'https://{host}/v1/subscriptions/{subscriptionId}/ship-to-address' \
--header 'Authorization: Basic ****' \
...
--data-raw '{
    "firstName": "Jane", 
    "lastName": "Doe", 
    "companyName": "Acme Company", 
    "line1": "1234 Fake Street",
    "line2": "Apt. 2", 
    "line3": null, 
    "city": "Minnetonka",
    "countrySubdivision": "MN", 
    "postalCode": "55343", 
    "country": "US", 
    "phoneNumber": "555-253-1234", 
    "countyName" : null, 
    "emailAddress": "jdoe@acme.com" 
}'
```
{% endcode %}
{% endtab %}
{% endtabs %}

You will receive a `202 Accepted` response.
