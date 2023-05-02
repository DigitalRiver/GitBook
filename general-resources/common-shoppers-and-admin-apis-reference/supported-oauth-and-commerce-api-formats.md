---
description: Learn about supported OAuth and Commerce API formats
---

# Supported OAuth and Commerce API formats

The Commerce API and OAuth support requests and responses in XML and JSON formats. XML is the default for the Commerce API; JSON is the default for the OAuth API. You can override the default in the Accept header for both the OAuth and Commerce API. You can also override the default format using the format query parameter in the Commerce API.

## Accept header format for OAuth

The following example shows the supported accept header format for the [OAuth ](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Token)resource.

{% tabs %}
{% tab title="Request Header" %}
```http
Accept: application/json (default)
Accept: application/xml
```
{% endtab %}
{% endtabs %}

### Accept header format for Commerce API

The following example shows the supported accept header format for [Shopper ](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Shoppers)resource.

{% tabs %}
{% tab title="Request Header" %}
```http
Accept: application/xml (default)
Accept: application/json
```
{% endtab %}
{% endtabs %}

### Query parameter format

The following GET request sets the parameter format to JSON:

{% tabs %}
{% tab title="Request Header" %}
```http
GET /shoppers/me/categories?format=json
Accept: */*
Authorization: bearer your_access_token
```
{% endtab %}
{% endtabs %}

### Supported webhook formats

Digital River supports the XML format for webhooks.
