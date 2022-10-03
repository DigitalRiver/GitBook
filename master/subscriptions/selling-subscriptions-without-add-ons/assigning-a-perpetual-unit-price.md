---
description: Learn how to assign a perpetual unit price to a subscription.
---

# Assigning a perpetual unit price

## Assigning a perpetual unit price to a subscription

In this scenario, you assign a perpetual unit price to the customer's subscription.

Use the `POST /v1/subscriptions/{subscriptionId}/perpetual-price` resource to assign a perpetual unit price. You need to provide the subscription identifier (`subscriptionId`) and the perpetual unit price (`perpetUnitPrice`). In the following example, the value for the product's `perpetualUnitPrice` is `50`.&#x20;

{% tabs %}
{% tab title="cURL" %}
```javascript
curl --location --request POST 'https://{host}/v1/subscriptions/{subscriptionId}/perpetual-price' \
--header 'Content-Type:  application/json' \
--header 'authorization: bearer ***\
--data-raw '{
    "perpetualUnitPrice": 120,
}'
```
{% endtab %}
{% endtabs %}

You will receive a `202 Accepted` response.

## Creating a cart with a perpetual unit price

In this scenario, you create a cart and assign a perpetual unit price to the customer's subscription.

Use the `POST /v1/shoppers/me/carts/active` or the `POST /v1/shoppers/me/carts/active/line-items` resource to create a cart request with a perpetual unit price. You need to include the perpetual unit price (`perpetualUnitPrice`) in the subscription override info (`subscriptionOverrideInfo`). The response to this request creates a shopping cart and returns an access token to be included in all other cart interactions.

{% tabs %}
{% tab title="/active cURL" %}
```javascript
curl --location --request POST 'https://{host}/v1/shoppers/me/carts/active' \
--header 'Content-Type:  application/json' \
--header 'authorization: bearer ***\
--data-raw '{
   "cart":{
      "customAttributes":{
         
      },
      "lineItems":{
         "lineItem":[
            {
               "quantity":"1",
               "product":{
                  "id":"5367865200"
               },
  "subscriptionOverrideInfo" : {
                    "perpetualUnitPrice": {
                        "currencyCode" : "USD",
                        "amount" : 56.87
                    }
               
                },
               "customAttributes":{
                  "attribute":[
                     
                  ]
               }
            }
         ]
      },
      "billingAddress":{
         "firstName":"First",
         "lastName":"Last",
         "companyName":null,
         "line1":"10380 Bren Rd",
         "line2":null,
         "line3":null,
         "city":"Eden Prairie",
         "countrySubdivision":"MN",
         "postalCode":"55344",
         "emailAddress":"email@dr.com",
         "country":"US",
         "phoneNumber":"+1234567896"
      },
      "shippingAddress":{
         "firstName":"First",
         "lastName":"Last",
         "companyName":null,
         "line1":"10380 Bren Rd",
         "line2":null,
         "line3":null,
         "city":"Eden Prairie",
         "countrySubdivision":"MN",
         "postalCode":"55344",
         "emailAddress":"email@dr.com",
         "country":"US",
         "phoneNumber":"+1234567896"
      }
}'
```
{% endtab %}

{% tab title="/line-items cURL" %}
```javascript
curl --location --request POST 'https://<<host>>/v1/shoppers/me/carts/line-items' \
--header 'Content-Type:  application/json' \
--header 'authorization: bearer ***\
--data-raw '{
{
  "lineItem": [{
    "quantity": 6,
    "product": {
      "id": "{{productID}}"
    },
    "subscriptionOverrideInfo": {
      "perpetualUnitPrice": {
      "currencyCode": "USD",
      "amount": 175.00
      }
    }
  }]
}'
```
{% endtab %}
{% endtabs %}

Apply the shopper and submit the cart using the  [Shoppers ](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Shoppers/paths/\~1v1\~1shoppers/post)resource.

## Creating or changing a perpetual price

In this scenario, you create a cart or change the perpetual unit price for the customer's subscription.

Use the `POST /v1/subscriptions/{subscriptionId}/perpetual-price` resource to apply a forever price for the remaining subscription cycle. You can use it to change a non-perpetual subscription to a perpetual subscription if the supplied subscription is not a perpetual subscription. You need to provide the `subscriptionId` and the `perpetualUnitPrice`. Note that the `perpetualUnitPrice` cannot be higher than the existing price.

{% tabs %}
{% tab title="cURL" %}
```javascript
curl -X POST \
  https://{host}/v1/subscriptions/{ubscriptionId}/perpetual-price \
  -H 'authorization: Basic ****' \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/json' \
  -H 'postman-token: 5cb141b9-8077-8b12-3eff-ebb45db3ffa6' \
  -d '{
        "perpetualUnitPrice" : 59.99
      }'
```
{% endtab %}
{% endtabs %}

You will receive a `202 Accepted` response.
