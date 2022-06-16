---
description: >-
  Learn how to apply a midterm change with a price override for a subscription
  with add-ons.
---

# Applying a midterm change with price override

## Applying a midterm change with price override using the Preview cart resource <a href="#apply-a-unit-prorated-price-using-the-preview-cart-resource" id="apply-a-unit-prorated-price-using-the-preview-cart-resource"></a>

In this scenario, the customer has a basic subscription and decided to upgrade the subscription product with add-on using `POST /v1/subscriptions/{subscriptionId}/preview-cart`.

Use the [`POST /v1/subscriptions/{subscriptionId}/preview-cart`](https://www.digitalriver.com/docs/commerce-api-reference/#operation/previewCartSubscription) resource to upgrade the customer's subscription product. You need to include the product identifier (`id`), the quantity (`quantity`), and the prorated Unit Price (`proratedUnitPrice`). In the following example, the value for the `proratedUnitPrice` is `20.5`.&#x20;

{% tabs %}
{% tab title="cURL" %}
```javascript
curl --location --request POST 'https://<<host>>/v1/subscriptions/{subscriptionId}/preview-cart' \
--header 'Content-Type:  application/json' \
--header 'authorization: bearer ***\
--data-raw '{
  "product" : {
    "id" : "5396391700"
  },
  "quantity" : 1,
  "addOns" : [ {
    "product" : {
      "id" : "5400082600"
    },
    "quantity" : 1,
    "proratedUnitPrice" : 0.0
  } ],
  "proratedUnitPrice" : 20.5
}'
```
{% endtab %}
{% endtabs %}

You will receive a `200 OK` response.

{% tabs %}
{% tab title="JSON" %}
```javascript
{
  "subscriptionId" : "15682787789",
  "subTotal" : 20.5,
  "credit" : 0.0,
  "totalTax" : 0.0,
  "totalAmountDue" : 20.5,
  "currency" : "USD",
  "prorationDate" : "2021-03-03",
  "previewCharges" : [ {
    "product" : "5396391700",
    "quantity" : 1,
    "unitPrice" : 20.5,
    "proratedUnitPrice" : 20.5
  } ],
  "previewSubscription" : {
    "addOns" : [ {
      "product" : {
        "id" : "5400082600"
      },
      "quantity" : 1,
      "proratedUnitPrice" : 0.0
    } ],
    "product" : {
      "id" : "5396391700"
    },
    "quantity" : 1,
    "proratedUnitPrice" : 20.5
  },
  "cart" : {
    "token" : "bearer dbea3e7a3605b764afe1113c3bd539aee2645ebef2c5581584663d957b514f24d205a4b72aa404acc03d85062b1b7c99954ef1e22c9a2de5a9214082273e2ee0e5480ea0e38cc85260e9c7d22d7e8851",
    "url" : "[https://drhadmin-sys-drx.drextenv.net/store?Action=DisplayHGOP2LandingPage&Locale=en_US&SiteID=sub2test&Token=eHBLKQgMBhgUBTIFSVpVSVxFXVhBW1RJUk1fVU9TVktVewA%3D&session=CB289EB23D78E50C7203166BFDD6CF1AAA48BA8DDDED419570AB88C662F4B8480D9146F3517FB71E6658420B74105DE424E90940F72DAC34E5F9EF1E089976E25ED5A6AEB92345D8420A79758692FFFE]"
  },
  "isCartNeeded" : true,
  "isPaymentOnFile" : true
}
```
{% endtab %}
{% endtabs %}

## Applying a midterm change with price override using the Preview resource <a href="#apply-a-unit-prorated-price-using-the-preview-resource" id="apply-a-unit-prorated-price-using-the-preview-resource"></a>

In this scenario, the customer has a basic subscription and decided to upgrade the subscription product with add-ons using `POST /v1/subscriptions/{subscriptionId}/preview`.

Use the [`POST /v1/subscriptions/{subscriptionId}/preview`](https://www.digitalriver.com/docs/commerce-api-reference/#operation/previewSubscription) resource to upgrade the customer's subscription product. You need to include the product identifier (`id`), the quantity (`quantity`), the prorated Unit Price (`proratedUnitPrice`). In the following example, the value for the `proratedUnitPrice` is `20.5`.&#x20;

{% tabs %}
{% tab title="cURL" %}
```javascript
curl --location --request POST 'https://{host}/v1/subscriptions/{subscriptionId}/preview' \
--header 'Content-Type:  application/json' \
--header 'authorization: bearer ***\
--data-raw '{    
  "product" : {
    "id" : "5363866300"
  },
  "product" : {
    "id" : "5396391700"
  },
  "product" : {
    "id" : "5396391700"
  },
  "quantity" : 1,
  "addOns" : [ {
    "product" : {
      "id" : "5400082600"
    },
    "quantity" : 1,
    "proratedUnitPrice" : 0.0
  } ],
  "proratedUnitPrice" : 20.5
}

```
{% endtab %}
{% endtabs %}

You will receive a `200 OK` response.

{% tabs %}
{% tab title="JSON" %}
```javascript
{
  "subscriptionId" : "15684493989",
  "subTotal" : 20.5,
  "credit" : 0.0,
  "totalTax" : 0.0,
  "totalAmountDue" : 20.5,
  "currency" : "USD",
  "prorationDate" : "2021-03-05",
  "previewCharges" : [ {
    "product" : "5396391700",
    "quantity" : 1,
    "unitPrice" : 20.5,
    "proratedUnitPrice" : 20.5
  } ],
  "previewSubscription" : {
    "addOns" : [ {
      "product" : {
        "id" : "5400082600"
      },
      "quantity" : 1,
      "proratedUnitPrice" : 0.0
    } ],
    "product" : {
      "id" : "5396391700"
    },
    "quantity" : 1,
    "proratedUnitPrice" : 20.5
  },
  "isCartNeeded" : true,
  "isPaymentOnFile" : true
}

```
{% endtab %}
{% endtabs %}
