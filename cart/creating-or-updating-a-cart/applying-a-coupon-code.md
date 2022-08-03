---
description: Learn how to apply a coupon code.
---

# Applying a coupon code

You can apply a coupon code to an active shopping cart to encourage sales in your stores by providing discounts on products or shipping costs.

During the checkout process, a customer manually enters a coupon code in your storefront and clicks the Apply button. The API applies the discount associated with the POP (Point-of-Promotion) offer to the cart. The call returns the contents of the cart with the adjusted pricing information.

### How to apply a promo code

Send a `POST shoppers/me/carts/active` request to the [Carts ](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Carts)resource with the required `promoCode` query parameter. The request must include a valid anonymous or authenticated customer token. There is no payload associated with this request; the request body is empty.

The request in the following example applies a promotional code value of `wb32xjtam`. The ID of the cart is `1234567890`.

{% hint style="info" %}
**Note**: A successful request returns a status code of 200 in the response header. An unsuccessful request returns an error code in the response.
{% endhint %}

{% tabs %}
{% tab title="Request sample" %}
```json
curl --location --request POST https://api.digitalriver.com/v1/shoppers/me/carts/active?promoCode=wb32xjtam
--header 'Content-Type:  application/json' \
--header 'authorization: bearer ***\ 
```
{% endtab %}

{% tab title="Response sample" %}
```javascript
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
{% endtab %}
{% endtabs %}

Typically, the next steps after applying a coupon code are either re-directing the customer to the Digital River hosted checkout to complete the purchase process or submitting the cart and creating an order to complete the checkout process.
