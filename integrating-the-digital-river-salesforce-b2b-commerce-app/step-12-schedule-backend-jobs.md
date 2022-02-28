---
description: Learn how to schedule a backend job.
---

# Step 12: Schedule backend jobs

For the Salesforce B2B Commerce App to continuously synchronize data between Salesforce and Digital River, you need to schedule backend batch jobs. To schedule the backend jobs:

1. Click **Setup** ![](<../.gitbook/assets/setupicon (8) (6).png>) and select **Developer Console** from the dropdown list. The Developer window appears. \
   ![](<../.gitbook/assets/Install DR B2B API Connector80.png>)
2. Click **Debug** and select **Open Execute Anonymous Window**. The Enter Apex Code dialog appears.\
   ![](<../.gitbook/assets/Install DR B2B API Connector81.png>)
3. Copy the script from the first row of the table under **Batch Job Scripts** and run it in the Developer console Anonymous window.
4. Repeat Step 3 for every script in the [batch job scripts table](step-12-schedule-backend-jobs.md#batch-job-scripts).

## Batch job scripts <a href="#batch-job-scripts" id="batch-job-scripts"></a>

The following table lists the jobs that you need to schedule and the apex code that you can run to set up the jobs. You can also find these settings on the Schedule Jobs tab in the DR CC Config Settings spreadsheet.

| Batch Job Name                            | Script to Schedule Batch Job                                                                                                                                                                                                                                                                                      | Comments                                                                                                                                                                                       |
| ----------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Order Fulfillment Job                     | <p><code>// To run every 5 minutes</code> <br><code>for(Integer i=0; i&#x3C;60; i=i+5) {</code> </p><p><code>String cronTrigger = '0 ' + i + ' * * * ?';</code> </p><p><code>System.schedule('Order Fulfillment Job: ' + i, cronTrigger, new digitalriverv2.DRB2B_ScheduleOrderLevel_Fulfillment()); }</code></p> | This job sends Order Level Fulfillment Information to Digital River. Currently, this is used only for order cancellations.                                                                     |
| Line Item  Fulfillment Job                | <p><code>// Run Every 5 minutes</code> </p><p><code>for(Integer i=0; i&#x3C;60; i=i+5){ String cronTrigger = '0 ' + i + ' * * * ?'; System.schedule('Line Item Fulfillment Job: ' + i, cronTrigger, new digitalriverv2.DRB2B_ScheduleLineItem_Fulfillment());</code> </p><p><code>}</code></p>                    | This job sends line-item level fulfillment Information to Digital River.                                                                                                                       |
| CC Subscription Installment Processor Job | `Database.executeBatch(new ccrz.cc_batch_SubscriptionProcessor('DefaultStore', ccrz.cc_hk_Subscriptions.PARAM_CONTEXT_RECURR_INSTALL_ONLY, false));`                                                                                                                                                              | Schedule this job to run at least once every day.                                                                                                                                              |
| DR  Subscription Processor Job            | `//Schedule DR Subscription Processor Job every hour System.schedule('DR Subscription Processor Job, '0 0 * * * ?', new digitalriverv2.DRB2B_InstallmentSubscriptionProcessor());`                                                                                                                                | This job currently processes only 1 record at a time. Please schedule this more often in a day based on the number of installments that need to be processed.                                  |
| DCM Application Logs Cleanup Job          | <p><code>// Run once a day. You can configure this to run more often in lower environments where Logging Level might be set to DEBUG</code> <br><code>System.schedule('DCM Application Log Cleanup Job, '0 0 0 ? * * *', new digitalriverv2.DCM_ApplicationLogCleanupJob());</code></p>                           | This job cleans up the DCM Application logs based on the configuration “Delete Logs older than” in the Custom Metadata type **digitalriverv2\_\_DCM\_Application\_Log\_Configuration\_\_mdt**. |
