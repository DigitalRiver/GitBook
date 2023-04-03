---
description: Learn how to apply an immediate midterm change to a subscription.
---

# Applying an immediate midterm change

## Applying a midterm change with price override using the Preview cart resource <a href="#apply-a-unit-prorated-price-using-the-preview-cart-resource" id="apply-a-unit-prorated-price-using-the-preview-cart-resource"></a>

In this scenario, the customer has a basic subscription and decided to upgrade the subscription product.&#x20;

Use the [`POST /v1/subscriptions/{subscriptionId}/preview-cart`](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Immediate-Midterm-Change/operation/previewCartSubscription) resource to upgrade the customer's subscription product. You must include the product identifier (`id`), the quantity (`quantity`), and the prorated Unit Price (`proratedUnitPrice`). In the following example, the value for the `proratedUnitPrice` is `20.5`.  See the [preview-cart](../../general-resources/admin-apis-reference/subscriptions/#preview-cart-resource) resource for more information.

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```javascript
curl --location --request POST 'https://api.digitalriver.com/v1/subscriptions/{subscriptionId}/preview-cart' \
--header 'authorization: bearer ***\
...
--data-raw '{
  "product" : {
    "id" : "5410723500"
  },
  "quantity" : 1,
  "proratedUnitPrice" : 20.5
}'
```
{% endcode %}
{% endtab %}

{% tab title="200 OK response" %}
You will receive a `200 OK` response.

{% code overflow="wrap" %}
```json
{
  "subscriptionId" : "29123",
  "subTotal" : 20.5,
  "credit" : 0.0,
  "totalTax" : 1.54,
  "totalAmountDue" : 22.04,
  "currency" : "USD",
  "prorationDate" : "2020-11-26",
  "previewCharges" : [ {
    "product" : "5410723500",
    "quantity" : 1,
    "unitPrice" : 20.5,
    "proratedUnitPrice" : 20.5
  } ],
  "previewSubscription" : {
    "product" : {
      "id" : "5410723500"
    },
    "quantity" : 1,
    "proratedUnitPrice" : 20.5
  },
  "cart" : {
    "token" : "bearer ff3d0ca3f03a9805f7bb7ba6d6f3ff437d6bece8fbf59bbe6041ba51520d6e135200848bdb30735576b68113ec68da16fba1379afb620d4d9a7240f50178191dd98fdd9bc7f5562d4a1fe30922798cd6616a3e0eef029b1f9d594bc8381ebace1b8cf24d2cee7a0a",
    "url" : "[https://subsgc-abe-sprint-2-ods.digitalriver.engineering/store?Action=DisplayHGOP2LandingPage&Locale=en_US&SiteID=sub2test&Token=cXYfXElGUklJQEBfT0ZUTFVGWlVJW11IJbQA&session=C629A67BACB2B8E4CD297DFBCC96A0B24E36D4E70B6C6B646C065A28D8C0AB7B27A01188AD4D093E99A0B8CF2A7A90EC3ECBAEC46E56A5BFAB6C29D2B248DAB2CA9093DA7085A931243E1C5C6C865F24009BE7A5BAF2930FF725F9FBDDE93573E12F891EB4A0EF73]"
  },
  "isCartNeeded" : true,
  "isPaymentOnFile" : true
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

See [Midterm change](../../general-resources/admin-apis-reference/subscriptions/midterm-change.md) for more information.

## Applying a midterm change with price override using the Preview resource <a href="#apply-a-unit-prorated-price-using-the-preview-resource" id="apply-a-unit-prorated-price-using-the-preview-resource"></a>

In this scenario, the customer has a basic subscription and decided to upgrade the subscription product.&#x20;

Use the  [`POST /v1/subscriptions/{subscriptionId}/preview`](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Immediate-Midterm-Change/operation/previewSubscription) resource to upgrade the customer's subscription product. You need to include the product identifier (`id`), the quantity (`quantity`), and the prorated Unit Price (`proratedUnitPrice`). In the following example, the value for the `proratedUnitPrice` is `20.5`. See the [preview ](../../general-resources/admin-apis-reference/subscriptions/#preview-resource)resource for more information.

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```javascript
curl --location --request POST 'https://api.digitalriver.com/v1/subscriptions/{subscriptionId}/preview' \
--header 'Content-Type:  application/json' \
--header 'authorization: bearer ***\
--data-raw '{    
  "product" : {
    "id" : "5410723500"
  },
  "quantity" : 1,
  "proratedUnitPrice" : 20.5
}'
```
{% endcode %}
{% endtab %}

{% tab title="200 OK response" %}
You will receive a `200 OK` response.

{% code overflow="wrap" %}
```json
{
  "subscriptionId" : "29123",
  "subTotal" : 20.5,
  "credit" : 0.0,
  "totalTax" : 1.54,
  "totalAmountDue" : 22.04,
  "currency" : "USD",
  "prorationDate" : "2020-11-26",
  "previewCharges" : [ {
    "product" : "5410723500",
    "quantity" : 1,
    "unitPrice" : 20.5,
    "proratedUnitPrice" : 20.5
  } ],
  "previewSubscription" : {
    "product" : {
      "id" : "5410723500"
    },
    "quantity" : 1,
    "proratedUnitPrice" : 20.5
  },
    "isCartNeeded" : false,
  "isPaymentOnFile" : true
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Applying an immediate midterm change

In this scenario, you agreed with the customer to change the subscription renewal price.

Use the [`POST /v1/subscriptions/{subscriptionId}/renewal-price`](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Subscription-Renewal/operation/changeSubscriptionRenewalPrice) resource to change the subscription renewal price. You need to include the `subscriptionId` and the `renewalUnitPrice`. Note that the `renewalUnitPrice` cannot be higher than the existing price. See the [renewal-price](../../general-resources/admin-apis-reference/subscriptions/#renewal-price-source) resource for more information.

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```javascript
curl --location --request POST 'https://api.digitalriver.com/v1/subscriptions/{subscriptionId}/renewal-price' \
--header 'Content-Type:  application/json' \
--header 'authorization: bearer ***\
--data-raw '{    
"renewalUnitPrice" : 4
}'
```
{% endcode %}
{% endtab %}
{% endtabs %}

You will receive a `200 Accepted` response.

See [Midterm change](../../general-resources/admin-apis-reference/subscriptions/midterm-change.md) for more information.
