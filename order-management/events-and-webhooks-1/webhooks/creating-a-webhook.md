---
description: Learn how to create a webhook.
---

# Creating a webhook

You create a webhook to receive notifications using the following steps:

1. [Open your firewall to trusted Digital River IP addresses](creating-a-webhook.md#step-1-open-your-firewall-to-trusted-digital-river-ip-addresses).
2. [Create a webhook endpoint](creating-a-webhook.md#step-2-create-a-webhook-endpoint).
3. [Create webhooks](creating-a-webhook.md#step-3-create-webhooks).
4. [Respond to webhook events](creating-a-webhook.md#step-4-respond-to-webhook-events).
5. [Check signatures](creating-a-webhook.md#step-5-check-signatures).

## Step 1. Open your firewall to trusted Digital River IP addresses

To receive webhook notifications from Digital River, you'll need to open your firewall to all the IP addresses listed in the [Digital River safelist](digital-river-safelist.md).

## Step 2. Create a webhook endpoint

You can send webhook data as JSON in the POST request body. The POST request body contains the complete event details, and you can use it after parsing the JSON into an [Event ](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events)object.

## Step 3. Create webhooks

You can either create a webhook [programmatically](creating-a-webhook.md#create-a-webhook-programmatically) or from the [Digital River Dashboard](creating-a-webhook.md#create-a-webhook-from-the-dashboard).

### Create a webhook programmatically

The following table describes the required and optional parameters that can be sent in a create webhook request:

| Parameter       | Required/Optional | Description                                                                                                                                                                                                                                                                                                                                |
| --------------- | ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `types`         | Required          | Each element of the array represents [a type of event](../events-1/event-types.md).                                                                                                                                                                                                                                                        |
| `apiVersion`    | Optional          | <p>Indicates whether to use the current default version of the API or the latest version of the API. The enumerators are <code>latest</code> and <code>default</code>.<br><br>The default setting is <code>default</code>.</p>                                                                                                             |
| `enabled`       | Optional          | <p>Indicates whether the webhook is enabled and receives notifications.</p><p>The default is <code>true</code>.</p>                                                                                                                                                                                                                        |
| `address`       | Required          | URL of the webhook endpoint on your server that you set up to receive webhook notifications. We send webhook data as JSON in a `POST` request body. The full event details are included and can be used directly after parsing the JSON into an [Event](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events) object. |
| `transportType` | Optional          | <p>Indicates whether the transport type is <code>HTTP</code> or <code>OAUTH</code>.<br><br>The default is <code>HTTP</code>.<br><br>Refer to <a href="creating-a-webhook.md#transport-type-and-attributes">transport type and attributes</a> for more information.</p>                                                                     |

#### **Example create request and response**

The following `POST/webhooks` request creates a Webhook for three different event types:

{% tabs %}
{% tab title="POST/webhooks" %}
```javascript
curl --location --request POST 'https://api.digitalriver.com/webhooks' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer <API_key>' \
--data-raw '{
  "types": ["order.accepted", "order.charge.pending", "order.charge.cancel.failed"],
  "apiVersion": "default",
  "enabled": true,
  "authentication":{
      "userName": "some username",
      "password": "some password"
  },
  "address": "https://company.com"
}'
```
{% endtab %}
{% endtabs %}

A Webhook with a unique identifier and the default `transportType` of `HTTP` is returned in the response.

{% hint style="warning" %}
Even though `HTTP` was not explicitly passed as the `transportType` in the above request, the `userName` and `password` parameters within the `authentication` hash table were still accepted and returned in the response. This is because `HTTP` is the default setting.
{% endhint %}

{% tabs %}
{% tab title="201 Created response" %}
```java
{
    "id": "177ef997-db7f-42f5-a28d-b0a1ee1267e9",
    "types": [
        "order.charge.cancel.failed",
        "order.charge.pending",
        "order.accepted"
    ],
    "address": "https://company.com",
    "apiVersion": "default",
    "enabled": true,
    "liveMode": false,
    "transportType": "HTTP",
    "authentication": {
        "userName": "some username",
        "password": "some password"
    },
    "createdTime": "2020-11-19T15:44:34.622Z",
    "updatedTime": "2020-11-19T15:44:34.622Z"
}
```
{% endtab %}
{% endtabs %}

### Create a webhook from the Digital River Dashboard

Instructions for creating a webhook from the Dashboard are [here](../../../administration/dashboard/developers/webhooks/creating-a-webhook.md#step-3-create-webhooks).

{% hint style="info" %}
**Note:** An event triggers a webhook to send a notification to you. The [Create webhook page](../../../administration/dashboard/developers/webhooks/creating-a-webhook.md) lists and describes the available events.&#x20;
{% endhint %}

## Step 4. Respond to webhook events

Your endpoint must return a 2xx HTTP status code to acknowledge the receipt of an event. If the endpoint fails to acknowledge events over several days, your endpoint will be disabled.

If Digital River receives **any** [response codes](https://www.digitalriver.com/docs/digital-river-api-reference/#section/Response-status-codes) outside this range, it indicates that you did not receive the event. For example, Digital River treats a URL redirection as a failure.

Once you have verified your endpoint can receive, acknowledge, and handle events correctly:

1. Click **Test** and select **Production** from the dropdown list in the Dashboard.\
   ![](<../../../.gitbook/assets/testproductiondropdown (2) (1) (1).png>)
2. Go through the same configuration steps again to configure an endpoint for your live integration.

If you're using the same endpoint for both test and production environments, the signing token is unique to each data mode.

## Step 5. Check signatures

To verify signatures, you need to retrieve your endpoint's token from the [Dashboard](https://dashboard.digitalriver.com)'s Webhooks settings. To see an endpoint's token:

1. From the Webhooks page on the Dashboard, click the **Reveal token** or **Reveal test** token associated with the endpoint you want to verify.
2. Provide your credentials and click **Authenticate**. The **Token** field under **Signing secret** will display the token.

See [Digital River signature](digital-river-signature.md) for more information.

## Transport type and attributes

The Webhoooks API supports [HTTP](creating-a-webhook.md#http-transport-type) and [OAUTH](creating-a-webhook.md#oauth-transport-type) transport types. The `transportType` you specify in a [create](creating-a-webhook.md#create-a-webhook-programmatically) or [update](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/updateWebhooks) Webhook request determines what additional transport attributes you may need to provide.

### HTTP transport type

In a Webhook, the `transportType` is `HTTP` by default, so it's not required to specify this parameter in the request. Whether you explicitly set the parameter to `HTTP` or whether you don't provide a value at all, you can still use the `authentication` hash table to provide a `username` and `password`. These values configure basic authentication for webhook callback endpoints.

{% hint style="warning" %}
The `authentication` hash table is only accepted in the request and displayed in the response when `transportType` is `HTTP`.
{% endhint %}

### OAUTH transport type

You can create OAuth2 configured webhooks by setting the `transportType` parameter to `OAUTH`. Doing so means the callback is always accompanied by a valid bearer token.

If you set this parameter to `OAUTH`, then you must provide the `tokenEndPoint` , `clientID`, and `clientSecret` within the `oauth` hash table.

{% hint style="warning" %}
The `oauth` hash table is only accepted in the request and displayed in the response when `transportType` is `OAUTH`.
{% endhint %}

The `tokenEndPoint` is used to exchange an authorization grant for an access token. The `clientID` is issued to you during the [registration process](https://tools.ietf.org/html/rfc6749#section-2.3.1). The `clientSecret`is stored in encrypted format, but it is decrypted when exposed through the API. This is also true for the optional `password` parameter within `oauth`.
