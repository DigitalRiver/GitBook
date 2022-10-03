---
description: Learn how to retrieve a site's authorized billing countries.
---

# Getting a site's authorized billing countries

You can use the `GET /sites/{siteId}/authorized-billing-countries` resource to retrieve a list of all countries that are authorized to purchase products from your site. The list of [authorized billing countries](configuring-authorized-shipping-and-billing-countries.md) is configured in [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do).

{% tabs %}
{% tab title="cURL" %}
```javascript
curl --location --request GET 'https://{host}/sites/{siteId}/authorized-billing-countries' \
--header 'Content-Type:  application/json' \
--header 'authorization: bearer ***\
```
{% endtab %}
{% endtabs %}

You will receive a `200 OK` response. The response returns data by locale and countries.

To get the list of authorized billing countries by locale, add `?locale` at the end of the request. For example:

`GET 'https://{host}/sites/{siteId}/authorized-billing-countries?locale=en_US'`

{% tabs %}
{% tab title="JSON" %}
```javascript
{  
   "authorizedBillingCountries": [        
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
   ]
}
```
{% endtab %}
{% endtabs %}
