---
description: Learn how to apply a coupon or promo code.
---

# Applying a coupon or promo code

Coupons or promotional codes encourage store sales by providing discounts on products or shipping costs. You can configure a coupon or promo code offer in Global Commerce and apply that coupon or promo code to an active shopping cart to encourage sales in your stores by providing discounts on products or shipping costs.

Send a [`POST shoppers/me/carts/active`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Carts/paths/\~1v1\~1shoppers\~1me\~1carts\~1active/post) request to the [Carts ](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Carts)resource with the required `promoCode` query parameter. The request must include a valid anonymous or authenticated customer token. No payload is associated with this request; the payload could be empty.

The request in the following example applies a promotional code value of `wb32xjtam`.&#x20;

{% hint style="info" %}
**Note**: A successful request returns a 200 status code in the response header. An unsuccessful request returns an error code in the response.
{% endhint %}

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```json
curl --location --request POST https://api.digitalriver.com/v1/shoppers/me/carts/active?promoCode=wb32xjtam
--header 'authorization: Basic ***\ 
...
```
{% endcode %}
{% endtab %}

{% tab title="200 OK response" %}
{% code overflow="wrap" %}
```json
{
   "cart": {
      "id": "1234567890",
      "lineitems": {
         "lineitem": {
            "id": "12765711619",
            "quantity": "1",
            "product": {
               "displayname": "Displayable Product Name",
               "thumbnailimage": "http://drh1.img.digitalriver.com/DRHM/Storefront/images\n/product/thumbnail/small-product-image.jpg",
               "_uri": "https://api.digitalriver.com/v1/shoppers/me/products/232054400"
            },
            "pricing": {
               "listprice": {
                  "_currency": "USD",
                  "__text": "24.95"
               },
               "listpricewithquantity": {
                  "_currency": "USD",
                  "__text": "24.95"
               },
               "salepricewithquantity": {
                  "_currency": "USD",
                  "__text": "14.95"
               },
               "formattedlistprice": "$24.95",
               "formattedlistpricewithquantity": "$24.95",
               "formattedsalepricewithquantity": "$14.95"
            },
            "_uri": "https://api.digitalriver.com/v1/shoppers/me/carts/active /line-items/12765711619"
         },
         "_uri": "https://api.digitalriver.com/v1/shoppers/me/carts/active /line-items"
      },
      "billingaddress": {
         "shippingaddress": {
            "payment": {
               "name": "Visa",
               "displayablenumber": "************1111",
               "expirationyear": "2017"
            },
            "shippingmethod": {
               "code": "142400",
               "description": "USPS - Priority Mail"
            },
            "shippingoptions": {
               "pricing": {
                  "subtotal": {
                     "_currency": "USD",
                     "__text": "24.95"
                  },
                  "discount": {
                     "_currency": "USD",
                     "__text": "10.00"
                  },
                  "shippingandhandling": {
                     "_currency": "USD",
                     "__text": "0.00"
                  },
                  "tax": {
                     "_currency": "USD",
                     "__text": "0.00"
                  },
                  "ordertotal": {
                     "_currency": "USD",
                     "__text": "14.95"
                  },
                  "formattedsubtotal": "$24.95",
                  "formatteddiscount": "$10.00",
                  "formattedshippingandhandling": "$0.00",
                  "formattedtax": "$0.00",
                  "formattedordertotal": "$14.95"
               },
               "_uri": "https://api.digitalriver.com/v1/shoppers/me/shipping-options"
            },
            "_uri": "https://api.digitalriver.com/v1/shoppers/me/carts/active/shipping-address"
         },
         "_uri": "https://api.digitalriver.com/v1/shoppers/me/carts/active/billing-address"
      },
      "_uri": "https://api.digitalriver.com/v1/shoppers/me/carts/active"
   }
}
{
   "cart": {
      "id": "1234567890",
      "lineitems": {
         "lineitem": {
            "id": "12765711619",
            "quantity": "1",
            "product": {
               "displayname": "Displayable Product Name",
               "thumbnailimage": "http://drh1.img.digitalriver.com/DRHM/Storefront/images\n/product/thumbnail/small-product-image.jpg",
               "_uri": "https://api.digitalriver.com/v1/shoppers/me/products/232054400"
            },
            "pricing": {
               "listprice": {
                  "_currency": "USD",
                  "__text": "24.95"
               },
               "listpricewithquantity": {
                  "_currency": "USD",
                  "__text": "24.95"
               },
               "salepricewithquantity": {
                  "_currency": "USD",
                  "__text": "14.95"
               },
               "formattedlistprice": "$24.95",
               "formattedlistpricewithquantity": "$24.95",
               "formattedsalepricewithquantity": "$14.95"
            },
            "_uri": "https://api.digitalriver.com/v1/shoppers/me/carts/active /line-items/12765711619"
         },
         "_uri": "https://api.digitalriver.com/v1/shoppers/me/carts/active /line-items"
      },
      "billingaddress": {
         "shippingaddress": {
            "payment": {
               "name": "Visa",
               "displayablenumber": "************1111",
               "expirationyear": "2017"
            },
            "shippingmethod": {
               "code": "142400",
               "description": "USPS - Priority Mail"
            },
            "shippingoptions": {
               "pricing": {
                  "subtotal": {
                     "_currency": "USD",
                     "__text": "24.95"
                  },
                  "discount": {
                     "_currency": "USD",
                     "__text": "10.00"
                  },
                  "shippingandhandling": {
                     "_currency": "USD",
                     "__text": "0.00"
                  },
                  "tax": {
                     "_currency": "USD",
                     "__text": "0.00"
                  },
                  "ordertotal": {
                     "_currency": "USD",
                     "__text": "14.95"
                  },
                  "formattedsubtotal": "$24.95",
                  "formatteddiscount": "$10.00",
                  "formattedshippingandhandling": "$0.00",
                  "formattedtax": "$0.00",
                  "formattedordertotal": "$14.95"
               },
               "_uri": "https://api.digitalriver.com/v1/shoppers/me/shipping-options"
            },
            "_uri": "https://api.digitalriver.com/v1/shoppers/me/carts/active/shipping-address"
         },
         "_uri": "https://api.digitalriver.com/v1/shoppers/me/carts/active/billing-address"
      },
      "_uri": "https://api.digitalriver.com/v1/shoppers/me/carts/active"
   }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

Typically, the next steps after applying a coupon or promo code are either [redirecting the customer to the Digital River-hosted checkout](../redirecting-to-a-digital-river-hosted-cart.md) to complete the purchase process or [submitting the cart](../submitting-a-cart/) and creating an order to complete the checkout process.

## Primary versus secondary offers

When using a coupon, it's important to note that it's linked to a primary offer which may also have a secondary offer, typically tied to shipping discounts. Each offer has its specific criteria, which can be evaluated separately. A [`warnings object`](../../../common-shopper-and-admin-apis/warnings-object/) appears in the response only when neither set of criteria is met. For example, you create a discount offer with a second shipping discount as follows:

* The primary offer is a $5 discount for Product A.
* The secondary offer is a 50% shipping discount on orders over $200.

The following table shows when the A [`warnings object`](../../../common-shopper-and-admin-apis/warnings-object/) appears.

| Discount scenarios                                                                                             | Does the primary offer criteria match? | Does the secondary offer criteria match | Warning displayed when applying coupon in the cart |
| -------------------------------------------------------------------------------------------------------------- | -------------------------------------- | --------------------------------------- | -------------------------------------------------- |
| <p></p><ol><li>Empty cart</li><li>The cart amount is less than $200 and Product A is not in the cart</li></ol> | No                                     | No                                      | Yes                                                |
| <p></p><ol><li>Product A is in the cart</li></ol>                                                              | Yes                                    | No                                      | No                                                 |
| <p></p><ol><li>The cart amount has reached $200</li></ol>                                                      | Yes                                    | Yes                                     | No                                                 |
| <p></p><ol><li>The cart amount has reached $200 and the Product A is in the cart</li></ol>                     | No                                     | Yes                                     | No                                                 |

xx
