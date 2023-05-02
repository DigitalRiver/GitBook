---
description: >-
  Learn how to resume cart submission after completing a redirect payment
  method.
---

# Resuming cart submission

When a customer selects a [redirect payment method](../../general-resources/reference/guidelines-for-capturing-payment-details.md#redirect-payment-methods) when they submit the cart, they are redirected to the payment provider where they can authorize the payment. Once the payment is authorized, you can [resume submitting the cart](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Resume-Cart).

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```http
curl --location -g --request POST ' https://api.digitalriver.com/v1/shoppers/me/carts/active/resume-cart' \
--header 'Authorization: Basic {{access_token}}' \
...
```
{% endcode %}
{% endtab %}

{% tab title="200 OK response" %}
{% code overflow="wrap" %}
```json
{
    "resumeCart": {
        "order": {
            "uri": "https://dispatch-test.digitalriver.com/v1/shoppers/me/orders/1077950780082",
            "id": 1077950780082,
            "submissionDate": "2023-03-28T10:38:55.082Z",
            "displayName": "New Order",
            "locale": "en_US",
            "optIn": "false",
            "testOrder": "false",
            "taxExempt": "false",
            "businessEntityCode": "DR_INC-ENTITY",
            "orderState": "Submitted",
            "orderStateDetails": {
                "description": null,
                "settled": {
                    "currency": "USD",
                    "value": 0
                },
                "refunded": {
                    "currency": "USD",
                    "value": 0
                }
            },
            "customAttributes": {
                "attribute": [
                    {
                        "name": "orderSubmittedByShopperApiFlag",
                        "type": "string",
                        "value": "shopperApiV1Submitted"
                    },
                    {
                        "name": "DPL_SERVICE_PROVIDER",
                        "type": "string",
                        "value": "ComplianceService"
                    },
                    {
                        "name": "isLandedCostPrettyPrice",
                        "type": "string",
                        "value": "false"
                    },
                    {
                        "name": "feeJurisdiction",
                        "type": "string",
                        "value": "US.MN"
                    },
                    {
                        "name": "DPL_SCREENING_URL",
                        "type": "string",
                        "value": "http://compliance-sys.digitalriverws.net/compliance/resource/screening/VDC3-55916946"
                    },
                    {
                        "name": "orderGeneratedByFlag",
                        "type": "string",
                        "value": "systemGenerated"
                    },
                    {
                        "name": "DPLResult",
                        "type": "string",
                        "value": "Accept"
                    },
                    {
                        "name": "PURCHASEPLAN_INCENTIVE_TOTAL",
                        "type": "string",
                        "value": "0"
                    },
                    {
                        "name": "orderGeneratedByShopperApiFlag",
                        "type": "string",
                        "value": "shopperApiV1Generated"
                    },
                    {
                        "name": "feeShippingJurisdiction",
                        "type": "string",
                        "value": "US.MN"
                    }
                ]
            }
        },
        "lineItems": {
            "lineItem": [
                {
                    "id": 50587290082,
                    "quantity": 1,
                    "product": {
                        "uri": "https://dispatch-test.digitalriver.com/v1/shoppers/me/products/5303832100",
                        "id": 5303832100,
                        "name": "Physical Product - 2",
                        "displayName": "Physical Product - 2",
                        "shortDescription": "Short Description:",
                        "longDescription": "Long Description:",
                        "productType": "PHYSICAL",
                        "sku": "Physical Product - 2",
                        "externalReferenceId": "234",
                        "companyId": "shopx1",
                        "displayableProduct": "true",
                        "purchasable": "true",
                        "manufacturerName": "345",
                        "manufacturerPartNumber": "456",
                        "thumbnailImage": "https://drhods-sysaws.drextenv.net/DRHM/Storefront/Company/shopx1/images/product/thumbnail/lake.png",
                        "productImage": "https://drhods-sysaws.drextenv.net/DRHM/Storefront/Company/shopx1/images/product/detail/lake.png",
                        "keywords": "Keywords:",
                        "customAttributes": {
                            "attribute": [
                                {
                                    "name": "clonedFromStaging",
                                    "type": "Boolean",
                                    "value": "false"
                                },
                                {
                                    "name": "landedCost",
                                    "type": "Boolean",
                                    "value": "false"
                                },
                                {
                                    "name": "nonSolr",
                                    "type": "Boolean",
                                    "value": "false"
                                },
                                {
                                    "name": "needsRestrictedShippingOption",
                                    "type": "Boolean",
                                    "value": "false"
                                },
                                {
                                    "name": "originalIsOrderable",
                                    "type": "Boolean",
                                    "value": "true"
                                },
                                {
                                    "name": "length",
                                    "type": "Quantity",
                                    "value": "10.000 in"
                                },
                                {
                                    "name": "upc",
                                    "type": "String",
                                    "value": "34"
                                },
                                {
                                    "name": "weight",
                                    "type": "Quantity",
                                    "value": "10.000 lb"
                                },
                                {
                                    "name": "unit",
                                    "type": "String",
                                    "value": "666"
                                },
                                {
                                    "name": "shippingID",
                                    "type": "String",
                                    "value": "345"
                                },
                                {
                                    "name": "width",
                                    "type": "Quantity",
                                    "value": "10.000 in"
                                },
                                {
                                    "name": "privateStoreOnly",
                                    "type": "Boolean",
                                    "value": "false"
                                },
                                {
                                    "name": "originalIsViewable",
                                    "type": "Boolean",
                                    "value": "true"
                                }
                            ]
                        }
                    },
                    "lineItemState": "Submitted",
                    "lineItemStateDetails": {
                        "description": null,
                        "backOrdered": 0,
                        "shipped": 0,
                        "returned": 0,
                        "pendingReturn": 0
                    },
                    "pricing": {
                        "listPrice": {
                            "currency": "USD",
                            "value": 100
                        },
                        "listPriceWithQuantity": {
                            "currency": "USD",
                            "value": 100
                        },
                        "salePrice": {
                            "currency": "USD",
                            "value": 100
                        },
                        "salePriceWithQuantity": {
                            "currency": "USD",
                            "value": 100
                        },
                        "formattedListPrice": "100.00USD",
                        "formattedListPriceWithQuantity": "100.00USD",
                        "formattedSalePrice": "100.00USD",
                        "formattedSalePriceWithQuantity": "100.00USD",
                        "totalDiscountWithQuantity": {
                            "currency": "USD",
                            "value": 0
                        },
                        "formattedTotalDiscountWithQuantity": "0.00USD",
                        "productTax": {
                            "currency": "USD",
                            "value": 7.38
                        },
                        "shippingTax": {
                            "currency": "USD",
                            "value": 0.73
                        },
                        "feeTax": {
                            "currency": "USD",
                            "value": 0
                        },
                        "taxRate": 0.07375,
                        "discountDescription": "empty",
                        "importTax": {
                            "currency": "USD",
                            "value": 0
                        },
                        "formattedImportTax": "0.00USD",
                        "importDuty": {
                            "currency": "USD",
                            "value": 0
                        },
                        "formattedImportDuty": "0.00USD"
                    },
                    "downloads": {},
                    "digitalRights": {},
                    "customAttributes": {
                        "attribute": [
                            {
                                "name": "isTaxExempt",
                                "type": "string",
                                "value": "false"
                            }
                        ]
                    }
                }
            ]
        },
        "billingAddress": {
            "id": "billingAddress",
            "firstName": "firstName",
            "lastName": "lastName",
            "companyName": null,
            "line1": "line1",
            "line2": "line2",
            "line3": null,
            "city": "Minnetonka",
            "countrySubdivision": "MN",
            "postalCode": "55410",
            "country": "US",
            "countryName": "United States",
            "phoneNumber": "9522253720",
            "countyName": null,
            "emailAddress": "hold1@fraud.com",
            "phoneticFirstName": null,
            "phoneticLastName": null,
            "division": null,
            "title": null
        },
        "shippingAddress": {
            "id": "shippingAddress",
            "firstName": "darren",
            "lastName": "tang",
            "companyName": "DR",
            "line1": "10381 Bren Road West",
            "line2": "4321",
            "line3": "Suite Line 3",
            "city": "Waconia",
            "countrySubdivision": "MN",
            "postalCode": "05387",
            "country": "US",
            "countryName": "United States",
            "phoneNumber": "952-253-1234",
            "countyName": null,
            "emailAddress": "hold1@fraud.com",
            "phoneticFirstName": null,
            "phoneticLastName": null,
            "division": null
        },
        "shippingMethod": {
            "code": 265200,
            "description": "Standard"
        },
        "taxInclusive": "false",
        "landedCostState": "NOT_ELIGIBLE",
        "pricing": {
            "subtotal": {
                "currency": "USD",
                "value": 100
            },
            "subtotalWithDiscount": {
                "currency": "USD",
                "value": 100
            },
            "discount": {
                "currency": "USD",
                "value": 0
            },
            "shippingAndHandling": {
                "currency": "USD",
                "value": 9.9
            },
            "importTaxAndDuty": {
                "currency": "USD",
                "value": 0
            },
            "tax": {
                "currency": "USD",
                "value": 8.11
            },
            "orderTotal": {
                "currency": "USD",
                "value": 118.01
            },
            "formattedSubtotal": "100.00USD",
            "formattedSubtotalWithDiscount": "100.00USD",
            "formattedDiscount": "0.00USD",
            "formattedShippingAndHandling": "9.90USD",
            "formattedImportTaxAndDuty": "0.00USD",
            "formattedTax": "8.11USD",
            "formattedOrderTotal": "118.01USD"
        },
        "paymentMethod": {
            "type": "klarnaCredit",
            "sourceId": "33ead2d9-55ef-4ee8-a532-961fb70effb0",
            "sourceClientSecret": "33ead2d9-55ef-4ee8-a532-961fb70effb0_695c8a26-2431-4552-80a3-c5c07f00525e",
            "klarnaCredit": {
                "shipping": "{recipient=darren tang, phoneNumber=952-253-1234, address={line1=10381 Bren Road West, line2=4321, city=Waconia, state=MN, country=US, postalCode=05387}, email=ttang@digitalriver.com}",
                "clientSecret": "33ead2d9-55ef-4ee8-a532-961fb70effb0_695c8a26-2431-4552-80a3-c5c07f00525e",
                "flow": "redirect",
                "token": "17570312550000000000000575239905",
                "paymentType": "2023-03-30T09:44:01.295Z",
                "reusable": "false"
            },
            "amountContributed": {
                "currency": "USD",
                "value": 68.01
            },
            "supplementaryPaymentMethods": [
                {
                    "type": "customerCredit",
                    "sourceId": "202bb87b-e393-4ef4-a4d0-6fad5970ebd0",
                    "sourceClientSecret": "202bb87b-e393-4ef4-a4d0-6fad5970ebd0_0a5d5f4f-1bd2-4fcf-b96f-b7127ebbe35f",
                    "customerCredit": {
                        "clientSecret": "202bb87b-e393-4ef4-a4d0-6fad5970ebd0_0a5d5f4f-1bd2-4fcf-b96f-b7127ebbe35f",
                        "flow": "standard",
                        "reusable": "false"
                    },
                    "amountContributed": {
                        "currency": "USD",
                        "value": 50
                    }
                }
            ]
        },
        "paymentCompletionResources": {},
        "termsOfSalesAcceptance": null,
        "paymentSession": {
            "id": "6a92bfac-072b-4e2c-8066-9bd2e4ab4fa0",
            "clientSecret": "6a92bfac-072b-4e2c-8066-9bd2e4ab4fa0_21ed1510-c504-47ae-a345-f7d5d17a1944",
            "status": "complete"
        }
    }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

See [Resume cart query parameters](../../general-resources/shopper-apis-reference/resume-cart.md#resume-cart-query-parameters) for more information.
