---
description: Understand the 401 Unauthorized error codes.
---

# 401 Unauthorized

## `invalid_client`

The provided client is invalid. Provide the correct client information and try again.

## `invalid_request`

The required parameter is missing or empty. Provide the missing parameter and try again.

## `invalid_token`

Invalid token for the Shopper Session. The token is no longer valid and must be refreshed to continue making API calls. This error occurs when there is a bad Dispatch token or Global Commerce User API token. To resolve this error, issue an API call to identify where the token originated and when it expired, for example:

`GET /oauth20/access-tokens?token=your_access_token HTTP/1.1 Host: api.digitalriver.com`

Where `your_access_token` is a placeholder for the actual token.

The response shows you where the token originated in the `domain` field and when it expired in the `expiresIn` field. The possible error descriptions are as follows:

*   `Invalid token for specified shopper`

    The provided token is invalid for the specified shopper.
* `Session expired`–The shopper session is expired. Try refreshing the token.
*   `Request Site ID does not match Token Site ID`

    The value of the Header `siteId` does not match the site ID in the token.
*   `Invalid Token for Shapper Session`

    The provided token is invalid.
