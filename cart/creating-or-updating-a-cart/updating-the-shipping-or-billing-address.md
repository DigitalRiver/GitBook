---
description: Learn how to update the shipping or billing address.
---

# Updating the shipping or billing address

You can update a customer's billing or shipping address by incuding the billing address (`billingAddress`) or shipping address (`shippingAddress`) object in the payload..

{% code title="Request example" overflow="wrap" %}
```html
curl --location -g --request POST ' https://api.digitalriver.com/v1/shoppers/me/carts/active?expand=all' \
--header 'Accept: application/json' \
--header 'Authorization: bearer {{access_token}}' \
--header 'Content-Type: application/json' \
```
{% endcode %}

{% code title="Payload example" overflow="wrap" %}
```json
{
    "cart": {
        "billingAddress": {
            "uri": https://api.digitalriver.com/v1/shoppers/me/address/47278020023,
            "relation": https://developers.digitalriver.com/v1/shoppers/AddressesResource,
            "id": "billingAddress",
            "firstName": "Automation",
            "lastName": "Tester",
            "companyName": "Digital River",
            "line1": "PO BOX 6930",
            "line2": "123",
            "line3": "Suite Line 3",
            "city": "Waconia",
            "countrySubdivision": "MN",
            "postalCode": 5387,
            "country": "US",
            "countryName": "United States",
            "phoneNumber": "099-222-44454",
            "emailAddress": kenyeh@digitalriver.com,
            "countyName": "Hennepin",
            "phoneticFirstName": "クリス",
            "phoneticLastName": "ミラー",
            "division": "製品開発"
        },
        "shippingAddress": {
            "uri": https://api.digitalriver.com/v1/shoppers/me/address/47278020023,
            "relation": https://developers.digitalriver.com/v1/shoppers/AddressesResource,
            "id": "shippingAddress",
            "firstName": "Automation",
            "lastName": "Tester",
            "companyName": "Digital River",
            "line1": "PO BOX 6930",
            "line2": "123",
            "line3": "Suite Line 3",
            "city": "Waconia",
            "countrySubdivision": "MN",
            "postalCode": 5387,
            "country": "US",
            "countryName": "United States",
            "phoneNumber": "099-222-44454",
            "countyName": "Hennepin",
            "emailAddress": automatedTester@digitalriver.com,
            "phoneticFirstName": "クリス",
            "phoneticLastName": "ミラー",
            "division": "製品開発"
        },
        "termsOfSalesAcceptance": "true",
        "chargeType": "moto",
        "organizationId": "digitalriver12345"
    }
}
```
{% endcode %}

&#x20;
