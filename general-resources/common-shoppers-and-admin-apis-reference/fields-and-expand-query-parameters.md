---
description: Learn how to use field and expand query parameters.
---

# Fields and expand query parameters

Most of the [Shoppers ](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Shoppers)resources support query parameters. When you add parameters to a request, you modify the results in ways such as changing the resource representation, refining your query, and paginating the results. Some query parameters modify the resource by changing the locale or pricing information. The API returns a default set of fields for each resource you request. You can override the default fields returned by using the `fields` and `expand` query parameters when the default fields do not meet your specific needs.

## Fields query parameter

Use the `fields` query parameter to specify the fields that appear in the response. Filtering the fields returned in the response can conserve bandwidth and accelerate response time.

{% tabs %}
{% tab title="cURL" %}
This following example does not use the `fields` query parameter.

{% code overflow="wrap" %}
```
curl --location -g --request GET ' https://api.digitalriver.com/v1/shoppers/me' \
--header 'Authorization: bearer {{access_token}}' \
...
```
{% endcode %}
{% endtab %}

{% tab title="200 OK response" %}
The following response gets the fields that are available by default for an authenticated shopper. Line numbers `9` to `21` display links that are only available for an authenticated shopper.

{% code overflow="wrap" lineNumbers="true" %}
```json
{
  "shopper": {
    "uri": "https://api.digitalriver.com/v1/shoppers/me",
    "id": 1234567890,
    "username": "jdoe@digitalriver.com",
    "firstName": "Automation",
    "lastName": "Tester",
    "emailAddress": "jdoe@digitalriver.com",
    "paymentOptions": {
      "uri": "https://api.digitalriver.com/v1/shoppers/me/payment-options"
    },
    "addresses": {
      "uri": "https://api.digitalriver.com/v1/shoppers/me/addresses"
    },
    "orders": {
      "uri": "https://api.digitalriver.com/v1/shoppers/me/orders"
    },
    "subscriptions": {
      "uri": "https://api.digitalriver.com/v1/shoppers/me/subscriptions"
    }
  }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="cURL" %}
The following example uses the `fields` query parameter to filter the response by the shopper's first and last name only.&#x20;

{% code overflow="wrap" %}
```
curl --location -g --request GET ' https://api.digitalriver.com/v1/shoppers/me?fields=firstName,lastName' \
--header 'Authorization: bearer {{access_token}}' \
...
```
{% endcode %}
{% endtab %}

{% tab title="200 OK response" %}
The following response returns only the fields specified in your request.

{% code overflow="wrap" %}
```json
{
	"shopper": {
		"firstname": "John",
		"lastname": "Smith",
		"_uri": "https://api.digitalriver.com/v1/shoppers/me"
	}
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Expand query parameter

Use the `expand` query parameter when you want additional field to appear in the response. The `expand` query parameter provides additional fields in the response. Expanding resources reduces the number of API calls required to accomplish a task.

The following example gets the same customer and requests specific resource fields: `locale` and `currency`.&#x20;

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```
curl --location -g --request GET ' https://api.digitalriver.com/v1/shoppers/me?expand=locale,currency' \
--header 'Authorization: bearer {{access_token}}' \
...
```
{% endcode %}
{% endtab %}

{% tab title="200 OK response" %}
Line numbers `8` and `9` show the `locale` and `currency` for the customer in the response.

{% code overflow="wrap" lineNumbers="true" %}
```json
    {
    	"shopper": {
    		"id": "161784673509",
    		"username": "jsmith",
    		"firstname": "John",
    		"lastname": "Smith",
    		"emailaddress": "jsmith@email.com",
    		"locale": "en_US",
    		"currency": "USD",
   		"paymentoptions": {
    			"_uri": "https:// api.digitalriver.com v1/shoppers/me/payment-options"
    		},
    		"addresses": {
    			"_uri": "https://api.digitalriver.com/v1/shoppers/me/addresses"
    		},
  		"orders": {
  			"_uri": "https://api.digitalriver.com/v1/shoppers/me/orders"
  		},
  		"subscriptions": {
  			"_uri": "https://api.digitalriver.com/v1/shoppers/me/subscriptions"
  		},
  		"_uri": "https://api.digitalriver.com/v1/shoppers/me"
  	}
  }
```
{% endcode %}
{% endtab %}
{% endtabs %}

The next example gets the same customer and requests all the fields with `expand=all`.

{% hint style="success" %}
**Tip**: Avoid using the `expand=all` parameter if you want to reduce the information returned and ensure optimal performance.
{% endhint %}

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```
curl --location -g --request GET ' https://api.digitalriver.com/v1/shoppers/me?expand=all' \
--header 'Authorization: bearer {{access_token}}' \
...
```
{% endcode %}
{% endtab %}

{% tab title="200 OK response" %}
As you can see in this example, there are more fields available with full expansion of a resource. Notice that an authenticated customer session also provides links (non-expandable) to orders and subscriptions. You can expand addresses and payment options; however, for orders and subscriptions, you must make follow-up calls.

{% code overflow="wrap" lineNumbers="true" %}
```json
   {
  	"shopper": {
  		"id": "161784673509",
  		"username": "jsmith",
   		"externalreferenceid": "123456",
  		"firstname": "John",
  		"lastname": "Smith",
  		"emailaddress": "jsmith@email.com",
  		"locale": "en_US",
 		"currency": "USD",
 		"sendmail": "false",
 		"sendemail": "true",
 		"paymentoptions": {
 			"paymentoption": {
 				"id": "1695808409",
  				"nickname": "Default",
  				"isdefault": "true",
 				"creditcard": {
  					"expirationmonth": "5",
 					"expirationyear": "2017",
 					"issuecode": {
 						"startmonth": {
 							"startyear": {
 								"displayablenumber": "************1111",
 								"type": "Visa"
 							}
 						}
 					}
 				},
  				"_uri": "https://api.digitalriver.com/v1/shoppers/me/payment-option/1695808409"
 			},
 			"_uri": "https://api.digitalriver.com/v1/shoppers/me/payment-options"
 		},
 		"addresses": {
 			"address": {
 				"id": "2268768209",
 				"nickname": "Office address",
 				"isdefault": "true",
 				"firstname": "John",
 				"lastname": "Smith",
 				"companyname": "Acme Inc.",
 				"line1": "1234 Main Street",
 				"line2": "Suite 1",
 				"line3": "Building D",
 				"city": "Eden Prairie",
 				"countrysubdivision": "MN",
  				"postalcode": "55344-3765",
 				"country": "US",
 				"countryname": "United States",
 				"phonenumber": "952-123-1234",
 				"countyname": "",
 				"_uri": "https://api.digitalriver.com/v1/shoppers/me/address/2268768209"
 			},
 			"_uri": "https://api.digitalriver.com/v1/shoppers/me/addresses"
 		},
 		"orders": {
 			"_uri": "https://api.digitalriver.com/v1/shoppers/me/orders"
 		},
 		"subscriptions": {
 			"_uri": "https://api.digitalriver.com/v1/shoppers/me/subscriptions"
  		},
 		"_uri": "https://api.digitalriver.com/v1/shoppers/me"
 		}
  }
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Parameter precedence

The `expand` parameter with a value of `all` overrides the `fields` parameter when both are specified within a URL. For example, the results for `GET v1/shoppers/me?fields=firstName&expand=all` returns all fields for a customer.
