---
description: Learn how to use field and expand query parameters.
---

# Fields and expand query parameters

Most of the [Shoppers ](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Shoppers)resources support query parameters. When you add parameters to a request, you modify the results in ways such as changing the resource representation, refining your query, and paginating the results. Some query parameters modify the resource by changing the locale or pricing information. The API returns a default set of fields for each resource you request. You can override the default fields returned by using the `fields` and `expand` query parameters when the default fields do not meet your specific needs.

### Fields query parameter

Use the `fields` query parameter to filter the fields that appear in a response to just the fields you specifically request. Filtering the fields returned in the response can conserve bandwidth and accelerate response time.

The following example gets the fields are available by default to an authenticated customer. Line numbers `8` to `21` display links that are only available for an authenticated customer.

{% tabs %}
{% tab title="URI" %}
{% code overflow="wrap" %}
```
GET /v1/shoppers/me
```
{% endcode %}
{% endtab %}

{% tab title="JSON" %}
```
{
 	"shopper": {
   	"id": "161784673509",
  		"username": "jsmith",
  		"firstname": "John",
  		"lastname": "Smith",
  		"emailaddress": "jsmith@email.com",
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
{% endtab %}
{% endtabs %}

The next example gets the same customer's first and last name only. Notice that the response only includes the fields you specified.

{% tabs %}
{% tab title="URI" %}
{% code overflow="wrap" %}
```
GET /v1/shoppers/me?fields=firstName,lastName
```
{% endcode %}
{% endtab %}

{% tab title="JSON" %}
```
{
	"shopper": {
		"firstname": "John",
		"lastname": "Smith",
		"_uri": "https://api.digitalriver.com/v1/shoppers/me"
	}
}
```
{% endtab %}
{% endtabs %}

### Expand query parameter

Use the `expand` query parameter when you need additional information. The `expand` query parameter increases the set of fields that appear in the response in addition to the default fields. Expanding resources reduces the number of API calls required to accomplish a task.

The following example gets the same customer and requests specific resource fields: locale and currency. Line numbers `8` and `9` show the `locale` and `currency` for the customer in the response.

{% tabs %}
{% tab title="URI" %}
{% code overflow="wrap" %}
```
GET /v1/shoppers/me?expand=locale,currency
```
{% endcode %}
{% endtab %}

{% tab title="" %}
{% code overflow="wrap" %}
```json
1.  {
2.  	"shopper": {
3.  		"id": "161784673509",
4.  		"username": "jsmith",
5.  		"firstname": "John",
6.  		"lastname": "Smith",
7.  		"emailaddress": "jsmith@email.com",
8.  		"locale": "en_US",
9.  		"currency": "USD",
10. 		"paymentoptions": {
11. 			"_uri": "https:// api.digitalriver.com v1/shoppers/me/payment-options"
12. 		},
13. 		"addresses": {
14. 			"_uri": "https://api.digitalriver.com/v1/shoppers/me/addresses"
15. 		},
16. 		"orders": {
17. 			"_uri": "https://api.digitalriver.com/v1/shoppers/me/orders"
18. 		},
19. 		"subscriptions": {
20. 			"_uri": "https://api.digitalriver.com/v1/shoppers/me/subscriptions"
21. 		},
22. 		"_uri": "https://api.digitalriver.com/v1/shoppers/me"
23. 	}
24. }
```
{% endcode %}
{% endtab %}
{% endtabs %}

The next example gets the same customer and requests all the fields with `expand=all`.

{% hint style="success" %}
**Tip**: Avoid using the `expand=all` parameter if you want to reduce the information returned and ensure optimal performance.
{% endhint %}

As you can see in this example, there are more fields available with full expansion of a resource. Notice that an authenticated customer session also provides links (non-expandable) to orders and subscriptions. You can expand addresses and payment options; however, for orders and subscriptions, you must make follow-up calls.

{% tabs %}
{% tab title="URI" %}
{% code overflow="wrap" %}
```
GET /v1/shoppers/me?expand=all
```
{% endcode %}
{% endtab %}

{% tab title="JSON" %}
{% code overflow="wrap" %}
```
1. {
2. 	"shopper": {
3. 		"id": "161784673509",
4. 		"username": "jsmith",
5. 		"externalreferenceid": "123456",
6. 		"firstname": "John",
7. 		"lastname": "Smith",
8. 		"emailaddress": "jsmith@email.com",
9. 		"locale": "en_US",
10.		"currency": "USD",
11.		"sendmail": "false",
12.		"sendemail": "true",
13.		"paymentoptions": {
14.			"paymentoption": {
15.				"id": "1695808409",
16.				"nickname": "Default",
17.				"isdefault": "true",
18.				"creditcard": {
19.					"expirationmonth": "5",
20.					"expirationyear": "2017",
21.					"issuecode": {
22.						"startmonth": {
23.							"startyear": {
24.								"displayablenumber": "************1111",
25.								"type": "Visa"
26.							}
27.						}
28.					}
29.				},
30.				"_uri": "https://api.digitalriver.com/v1/shoppers/me/payment-option/1695808409"
32.			},
32.			"_uri": "https://api.digitalriver.com/v1/shoppers/me/payment-options"
33.		},
34.		"addresses": {
35.			"address": {
36.				"id": "2268768209",
37.				"nickname": "Office address",
38.				"isdefault": "true",
39.				"firstname": "John",
40.				"lastname": "Smith",
41.				"companyname": "Acme Inc.",
42.				"line1": "1234 Main Street",
43.				"line2": "Suite 1",
44.				"line3": "Building D",
45.				"city": "Eden Prairie",
46.				"countrysubdivision": "MN",
47.				"postalcode": "55344-3765",
48.				"country": "US",
49.				"countryname": "United States",
50.				"phonenumber": "952-123-1234",
51.				"countyname": "",
52.				"_uri": "https://api.digitalriver.com/v1/shoppers/me/address/2268768209"
53.			},
54.			"_uri": "https://api.digitalriver.com/v1/shoppers/me/addresses"
55.		},
56.		"orders": {
57.			"_uri": "https://api.digitalriver.com/v1/shoppers/me/orders"
58.		},
59.		"subscriptions": {
60.			"_uri": "https://api.digitalriver.com/v1/shoppers/me/subscriptions"
61.		},
62.		"_uri": "https://api.digitalriver.com/v1/shoppers/me"
63.		}
64. }
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Parameter precedence

The `expand` parameter with a value of `all` overrides the `fields` parameter when both are specified within a URL. For example, the results for `GET v1/shoppers/me?fields=firstName&expand=all` returns all fields for a customer.
