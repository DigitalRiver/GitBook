---
description: Understand OAuth 2.0 APIs.
---

# OAuth 2.0 APIs

Digital River uses OAuth 2.0 to provide authentication and authorization for the Commerce APIs. The Digital River OAuth 2.0 API allows third-party applications to authenticate and perform actions on behalf of a shopper without acquiring the shopper's password. Public resources do not require an access token, but they do require an API key configured as a public key.

You can invoke various OAuth APIs and sequences of API calls to implement the OAuth workflows.

You can implement the OAuth 2.0 APIs workflows using the following resources:

* `/oauth20/token`
* `/oauth20/authorize`

Use the `/oauth20/token` API to establish an anonymous shopper (limited access) token. You can use the anonymous shopper token to access resources before shopper authentication. You must provide your API key as a query parameter when you request an access token from the `/oauth20/token` resource.

![Anonymous Shopper Token](https://files.readme.io/b77d813-Oauth\_2.0-01.png)

The **anonymous shopper token** is an authenticated token, but not an authorized token. You can use the `/oauth20/authorize` resource to authenticate a shopper and establish an authenticated shopper token. An authenticated shopper token allows an application to use all of the shoppers/me APIs. You must send a request to the `oauth20/authorize` resource that includes:

* Your API key or access token as a query parameter
* The redirect URI sends the shopper to the correct page after the shopper successfully signs in

This request redirects the shopper to the Global Commerce platform for authentication. After the shopper successfully signed in, the system redirects the shopper to the specified URI and adds the new authenticated token as a parameter.

![Authenticated Shopper Token](https://files.readme.io/437002b-Oauth\_2.0\_b-01-01.png)

In this instance, the full access token replaces the limited access token, and future requests will use the full access token.

The OAuth 2.0 API uses application/json format by default.

### About OAuth access tokens

OAuth is an open standard for authorization. OAuth allows users to share their confidential resources stored on one site with another site without submitting their user credentials. Each token grants access to a specific site for specific resources and a defined duration. This allows a user to grant third-party site access to the information they provided to another service provider without sharing their access permissions or the full extent of their data.

Digital River Connect APIs grant [anonymous ](oauth-2.0-apis.md#anonymous-shopper-token)and [authenticated shopper tokens](oauth-2.0-apis.md#authenticated-shopper-token).

### Valid token types

The [OAuth specification](https://tools.ietf.org/html/rfc6749) defines the available application type as follows:

* **Public applications**—Applications that are incapable of maintaining the confidentiality of their credentials or securely authenticating by any other means. All calls use an HTTP Basic Authentication header, with the client ID (API key) as the username, and never use the secret key.
* **Confidential applications**—Applications that are capable of maintaining the confidentiality of their credentials, or are otherwise capable of secure client authentication. All calls include an HTTP Basic Authentication header. The header contains the client ID (API key) as the username and the secret key as the password.

### Access Token TTL

The access token time-to-live (TTL) limits the lifespan of the access token in seconds. When using TTL, consider the following:

* The default value is 24 hours (86397 seconds)
* By default, tokens remain valid for the same duration as Digital River-hosted storefront pages

The `expires_in` property is the TTL value for the access token. An application can store a valid access token and reuse it until it expires.

### Public versus confidential authentication flows

**Public flow**

Your API key and OAuth tokens (both anonymous and authenticated) are obfuscated yet publicly available with the technical effort that likely takes some time. Use this flow only when replay attacks are unlikely within the span of the token lifetime and when the API key and tokens are obfuscated (such as behind a decompiler).

![Public Authentication Flow](https://files.readme.io/9a25c95-Oauth\_2.0\_cont.png)

**Confidential flow**

Your API key remains completely hidden from public view. You can obfuscate or hide OAuth anonymous tokens from public view. The OAuth authenticated token is fully hidden from the public and typically hidden via a server proxy between the application and Digital River servers.

![Confidential Authentication Flow](https://files.readme.io/14e138b-Oauth\_2.0\_cont\_b.png)

### OAuth flows allowed by grant and client types

The following table shows the OAuth flows allowed by grant type and client type (including the application type). The table also indicates support for refresh tokens.

| Grant Type         | Public Application | Confidential Application | Refresh Token Supported? |
| ------------------ | ------------------ | ------------------------ | ------------------------ |
| Implicit           | Yes                | No                       | No                       |
| Client Credentials | No                 | Yes                      | No                       |
| ROPC               | Yes                | Yes                      | Yes                      |

See [Public vs. confidential application flows](oauth-2.0-apis.md#public-versus-confidential-authentication-flows) for more information.
