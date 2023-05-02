---
description: Understand how JSONP works.
---

# JSONP support

You can use JSONP (JavaScript Object Notation with Padding) when sending a call from a server in a different domain.

Most browsers enforce a same-origin policy for asynchronous data requests, sometimes called AJAX. Under the same-origin policy, a browser serving a page from server.example.com could not normally request a document from api.digitalriver.com. Some exceptions are provided–most browsers make an exception for HTML.
