---
description: Learn how to get the order's details.
---

# Getting the order's details

Use the [`GET /v1/orders/{orderId}`](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Retrieve-Order/paths/\~1v1\~1orders\~1%7BorderId%7D/get) request to retrieve the order details for the specified order (`orderId`) for either anonymous or authenticated shoppers.&#x20;

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```http
curl --location --request GET 'https://api.digitalriver.com/v1/orders/{orderid}' \
--header 'authorization: basic ***\
...
```
{% endcode %}
{% endtab %}

{% tab title="200 OK response" %}
{% code overflow="wrap" %}
```json
{
    "id": "1110612650080",
    "totalItemsInCart": 3,
    "testOrder": false,
    "sendEmail": true,
    "locale": "en_US",
    "currency": "USD",
    "taxExempt": false,
    "shopperLoginType": "authenticated",
    "shopperId": "637326460289",
    "softDescriptor": "DRI*shopx1",
    "orderState": "In Process",
    "lineItems": [
        {
            "id": "51065820080",
            "quantity": 1,
            "lineItemState": "Pending Fulfillment",
            "product": {
                "id": "50540890080",
                "sku": "Ken test VP child physical",
                "displayName": "Ken test VP child physical",
                "systemProductName": "Ken test VP child physical"
            },
            "pricing": {
                "netPrice": {
                    "value": 50.0
                },
                "listPrice": {
                    "value": 50.0
                },
                "salePriceWithQuantity": {
                    "value": 53.76
                },
                "totalDiscountWithQuantity": {
                    "value": 0.0
                },
                "importTax": {
                    "value": 0.0
                },
                "importDuty": {
                    "value": 0.0
                }
            },
            "subscriptions": [],
            "downloads": [],
            "digitalRights": {}
        },
        {
            "id": "51065830080",
            "quantity": 1,
            "lineItemState": "Complete",
            "product": {
                "id": "50540860080",
                "sku": "Ken test VP child software",
                "displayName": "Ken test VP child software",
                "systemProductName": "Ken test VP child software"
            },
            "pricing": {
                "netPrice": {
                    "value": 500.0
                },
                "listPrice": {
                    "value": 500.0
                },
                "salePriceWithQuantity": {
                    "value": 537.63
                },
                "totalDiscountWithQuantity": {
                    "value": 0.0
                },
                "importTax": {
                    "value": 0.0
                },
                "importDuty": {
                    "value": 0.0
                }
            },
            "subscriptions": [],
            "downloads": [
                {
                    "downloadUri": "https://wgt-sys-ods.drextenv.net/wgt/9B5A4FCEF11DA80C/171F14235882A3D3DD49F67E037FAFB341840BE5728728C5B0585FF6616900300F64CFB0C1A417766F1089293F9604D4F5537E6263B95611ABDBF4E2F02512F3BC7716CC833ADA461CEC4F75E682DF6B97A693A7BBF30D56/shopx1/7.png"
                }
            ],
            "digitalRights": {}
        },
        {
            "id": "51065840080",
            "quantity": 1,
            "lineItemState": "Pending Fulfillment",
            "product": {
                "id": "5653222800",
                "sku": "Physical BackOrder",
                "displayName": "Physical BackOrder",
                "systemProductName": "Physical BackOrder"
            },
            "pricing": {
                "netPrice": {
                    "value": 50.0
                },
                "listPrice": {
                    "value": 100.0
                },
                "salePriceWithQuantity": {
                    "value": 53.76
                },
                "totalDiscountWithQuantity": {
                    "value": 50.0
                },
                "importTax": {
                    "value": 0.0
                },
                "importDuty": {
                    "value": 0.0
                }
            },
            "subscriptions": [],
            "downloads": [],
            "digitalRights": {}
        }
    ],
    "pricing": {
        "total": {
            "value": 655.9
        },
        "subTotal": {
            "value": 600.0
        },
        "subtotalWithDiscount": {
            "value": 600.0
        },
        "shippingAndHandling": {
            "value": 9.99
        },
        "discount": {
            "value": 50.0
        },
        "tax": {
            "value": 45.91
        },
        "importTaxAndDuty": {
            "value": 0.0
        },
        "fees": {
            "value": 0.0
        }
    },
    "businessEntityCode": "DR_INC-ENTITY",
    "paymentMethods": [
        {
            "name": "Visa",
            "displayableNumber": "************1111",
            "expirationMonth": "12",
            "expirationYear": "2034"
        }
    ],
    "shippingMethod": {
        "code": "265200",
        "description": null
    },
    "billingAddress": {
        "firstName": "Ken",
        "lastName": "Yeh",
        "line1": "10380 Bren Rd W",
        "city": "Minnetonka",
        "postalCode": "55343",
        "country": "US",
        "countryName": "United States",
        "phoneNumber": "9525555784",
        "emailAddress": "kenyeh@digitalriver.com",
        "countrySubdivision": "MN"
    },
    "shippingAddress": {
        "firstName": "Ken",
        "lastName": "Yeh",
        "line1": "10380 Bren Rd W",
        "city": "Minnetonka",
        "postalCode": "55343",
        "country": "US",
        "countryName": "United States",
        "phoneNumber": "9525555784",
        "emailAddress": "kenyeh@digitalriver.com",
        "countrySubdivision": "MN"
    },
    "taxInclusive": false,
    "submissionDate": "2023-02-02T06:48:50.000Z"
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

{% hint style="info" %}
The `GET /v1/orders/{orderId}` differs from the [`GET /v1/shoppers/me/orders/{orderId}`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Orders/paths/\~1v1\~1shoppers\~1me\~1orders\~1%7BorderId%7D/get) in the following ways:

* `GET /v1/orders/{orderId}` requires an admin key/secret to fetch the order information, regardless of whether an authenticated or anonymous shopper placed the order.
* `GET /v1/shoppers/me/orders/{orderId}` requires a shopper token to fetch the order information.
{% endhint %}
