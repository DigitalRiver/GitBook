---
description: Learn how to schedule backend jobs.
---

# Step 9: Schedule backend jobs

In order for the Salesforce Lightning app to continuously synchronize data between Salesforce and Digital River, you will need to schedule backend batch jobs.&#x20;

## Batch job overview

The following batch jobs are part of the Salesforce Lightning app:

* Product Sync batch job
* Fulfillment batch job
* DCM Purge Logs batch job

### Product Sync batch job

This batch job is used for product synchronization between Salesforce and Digital River. The Product Sync job will run automatically based on the setting in the batch job configuration record. To update the Product Sync settings, see [Configure and synchronize the products](step-7.-update-the-product-sync-settings.md).

### Fulfillment batch job

This job sends **Order and Line Item Level Fulfillment/Cancellation** requests to Digital River. This is used for Order and Line Item Level Fulfillment/Cancellation.

### DCM purge logs batch job

This job cleans up the DCM purge logs based on the configuration **Retention Days** using the custom setting **Digital River Logger Settings**. &#x20;

![](<../.gitbook/assets/DCM purge logs job.png>)

## Batch job scheduler

This section lists the scripts to schedule the following batch jobs with various **batch job run frequency** and **batch size options**.

| Batch job name           | Description                                                                                        | Default batch size |
| ------------------------ | -------------------------------------------------------------------------------------------------- | ------------------ |
| Fulfillment/Cancellation | `OrderFulfillment` is the batch job that needs to be specified while using scripts for scheduling. | 100                |
| DCM Purge Log            | `PurgeLogs` is the batch job which needs to be specified while using the scripts for scheduling.   | 200                |

{% hint style="info" %}
The `withSize`parameter can be used to specify batch sizes in the batch job scheduler.&#x20;

The maximum batch size for the `Fulfillment/Cancellation` batch job is 100.
{% endhint %}

## Batch run frequency&#x20;

The following batch job frequencies are used for various batch jobs:

| Batch frequency          | Description                                            | Example                                                                                                                                   |
| ------------------------ | ------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------- |
| Every X minutes          | Schedules fewer jobs to run every X minutes in an hour | `digitalriverv3.DRB2B_ConnectorScheduler. <BatchJobName>.scheduleEveryXMinutes(Integer everyMinute)`                                      |
| Every hour               | Schedules jobs to run every hour at a specified minute | `digitalriverv3.DRB2B_ConnectorScheduler. <BatchJobName>.scheduleHourly(Integer minute)`                                                  |
| Every day                | Schedules jobs to run every day at a specified time    | `digitalriverv3.DRB2B_ConnectorScheduler. <BatchJobName>.scheduleDaily(Integer hour, integer minute)`                                     |
| Based on cron expression | Schedules jobs based on cron expression                | `digitalriverv3.DRB2B_ConnectorScheduler. <BatchJobName>.scheduleCronExpr(String jobNameToShowUnderScheduledJobs, String cronExpression)` |

Specifying the batch size is optional while scheduling the jobs. Using the `withSize` parameter, the following syntax is used for specifying the batch size when scheduling a job to run every hour:&#x20;

```
digitalriverv3.DRB2B_ConnectorScheduler. <BatchJobName>.withSize(50).scheduleHourly
(Integer minute)
```

## Sample batch run frequency and batch size examples&#x20;

The following examples are sample frequency and batch size settings for the **Fulfillment/Cancellation** batch job and **DCM Purge Logs** batch job:

#### **Schedule Order Fulfillment/Cancellation batch job to run hourly with a batch size of 1.**

```
digitalriverv3.DRB2B_ConnectorScheduler.OrderFulfillment.withSize(1).
scheduleHourly
(1);
```

#### Schedule Order Fulfillment/Cancellation batch job to run hourly, using the default batch size of 100.

```
digitalriverv3.DRB2B_ConnectorScheduler.OrderFulfillment.scheduleHourly
(1);
```

#### Schedule Order Fulfillment batch job to run every 5 minutes with a batch size of 50.

```
digitalriverv3.DRB2B_ConnectorScheduler.OrderFulfillment.withSize(50).
scheduleEveryXMinutes(5);
```

#### Schedule Order Fulfillment/Cancellation batch job to run every 4 hours using cron expression. Use the default batch size of 100.

```
digitalriverv3.DRB2B_ConnectorScheduler.OrderFulfillment.
scheduleCronExpr('Fulfillment Every 4 hours', '0 0 0,4,8,12,16,20 ? 
* *');
```

#### Schedule DCM Purge Logs batch job to run nightly at 2AM, using the default batch size of 200.

```
digitalriverv3.DRB2B_ConnectorScheduler.PurgeLogs.scheduleDaily(2, 0);
```

