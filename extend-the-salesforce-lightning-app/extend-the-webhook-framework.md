---
description: Learn how to extend the webhook framework.
---

# Extend the webhook framework



The Salesforce Lightning—Digital River Connector App comes with a webhook framework that is capable of accepting and consuming any webhook that can be configured in the Digital River [Dashboard](https://docs.digitalriver.com/digital-river-api/administration/dashboard). For OOTB (out-of-the-box) webhook events, see the [set up webhooks](broken-reference) section.

You can always extend this framework to implement custom code that will fire upon receipt of a [Webhook](https://docs.digitalriver.com/digital-river-api/events-and-webhooks-1/webhooks) from Digital River. The event needs to be added to the previously-created webhook in the Digital River [Dashboard](https://docs.digitalriver.com/digital-river-api/administration/dashboard).&#x20;

## Extending the webhook

To implement the custom business logic for your organization, write the subscriber code that extends the default Webhook Framework Extension point class **** `digitalriverv3.DRB2B_WebhookHandler`.

For example, suppose you want to implement custom business logic for the event `refund.pending`

* In your organization, create an Apex class that extends the extension point class `digitalriverv3.DRB2B_WebhookHandler global with sharing class DRB2B_RefundPendingWebhook extends the digitalriverv3.DRB2B_WebhookHandler { }`
* Inside the class definition, override the method `processWebhookEvent` of the extension point class `digitalriverv3.DRB2B_WebhookHandler`. This method will have the **Event Payload** as one of its Input parameters.

```
global class DRB2B_RefundPendingWebhook extends 
digitalriverv3.DRB2B_WebhookHandler {
    
    global override void processWebhookEvent(RestResponse response, 
    String webhookEventPayload) {
        // Custom Implementation
    }
 
}
```

* Inside your method override, add your custom business logic. Ensure the `RestResponse` status code is set to 200 as shown in the sample implementation for the `refund.pending` webhook event below.

#### DRB2B\_RefundPendingWebhook

```
global class DRB2B_RefundPendingWebhook extends 
digitalriverv3.DRB2B_WebhookHandler {
 
private static final digitalriverv3.DCM_Logger 
logger = digitalriverv3.DCM_Logger.getInstance('Webhook Event');
        
    global override void processWebhookEvent(RestResponse response, 
    String 
    webhookEventPayload) {
       // Log the event to DCM Application log object
       logger.debug('Event: refund.pending; Refund Pending Webhook 
Event Payload: ' + webhookEventPayload);
       
        Messaging.SingleEmailMessage email = new 
        Messaging.SingleEmailMessage();
        email.setSubject('Process Webhook for event: refund.pending');
        email.setToAddresses(new List<String> 
        { 'example@digitalriver.com'});
        email.setHtmlBody(webhookEventPayload + '<br/> <br/>');
        Messaging.sendEmail(new Messaging.SingleEmailMessage[] 
        { email });
        
        response.statusCode = 200;
    }
 
}
```

Save your class and resolve any compilation errors.&#x20;

## Configuring the Apex class

Your Apex class must be configured so that the Connector is aware and executes this Custom Webhook handler implementation whenever it receives the event `refund.pending` from Digital River.

1.  Go to the Custom Metadata Type `digitalriverv3_DR_Webhook_Configuration_`

    `mdt` and click **Manage Records**. \
    ![](<../.gitbook/assets/Custom metadata type.png>)&#x20;
2. Create a new **Metadata Type Record** for the **DR Webhook Configuration**. \
   ![](<../.gitbook/assets/Refund pending webhook handler.png>)&#x20;
   * **Label**: Refund Pending Webhook Handler &#x20;
   * **DR Webhook Configuration Name**: Refund\_Pending\_Webhook\_Handler
   * **Webhook Event Name**: refund.pending (This is the [event type](https://docs.digitalriver.com/digital-river-api/events-and-webhooks-1/events-1/event-types) of the webhook.)
   * **Webhook Handler Name**: DRB2B\_RefundPendingWebhook (Custom Class Name)&#x20;
3. Click **Save**.
4. Set up the webhook for the Event Type `refund.pending` in the [Dashboard](https://docs.digitalriver.com/digital-river-api/administration/dashboard).
5. Configure the webhook for this event by going to **Webhooks** and click the Webhooks endpoint that was[ previously configured](broken-reference) for your organization. It will have an address of `https://<<SF_My_Domain_Name>>/services/apexrest/digitalriverv3/webhooks`\
   &#x20;![](broken-reference)&#x20;
6. Select the event `refund.pending` for the Webhook Endpoint selected in the previous step. &#x20;

### Webhook framework extension (example 2)

This section details another example of how to extend the webhook framework, this time for the `refund.complete event`. In this example, an email is sent with the event payload.

#### DRB2B\_RefundCompleteWebhook

```
   global class DRB2B_RefundCompleteWebhook extends 
   digitalriverv3.DRB2B_WebhookHandler {
 
    private static final digitalriverv3.DCM_Logger logger = 
    digitalriverv3.DCM_Logger.getInstance('Webhook Event');
        
    global override void processWebhookEvent(RestResponse response, 
    String webhookEventPayload) {// Log the event to Application log object
    logger.debug('Event: refund.complete; Refund Complete Webhook Event 
    Payload: ' + webhookEventPayload);

     // Send Email
      Messaging.SingleEmailMessage email = 
      new Messaging.SingleEmailMessage();
      email.setSubject('Process Webhook for event: refund.complete');
      email.setToAddresses(new List<String> 
      { 'example@digitalriver.com' });
      email.setHtmlBody(webhookEventPayload + '<br/> <br/>');
      Messaging.sendEmail(new Messaging.SingleEmailMessage[] { email });
        
        response.statusCode = 200;
    }
 
}

```

{% hint style="info" %}
Continue with the steps detailed in [Configuring the Apex class](broken-reference) to complete the configuration of the webhook extension.
{% endhint %}
