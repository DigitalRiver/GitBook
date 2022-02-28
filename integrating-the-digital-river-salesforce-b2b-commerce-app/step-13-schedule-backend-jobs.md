---
description: Learn how to schedule a backend job.
---

# Step 13: Schedule backend jobs

For the App to continuously synchronize data between Salesforce and Digital River, you need to schedule several backend jobs. To schedule the backend jobs:

1. Click **Setup** ![](../.gitbook/assets/Setup.png) and select **Developer Console** from the dropdown list. The Developer Console opens.\
   &#x20;![](<../.gitbook/assets/developer-console (1).png>)
2. Click **Debug** and select **Open Execute Anonymous Window**. The Enter Apex Code dialog appears.\
   &#x20;![](../.gitbook/assets/Open-Execute-Anonymous-Window.png)
3. Copy the script from the first row of the table under [Backend job scripts](step-13-schedule-backend-jobs.md#backend-job-scripts), paste it in the Enter Apex Code dialog, and click **Execute**. Repeat this step for each additional script in the table.

## Backend job scripts <a href="#backend-job-scripts" id="backend-job-scripts"></a>

The following table lists the jobs that you need to schedule and the apex code that you can run to set up the jobs. You can also find these settings on the Schedule Jobs tab in the DR CC Config Settings spreadsheet.

| Job Name                                  | Script for Scheduled Job                                                                                                                                                                                                                                                                                                                                                                                                 | Comments                                                                                                                      |
| ----------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------- |
| Order Level Electronic Fulfillment Job    | <p><code>// EFN To run every 5 minute</code> <br><code>for(Integer i=0; i&#x3C;60; i=i+5){</code> <br>   <code>String cronTrigger = '0 ' + i + ' * ?';</code> <br>   <code>String jobID = System.schedule('Job Send EFN every 5 minutes' + i, cronTrigger, new digitalriverb2b.DRB2B_ScheduleOrderLevelEFN());</code> <br>   <code>System.debug('Scheduled Job ID: ' + jobID);</code> <br><code>}</code></p>             |                                                                                                                               |
| Line Item Electronic Fulfillment Job      | <p><code>// Line Item EFN every 5 minutes</code> <br><code>for(Integer i=0; i&#x3C;60; i=i+5){</code> <br>   <code>String cronTrigger = '0 ' + i + ' * ?';</code> <br>   <code>String jobID = System.schedule('Job Send Line Item EFN every 5 minutes' + i, cronTrigger, new digitalriverb2b.DRB2B_ScheduleLineItemEFN());</code> <br>   <code>System.debug('Scheduled Job ID: ' + jobID);</code> <br><code>}</code></p> |                                                                                                                               |
| CC Subscription Processor Job             | <p><code>// Schedule CC Subscription Processor Job</code> <br><code>System.schedule('CC Subscription Procesor Job Hourly', '0 0 * ?', new digitalriverb2b.DRB2B_ScheduledSubscriptionProcess());</code></p>                                                                                                                                                                                                              | Only enable this script if you need to support subscriptions. Consult with the Digital River team before scheduling this Job. |
| DR Installment Subscription Processor Job | <p><code>//Schedule Installment Subscription Processor Job every hour</code> <br><code>System.schedule('DR Installment Subscription Processor Job Hourly', '0 0 * ?', new digitalriverb2b.DRB2B_InstallmentSubscriptionProcessor());</code></p>                                                                                                                                                                          | Only enable this script if you need to support subscriptions. Consult with the Digital River team before scheduling this Job. |
