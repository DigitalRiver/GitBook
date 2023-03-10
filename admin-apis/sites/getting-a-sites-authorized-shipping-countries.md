---
description: Learn how to retrieve a site's authorized shipping countries.
---

# Getting a site's authorized shipping countries

You can use the [`GET /v1/sites/{siteId}/authorized-shipping-countries`](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Authorized-Countries/paths/\~1v1\~1sites\~1%7BsiteId%7D\~1authorized-shipping-countries/get) resource to retrieve a list of all countries that are authorized to purchase products from your site. The list of [authorized shipping countries](configuring-authorized-shipping-and-billing-countries.md) is configured in [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do).&#x20;

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```javascript
curl --location --request GET 'https://api.digitalriver.com/v1/sites/{siteId}/authorized-shipping-countries' \
--header 'authorization: bearer ***\
...
```
{% endcode %}
{% endtab %}

{% tab title="200 OK response" %}
You will receive a `200 OK` response. The response returns data by locale and county.

{% code overflow="wrap" %}
```json
{  
   "authorizedShippingCountries": [        
      {          
         "locale": "en_US",          
         "countries": [            
            {              
               "displayName": "Taiwan",              
               "countryCode": "TW"            
            },            
            {              
               "displayName": "Japan",              
               "countryCode": "JP"            
            }          
         ]        
      },        
      {          
         "locale": "en_GB",          
         "countries": [            
            {              
               "displayName": "France",              
               "countryCode": "FR"            
            },            
            {              
               "displayName": "Germany",              
               "countryCode": "DE"            
            }          
         ]        
      }      
   ]
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

To get the list of authorized shipping countries by locale, add the `?locale` query parameter at the end of the request. For example:

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```http
curl --location --request GET 'https://api.digitalriver.com/v1/sites/{siteId}/authorized-shipping-countries?locale=en_US' \
--header 'authorization: bearer ***\
...
```
{% endcode %}
{% endtab %}
{% endtabs %}

See [Authorized shipping country query parameters](../../general-resources/admin-apis-reference/sites/authorized-shipping-and-billing-countries.md#authorized-shipping-countries-query-parameters) for more information.
