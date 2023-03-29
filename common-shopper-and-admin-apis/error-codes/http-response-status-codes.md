---
description: Understand HTTP response status codes.
---

# HTTP response status codes

The Commerce API uses HTTP response status codes. These codes indicate whether an API request succeeded or failed. HTTP status codes group responses into the following classes:

* The `2xx` range indicates success.
* The `4xx` range indicates an error that failed based on the provided information provided (for example, you omitted a parameter, or a charge failed).
* The `5xx` range indicates an error with Digital River's servers.

Some errors `4xx` errors include an [error code](./#error-codes). The error code is a short string with a brief explanation.
