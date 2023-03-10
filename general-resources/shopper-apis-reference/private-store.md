# Private store

## Private store query parameters

You can specify one or more query parameters separated by an ampersand (&) to filter the private store response. The following topics describe the query parameters available for the private store ([purchase-plan](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Purchase-Plan/paths/\~1v1\~1shoppers\~1me\~1purchase-plan/get)). For more information on how to use query parameters, see [Fields and query parameters](../common-shoppers-and-admin-apis-reference/fields-and-expand-query-parameters.md).

### Expand

Use the `expand` query parameter when you want additional fields to appear in the response. The `expand` query parameter provides additional fields in the response. Expanding resources reduces the number of API calls required to accomplish a task. See [Expand query parameter](../common-shoppers-and-admin-apis-reference/fields-and-expand-query-parameters.md#expand-query-parameter) for more information.

### Fields

Use the `fields` query parameter to specify the fields that appear in the response. Filtering the fields returned in the response can conserve bandwidth and accelerate response time. See [Fields query parameter](../common-shoppers-and-admin-apis-reference/fields-and-expand-query-parameters.md#fields-query-parameter) for more information.

### Token

The `token` is the authorized or anonymous token for the shopper.

## Authorize private store query parameters

You can specify one or more query parameters separated by an ampersand (&) to filter the private store authorize response. The following topics describe the query parameters available for authenticating the shopper session for a private store ([purchase-plan/authorize](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Purchase-Plan-Authorize/paths/\~1v1\~1shoppers\~1me\~1purchase-plan\~1authorize/post)). For more information on how to use query parameters, see [Fields and query parameters](../common-shoppers-and-admin-apis-reference/fields-and-expand-query-parameters.md).

### Expand

Use the `expand` query parameter when you want additional fields to appear in the response. The `expand` query parameter provides additional fields in the response. Expanding resources reduces the number of API calls required to accomplish a task. See [Expand query parameter](../common-shoppers-and-admin-apis-reference/fields-and-expand-query-parameters.md#expand-query-parameter) for more information.

### Fields

Use the `fields` query parameter to specify the fields that appear in the response. Filtering the fields returned in the response can conserve bandwidth and accelerate response time. See [Fields query parameter](../common-shoppers-and-admin-apis-reference/fields-and-expand-query-parameters.md#fields-query-parameter) for more information.

### Token

The `token` is the authorized or anonymous token for the shopper.

## Search private store query parameters

You can specify one or more query parameters separated by an ampersand (&) to filter the private store search response. The following topics describe the query parameters available for private store search ([purchase-plan/search](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Purchase-Plan-Search)). For more information on how to use query parameters, see [Fields and query parameters](../common-shoppers-and-admin-apis-reference/fields-and-expand-query-parameters.md).

### Email address

Use the `emailAddress` to supply the shopper's email address you want to use for the search. This query parameter only applies to [Searching for a private store](private-store.md#searching-for-a-private-store).

### Email domain

Use the `emailDomain` to supply the domain name you want to use for the search. This query parameter only applies to [Searching for a private store](private-store.md#searching-for-a-private-store).

#### `emailInvitationAddress`

An email address associated with an invitation to a private store. When a private store shopper invites a friend to view a private store, the invitation email address is that of the inviter. This query parameter only applies to [Searching for a private store](private-store.md#searching-for-a-private-store).

#### `emailInvitationPin`

The PIN that is associated with an email invitation. If a private store shopper invites a friend to view a private store, the PIN is provided with the invitation. Note, Required only if emailInvitationAddress was provided. This query parameter only applies to [Searching for a private store](private-store.md#searching-for-a-private-store).

### Expand

Use the `expand` query parameter when you want additional fields to appear in the response. The `expand` query parameter provides additional fields in the response. Expanding resources reduces the number of API calls required to accomplish a task. See [Expand query parameter](../common-shoppers-and-admin-apis-reference/fields-and-expand-query-parameters.md#expand-query-parameter) for more information.

#### `genericIdentifier`

The generic identifier to use for the search. This query parameter only applies to [Searching for a private store](private-store.md#searching-for-a-private-store).

#### `genericIdentifierPin`

The PIN that accompanies the generic identifier for the search. This query parameter is required if provide the [`genericIdentifier`](private-store.md#genericidentifier). This query parameter only applies to [Searching for a private store](private-store.md#searching-for-a-private-store).

#### `ipAddress`

The IP address to use for the search. This query parameter only applies to [Searching for a private store](private-store.md#searching-for-a-private-store).

#### `referralUrl`

The referral URL to use for the search. This query parameter only applies to [Searching for a private store](private-store.md#searching-for-a-private-store).

### Token

The `token` is the authorized or anonymous token for the shopper.
