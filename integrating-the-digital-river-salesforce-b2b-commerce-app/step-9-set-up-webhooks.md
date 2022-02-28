---
description: Learn how to set up webhooks for fulfillment and for VAT invoicing.
---

# Step 9: Set up webhooks

## Set up webhooks for fulfillment using Postman <a href="#step-7e-set-up-webhooks-for-fulfillment-using-postman" id="step-7e-set-up-webhooks-for-fulfillment-using-postman"></a>

Digital River uses webhooks to notify the app when events occur. As part of the fulfillment process, the app looks for two events: `order.accepted` and `order.complete`.

The `order.accepted` event occurs whenever a Digital River order is submitted, and the payment is **Authorized** (funds are not captured yet).

The `order.complete` event occurs whenever an order is both fulfilled and captured (funds are captured).

Follow the steps below to register webhook URLs for your Digital River site so that Digital River can notify the app when the `order.accepted` and `order.complete` events occur.

### Prerequisites <a href="#prerequisites" id="prerequisites"></a>

You will need the following information before you set up the webhook URLs.

* **Username** of Fulfillment Integration User.
* **Password** of Fulfillment Integration User.
* **Client Id** of Connected App **DigitalRiver B2B Fulfillment** created in [step 8a](step-8-set-up-digital-river-fulfillments.md#step-7a-create-a-connected-app).
* **Client Secret** of Connected App **DigitalRiver B2B Fulfillment** created in [step 8a](step-8-set-up-digital-river-fulfillments.md#step-7a-create-a-connected-app).
* **Security Token** of Fulfillment Integration User.

### Register the Webhook URL for the `order.accepted` event <a href="#register-the-webhook-url-for-the-order-accepted-event" id="register-the-webhook-url-for-the-order-accepted-event"></a>

1. Open a REST client such as Postman.
2. Set the HTTP method to **POST**.
3. Set the URL as `https://api.digitalriver.com/webhooks`.
4. Set the HTTP body as shown in the following example:&#x20;

```
{
    "types": [
        "order.accepted"
    ],
    "address": "<<SF_My_Domain_Name>>/services/apexrest/digitalriverv2/DROFIOrderMgmNotification/",
    "apiVersion": "default",
    "enabled": true,
    "transportType": "OAUTH",
    "oauth": {
        "tokenEndPoint": "<<SF_OAuth_Access_Token_Endpoint>",
        "userName": "<<Fulfillment_User_SF_Username>>",
        "password": "<<Fulfillment_User_SF_Password+SecurityToken>>",
        "clientID": "<<Fulfillment_ConnectedApp_Client_Id>>",
        "clientSecret": "<<Fulfillment_ConnectedApp_Client_Secret>>",
        "grantType": "password"
    }
}  
```

{% hint style="info" %}
**Note:** The URL for the `tokenEndpoint`is “https://test.salesforce.com/services/oauth2/token” for the sandbox and “https://login.salesforce.com/services/oauth2/token” for production.
{% endhint %}

### Register the webhook URL for the `order.complete` event <a href="#register-the-webhook-url-for-the-order-complete-event" id="register-the-webhook-url-for-the-order-complete-event"></a>

1. Open Postman.
2. Set the HTTP method to **POST**.
3. Set the URL as https://api.digitalriver.com/webhooks.
4. Set the HTTP body as shown in the following example:

```

    "types": [
        "order.complete"
    ],
    "address": "<<SF_My_Domain_Name>>/services/apexrest/digitalriverv2/DROrderCompleteNotification/",
    "apiVersion": "default",
    "enabled": true,
    "transportType": "OAUTH",
    "oauth": {
        "tokenEndPoint": "<<SF_OAuth_Access_Token_Endpoint>",
        "userName": "<<Fulfillment_User_SF_Username>>",
        "password": "<<Fulfillment_User_SF_Password+SecurityToken>>",
        "clientID": "<<Fulfillment_ConnectedApp_Client_Id>>",
        "clientSecret": "<<Fulfillment_ConnectedApp_Client_Secret>>",
        "grantType": "password"
    }
} 
```

A successful request returns a 200 OK response. Once configured, you can see these [webhooks](https://docs.digitalriver.com/digital-river-api/administration/dashboard/developers/webhooks) in the [Digital River Dashboard](https://dashboard.digitalriver.com).

![](<../.gitbook/assets/Install DR B2B API Connector53 (1).jpg>)

## Set up webhooks for VAT invoicing​

Support for retrieving VAT Invoices is now available within this app.

Sample Webhook registration for the event `order.invoice.created`.

```
{  
  "types": [  
    "order.invoice.created"  
  ],  
  "address": "<<SF_My_Domain_Name>>/services/apexrest/digitalriverv2/webhooks/",  
  "apiVersion": "default",  
  "enabled": true,  
  "transportType": "OAUTH",  
  "oauth": {  
    "tokenEndPoint": "<<SF_OAuth_Access_Token_Endpoint>",  
    "userName": "<<Fulfillment_User_SF_Username>>",  
    "password": "<<Fulfillment_User_SF_Password+SecurityToken>>",  
    "clientID": "<<Fulfillment_ConnectedApp_Client_Id>>",  
    "clientSecret": "<<Fulfillment_ConnectedApp_Client_Secret>>",  
    "grantType": "password"  
  }  
}  
```

{% hint style="info" %}
**Note:** The URL for the `tokenEndpoint`is \
`https://test.salesforce.com/services/oauth2/token` for the sandbox and \
`https://login.salesforce.com/services/oauth2/token` for production.

For the `address`, the MyDomain URL should be\
(`https://example-domain.my.salesforce.com`), not the Lightning Force URL (`https://example-domain.lightning.force.com`).
{% endhint %}
