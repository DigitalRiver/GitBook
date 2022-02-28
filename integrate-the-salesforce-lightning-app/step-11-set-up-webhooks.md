---
description: Learn how to set up webhooks.
---

# Step 11: Set up webhooks

Digital River uses [webhooks](https://docs.digitalriver.com/digital-river-api/events-and-webhooks-1/webhooks) to notify the app when events occur.  The following instructions explain how to register a client webhook endpoint to set up webhook integration between Salesforce and Digital River

To register the Client Webhook Endpoint:

1. Log in to the [Digital River Dashboard](https://docs.digitalriver.com/digital-river-api/administration/dashboard).
2. Go to **Webhooks** and select **Create webhook**.\
   &#x20;![](<../.gitbook/assets/Create webhook.png>)&#x20;
3. Set up the **OAuth Integration** and select **OAuth** as the authentication method. \
   ![](<../.gitbook/assets/OAuth integration 2 (1).png>)&#x20;
4. Complete the following fields:

| Field name     | Description                                                                                                                                                                                                            |
| -------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Token Endpoint | https://<\<SF\_OAuth\_Access\_Token\_Endpoint>                                                                                                                                                                         |
| Endpoint URL   | https://<\<SF\_My\_Domain\_Name>>/services/apexrest/digitalriverv3/webhooks/                                                                                                                                           |
| Client ID      | <p>Client Id (Consumer Key) of the Connected App "Salesforce DigitalRiver Integration" <br>which was created in the <a href="step-10-set-up-integration-between-salesforce-and-digital-river.md">previous step</a></p> |
| Client Secret  | Client Secret of the Connected App "Salesforce DigitalRiver Integration"                                                                                                                                               |
| Username       | Integration User's username                                                                                                                                                                                            |
| Password       | <\<IntegrationUserPassword>><\<IntegrationUserSecurityToken>>                                                                                                                                                          |

![](<../.gitbook/assets/OAuth integration 3.png>)

![](<../.gitbook/assets/OAuth integration 4.png>)

{% hint style="info" %}
The **Token Endpoint** for the **Sandbox** environment is`https://test.salesforce.com/services/oauth2/token and https://login.salesforce.com/services/oauth2/token` for the **Production** environment.&#x20;
{% endhint %}

{% hint style="info" %}
The **Endpoint URL** address named **MyDomain URL** should be `https://example-domain.my.salesforce.com` and not the Lightning Force URL `https://example-domain.lightning.force.com`
{% endhint %}

## Webhook event types

The Digital River Salesforce Lightning app supports the following out of the box (OOTB) webhook events:

* `order.accepted`
* `order.cancelled`
* `order.complete`
* `order.pending_payment`
* `order.review_opened`
* `order.blocked`
* `order.credit_memo.created`
* `order.invoice.created`

Ensure that all the supported Webhook events (Event types) that need to be sent to the configured Endpoint URL are selected (and saved) in the [Event types](https://docs.digitalriver.com/digital-river-api/events-and-webhooks-1/events-1/event-types) section located in the Digital River Dashboard's [webhook](https://docs.digitalriver.com/digital-river-api/events-and-webhooks-1/webhooks) section.

![](<../.gitbook/assets/Webhook 5.png>)

![](<../.gitbook/assets/Webhook 4.png>)

