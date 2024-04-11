---
description: Learn how to set a purchase location.
---

# Setting the purchase location

{% hint style="warning" %}
The purchase location feature is scheduled to be deprecated in a future version.
{% endhint %}

In the [Checkouts](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) resource, you can provide a `purchaseLocation` that generates a useful tax estimate for customers. The data contained in the object, along with [other values](tax-calculations.md), allows Digital River to estimate taxes on an order.

Use `purchaseLocation` when customers have yet to supply the [address-related information required](providing-address-information.md#address-related-requirements) to successfully create an order.

You can use the following parameters to define a purchase location:

| Parameter    | Optional/Required                                             | Description.                                                                             |
| ------------ | ------------------------------------------------------------- | ---------------------------------------------------------------------------------------- |
| `country`    | Required                                                      | An [ISO 3166-1 alpha-2](https://en.wikipedia.org/wiki/ISO\_3166-1\_alpha-2) country code |
| `state`      | Optional                                                      | The state, county, province, or region                                                   |
| `postalCode` | Optional (except for purchase locations in the United States) | ZIP or postal code                                                                       |

## Using purchase location to get a tax estimate

A purchase location can generate a tax estimate when the customer has not yet provided a shipping or billing address. The following shows two simple `POST/checkouts` requests, with and without a specified `purchaseLocation`:

{% hint style="info" %}
You're only required to provide a `postalCode` for purchase locations within the United States.
{% endhint %}

{% tabs %}
{% tab title="curl (no purchaseLocation provided)" %}
```
curl --location --request POST 'https://api.digitalriver.com/checkouts' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer <API_key>' \
--header 'Content-Type: text/plain' \
--data-raw '{
    "currency": "USD",
    "items": [
        {
            "skuId": "05081978",
            "price": 100.00,
            "quantity": 1
        }
    ]
}'
```
{% endtab %}

{% tab title="curl (purchaseLocation provided)" %}
```
curl --location --request POST 'https://api.digitalriver.com/checkouts' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer <API_key>' \
--header 'Content-Type: text/plain' \
--data-raw '{
    "currency": "USD",
    "items": [
        {
            "skuId": "05081978",
            "price": 100.00,
            "quantity": 1
        }
    ],
    "purchaseLocation": {
        "country": "US",
        "state": "MN",
        "postalCode": "55116"
    }    
}'
```
{% endtab %}
{% endtabs %}

When the `purchaseLocation` is provided, the response returns a tax estimate at both the line item and checkout level:

{% tabs %}
{% tab title="JSON (no purchaseLocation provided)" %}
```javascript
{
    "id": "177375830336",
...
    "totalAmount": 100.0,
    "subtotal": 100.0,
    "totalFees": 0.0,
    "totalTax": 0.0,
    "totalDuty": 0.0,
    "totalDiscount": 0.0,
    "totalShipping": 0.0,
    "items": [
        {
            "skuId": "05081978",
            "amount": 100.0,
            "quantity": 1,
            "tax": {
                "rate": 0.0,
                "amount": 0.0
            }
        }
    ],
    "purchaseLocation": {
        "country": "US",
        "state": "MN",
        "postalCode": "55116"
    },
...
}
```
{% endtab %}

{% tab title="JSON (purchaseLocation provided)" %}
```javascript
{
    "id": "177374720336",
...
    "totalAmount": 107.88,
    "subtotal": 100.0,
    "totalFees": 0.0,
    "totalTax": 7.88,
    "totalDuty": 0.0,
    "totalDiscount": 0.0,
    "totalShipping": 0.0,
    "items": [
        {
            "skuId": "05081978",
            "amount": 100.0,
            "quantity": 1,
            "tax": {
                "rate": 0.07875,
                "amount": 7.88
            }
        }
    ],
    "purchaseLocation": {
        "country": "US",
        "state": "MN",
        "postalCode": "55116"
    },
...
}
```
{% endtab %}
{% endtabs %}

### Use case: Storefronts with mostly domestic customers

Your company is located in Italy and the vast majority of your storefront customers are Italians. By specifying `country`, you can give them an initial tax estimate before they provide a [ship to or billing address](providing-address-information.md#ship-to-address).

### Use case: Different postal code values in the United States

For purchase within the United States, you might need to provide tax estimates for different delivery postal codes. The following two `POST/checkouts` requests specify different `postalCode` values in the `purchaseLocation` hash table:

{% tabs %}
{% tab title="Postal Code: 95969" %}
```
curl --location --request POST 'https://api.digitalriver.com/checkouts' \
--header 'Authorization: Bearer <API_key>' \
--header 'Content-Type: text/plain' \
--data-raw '{
     "currency": "USD",
     "items": 
     [ 
        {
          "skuId": "09062016",
          "price": 10.00
        },
        {
          "skuId": "11141976",
          "price": 10.00
        }
    ],
    "purchaseLocation": 
    {
          "country": "US",
          "postalCode": "95969"
    }
}'
```
{% endtab %}

{% tab title="Postal Code: 55343" %}
```
curl --location --request POST 'https://api.digitalriver.com/checkouts' \
--header 'Authorization: Bearer <API_key>' \
--header 'Content-Type: text/plain' \
--data-raw '{
     "currency": "USD",
     "items": 
     [ 
        {
          "skuId": "09062016",
          "price": 10.00
        },
        {
          "skuId": "11141976",
          "price": 10.00
        }
    ],
    "purchaseLocation": 
    {
          "country": "US",
          "postalCode": "55343"
    }
}'
```
{% endtab %}
{% endtabs %}

The responses show how the initial tax estimate provided to the customer is affected by the `postalCode`. This is because different `tax.rate` values are used to compute taxes:

{% tabs %}
{% tab title="Postal Code: 95969" %}
```javascript
{
...
    "totalAmount": 21.56,
    "subtotal": 20.0,
    "totalFees": 0.0,
    "totalTax": 1.56,
    "totalDuty": 0.0,
    "totalDiscount": 0.0,
    "totalShipping": 0.0,
    "items": [
        {
            "skuId": "09062016",
            "amount": 10.0,
            "quantity": 1,
            "tax": {
                "rate": 0.0775,
                "amount": 0.78
            }
        },
        {
            "skuId": "11141976",
            "amount": 10.0,
            "quantity": 1,
            "tax": {
                "rate": 0.0775,
                "amount": 0.78
            }
        }
    ],
    "locale": "en_US",
    "purchaseLocation": {
        "country": "US",
        "postalCode": "95969"
    },
...
}
```
{% endtab %}

{% tab title="Postal Code: 55343" %}
```javascript
{
...
    "totalAmount": 21.5,
    "subtotal": 20.0,
    "totalFees": 0.0,
    "totalTax": 1.5,
    "totalDuty": 0.0,
    "totalDiscount": 0.0,
    "totalShipping": 0.0,
    "items": [
        {
            "skuId": "09062016",
            "amount": 10.0,
            "quantity": 1,
            "tax": {
                "rate": 0.07525,
                "amount": 0.75
            }
        },
        {
            "skuId": "11141976",
            "amount": 10.0,
            "quantity": 1,
            "tax": {
                "rate": 0.07525,
                "amount": 0.75
            }
        }
    ],
    "locale": "en_US",
    "purchaseLocation": {
        "country": "US",
        "postalCode": "55343"
    },
...
}
```
{% endtab %}
{% endtabs %}
