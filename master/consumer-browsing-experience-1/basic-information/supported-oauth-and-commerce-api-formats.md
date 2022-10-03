---
description: Learn about supported OAuth and Commerce API formats
---

# Supported OAuth and Commerce API formats

The Commerce API and OAuth support requests and responses in XML and JSON formats. XML is the default for the Commerce API; JSON is the default for the OAuth API. You can override the default in the Accept header for both the OAuth and Commerce API. In the Commerce API, you can also override the default format using the format query parameter.

### Accept header format for OAuth

The following list shows the supported accept header formats for the [OAuth ](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Token)resource.

{% tabs %}
{% tab title="Request Header" %}
{% code overflow="wrap" %}
```http
Accept: application/json (default)
Accept: application/xml
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Accept header format for Commerce API

The following list shows the supported accept header formats for [Shopper ](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Shoppers)resource.

{% tabs %}
{% tab title="Request Header" %}
{% code overflow="wrap" %}
```http
Accept: application/xml (default)
Accept: application/json
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Query parameter format

The following GET request sets the format parameter format to json:

{% tabs %}
{% tab title="Request Header" %}
{% code overflow="wrap" %}
```http
GET /shoppers/me/categories?format=json
Accept: */*
Authorization: bearer your_access_token
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Supported webhook formats

Digital River supports the XML format for webhooks.
