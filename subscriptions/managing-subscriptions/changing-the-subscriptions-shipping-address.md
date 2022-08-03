---
description: Learn how to change the subscription's shipping address.
---

# Changing the subscription's shipping address

The following [`POST /v1/subscriptions/{subscriptionId}/ship-to-address`](https://www.digitalriver.com/docs/commerce-api-reference/#operation/modifyShippingAddress) request changes the subscription's shipping address. You need to provide the `subscriptionId` and provide the updated [address information](../../cart/creating-or-updating-a-cart/providing-address-information.md#basic-address-information).

{% tabs %}
{% tab title="cURL" %}
```javascript
curl --location --request POST 'https://{host}/v1/subscriptions/{subscriptionId}/ship-to-address' \
--header 'Content-Type: application/json' \
--header 'Authorization: Basic ****' \
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
{% endtab %}
{% endtabs %}

You will receive a `202 Accepted` response.
