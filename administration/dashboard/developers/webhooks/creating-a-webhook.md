---
description: Learn how to create webhooks from the Digital River Dashboard.
---

# Creating a webhook

You can create a webhook to send notifications in five easy steps.

1. [Open your firewall to trusted Digital River IP addresses](creating-a-webhook.md#step-1-open-your-firewall-to-trusted-digital-river-ip-addresses)
2. [Create a webhook endpoint](creating-a-webhook.md#step-2-create-a-webhook-endpoint)
3. [Create webhooks](creating-a-webhook.md#step-3-create-webhooks)
4. [Respond to webhook events](creating-a-webhook.md#step-4-respond-to-webhook-events)
5. [Check signatures](creating-a-webhook.md#step-5-check-signatures)

## Step 1: Open your firewall to trusted Digital River IP addresses

To receive webhook notifications from Digital River, you'll need to open your firewall to all the IP addresses listed in the [Digital River safelist](../../../../order-management/events-and-webhooks-1/webhooks/digital-river-safelist.md).

## Step 2: Create a webhook endpoint

You can send webhook data as JSON in the POST request body. The POST request body contains the complete event details, and you can use it after parsing the JSON into an [Event ](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events)object.

## Step 3: Create webhooks

When creating a webhook from the Digital River Dashboard, you need to determine the type of authentication you want to use (either, none, [basic](../../../../order-management/events-and-webhooks-1/webhooks/creating-a-webhook.md#http-transport-type), or [OAuth](../../../../order-management/events-and-webhooks-1/webhooks/creating-a-webhook.md#oauth-transport-type)) and add the endpoint.

### Create a webhook requiring basic authentication

1.  From the Webhooks page, click **Create Webhook**.\
    \
    **Note:** An event triggers a webhook to send a notification to you. The Create webhook page lists and describes the available events. \


    <div align="left">

    <figure><img src="../../../../.gitbook/assets/1 Creating webhooks.png" alt=""><figcaption></figcaption></figure>

    </div>
2. Toggle **Disabled** to **Enabled**.
3.  If required, select the API version you want to associate with events from the **API Version** dropdown list. By default, the confidential key version is selected.\


    <div align="left">

    <figure><img src="../../../../.gitbook/assets/2 Creating webhooks - api version.png" alt=""><figcaption></figcaption></figure>

    </div>
4.  Click **HTTP** for the **Authentication method** and complete the **Username** and **Password** fields. \


    <div align="left">

    <figure><img src="../../../../.gitbook/assets/3 Creating webhooks - transport type.png" alt=""><figcaption></figcaption></figure>

    </div>
5. Enter the URL for the endpoint in the **Endpoint URL** field.
6. Select the check box next to each event you want to associate with the endpoint or select the **Events Selected** check box to select all events. At least one event type must be selected.
7. Scroll down and click **Save**.

### Create a webhook requiring OAuth authentication

1.  From the Webhooks page, click **Create Webhook**.\


    <div align="left">

    <figure><img src="../../../../.gitbook/assets/1 Creating webhooks.png" alt=""><figcaption></figcaption></figure>

    </div>
2. Toggle **Disabled** to **Enabled**.
3.  If required, select the API version you want to associate with events from the **API Version** dropdown list. By default, the confidential key version is selected.\


    <div align="left">

    <figure><img src="../../../../.gitbook/assets/4 Creating webhooks - api version2.png" alt=""><figcaption></figcaption></figure>

    </div>
4.  Click **OAuth** for the **Authentication method**.\


    <div align="left">

    <figure><img src="../../../../.gitbook/assets/image (249).png" alt=""><figcaption></figcaption></figure>

    </div>
5.  Select one of the following options from the Grant type dropdown list and complete the \*\*\*\* fields.\


    <div align="left">

    <figure><img src="../../../../.gitbook/assets/6 Creating webhooks - grant type dropdown.png" alt=""><figcaption></figcaption></figure>

    </div>

    * **Password**\
      ![](<../../../../.gitbook/assets/7 Creating webhooks - grant type pw.png>)
    * **Client credentials**\
      \
      ![](<../../../../.gitbook/assets/8 Creating webhooks - grant type clientcreds.png>)
6. [Select the check box next to each event](../../../../order-management/events-and-webhooks-1/events-1/event-types.md) you want to associate with the endpoint or select the **Events Selected** check box to select [all events](../../../../order-management/events-and-webhooks-1/events-1/all-event-types.md). At least one event type must be selected.
7. Scroll down and click **Save**.

## Step 4: Respond to webhook events

Your endpoint must return a 2xx HTTP status code to acknowledge the receipt of an [event](../../../../order-management/events-and-webhooks-1/events-1/all-event-types.md). If the endpoint fails to acknowledge events over several days, your endpoint will be disabled.

If Digital River receives **any** [response codes](https://www.digitalriver.com/docs/digital-river-api-reference/#section/Errors) outside this range, it indicates that you did not receive the event. For example, Digital River treats a URL redirection as a failure.

Once you have verified your endpoint can receive, acknowledge, and handle events correctly:

1. Toggle from **Test** to **Production** in the Dashboard.
2. Go through the same configuration steps again to configure an endpoint for your production integration.

If you're using the same endpoint for both test and production modes, the signing token is unique to each data mode.

## Step 5: Check signatures

To verify signatures, you need to retrieve your endpoint's token from the [Dashboard](https://dashboard.digitalriver.com)'s Webhook settings. To see an endpoint's token:

1. From the Webhooks page on the Dashboard, click the **Reveal secret** token associated with the endpoint you want to verify.
2. Provide your credentials and click **Authenticate**. The **Token** field under **Signing secret** will display the token.

See [Digital River signature](broken-reference) for more information.
