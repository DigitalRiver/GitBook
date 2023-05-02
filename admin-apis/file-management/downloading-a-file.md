---
description: Learn how to download a file.
---

# Downloading a file

Use the [`GET /files/{fileId}/content`](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Retrieve-File/operation/downloadFiles) request for the specified file identifier (`fileId`) to fetch a file. For more information, see [Downloading the invoice](../order-management/downloading-the-invoice.md).

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```http
curl --location --request GET 'https://api.digitalriver.com/files/{fielId}/content' \
--header 'authorization: Basic ***\
--header 'x-siteid: acme' \
...
```
{% endcode %}
{% endtab %}

{% tab title="200 OK response" %}
{% code overflow="wrap" %}
```json
{
  "id": "9e00869b-e2f5-4663-aacb-e33687466020",
  "fileName": "File Name"
}
```
{% endcode %}
{% endtab %}
{% endtabs %}
