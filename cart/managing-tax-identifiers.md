---
description: Learn how to manage tax identifiers.
---

# Managing tax identifiers

Specifying a [customer's type](managing-tax-identifiers.md#customer-type), as well as adding any [tax identifiers](managing-tax-identifiers.md#tax-identifiers) associated with the customer, allows you to [attach this data in a cart](managing-tax-identifiers.md#attaching-a-tax-identifier-to-a-cart) and helps ensure that Digital River's tax computations are accurate.

## Customer type

Use the `customerType` parameter to differentiate between business and individual customers. Specifying a customer's type, as well as adding any tax identifiers associated with a customer, allows you to pass this data to a cart and helps ensure that Digital River's tax computations are accurate. See [Attaching a tax identifier to a cart](managing-tax-identifiers.md#attaching-a-tax-identifier-to-a-cart) to learn how to set the customer's type.

## Attaching a tax identifier to a cart

You must attach the tax identifier to the cart before you can use the source.&#x20;

To attach a tax identifier, [create a cart](creating-or-updating-a-cart/#creating-a-cart).

Optional. Send a [`GET /v1/shopper/me/carts/active/tax-registrations/schema`](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Tax-Registration/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1tax-registrations\~1schema/get) request to get the tax-registrations JSON schema. You can use this schema when attaching the tax identifier to the cart.&#x20;

{% tabs %}
{% tab title="Schema response body" %}
{% code overflow="wrap" %}
```json
{
    "$schema": http://json-schema.org/draft-04/schema#,
    "id": https://dispatch-test.digitalriver.com:443/cart-api/active/tax-registrations/schema,
    "oneOf": [
        {
            "type": "object",
            "title": "Individual",
            "additionalProperties": false,
            "required": [
                "customerType"
            ],
            "properties": {
                "customerType": {
                    "type": "string",
                    "readOnly": true,
                    "enum": [
                        "I"
                    ]
                },
                "taxRegistrations": {
                    "type": "array",
                    "title": "Tax Registrations",
                    "minItems": 1,
                    "maxItems": 1,
                    "items": [
                        {
                            "$ref": "#/definitions/CPF"
                        }
                    ]
                },
                "companyId": {
                    "type": "string"
                },
                "siteId": {
                    "type": "string"
                }
            }
        },
        {
            "type": "object",
            "title": "Business",
            "additionalProperties": false,
            "required": [
                "customerType"
            ],
            "properties": {
                "customerType": {
                    "type": "string",
                    "readOnly": true,
                    "enum": [
                        "B"
                    ]
                },
                "taxRegistrations": {
                    "type": "array",
                    "title": "Tax Registrations",
                    "minItems": 2,
                    "maxItems": 2,
                    "items": [
                        {
                            "$ref": "#/definitions/CNPJ"
                        },
                        {
                            "$ref": "#/definitions/IE"
                        }
                    ]
                },
                "companyId": {
                    "type": "string"
                },
                "siteId": {
                    "type": "string"
                }
            }
        }
    ],
    "definitions": {
        "CPF": {
            "type": "object",
            "additionalProperties": false,
            "required": [
                "key",
                "value"
            ],
            "properties": {
                "key": {
                    "type": "string",
                    "readOnly": true,
                    "enum": [
                        "CPF"
                    ]
                },
                "value": {
                    "type": "string",
                    "title": "CPF",
                    "description": "Digite seu número CPF individual. O número deve ter 11 dígitos e ser inserido sem espaços, períodos ou hifens como 12345678901.",
                    "pattern": "^[0-9]{1}[0-9]{1}[0-9]{1}[0-9]{1}[0-9]{1}[0-9]{1}[0-9]{1}[0-9]{1}[0-9]{1}[0-9]{1}[0-9]{1}$"
                }
            }
        },
        "IE": {
            "type": "object",
            "additionalProperties": false,
            "required": [
                "key",
                "value"
            ],
            "properties": {
                "key": {
                    "type": "string",
                    "readOnly": true,
                    "enum": [
                        "IE"
                    ]
                },
                "value": {
                    "type": "string",
                    "title": "Inscrição Estadual (IE)",
                    "description": "Por favor, insira a Inscrição Estadual da sua empresa. O número deve ter 8-13 dígitos e ser inserido sem espaços, períodos ou hifens como 12345678, 1234567890123 ou ISENTO. Para encontrar a sua Inscrição Estadual, visite o site SINTEGRA.",
                    "pattern": "^[0-9]{1}[0-9]{1}[0-9]{1}[0-9]{1}[0-9]{1}[0-9]{1}[0-9]{1}[0-9]{1}[0-9]{1}[0-9]{1}[0-9]{1}[0-9]{1}$,^[0-9]{1}[0-9]{1}[0-9]{1}[0-9]{1}[0-9]{1}[0-9]{1}[0-9]{1}[0-9]{1}[0-9]{1}[0-9]{1}[0-9]{1}[0-9]{1}[0-9]{1}$,^[0-9]{1}[0-9]{1}[0-9]{1}[0-9]{1}[0-9]{1}[0-9]{1}[0-9]{1}[0-9]{1}[0-9]{1}[0-9]{1}[0-9]{1}$,^[0-9]{1}[0-9]{1}[0-9]{1}[0-9]{1}[0-9]{1}[0-9]{1}[0-9]{1}[0-9]{1}$,^[0-9]{1}[0-9]{1}[0-9]{1}[0-9]{1}[0-9]{1}[0-9]{1}[0-9]{1}[0-9]{1}[0-9]{1}[0-9]{1}$,^[0-9]{1}[0-9]{1}[0-9]{1}[0-9]{1}[0-9]{1}[0-9]{1}[0-9]{1}[0-9]{1}[0-9]{1}$,^[Ii]{1}[Ss]{1}[Ee]{1}[Nn]{1}[Tt]{1}[Oo]{1}$"
                }
            }
        },
        "CNPJ": {
            "type": "object",
            "additionalProperties": false,
            "required": [
                "key",
                "value"
            ],
            "properties": {
                "key": {
                    "type": "string",
                    "readOnly": true,
                    "enum": [
                        "CNPJ"
                    ]
                },
                "value": {
                    "type": "string",
                    "title": "CNPJ",
                    "description": "Digite o número CNPJ da sua empresa. O número deve ter 14 dígitos e ser inserido sem espaços, períodos ou hifens como 12345678901234.",
                    "pattern": "^[0-9]{1}[0-9]{1}[0-9]{1}[0-9]{1}[0-9]{1}[0-9]{1}[0-9]{1}[0-9]{1}[0-9]{1}[0-9]{1}[0-9]{1}[0-9]{1}[0-9]{1}[0-9]{1}$"
                }
            }
        }
    },
    "liveMode": false
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

Send a [`POST /v1/shopper/me/carts/active/tax-registrations`](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Tax-Registration/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1tax-registrations/post) request to attach the tax identifier to the cart.  The following examples show the request body or response for `customerType` with the value of `B` for the business shopper and `I` for the individual shopper. You determine the value for the `customerType` enumerations in the schema when you attach it to the cart. ****&#x20;

{% tabs %}
{% tab title="Tax-registrations response body for Business shopper" %}
{% code overflow="wrap" %}
```json
{
    "customerType": "B",
    "taxRegistrations": [
        {
            "key": "CNPJ",
            "value": "77844699000109"
        },
        {
            "key": "IE",
            "value": "ISENTO"
        }
    ]
}
```
{% endcode %}
{% endtab %}

{% tab title="Tax registrations response body for Individual shopper" %}
{% code overflow="wrap" %}
```json
{
    "customerType": "I",
    "taxRegistrations": [
        {
            "key": "CPF",
            "value": "03927107492"
        }
    ]
}

```
{% endcode %}
{% endtab %}
{% endtabs %}

If [Global Tax ID Management is not enabled](https://help.digitalriver.com/help/gc/Administration/Site/Configuring-site-settings.htm) in [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do),  we return a `409 Conflict`.

{% tabs %}
{% tab title="409 Not Found" %}
{% code overflow="wrap" %}
```json
{
    "errors": [
        {
            "code": "vat-exemption-failure",
            "subcode": "vat-exemption-unavailable",
            "description": "Tax Exemption Rest of the World is not enabled on this site."
        }
    ]
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

Optional. Send a `GET /v1/shopper/me/carts/active` request to confirm the tax information is present. The following examples show the response for `customerType` with the value of `B` for a business shopper and `I` for an individual shopper.&#x20;

{% tabs %}
{% tab title="Active response body for a Business shopper" %}
{% code overflow="wrap" %}
```json
JSO{
    "cart": {
    ...
        "pricing": {
            "subtotal": {
                "currency": "BRL",
                "value": 10
            },
            "subtotalWithDiscount": {
                "currency": "BRL",
                "value": 10
            },
            "discount": {
                "currency": "BRL",
                "value": 0
            },
            "shippingAndHandling": {
                "currency": "BRL",
                "value": 0
            },
            "importTaxAndDuty": {
                "currency": "BRL",
                "value": 0
            },
            "tax": {
                "currency": "BRL",
                "value": 1.38
            },
            "orderTotal": {
                "currency": "BRL",
                "value": 11.38
            },
            "formattedSubtotal": "10,00 BRL",
            "formattedSubtotalWithDiscount": "10,00 BRL",
            "formattedDiscount": "0,00 BRL",
            "formattedShippingAndHandling": "0,00 BRL",
            "formattedImportTaxAndDuty": "0,00 BRL",
            "formattedTax": "1,38 BRL",
            "formattedOrderTotal": "11,38 BRL"
        },
    ...
        "customerType": "B",
        "taxRegistrations": [
            {
                "key": "CNPJ",
                "value": "77844699000109"
            },
            {
                "key": "IE",
                "value": "ISENTO"
            }
    }
 
}

```
{% endcode %}
{% endtab %}

{% tab title="Active response body for an Individual shopper" %}
{% code overflow="wrap" %}
```json
{
    "cart": {
    ...
        "pricing": {
            "subtotal": {
                "currency": "BRL",
                "value": 10
            },
            "subtotalWithDiscount": {
                "currency": "BRL",
                "value": 10
            },
            "discount": {
                "currency": "BRL",
                "value": 0
            },
            "shippingAndHandling": {
                "currency": "BRL",
                "value": 0
            },
            "importTaxAndDuty": {
                "currency": "BRL",
                "value": 0
            },
            "tax": {
                "currency": "BRL",
                "value": 1.38
            },
            "orderTotal": {
                "currency": "BRL",
                "value": 11.38
            },
            "formattedSubtotal": "10,00 BRL",
            "formattedSubtotalWithDiscount": "10,00 BRL",
            "formattedDiscount": "0,00 BRL",
            "formattedShippingAndHandling": "0,00 BRL",
            "formattedImportTaxAndDuty": "0,00 BRL",
            "formattedTax": "1,38 BRL",
            "formattedOrderTotal": "11,38 BRL"
        },
    ...
        "customerType": "I",
        "taxRegistrations": [
            {
                "key": "CPF",
                "value": "03927107492"
            }
        ]
    }
 
}

```
{% endcode %}
{% endtab %}
{% endtabs %}

Apply the source to the cart using one of the following options:

* [Attach the shopper to the cart](broken-reference). The authenticated shopper's default payment option will be applied to the cart.
* [Attach the source directly to the cart](broken-reference).
* [Submit the cart](submitting-a-cart/initiating-a-charge.md).&#x20;

The following example shows the response body for the cart.

{% tabs %}
{% tab title="Submit cart response body" %}
{% code overflow="wrap" %}
```json
{
    "submitCart": {
        "order": {
            "uri": https://dispatch-test.digitalriver.com/v1/shoppers/me/orders/997463190080,
            "id": 997463190080,
            "submissionDate": null,
            "displayName": "Novo pedido",
            "locale": "pt_BR",
            "optIn": "false",
            "testOrder": "false",
            "taxExempt": "false",
            "businessEntityCode": "DR_BRAZIL-ENTITY",
            "orderState": "Source Pending Redirect",
            "orderStateDetails": {
                "description": null,
                "settled": {
                    "currency": "BRL",
                    "value": 0
                },
                "refunded": {
                    "currency": "BRL",
                    "value": 0
                }
            }
        },
        "lineItems": {
            "lineItem": [
                {
                    "id": 997502760080,
                    "quantity": 1,
                    "product": {
                        "uri": https://dispatch-test.digitalriver.com/v1/shoppers/me/products/328207600,
                        "displayName": "Download Product - Klarna",
                        "thumbnailImage": null
                    },
                    "lineItemState": "Source Pending Redirect",
                    "lineItemStateDetails": {
                        "description": null,
                        "backOrdered": 0,
                        "shipped": 0,
                        "returned": 0,
                        "pendingReturn": 0
                    },
                    "pricing": {
                        "listPrice": {
                            "currency": "BRL",
                            "value": 10
                        },
                        "listPriceWithQuantity": {
                            "currency": "BRL",
                            "value": 10
                        },
                        "salePrice": {
                            "currency": "BRL",
                            "value": 10
                        },
                        "salePriceWithQuantity": {
                            "currency": "BRL",
                            "value": 10
                        },
                        "formattedListPrice": "10,00 BRL",
                        "formattedListPriceWithQuantity": "10,00 BRL",
                        "formattedSalePrice": "10,00 BRL",
                        "formattedSalePriceWithQuantity": "10,00 BRL",
                        "totalDiscountWithQuantity": {
                            "currency": "BRL",
                            "value": 0
                        },
                        "formattedTotalDiscountWithQuantity": "0,00 BRL",
                        "productTax": {
                            "currency": "BRL",
                            "value": 1.38
                        },
                        "shippingTax": {
                            "currency": "BRL",
                            "value": 0
                        },
                        "feeTax": {
                            "currency": "BRL",
                            "value": 0
                        },
                        "taxRate": 0.1215,
                        "discountDescription": "empty",
                        "importTax": {
                            "currency": "BRL",
                            "value": 0
                        },
                        "formattedImportTax": "0,00 BRL",
                        "importDuty": {
                            "currency": "BRL",
                            "value": 0
                        },
                        "formattedImportDuty": "0,00 BRL"
                    },
                    "downloads": {},
                    "digitalRights": {}
                }
            ]
        },
        "billingAddress": {
            "id": "billingAddress",
            "firstName": "Zachariah",
            "lastName": "Harris",
            "companyName": "Digital River",
            "line1": "1067 Rua Coronel Quirino",
            "line2": null,
            "line3": null,
            "city": "Centro",
            "countrySubdivision": "SP",
            "postalCode": "13025-002",
            "country": "BR",
            "countryName": "Brazil",
            "phoneNumber": "246-838-8386",
            "countyName": null,
            "emailAddress": Presley_Aufderhar@yahoo.com,
            "phoneticFirstName": null,
            "phoneticLastName": null,
            "division": null
        },
        "shippingAddress": {
            "id": "shippingAddress",
            "firstName": "Zachariah",
            "lastName": "Harris",
            "companyName": "Digital River",
            "line1": "1067 Rua Coronel Quirino",
            "line2": null,
            "line3": null,
            "city": "Centro",
            "countrySubdivision": "SP",
            "postalCode": "13025-002",
            "country": "BR",
            "countryName": "Brazil",
            "phoneNumber": "246-838-8386",
            "countyName": null,
            "emailAddress": Presley_Aufderhar@yahoo.com,
            "phoneticFirstName": null,
            "phoneticLastName": null,
            "division": null
        },
        "shippingMethod": {},
        "taxInclusive": "false",
        "landedCostState": "NOT_ELIGIBLE",
        "pricing": {
            "subtotal": {
                "currency": "BRL",
                "value": 10
            },
            "subtotalWithDiscount": {
                "currency": "BRL",
                "value": 10
            },
            "discount": {
                "currency": "BRL",
                "value": 0
            },
            "shippingAndHandling": {
                "currency": "BRL",
                "value": 0
            },
            "importTaxAndDuty": {
                "currency": "BRL",
                "value": 0
            },
            "tax": {
                "currency": "BRL",
                "value": 1.38
            },
            "orderTotal": {
                "currency": "BRL",
                "value": 11.38
            },
            "formattedSubtotal": "10,00 BRL",
            "formattedSubtotalWithDiscount": "10,00 BRL",
            "formattedDiscount": "0,00 BRL",
            "formattedShippingAndHandling": "0,00 BRL",
            "formattedImportTaxAndDuty": "0,00 BRL",
            "formattedTax": "1,38 BRL",
            "formattedOrderTotal": "11,38 BRL"
        },
        "paymentMethod": {
            "type": "boletoBancario",
            "sourceId": "729bfe56-93cc-4759-a6b5-cd40236d126e",
            "sourceClientSecret": "729bfe56-93cc-4759-a6b5-cd40236d126e_0984ec75-f984-4d6d-a634-fd7f6b8dd20e",
            "boletoBancario": {
                "documentCode": "23790001246004987209031123456704579990000010000",
                "clientSecret": "729bfe56-93cc-4759-a6b5-cd40236d126e_0984ec75-f984-4d6d-a634-fd7f6b8dd20e",
                "flow": "redirect",
                "document": https://link/to/the/payment-slip.pdf,
                "reusable": "false"
            }
        },
        "paymentCompletionResources": {},
        "termsOfSalesAcceptance": null,
        "paymentSession": {
            "id": "03aede3b-29d9-4aca-a5c2-9e3707861e68",
            "clientSecret": "03aede3b-29d9-4aca-a5c2-9e3707861e68_9e4f4089-0823-4dac-8915-0b2e2f8b085b",
            "status": "pending_redirect",
            "redirectUrl": https://api.digitalriver.com:443/payments/redirects/797e027a-6a75-482e-b18f-2ba02beddda6?apiKey=pk_sys_704d8a7ccbc44f38ab218da662bc347b
        },
        "customerType": "I",
        "taxRegistrations": [
            {
                "key": "CPF",
                "value": "03927107492"
            }
        ]
    }
}

```
{% endcode %}
{% endtab %}
{% endtabs %}

## Removing a tax identifier from a cart

You can remove the tax identifier with or without specifying the cart identifier (`cartId`).

### Removing a tax identifier with the cart identifier

To remove a tax identifier associated with a specific cart, use [DELETE /v1/shoppers/me/carts/active/tax-registrations](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Tax-Registration/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1tax-registrations/delete) and include the cart identifier (`cartId`).

A successful response returns a `204 Not Content`.

### Removing a tax identifier without the cart identifier

To remove a tax identifier without a cart identifier, use [`DELETE /v1/shoppers/me/carts/active/tax-registrations`](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Tax-Registration/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1tax-registrations/post).&#x20;

A successful response returns a `204 Not Content`.

If [Global Tax ID Management is not enabled](https://help.digitalriver.com/help/gc/Administration/Site/Configuring-site-settings.htm) in [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do),  we return a `409 Conflict`.

{% tabs %}
{% tab title="409 Not Found" %}
{% code overflow="wrap" %}
```json
{
    "errors": [
        {
            "code": "vat-exemption-failure",
            "description": "Tax Exemption Rest of the World is not enabled on this site."
        }
    ]
}
```
{% endcode %}
{% endtab %}
{% endtabs %}
