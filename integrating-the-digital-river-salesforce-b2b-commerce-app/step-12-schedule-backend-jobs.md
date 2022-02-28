---
description: Learn how to schedule a backend job.
---

# Step 12: Schedule backend jobs



For the Salesforce B2B Commerce App to continuously synchronize data between Salesforce and Digital River, you need to schedule backend batch jobs. To schedule the backend jobs:‌

1. Click **Setup** ​![](https://firebasestorage.googleapis.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-MNZuPvN3iGOwRD0PjQh%2F-MRVrQ1ufxwn-s8BpGW2%2F-MRVrv14OLV-oqRNPKJF%2FSetupIcon.png?alt=media\&token=fa294a7a-8ad2-4272-80c9-ae537afde283) and select **Developer Console** from the dropdown list. The Developer window appears. ​![](https://firebasestorage.googleapis.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-MNZuPvN3iGOwRD0PjQh%2F-MRS2TDFKNKGtbIVxZf6%2F-MRS2pVzg1HxTIScU2AW%2FInstall%20DR%20B2B%20API%20Connector80.png?alt=media\&token=15839e4e-b224-4224-90ac-5172d8ff73f6)​
2. Click **Debug** and select **Open Execute Anonymous Window**. The Enter Apex Code dialog appears. ​![](https://firebasestorage.googleapis.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-MNZuPvN3iGOwRD0PjQh%2F-MRS2sHy-DwyObgbJRlP%2F-MRS2x4PLD5WWtVztf7o%2FInstall%20DR%20B2B%20API%20Connector81.png?alt=media\&token=e2ae2c8e-0dc8-4ed8-9bc8-bb5b34250d69)​
3. Copy the script from the first row of the table under **Batch Job Scripts** and run it in the Developer console Anonymous window.
4. Repeat Step 3 for every script in the [batch job scripts table](https://app.gitbook.com/@digital-river/s/salesforce-b2b/\~/drafts/-MUFD89-u-0FP\_Ew0TXJ/v/2.1.1/integrating-the-digital-river-salesforce-b2b-commerce-app/step-12-schedule-backend-jobs#batch-job-scripts/@drafts).

‌

## Batch job scripts <a href="#batch-job-scripts" id="batch-job-scripts"></a>

‌

The following table lists the jobs that you need to schedule and the apex code that you can run to set up the jobs. (Replace `<<STOREFRONT_NAME>>` with your own storefront name).

| Batch Job Name                      | Script to Schedule Batch Job                                                                                                                                                                                                                                                                   | Comments                                                                                                                                                                                       |
| ----------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Order Fulfillment Job               | <p><code>// To run every 5 minutes for(Integer i=0; i&#x3C;60; i=i+5) {</code></p><p><code>String cronTrigger = '0 ' + i + ' * * * ?';</code></p><p><code>System.schedule('Order Fulfillment Job: ' + i, cronTrigger, new digitalriverv2.DRB2B_ScheduleOrderLevel_Fulfillment()); }</code></p> | This job sends Order Level Fulfillment Information to Digital River. Currently, this is used only for order cancellations.                                                                     |
| Line Item Fulfillment Job           | <p><code>// Run Every 5 minutes</code></p><p><code>for(Integer i=0; i&#x3C;60; i=i+5){ String cronTrigger = '0 ' + i + ' * * * ?'; System.schedule('Line Item Fulfillment Job: ' + i, cronTrigger, new digitalriverv2.DRB2B_ScheduleLineItem_Fulfillment());</code></p><p><code>}</code></p>   | This job sends line-item level fulfillment Information to Digital River.                                                                                                                       |
| DR Batch Subscription Processor Job | `System.schedule('DR Batch Subscription Processor Job', '0 0 * * * ?', new digitalriverv2.DRB2B_Schedule_BatchSubscriptionProcess('<<STOREFRONT_NAME>>', 'RECURR_INSTALL'));`                                                                                                                  | Schedule this job to run at least once every day.                                                                                                                                              |
| DR Recurring Payment Processor Job  | `Schedule System.schedule('DR Recurring Payment Processor Job', '0 0 * * * ?', new digitalriverv2.DRB2B_Schedule_RecurringPaymentProcess('RECURR_INSTALL'));`                                                                                                                                  | This job currently processes only 1 record at a time. Please schedule this more often in a day based on the number of installments that need to be processed.                                  |
| DCM Application Logs Cleanup Job    | `// Run once a day. You can configure this to run more often in lower environments where Logging Level might be set to DEBUG System.schedule('DCM Application Log Cleanup Job, '0 0 0 ? * * *', new digitalriverv2.DCM_ApplicationLogCleanupJob());`                                           | This job cleans up the DCM Application logs based on the configuration “Delete Logs older than” in the Custom Metadata type **digitalriverv2\_\_DCM\_Application\_Log\_Configuration\_\_mdt**. |
