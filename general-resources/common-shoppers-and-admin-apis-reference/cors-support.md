---
description: Understand how CORS defines how a browser and server communicate.
---

# CORS support

[CORS (Cross-Origin Resource Sharing)](https://www.w3.org/TR/cors/) is a W3C recommendation that defines how a browser and server communicate when requesting resources across domains. Browsers have an inherent security restriction known as the same-origin policy. CORS allows servers to relax the same-origin policy, thereby allowing HTTP requests for resources from a different domain. To learn more about CORS, review the HTML5 ROCKS [Using CORS](https://www.w3.org/TR/cors/) tutorial.

Both the Commerce API and OAuth API suites provide support for CORS.

## CORS request terms

### Preflight request

A request that determines if an actual request is safe to send. A preflight request sends the OPTIONS method to a resource on another domain, querying the server for supported headers and methods. As part of a preflight request, a resource indicates whether it supports credentials. The user agent can cache preflight requests for several seconds if the Access-Control-Max-Age response header is configured. The Commerce API does not configure a preflight result cache value.

### Simple request

A request that uses simple methods (GET, POST, HEAD_)_, text/plain content type for the request body, and does not use custom headers. A simple request is a singular request to a server. Commerce API does not currently support the HEAD method.

### Non-simple request

A request that uses non-simple methods (such as PUT or DELETE), custom headers, or request bodies other than text/plain. For requests other than simple requests, a browser makes two requests to the server: one for the preflight request, and another for the actual request after server approval of the preflight.

### OPTIONS command example

The following example sends the OPTIONS command to the token resource in the Digital River OAuth resource, reflecting the server-side CORS configuration:

{% tabs %}
{% tab title="HTTP" %}
{% code overflow="wrap" %}
```http
OPTIONS https://api-digitalriver.com/oauth20/token HTTP/1.1 
Accept-Encoding: gzip,deflate 
Accept: application/xml 
Host: api.digitalriver.com 
Connection: Keep-Alive 
User-Agent: Apache-HttpClient/4.1.1 (java 1.5)  
HTTP/1.1 200 OK 
Content-Length: 5 
Content-Type: text/plain; charset=UTF-8 
Access-Control-Allow-Headers: Authorization,Content-Type,Accept,Accept-Language 
Access-Control-Allow-Credentials: true 
Access-Control-Allow-Origin: * 
Access-Control-Allow-Methods: POST,OPTIONS
```
{% endcode %}
{% endtab %}
{% endtabs %}

### CORS server-side settings

CORS uses HTTP response headers to control access to a remote resource. For access control requests made by a user-agent (browser), the server returns HTTP response headers. If a browser supports CORS, it sets these response headers automatically for cross-origin requests. The response headers configured for Commerce APIs are as follows:

#### Access-Control-Allow-Origin

The Access-Control-Allow-Origin response header specifies whether you can share a resource. This is the only header required to enable CORS on a server. The public content accessed by the Commerce API allows receiving resource requests (without credentials) from any domain, as indicated by the asterisk wildcard:

`Access-Control-Allow-Origin:*`

#### Access-Control-Allow-Methods

The Access-Control-Allow-Methods response header indicates which methods you can use in a cross-origin request. The Commerce API allows GET, POST, PUT, DELETE request methods in cross-site requests. The comma-separated list of methods can provide flexibility when caching preflight requests. Commerce API does not cache preflight requests.

{% hint style="info" %}
You cannot use the wildcard \* for a request with credentials. When responding to a credentialed request, the server must specify (echo) a domain.
{% endhint %}

`Access-Control-Allow-Methods: GET, POST, PUT, DELETE`

#### Access-Control-Allow-Headers

The Allow Headers HTTP response header indicates which headers you use in an actual request as part of a preflight request. The Commerce API supports Authorization, Content-Type, and Accept headers.

`Access-Control-Allow-Headers: Authorization, Content-Type, Accept`

#### Access-Control-Allow-Credentials

Use the Allow Credentials HTTP response header to expose a response to a request when this flag is set to true. Credentials refer to cookies, HTTP authentication, and client-side SSL certificates. Sending cookies and authentication facilitates user-specific cross-origin APIs. When responding to a preflight request, this flag indicates whether the actual request can include user credentials. This header works in conjunction with the `withCredentials` property on the XHR object. For the CORS request to succeed, the value must be set to true in both. The Commerce APIs support credentialed requests.

`Access-Control-Allow-Credentials: true`
