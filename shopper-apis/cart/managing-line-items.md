---
description: Learn how to manage line items.
---

# Managing line items

## Getting all line items from a cart

You can use the [Line Items](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Line-Items) resource to get all line items, including products, pricing, and tax information from a cart.

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```http
curl --location --request GET 'https://api.digitalriver.com/v1/shoppers/me/carts/active/line-items' \
--header 'authorization: bearer ***\
...
```
{% endcode %}
{% endtab %}

{% tab title="200 OK response" %}
{% code overflow="wrap" %}
```json
{
  "uri": "https://api.digitalriver.com/v1/shoppers/me/carts/active/line-items",
  "lineItems": [
    {
      "uri": "https://api.digitalriver.com/v1/shoppers/me/carts/active/line-items/488822300023",
      "id": "488822300023",
      "quantity": "1",
      "product": {
        "uri": "https://api.digitalriver.com/v1/shoppers/me/products/64578500",
        "parentProduct": {
          "uri": "https://api.digitalriver.com/v1/shoppers/me/products/64358200"
        },
        "id": "64578500",
        "name": "Class I",
        "displayName": "Class I",
        "shortDescription": "Class I is the perfect GPS waypoint and route manager for the beginning or occasional GPS user.",
        "longDescription": "Class I is the fast and easy way to create, edit, and transfer waypoints and routes between your computer and your Garmin, Magellan, or Lowrance GPS. Using Class I, you can manage all of your waypoints and routes, and display them in lists sorted by name, elevation, or distance. Class I connects your GPS to the best mapping and information sites on the Internet, giving you one-click access to street and topo maps, aerial photos, weather forecasts, and nearby attractions.",
        "productType": "DOWNLOAD",
        "sku": "Class I",
        "externalReferenceId": "Test External Reference Number",
        "companyId": "demosft1",
        "displayableProduct": "true",
        "purchasable": "true",
        "manufacturerName": "Test Manufacturer Name",
        "manufacturerPartNumber": "Test Manufacturer Part Number",
        "thumbnailImage": "https://drh-int-ora.img.digitalriver.com/Storefront/Company/demosft1/images/product/thumbnail/classIThumb.jpg",
        "productImage": "https://drh-int-ora.img.digitalriver.com/Storefront/Company/demosft1/images/product/detail/classIBox.jpg",
        "keywords": "testKeyword",
        "customAttributes": {
          "attribute": [
            {
              "name": "name",
              "value": "string",
              "type": "string"
            }
          ]
        }
      },
      "pricing": {
        "listPrice": {
          "currency": "USD",
          "value": 101
        },
        "listPriceWithQuantity": {
          "currency": "USD",
          "value": 1010
        },
        "salePriceWithQuantity": {
          "currency": "USD",
          "value": 959.5
        },
        "formattedListPrice": "101.00USD",
        "formattedListPriceWithQuantity": "1010.00USD",
        "formattedSalePriceWithQuantity": "959.50USD",
        "formattedCommitmentPrice": "$240.00",
        "commitmentPrice": {
          "currency": "USD",
          "value": "240.00"
        },
        "productTax": {
          "currency": "USD",
          "value": "1.35"
        },
        "shippingTax": {
          "currency": "USD",
          "value": "0.65"
        },
        "feeTax": {
          "currency": "USD",
          "value": "2.00"
        },
        "taxRate": "0.1111",
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
      }
    }
  ]
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Getting a specific line item from a cart

You can use the Line Items resource to [get all line items](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Line-Items), including products, pricing, and tax information from a cart.

{% tabs %}
{% tab title="cURL" %}
<pre class="language-http" data-overflow="wrap"><code class="lang-http">curl --location --request GET 'https://api.digitalriver.com/v1/shoppers/me/carts/active/line-items/{lineItesId}' \
--header 'authorization: bearer<a data-footnote-ref href="#user-content-fn-1"> </a>***\
...
</code></pre>
{% endtab %}

{% tab title="200 OK response" %}
{% code overflow="wrap" %}
```json
{
  "uri": "https://api.digitalriver.com/v1/shoppers/me/carts/active/line-items/488822300023",
  "id": "488822300023",
  "quantity": "1",
  "product": {
    "uri": "https://api.digitalriver.com/v1/shoppers/me/products/64578500",
    "parentProduct": {
      "uri": "https://api.digitalriver.com/v1/shoppers/me/products/64358200"
    },
    "id": "64578500",
    "name": "Class I",
    "displayName": "Class I",
    "shortDescription": "Class I is the perfect GPS waypoint and route manager for the beginning or occasional GPS user.",
    "longDescription": "Class I is the fast and easy way to create, edit, and transfer waypoints and routes between your computer and your Garmin, Magellan, or Lowrance GPS. Using Class I, you can manage all of your waypoints and routes, and display them in lists sorted by name, elevation, or distance. Class I connects your GPS to the best mapping and information sites on the Internet, giving you one-click access to street and topo maps, aerial photos, weather forecasts, and nearby attractions.",
    "productType": "DOWNLOAD",
    "sku": "Class I",
    "externalReferenceId": "Test External Reference Number",
    "companyId": "demosft1",
    "displayableProduct": "true",
    "purchasable": "true",
    "manufacturerName": "Test Manufacturer Name",
    "manufacturerPartNumber": "Test Manufacturer Part Number",
    "thumbnailImage": "https://drh-int-ora.img.digitalriver.com/Storefront/Company/demosft1/images/product/thumbnail/classIThumb.jpg",
    "productImage": "https://drh-int-ora.img.digitalriver.com/Storefront/Company/demosft1/images/product/detail/classIBox.jpg",
    "keywords": "testKeyword",
    "customAttributes": {
      "attribute": [
        {
          "name": "name",
          "value": "string",
          "type": "string"
        }
      ]
    }
  },
  "pricing": {
    "listPrice": {
      "currency": "USD",
      "value": 101
    },
    "listPriceWithQuantity": {
      "currency": "USD",
      "value": 1010
    },
    "salePriceWithQuantity": {
      "currency": "USD",
      "value": 959.5
    },
    "formattedListPrice": "101.00USD",
    "formattedListPriceWithQuantity": "1010.00USD",
    "formattedSalePriceWithQuantity": "959.50USD",
    "formattedCommitmentPrice": "$240.00",
    "commitmentPrice": {
      "currency": "USD",
      "value": "240.00"
    },
    "productTax": {
      "currency": "USD",
      "value": "1.35"
    },
    "shippingTax": {
      "currency": "USD",
      "value": "0.65"
    },
    "feeTax": {
      "currency": "USD",
      "value": "2.00"
    },
    "taxRate": "0.1111",
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
  }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Getting line items for an order

You can [get all line items for an order](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Line-Items/paths/\~1v1\~1shoppers\~1me\~1orders\~1%7BorderId%7D\~1line-items/get) when you specify the `orderId`.

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```http
curl --location --request GET 'https://api.digitalriver.com/v1/shoppers/me/orders/{orderId}/line-items' \
--header 'authorization: bearer ***\
...
```
{% endcode %}
{% endtab %}

{% tab title="200 OK response" %}
{% code overflow="wrap" %}
```json
{
  "uri": "https://api.digitalriver.com/v1/shoppers/me/orders/47276010023/line-items",
  "lineItem": [
    {
      "uri": "https://api.digitalriver.com/v1/shoppers/me/orders/47276010023/line-items/488822300023",
      "id": "488822300023",
      "quantity": 1,
      "product": {
        "uri": "https://api.digitalriver.com/v1/shoppers/me/products/5112133200",
        "displayName": "Good Product",
        "thumbnailImage": "string"
      },
      "lineItemState": "Complete",
      "lineItemStateDetails": {
        "description": "Downloadable - 1",
        "backOrdered": 0,
        "shipped": 0,
        "returned": 0,
        "pendingReturn": 0
      },
      "pricing": {
        "listPrice": {
          "currency": "USD",
          "value": 101
        },
        "listPriceWithQuantity": {
          "currency": "USD",
          "value": 1010
        },
        "salePriceWithQuantity": {
          "currency": "USD",
          "value": 959.5
        },
        "formattedListPrice": "101.00USD",
        "formattedListPriceWithQuantity": "1010.00USD",
        "formattedSalePriceWithQuantity": "959.50USD",
        "formattedCommitmentPrice": "$240.00",
        "commitmentPrice": {
          "currency": "USD",
          "value": "240.00"
        },
        "productTax": {
          "currency": "USD",
          "value": "1.35"
        },
        "shippingTax": {
          "currency": "USD",
          "value": "0.65"
        },
        "feeTax": {
          "currency": "USD",
          "value": "2.00"
        },
        "taxRate": "0.1111",
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
      "downloads": {
        "downloadUri": [
          "https://wgtsysot12.digitalriver.com/wgt/9B5A4FCEF11DA80C/171F14235882A3D349C4DF3E9F68F51B28573D6CB50E888238DC305C96D769176F6A4F895B77C58CF0F67A3572E1FE49934F924414F2486E45C01D39B94ADFA2E0920C4390CBA6042FE0C88CD46AAEA99C060E2044E521050A7DE0793B014624647C638FDE4F6D4D/demosft1/WaterLilies.jpg"
        ]
      },
      "digitalRights": {
        "serialNumber": {}
      },
      "billingAgreementId": "fc86a666-9f2f-4294-b591-468ae34122ff",
      "subscriptionIds": [
        "[15564325189,15564325289]"
      ]
    }
  ]
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Getting a specific line item for an order

You can [get a specific line item for an order](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Line-Items/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1line-items\~1%7BlineItemsId%7D/get) when you specify the `orderId`.

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```http
curl --location --request GET 'https://api.digitalriver.com/v1/shoppers/me/orders/{orderId}/line-items/[lineItemId]' \
--header 'authorization: bearer ***\
...
```
{% endcode %}
{% endtab %}

{% tab title="200 OK response" %}
{% code overflow="wrap" %}
```json
{
  "uri": "https://api.digitalriver.com/v1/shoppers/me/orders/47276010023/line-items/488822300023",
  "id": "488822300023",
  "quantity": 1,
  "product": {
    "uri": "https://api.digitalriver.com/v1/shoppers/me/products/5112133200",
    "displayName": "Good Product",
    "thumbnailImage": "string"
  },
  "lineItemState": "Complete",
  "lineItemStateDetails": {
    "description": "Downloadable - 1",
    "backOrdered": 0,
    "shipped": 0,
    "returned": 0,
    "pendingReturn": 0
  },
  "pricing": {
    "listPrice": {
      "currency": "USD",
      "value": 101
    },
    "listPriceWithQuantity": {
      "currency": "USD",
      "value": 1010
    },
    "salePriceWithQuantity": {
      "currency": "USD",
      "value": 959.5
    },
    "formattedListPrice": "101.00USD",
    "formattedListPriceWithQuantity": "1010.00USD",
    "formattedSalePriceWithQuantity": "959.50USD",
    "formattedCommitmentPrice": "$240.00",
    "commitmentPrice": {
      "currency": "USD",
      "value": "240.00"
    },
    "productTax": {
      "currency": "USD",
      "value": "1.35"
    },
    "shippingTax": {
      "currency": "USD",
      "value": "0.65"
    },
    "feeTax": {
      "currency": "USD",
      "value": "2.00"
    },
    "taxRate": "0.1111",
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
  "downloads": {
    "downloadUri": [
      "https://wgtsysot12.digitalriver.com/wgt/9B5A4FCEF11DA80C/171F14235882A3D349C4DF3E9F68F51B28573D6CB50E888238DC305C96D769176F6A4F895B77C58CF0F67A3572E1FE49934F924414F2486E45C01D39B94ADFA2E0920C4390CBA6042FE0C88CD46AAEA99C060E2044E521050A7DE0793B014624647C638FDE4F6D4D/demosft1/WaterLilies.jpg"
    ]
  },
  "digitalRights": {
    "serialNumber": {}
  },
  "billingAgreementId": "fc86a666-9f2f-4294-b591-468ae34122ff",
  "subscriptionIds": [
    "[15564325189,15564325289]"
  ]
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Adding line items to a cart

You can [add one or more line items to a cart](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Line-Items/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1line-items/post).

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```http
curl --location --request POST 'https://api.digitalriver.com/shoppers/v1/shoppers/me/carts/active/line-items' \
--header 'authorization: bearer ***\
...
--data-raw '{
  "lineItems": {
    "lineItem": {
      "id": "991101014",
      "quantity": "1",
      "product": {
        "id": 1234
      },
      "pricing": {
        "salePrice": {
          "currency": "USD",
          "value": "10.99"
        }
      },
      "customAttributes": {
        "attribute": [
          {
            "name": "name",
            "value": "string",
            "type": "string"
          }
        ]
      }
    }
  }
}'
```
{% endcode %}
{% endtab %}

{% tab title="200 OK response" %}
{% code overflow="wrap" %}
```json
{
  "uri": "https://api.digitalriver.com/v1/shoppers/me/carts/active/line-items",
  "lineItems": [
    {
      "uri": "https://api.digitalriver.com/v1/shoppers/me/carts/active/line-items/488822300023",
      "id": "488822300023",
      "quantity": "1",
      "product": {
        "uri": "https://api.digitalriver.com/v1/shoppers/me/products/64578500",
        "parentProduct": {
          "uri": "https://api.digitalriver.com/v1/shoppers/me/products/64358200"
        },
        "id": "64578500",
        "name": "Class I",
        "displayName": "Class I",
        "shortDescription": "Class I is the perfect GPS waypoint and route manager for the beginning or occasional GPS user.",
        "longDescription": "Class I is the fast and easy way to create, edit, and transfer waypoints and routes between your computer and your Garmin, Magellan, or Lowrance GPS. Using Class I, you can manage all of your waypoints and routes, and display them in lists sorted by name, elevation, or distance. Class I connects your GPS to the best mapping and information sites on the Internet, giving you one-click access to street and topo maps, aerial photos, weather forecasts, and nearby attractions.",
        "productType": "DOWNLOAD",
        "sku": "Class I",
        "externalReferenceId": "Test External Reference Number",
        "companyId": "demosft1",
        "displayableProduct": "true",
        "purchasable": "true",
        "manufacturerName": "Test Manufacturer Name",
        "manufacturerPartNumber": "Test Manufacturer Part Number",
        "thumbnailImage": "https://drh-int-ora.img.digitalriver.com/Storefront/Company/demosft1/images/product/thumbnail/classIThumb.jpg",
        "productImage": "https://drh-int-ora.img.digitalriver.com/Storefront/Company/demosft1/images/product/detail/classIBox.jpg",
        "keywords": "testKeyword",
        "customAttributes": {
          "attribute": [
            {
              "name": "name",
              "value": "string",
              "type": "string"
            }
          ]
        }
      },
      "pricing": {
        "listPrice": {
          "currency": "USD",
          "value": 101
        },
        "listPriceWithQuantity": {
          "currency": "USD",
          "value": 1010
        },
        "salePriceWithQuantity": {
          "currency": "USD",
          "value": 959.5
        },
        "formattedListPrice": "101.00USD",
        "formattedListPriceWithQuantity": "1010.00USD",
        "formattedSalePriceWithQuantity": "959.50USD",
        "formattedCommitmentPrice": "$240.00",
        "commitmentPrice": {
          "currency": "USD",
          "value": "240.00"
        },
        "productTax": {
          "currency": "USD",
          "value": "1.35"
        },
        "shippingTax": {
          "currency": "USD",
          "value": "0.65"
        },
        "feeTax": {
          "currency": "USD",
          "value": "2.00"
        },
        "taxRate": "0.1111",
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
      }
    }
  ]
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Updating one or more line items to a cart

You can [update one or more line items to a cart](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Line-Items/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1line-items\~1%7BlineItemsId%7D/post).

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```http
curl --location --request POST 'https://api.digitalriver.com/shoppers/v1/shoppers/me/carts/active/line-items/{lineItemId}' \
--header 'authorization: bearer ***\
...
```
{% endcode %}
{% endtab %}

{% tab title="200 OK response" %}
{% code overflow="wrap" %}
```json
{
  "uri": "https://api.digitalriver.com/v1/shoppers/me/carts/active/line-items/488822300023",
  "id": "488822300023",
  "quantity": "1",
  "product": {
    "uri": "https://api.digitalriver.com/v1/shoppers/me/products/64578500",
    "parentProduct": {
      "uri": "https://api.digitalriver.com/v1/shoppers/me/products/64358200"
    },
    "id": "64578500",
    "name": "Class I",
    "displayName": "Class I",
    "shortDescription": "Class I is the perfect GPS waypoint and route manager for the beginning or occasional GPS user.",
    "longDescription": "Class I is the fast and easy way to create, edit, and transfer waypoints and routes between your computer and your Garmin, Magellan, or Lowrance GPS. Using Class I, you can manage all of your waypoints and routes, and display them in lists sorted by name, elevation, or distance. Class I connects your GPS to the best mapping and information sites on the Internet, giving you one-click access to street and topo maps, aerial photos, weather forecasts, and nearby attractions.",
    "productType": "DOWNLOAD",
    "sku": "Class I",
    "externalReferenceId": "Test External Reference Number",
    "companyId": "demosft1",
    "displayableProduct": "true",
    "purchasable": "true",
    "manufacturerName": "Test Manufacturer Name",
    "manufacturerPartNumber": "Test Manufacturer Part Number",
    "thumbnailImage": "https://drh-int-ora.img.digitalriver.com/Storefront/Company/demosft1/images/product/thumbnail/classIThumb.jpg",
    "productImage": "https://drh-int-ora.img.digitalriver.com/Storefront/Company/demosft1/images/product/detail/classIBox.jpg",
    "keywords": "testKeyword",
    "customAttributes": {
      "attribute": [
        {
          "name": "name",
          "value": "string",
          "type": "string"
        }
      ]
    }
  },
  "pricing": {
    "listPrice": {
      "currency": "USD",
      "value": 101
    },
    "listPriceWithQuantity": {
      "currency": "USD",
      "value": 1010
    },
    "salePriceWithQuantity": {
      "currency": "USD",
      "value": 959.5
    },
    "formattedListPrice": "101.00USD",
    "formattedListPriceWithQuantity": "1010.00USD",
    "formattedSalePriceWithQuantity": "959.50USD",
    "formattedCommitmentPrice": "$240.00",
    "commitmentPrice": {
      "currency": "USD",
      "value": "240.00"
    },
    "productTax": {
      "currency": "USD",
      "value": "1.35"
    },
    "shippingTax": {
      "currency": "USD",
      "value": "0.65"
    },
    "feeTax": {
      "currency": "USD",
      "value": "2.00"
    },
    "taxRate": "0.1111",
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
  }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Deleting all line items from a cart

You can [delete all line items from a cart](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Line-Items/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1line-items/delete).

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```http
curl --location --request DELETE 'https://api.digitalriver.com/shoppers/v1/shoppers/me/carts/active/line-items' \
--header 'authorization: bearer ***\
...
```
{% endcode %}
{% endtab %}
{% endtabs %}

You will get a `204 No Content` response.

## Deleting a specific line item from a cart

You can [delete a specific line item from a cart](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Line-Items/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1line-items\~1%7BlineItemsId%7D/delete).

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```http
curl --location --request DELETE 'https://api.digitalriver.com/shoppers/v1/shoppers/me/carts/active/line-items/{lineItemId}' \
--header 'authorization: bearer ***\
...
```
{% endcode %}
{% endtab %}
{% endtabs %}

You will get a `204 No Content` response.

## Key attributes

### Line item

The `lineItems` in the cart's response body provide the details of a physical or digital product including, quantity, product, product ID, and pricing.

#### Product

A `product` provides the details of a physical or digital product.

#### Pricing

The `pricing` defines the pricing for the item and provides the tax information. Digital River provides the tax rate (`taxRate`) information and the amount (`tax`) at the line item level.

#### Tax

Digital River automatically calculates the tax rate. The `taxRate` requires a decimal value. For example, if the calculated tax rate is 19%, the value is `.19`, as shown in the following example.

{% tabs %}
{% tab title="Example" %}
{% code overflow="wrap" %}
```json
"tax": {
	"currency": "EUR",
	"value": 6.93
},
"taxRate": 0.19
```
{% endcode %}
{% endtab %}
{% endtabs %}

[^1]: 
