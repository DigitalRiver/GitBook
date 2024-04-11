---
description: Gain a better understanding of how to configure components
---

# Configuring components

The configuration object you're required to pass to [`components()`](./#creating-components) allows you to:

* [Specify a checkout session identifier](configuring-components.md#identify-the-checkout-session)
* [Redirect after successful checkouts](configuring-components.md#redirect-after-successful-checkouts)
* [Define how you want to handle callback events](configuring-components.md#callback-methods-in-components)

<pre class="language-javascript"><code class="lang-javascript">let components;
<strong>...
</strong><strong>const configuration = {
</strong>    checkoutSessionId: await createComponentsCheckoutSession(),
    redirectUrl: window.location.protocol + '//' + window.location.hostname + ':' + window.location.port + '/v1/thank-you.html',
    onReady: function (data) {},
    onChange: function (data) {},
    onSuccess: function (data) {}
}
...
components = digitalRiverCheckout.components(configuration);
</code></pre>

## Identify the checkout-session

In the [`components()`](./#creating-components) configuration object, you're required to define `checkoutSessionId`.

[DigitalRiverCheckout.js](../../) needs this identifier so that it can access the [checkout-session](../../../digital-river-api-reference/checkout-sessions.md).

```javascript
const configuration = {
      checkoutSessionId: await createComponentsCheckoutSession(),
      ...
}
```

To set this property, call an asynchronous function that [creates a checkout-session](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions/operation/createDropInCheckoutSession) and returns its unique identifier. Refer to [Build a configuration object](../../../../integration-options/low-code-checkouts/implementing-a-components-checkout.md#build-a-configuration-object) on the [Components checkout](../../../../integration-options/low-code-checkouts/implementing-a-components-checkout.md) page for details.&#x20;

## Redirect after successful checkouts

In the [`components()`](./#creating-components) configuration object, the optional `redirectUrl` can be assigned a URL. This represents where you'd like Digital River to redirect customers after payment is authorized and the [checkout-session](../../../digital-river-api-reference/checkout-sessions.md) is successfully converted to an [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders).&#x20;

```javascript
const configuration = {
      ...
      redirectUrl: window.location.protocol + '//' + window.location.hostname + ':' + window.location.port + '/v1/thank-you.html',
      ...
}
```

You could use `redirectUrl` to send your customers to a custom order confirmation page, but if you display the [thank you component](thank-you-component.md), then don't define this property.

## Callback methods in components

You can use the [`components()`](./#creating-components) configuration object to be notified of (1) [ready](configuring-components.md#ready-event), (2) [change](configuring-components.md#change-event), and (3) [success](configuring-components.md#success-event) events.

### Ready event

Define [`onReady`](configuring-components.md#onready) to be notified when components have successfully initialized.&#x20;

#### `onReady`

The `onReady` property can be assigned a method, which accepts `data`, that executes when the [checkout-session](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions/operation/createDropInCheckoutSession) has been successfully created and components are ready to accept input.

```javascript
const configuration = {
      ...
      onReady: function (data) {},
      ...
}
```

The method returns a `data` object that contains the [`requiresShipping`](configuring-components.md#requiresshipping) and [`showTaxIdentifiers`](configuring-components.md#showtaxidentifiers) booleans.

<pre class="language-javascript" data-title="data"><code class="lang-javascript"><strong>{
</strong>    "requiresShipping": true,
    "showTaxIdentifiers": true
}
</code></pre>

### Change event

Define [`onChange`](configuring-components.md#onchange) to be notified of changes that occur in components.

#### `onChange`

The `onChange` property can be assigned a method, which accepts `data`, that executes when customers use a component to successfully submit their information.

```javascript
const configuration = {
      ...
      onChange: function (data) {},
      ...
}
```

The returned `data` object, which represents the updated [checkout-session](../../../digital-river-api-reference/checkout-sessions.md), always contains [`requiresShipping`](configuring-components.md#requiresshipping) and [`showInvoiceAttribute`](configuring-components.md#showinvoiceattribute).&#x20;

It might also contain `optionalTaxIdentifiers[]` or `requiredTaxIdentifiers[]`. If the former array exists, your application can optionally display the [tax identifier component](tax-identifier-component.md) to users. If the latter exists, you're required to do so.&#x20;

{% code title="data" %}
```javascript
{
    "id": "9d133de3-1095-40bc-934a-19101be6ff0f",
    "checkoutId": "b9195f41-1864-42c2-afe6-ad1aa80d66e3",
    "createdTime": "2023-01-03T21:48:41Z",
    "currency": "EUR",
    "customerId": "590881960336",
    "email": "test@test.com",
    "shipFrom": {
        "address": {
            "country": "US"
        }
    },
    "billTo": {
        "address": {
            "country": "DE"
        },
        "saveForLater": false
    },
    "totalAmount": 300,
    "subtotal": 300,
    "totalFees": 0,
    "totalTax": 0,
    "totalImporterTax": 0,
    "totalDuty": 0,
    "totalDiscount": 0,
    "totalShipping": 0,
    "items": [
        {
            "id": "594f1af2-5a19-4158-90ab-b321a0260fcc",
            "sku": {
                "id": "30c1a732-61a7-426e-8580-12e7d1552694",
                "name": "Puppy shoes",
                "eccn": "EAR99",
                "taxCode": "5216",
                "image": "https://upload.wikimedia.org/wikipedia/commons/thumb/6/6e/Golde33443.jpg/640px-Golde33443.jpg",
                "physical": true,
                "metadata": {
                    "customAttribute1": "some value"
                }
            },
            "amount": 300,
            "quantity": 1,
            "tax": {
                "rate": 0,
                "amount": 0
            },
            "importerTax": {
                "amount": 0
            },
            "duties": {
                "amount": 0
            },
            "fees": {
                "amount": 0,
                "taxAmount": 0
            }
        }
    ],
    "updatedTime": "2023-01-03T21:48:41Z",
    "locale": "en_US",
    "customerType": "business",
    "sellingEntity": {
        "id": "DR_IRELAND-ENTITY",
        "name": "Digital River Ireland Ltd."
    },
    "options": {
        "shippingMethods": [
            {
                "amount": 5,
                "description": "Standard Shipping",
                "serviceLevel": "SG"
            },
            {
                "amount": 15,
                "description": "Next Day Air",
                "serviceLevel": "ND"
            }
        ],
        "addresses": [
            {
                "address": {
                    "line1": "10380 Bren Rd W",
                    "city": "Minnetonka",
                    "postalCode": "55129",
                    "state": "MN",
                    "country": "US"
                },
                "name": "John Smith",
                "phone": "952-111-1111",
                "email": "jsmith@dr.com"
            },
            {
                "address": {
                    "line1": "10-123 1/2 MAIN STREET NW",
                    "city": "MONTREAL",
                    "postalCode": "H3Z 2Y7",
                    "state": "QC",
                    "country": "CA"
                },
                "name": "John Jones",
                "phone": "9055438570",
                "email": "jj@dr.com"
            },
            {
                "address": {
                    "line1": "Neuer Wall 10",
                    "city": "Hamburg",
                    "postalCode": "20354",
                    "country": "DE"
                },
                "name": "Anna Brawner",
                "phone": "020143647453",
                "email": "ab@dr.com"
            }
        ],
        "sources": [
            {
                "id": "c7d8c974-4ea5-4549-be0b-49203e88d988",
                "createdTime": "2022-09-14T15:02:20Z",
                "type": "creditCard",
                "currency": "EUR",
                "amount": 327.5,
                "reusable": true,
                "state": "chargeable",
                "owner": {
                    "firstName": "John",
                    "lastName": "Smith",
                    "email": "jsmith@dr.com",
                    "address": {
                        "line1": "10380 Bren Rd W",
                        "city": "Minnetonka",
                        "postalCode": "55129",
                        "state": "MN",
                        "country": "US"
                    }
                },
                "paymentSessionId": "3376ae52-b1e6-4e95-a52c-726b0932285d",
                "clientSecret": "c7d8c974-4ea5-4549-be0b-49203e88d988_bdd2e28b-ec88-4902-bdd6-bd26ddb7732e",
                "mandate": {
                    "terms": "Yes, please save this account and payment information for future purchases.",
                    "signedTime": "2022-09-14T15:02:20.238Z"
                },
                "creditCard": {
                    "brand": "MasterCard",
                    "expirationMonth": 12,
                    "expirationYear": 2023,
                    "lastFourDigits": "0008",
                    "fundingSource": "credit"
                }
            }
        ],
        "taxIdentifiers": [
            {
                "id": "c61066b2-5de4-4172-903d-74077c70c0fe",
                "state": "verified",
                "verifiedName": "---",
                "verifiedAddress": "---",
                "liveMode": false,
                "customerId": "590881960336",
                "type": "de",
                "value": "DE123456789",
                "stateTransitions": {
                    "verified": "2022-09-14T13:40:31Z"
                },
                "createdTime": "2022-09-14T13:40:31Z",
                "updatedTime": "2022-09-14T13:41:12Z"
            }
        ],
        "storeCredits": [
            {
                "amount": 100,
                "name": "Gift Card",
                "upstreamId": "7654-2345-0987-123456-1",
                "lastFour": "7831",
                "iconUrl": "https://upload.wikimedia.org/wikipedia/commons/thumb/6/6e/Golde33443.jpg/640px-Golde33443.jpg"
            },
            {
                "amount": 500,
                "name": "Gift Card",
                "upstreamId": "7654-2345-0987-123456-2",
                "lastFour": "7831"
            }
        ],
        "consents": {
            "companyName": "Acme Incorporated",
            "emailPromotions": {
                "url": "https://www.mysite.com/promotions.html"
            },
            "eula": {
                "url": "https://www.mysite.com/EULA.html"
            },
            "termsOfService": {
                "url": "https://www.mysite.com/terms-of-service.html"
            }
        },
        "policies": {
            "refund": {
                "url": "https://www.mysite.com/refund-policy.html"
            },
            "return": {
                "url": "https://www.mysite.com/return-policy.html"
            }
        }
    },
    "payment": {
        "session": {
            "id": "c1e0fba0-4063-43d4-b751-2590fb4da939",
            "amountContributed": 0,
            "amountRemainingToBeContributed": 300,
            "state": "requires_source",
            "clientSecret": "c1e0fba0-4063-43d4-b751-2590fb4da939_d1bf7327-d545-4291-b9a2-8f61d99f2a7f"
        }
    },
    "taxInclusive": false,
    "requiresShipping": true,
    "optionalTaxIdentifiers": [
        "de"
    ],
    "fingerprint": "6f551d35-b60a-46ab-afe8-d8e18e114f6d",
    "billingAddressSchema": "{\"$schema\":\"http://json-schema.org/draft-07/schema#\",\"title\":\"Address\",\"type\":\"object\",\"properties\":{\"name\":{\"type\":\"string\",\"description\":\"purchaser full name\",\"minLength\":0,\"maxLength\":128},\"organization\":{\"type\":\"string\",\"description\":\"purchaser company or organization\",\"minLength\":0,\"maxLength\":128},\"line1\":{\"type\":\"string\",\"description\":\"purchaser residence number and street\",\"minLength\":0,\"maxLength\":128},\"line2\":{\"type\":\"string\",\"description\":\"supplimental address information such as apartment number or suite\",\"minLength\":0,\"maxLength\":128},\"city\":{\"type\":\"string\",\"description\":\"purchaser city of residence\",\"minLength\":0,\"maxLength\":64},\"postalCode\":{\"type\":\"string\",\"description\":\"purchaser postal code\",\"pattern\":\"^\\\\d{5}$\"},\"country\":{\"type\":\"string\",\"description\":\"Address country\",\"enum\":[\"DE\"]}},\"required\":[\"country\",\"postalCode\"]}",
    "shippingAddressSchema": "{\"$schema\":\"http://json-schema.org/draft-07/schema#\",\"title\":\"Address\",\"type\":\"object\",\"properties\":{\"name\":{\"type\":\"string\",\"description\":\"purchaser full name\",\"minLength\":0,\"maxLength\":128},\"organization\":{\"type\":\"string\",\"description\":\"purchaser company or organization\",\"minLength\":0,\"maxLength\":128},\"line1\":{\"type\":\"string\",\"description\":\"purchaser residence number and street\",\"minLength\":0,\"maxLength\":128},\"line2\":{\"type\":\"string\",\"description\":\"supplimental address information such as apartment number or suite\",\"minLength\":0,\"maxLength\":128},\"city\":{\"type\":\"string\",\"description\":\"purchaser city of residence\",\"minLength\":0,\"maxLength\":64},\"postalCode\":{\"type\":\"string\",\"description\":\"purchaser postal code\",\"pattern\":\"^\\\\d{5}$\"},\"country\":{\"type\":\"string\",\"description\":\"Address country\",\"enum\":[\"DE\"]}},\"required\":[\"country\",\"city\",\"postalCode\",\"line1\"]}",
    "billingAddressOnlySchema": "{\"$schema\":\"http://json-schema.org/draft-07/schema#\",\"title\":\"Address\",\"type\":\"object\",\"properties\":{\"name\":{\"type\":\"string\",\"description\":\"purchaser full name\",\"minLength\":0,\"maxLength\":128},\"organization\":{\"type\":\"string\",\"description\":\"purchaser company or organization\",\"minLength\":0,\"maxLength\":128},\"line1\":{\"type\":\"string\",\"description\":\"purchaser residence number and street\",\"minLength\":0,\"maxLength\":128},\"line2\":{\"type\":\"string\",\"description\":\"supplimental address information such as apartment number or suite\",\"minLength\":0,\"maxLength\":128},\"city\":{\"type\":\"string\",\"description\":\"purchaser city of residence\",\"minLength\":0,\"maxLength\":64},\"postalCode\":{\"type\":\"string\",\"description\":\"purchaser postal code\",\"pattern\":\"^\\\\d{5}$\"},\"country\":{\"type\":\"string\",\"description\":\"Address country\",\"enum\":[\"DE\"]}},\"required\":[\"country\",\"postalCode\"]}",
    "liveMode": false
}
```
{% endcode %}

### Success event

Define [`onSuccess`](configuring-components.md#onsuccess) to be notified of a successfully completed components checkout.&#x20;

#### `onSuccess`

The `onSuccess` property can be assigned a method, which accepts `data`, that executes when a customer's payment is authorized, and Digital River successfully converts the [checkout-session](../../../digital-river-api-reference/checkout-sessions.md) to an [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders). &#x20;

```javascript
const configuration = {
      ...
      onSuccess: function (data) {}
}
```

The method returns a `data` object, which represents the [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders).&#x20;

{% code title="data" %}
```javascript
{
    "order": {
        "id": "234236860336",
        "checkoutId": "07968dbc-7e0e-42a7-bdeb-6a13283ab865",
        "checkoutSessionId": "93ca0c41-a3c9-4e62-a955-dfad7931fcf5",
        "createdTime": "2022-07-26T20:56:19Z",
        "currency": "USD",
        "email": "ab@dr.com",
        "shipTo": {
            "address": {
                "line1": "Neuer Wall 10",
                "city": "Hamburg",
                "postalCode": "20354",
                "country": "DE"
            },
            "name": "Anna Brawner",
            "phone": "020143647453",
            "email": "ab@dr.com",
            "saveForLater": false
        },
        "shipFrom": {
            "address": {
                "country": "DE"
            }
        },
        "billTo": {
            "address": {
                "line1": "Neuer Wall 10",
                "city": "Hamburg",
                "postalCode": "20354",
                "country": "DE"
            },
            "name": "Anna Brawner",
            "phone": "020143647453",
            "email": "ab@dr.com",
            "saveForLater": false
        },
        "totalAmount": 362.95,
        "subtotal": 305,
        "totalFees": 0,
        "totalTax": 57.95,
        "totalImporterTax": 0,
        "totalDuty": 0,
        "totalDiscount": 0,
        "totalShipping": 5,
        "items": [
            {
                "id": "161531430336",
                "sku": {
                    "id": "sku_1630512988374",
                    "name": "Thors Hammer",
                    "eccn": "EAR99",
                    "taxCode": "4323.310_A",
                    "image": "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQyc7CIax_xuyc5lkppfI8iMZ6t7NpOVTmhhA&usqp=CAU",
                    "physical": true,
                    "skuGroupId": "demo-1630512830419",
                    "metadata": {
                        "application": "iOS-LLL"
                    },
                    "weight": 8125,
                    "weightUnit": "oz"
                },
                "amount": 300,
                "quantity": 1,
                "metadata": {
                    "shippingAmount": 5
                },
                "tax": {
                    "rate": 0.19,
                    "amount": 57
                },
                "importerTax": {
                    "amount": 0
                },
                "duties": {
                    "amount": 0
                },
                "availableToRefundAmount": 0,
                "shipFrom": {
                    "address": {
                        "line1": "10380 Bren Rd W",
                        "city": "Minnetonka",
                        "postalCode": "55129",
                        "state": "MN",
                        "country": "DE"
                    }
                },
                "fees": {
                    "amount": 0,
                    "taxAmount": 0
                }
            }
        ],
        "shippingChoice": {
            "amount": 5,
            "description": "Standard Shipping",
            "serviceLevel": "SG",
            "taxAmount": 0.95
        },
        "updatedTime": "2022-07-26T20:56:19Z",
        "locale": "en_US",
        "customerType": "individual",
        "sellingEntity": {
            "id": "DR_IRELAND-ENTITY",
            "name": "Digital River Ireland Ltd."
        },
        "payment": {
            "charges": [
                {
                    "id": "30414f85-a52f-4c94-a3a7-3ce418d51f62",
                    "createdTime": "2022-07-26T20:56:21Z",
                    "currency": "USD",
                    "amount": 362.95,
                    "state": "capturable",
                    "captured": false,
                    "refunded": false,
                    "sourceId": "d82add35-93e0-4917-8e54-3b595a997dfb",
                    "type": "customer_initiated"
                }
            ],
            "sources": [
                {
                    "id": "d82add35-93e0-4917-8e54-3b595a997dfb",
                    "type": "creditCard",
                    "amount": 362.95,
                    "owner": {
                        "firstName": "Anna",
                        "lastName": "Brawner",
                        "email": "ab@dr.com",
                        "address": {
                            "line1": "Neuer Wall 10",
                            "city": "Hamburg",
                            "postalCode": "20354",
                            "country": "DE"
                        }
                    },
                    "creditCard": {
                        "brand": "AmericanExpress",
                        "expirationMonth": 12,
                        "expirationYear": 2024,
                        "lastFourDigits": "2341"
                    }
                }
            ],
            "session": {
                "id": "522179af-8481-4078-88e3-c305cc55fc77",
                "amountContributed": 362.95,
                "amountRemainingToBeContributed": 0,
                "state": "complete",
                "clientSecret": "522179af-8481-4078-88e3-c305cc55fc77_be36a393-8432-4354-bb10-efcb90b40f45"
            }
        },
        "state": "accepted",
        "stateTransitions": {
            "accepted": "2022-07-26T20:56:22Z"
        },
        "fraudState": "passed",
        "fraudStateTransitions": {
            "passed": "2022-07-26T20:56:22Z"
        },
        "taxInclusive": false,
        "liveMode": false
    }
}
```
{% endcode %}

## `requiresShipping`

The `requiresShipping` boolean indicates whether it's necessary to display the [shipping component](shipping-component.md). If `false`, then the [checkout-session's](../../../digital-river-api-reference/checkout-sessions.md) `items[]` might only contain [digital products](../../../../product-management/skus.md#how-products-are-classified-as-physical-or-digital), or the customer might have opted to use the [wallet component](wallet-component.md). In either case, you won't need to display the shipping component to process the transaction successfully.

## `showTaxIdentifiers`

The `showTaxIdentifiers` boolean indicates whether it's necessary to display the [tax identifier component](tax-identifier-component.md). It's often `true` when the [checkout-session's](../../../digital-river-api-reference/checkout-sessions.md) `customerType` is `business` and (1) the customer selects a non-United States shipping and/or billing country in the [address component](address-component.md), or (2) you assign [`shoppingCountry`](../../../digital-river-api-reference/checkout-sessions.md#shopping-country) a non-`US` value.

## `showInvoiceAttribute`

The `showInvoiceAttribute` boolean indicates whether it's necessary to display the [invoice component](invoice-component.md). If `true`this indicates that a Taiwanese-based customer is making the purchase as an individual (i.e., a B2C transaction).



