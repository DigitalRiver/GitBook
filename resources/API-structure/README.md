---
description: Understand the Commerce API structure.
---

# API structure

The Commerce API is a [RESTful API](https://restfulapi.net/). That means we designed the API to allow you to create, read, update, and delete objects with the`POST`, `GET`, `PUT` and `DELETE` [HTTP methods](https://www.restapitutorial.com/lessons/httpmethods.html).

The Commerce API speaks exclusively in [JSON](https://www.json.org/json-en.html). So to ensure the API accepts and processes your requests, always set the `Content-Type` header to `application/json` .

All Commerce API requests are sent to `https://api.digitalriver.com`.

For more information on how Digital River ensures high availability and performance, see our [Service Level Agreement](https://www.digitalriver.com/legal-information/).
