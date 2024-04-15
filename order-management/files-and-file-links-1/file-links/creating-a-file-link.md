---
description: Learn how to create a file link.
---

# Creating a file link

When you create a file link, we also update the file associated with the link to include the file link's identifier. The file can have an array of file links that shows the relationship between the file and file links, including the file link that you just created.

## Setting the file links parameter

When you create a File Link, you'll need to provide the required parameters listed in the following table. The remaining parameters are optional:

| Parameter     | Required/Optional | Description                                                        |
| ------------- | ----------------- | ------------------------------------------------------------------ |
| `fileId`      | Required          | The file identifier.                                               |
| `expiresTime` | Required          | A future timestamp, after which the link will no longer be usable. |
| `metadata`    | Optional          | Additional structured information for the object.                  |

## Example create request and response for Digital River API

Create a [File Link](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/FileLinks) object with a `POST` request:

{% tabs %}
{% tab title="cURL" %}
```
curl --location --request POST 'https://api.digitalriver.com/file-links' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer <API_key>' \
  "fileId": "49ca4603-a718-424b-8a5e-0bfa95f98ae8",
  "expiresTime": "2020-10-25T20:36:00Z"
}'
```
{% endtab %}
{% endtabs %}

A `201 Created` response returns a File Link object:

{% tabs %}
{% tab title="JSON" %}
```javascript
{
    "id": "e8a63964-9a92-4c71-bc28-332681d8c815",
    "createdTime": "2020-08-10T13:08:33.389Z",
    "expired": false,
    "expiresTime": "2020-10-25T20:36:00Z",
    "fileId": "49ca4603-a718-424b-8a5e-0bfa95f98ae8",
    "url": "https://files-test.digitalriver.com/links/e8a63964-9a92-4c71-bc28-332681d8c815",
    "liveMode": false
}
```
{% endtab %}
{% endtabs %}
