---
description: >-
  Learn how to provide the customer's subscription information that Digital
  River needs to process recurring payments.
---

# Providing subscription information

## Billing agreement identifier

As part of the [PSD2 Strong Customer Authentication (SCA)](https://info.digitalriver.com/rs/348-QUY-258/images/Digital\_River\_Guide\_to\_PSD2\_Compliance\_2020.pdf) initiative, payment processors require extra information when processing merchant-initiated credit card transactions. To ensure that you adhere to the new mandate, you'll need to make use of billing agreements.

A billing agreement consists of the [terms](providing-subscription-information.md#terms) customers agree to when they consent to have their credit card details applied to any type of recurring purchase. The identifier of the agreement is then referenced on subsequent renewals.&#x20;

If you sell your product or service as part of a subscription and you want to use an external subscription engine to manage your subscriptions, you _must_ :

* [Create a product](https://help.digitalriver.com/help/gc/Products/All-Products/Creating-a-product.htm) in [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do) without selecting the Subscription option and [deploy the product](https://help.digitalriver.com/help/gc/Products/All-Products/Deploying-products.htm).
* Include the `subscriptionInfo` hash table.  As [reseller of record](../../../#working-with-digital-river), Digital River is required to collect the basic information contained in this data structure.&#x20;

To add a subscription to a product for a customer, include `subscriptionInfo`  in  the `LineItem` array. You can add `subsciptionInfo` to the [`POST/carts`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Carts/paths/\~1v1\~1shoppers\~1me\~1carts\~1active/post), [`POST /line-items`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Line-Items/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1line-items/post), or [`POST /line-items/{lineItemsId}`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Line-Items/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1line-items\~1{lineItemsId}/post) requests. The following [`POST/carts`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Carts/paths/\~1v1\~1shoppers\~1me\~1carts\~1active/post) request includes the subscription parameters related to [auto renewals](providing-subscription-information.md#auto-renewal), [free trials](providing-subscription-information.md#subscription-lifecycle), and the [terms](providing-subscription-information.md#terms) displayed to the customer. You can also provide the [subscription](providing-subscription-information.md#subscription-identifier) and the [billing agreement](providing-subscription-information.md#billing-agreement-identifier) identifiers.&#x20;

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```json
curl --location --request POST 'https://api.digitalriver.com/v1/shoppers/me/carts/active' \
--header 'Authorization: Bearer {{Token}}' \
...
--data-raw '{
    "cart": {
        "ipAddress": "{{BrowserIP}}",
        "lineItems": {
            "lineItem": [
                {
                    "quantity": 1,
                    "product": {
                        "id": "{{ExternalSubPID}}"
                    },
                    "subscriptionInfo": {
                        "autoRenewal": true,
                        "terms": "I agree to have client charge all my future bills on this card",
                        "freeTrial": false,
                        "billingAgreementId": null
                    }
                }
            ]
        }
    }
}'
```
{% endcode %}
{% endtab %}
{% endtabs %}

The `subscriptionInfo` hash table appears in the following responses: [`POST /carts/active`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Carts/paths/\~1v1\~1shoppers\~1me\~1carts\~1active/get), [`POST /line-items`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Line-Items/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1line-items/post), [`POST /line-items/{lineItemsId}`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Line-Items/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1line-items\~1{lineItemsId}/post), and [`POST /submit-cart`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Submit-Cart/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1submit-cart/post) , and [`GET /orders`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Orders/paths/\~1v1\~1shoppers\~1me\~1orders/get) (if available). To get the [`billingAgreementId`](providing-subscription-information.md#billing-agreement-identifier),  [submit the cart](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Submit-Cart/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1submit-cart/post).

The following `POST /submit-cart` response includes the `billingAgreementId` from the payment service.

{% tabs %}
{% tab title="JSON" %}
{% code overflow="wrap" %}
```json
...
  "lineItems": {
    "lineItem": [
      {
        "id": "12151550082",
        "quantity": "1",
        "product": {...
        },
      "lineItemState": "Downloadable",
      "lineItemStateDetails": {
        "description": "Downloadable - 1",
        "backOrdered": "0",
        "shipped": "0",
        "returned": "0",
        "pendingReturn": "0"
      },
      "pricing": {...
      },
      "downloads": {
        "downloadUri" : [
          "http://wgtintot12.digitalriver.com/wgt/9B5A4FCEF11DA80C/171F14235882A3D3E56B5723F9D46513279A35381E6ECCFA38DC305C96D769173E906E98A04A2B5B3CFFB85C93D810E7B365B18617EBAE4682F5E46FAD1C55CE291C52E8142F3D624C7461A8833978160451C577DBEF2976/demosft1/software.zip"
        ]
      },
      "digitalRights": {},
      "subscriptionInfo": {
        "autoRenewal": "true",
        "terms": "CAPI-395 Anonymous flow",
        "freeTrial": "false",
        "startTime": "2020-09-13T00:00:00.000z",
        "endTime": "2021-09-13T00:00:00.000z",
        "billingAgreementId": "c713ec4d-5fcf-4a3d-9a0c-bcb214480b8d"
      }
    }
  },
...
```
{% endcode %}
{% endtab %}
{% endtabs %}

To create a merchant-initiated transaction (MIT) that charges on renewal of the subscription, include the `billingAgreementId` and a `chargeType` of `merchant_initiated` in the  [`POST /carts`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Carts/paths/\~1v1\~1shoppers\~1me\~1carts\~1active/post) request. transaction (MIT) to add a subscription would look like this:

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```json
curl --location --request POST 'https://api.digitalriver.com/v1/shoppers/me/carts/active' \
--header 'Authorization: Bearer {{Token}}' \
...
--data-raw '{
    "cart": {
        "ipAddress": "{{ServerIP}}",
        "chargeType": "merchant_initiated",
        "lineItems": {
            "lineItem": [
                {
                    "quantity": 1,
                    "product": {
                        "id": "{{RenewalPID}}"
                    },
                    "subscriptionInfo": {
                        "billingAgreementId": "{{billingAgreementId}}"
                    }
                }
            ]
        }
    }
}'
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Auto renewal

Use the `autoRenewal` parameter to tell us whether the subscription is automatically or manually renewed.  If `true`, customers must have agreed to have their card information stored on file and charged at the start of every billing cycle. To do this, you must, at a minimum, [attach a Source to the payment option](../../../payments/sources/using-the-source-identifier.md#attaching-a-source-to-a-payment-option) associated with the subscription and make sure the [Source is reusable](../../../payments/sources/#reusable-or-single-use).&#x20;

If `false`, then the customer needs to manually renew the subscription by resupplying payment date. You can facilitate this by [creating a new instance of Drop-in](../../../payments/payments-solutions/drop-in/) to collect the payment source.&#x20;

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```json
curl --location --request POST 'https://api.digitalriver.com/v1/shoppers/me/carts/active' \
--header 'Authorization: Bearer {{Token}}' \
...
--data-raw '{
    "cart": {
        "ipAddress": "{{ServerIP}}",
        "chargeType": "merchant_initiated",
        "lineItems": {
            "lineItem": [
                {
                    "quantity": 1,
                    "product": {
                        "id": "{{RenewalPID}}"
                    },
                    "subscriptionInfo": {
                        "billingAgreementId": "{{billingAgreementId}}"
                    }
                }
            ]
        }
    }
}'
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Free trial

When you offer customers a free trial period to test run the membership, but you also collect their credit card information, ensure that you set the `freeTrial` attribute to `true`. Digital River needs to know that credit card details are being collected, even when a charge does not occur.

## Terms

Use the `terms` parameter to provide the subscription's auto-renewal terms that are displayed to the customer at the point of acquisition.

## Subscription identifier

At the time of the acquisition, your subscription management system, not Digital River, assigns the `subscriptionId` and passes the value in a `POST /carts` request. &#x20;

Whenever you process a renewal, give us the same `subscriptionId` you provided at the point of acquisition. If the values don't match, we treat the request as a subscription acquisition rather than a renewal. &#x20;

{% hint style="warning" %}
In the next version of the Digital River API, the `subscriptionId` attribute will be deprecated. For this reason, and to ensure you are PSD2 compliant, we recommend you use the [billing agreement identifier](providing-subscription-information.md#billing-agreement-identifier) to process subscription renewals. &#x20;
{% endhint %}

## Creating a billing agreement

You'll first need to ensure that you've [attached a source to the payment option](../../../payments/sources/using-the-source-identifier.md#attaching-a-source-to-a-payment-option) associated with the subscription and that the [source is reusable](../../../payments/sources/#reusable-or-single-use).

You'll then apply the shopper to a cart that includes `subscriptionInfo` hash table in a [`POST /apply-shopper`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Apply-Shopper/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1apply-shopper/post) request and include `billingAgreementId`.&#x20;

After you [submit the cart](../submitting-a-cart/), Digital River generates a billing agreement and returns the `billingAgreementId` in the [`POST /submit-cart`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Submit-Cart/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1submit-cart/post) response.

{% hint style="info" %}
A one-to-one relationship exists between a subscription item and a billing agreement. For example, if your `POST/submit-cart` request contains two line items and both have a `subscriptionInfo` hash table, then Digital River creates two separate billing agreements and returns two billing agreement identifiers.
{% endhint %}

For each subscription that you create, you should persist the `billingAgreementId` that is returned in the response. This is so that you can later provide the value when renewing the subscription.&#x20;

## Using the billing agreement identifier

When it's time to process a renewal, retrieve the `billingAgreementId` you persisted with that subscription. Then, you should include the value in the `subscriptionInfo` hash table of a `POST Cart` request.&#x20;

{% hint style="warning" %}
You should submit the same `billingAgreementId` when renewing the subscription, even if the customer is using a different credit card to pay for the transaction.&#x20;
{% endhint %}

Finally, pass the order identifier returned in the response to a create Cart request. Continue to persist the same `billingAgreementId` for future renewals.

## Commitment price

The `commitmentPrice` hash table appears when you [get a product by identifier](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Products/paths/\~1v1\~1shoppers\~1me\~1products\~1{productId}/get). A `commitmentPrice` is the committed purchase price for a loan or subscription. &#x20;

{% tabs %}
{% tab title="200 OK response" %}
{% code overflow="wrap" %}
```json
...
    "pricing": {
      "uri": "https://api.digitalriver.com/v1/shoppers/me/products/64578500/pricing",
      "listPrice": {
        "currency": "USD",
        "value": "19.99"
      },
      "salePriceWithQuantity": {
        "currency": "USD",
        "value": "19.99"
      },
      "formattedListPrice": "$19.99",
      "formattedSalePriceWithQuantity": "$17.99",
      "msrpPrice": {
        "currency": "USD",
        "value": "19.99"
      },
      "formattedMsrpPrice": "$2.00",
      "listPriceIncludesTax": "false",
      "formattedCommitmentPrice": "$240.00",
      "commitmentPrice": {
        "currency": "USD",
        "value": "240.00"
      }
    },
...
```
{% endcode %}
{% endtab %}
{% endtabs %}

A customer must provide a recurring payment method to pay for a commitment-based subscription. If a customer provides a non-recurring payment method, the following error appears.&#x20;

{% tabs %}
{% tab title="Error response" %}
{% code overflow="wrap" %}
```json
{
    "errors": {
        "error": [
            {
                "relation": "https://api.digitalriver.com/v1/shoppers/CartsResoure",
                "code": "invalid-payment-method",
                "description": "Cannot use non-recurring payment method to purchase a commitment type subscription"
            }
        ]
    }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}
