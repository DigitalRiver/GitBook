---
description: >-
  Understand how the Salesforce B2B Commerce App supports the processing of
  recurring installment payments.
---

# Managing subscriptions

A subscription is an arrangement for providing, receiving, or making use of something of a continuing or periodic nature on a (pre)payment plan. The Salesforce B2B Commerce App currently supports the processing of recurring installment payments.

The app comes with two batch jobs to process recurring installment payments.

## DR Batch Subscription Processor job

1. Runs on a schedule and picks the CC Subscription records for which recurring Installment payment needs to be processed.
2. Creates a CC Cart and adds the subscription product that is stamped on the CC Subscription record.
3. The Cart status will be set to the Custom Digital River status "Open-DR" so that it is not visible in the Storefront when the user logs in.
4. Updates the Subscription Installment Count and Installment Next Run date on the CC Subscription record.
5. Creates a DR Subscription Process Data record and populates it with Cart, Cart Item, Parent Order Id, Transaction Payment, Stored Payment, Subscribed Product, User, Contact, Account, and other information required for DR Order submission.

{% hint style="info" %}
**Notes:** The number of CC Subscription records processed per batch run is specified in the Metadata Record "CC\_Subscriptions\_Batch\_Query\_Limit" under Custom Metadata Type "DR Application Configuration".

The Batch Scope size is specified in the Metadata Record "CC\_Subscription\_Processor\_Batch\_Size" under Custom Metadata Type "DR Application Configuration".
{% endhint %}

## DR Recurring Payment Processor job

1. Query all DR Subscription Process Data records whose `Is Recurring Payment Processed` flag is `False` and the Subscription Job Run status field is set to `Open` ordered by Installment Run date.
2. This job goes through the entire checkout flow. That is, it makes calls to Digital River to get Tax, Create DR Order and Populate the DR Order information in Salesforce.
3. If this job is successful, then it sets the `Is Recurring Payment Processed` flag to `true` and Subscription Job Run Status to `Successful`.
4. If this job fails, then it sets the `Is Recurring Payment Processed` flag to `false` and Subscription `Job Run Status` to `Open` or `Failed` depending on the Subscription Retry Count value on this record.

### Subscription Retry Count Settings

1. If the Subscription Retry count field on this record exceeds the maximum retry count set in the configuration, then the `Subscription Job Run Status` is set to `Failed`.
2. If the Subscription Retry count field on this record is less than the maximum Retry count set in the Configuration, then the `Subscription Job Run Status` is set to `Open` so that this record is processed again next time.

{% hint style="info" %}
**Note:** The number of DR Subscription Process Data records processed per batch run is specified in the Metadata Record "Recurring\_Payment\_Process\_Query\_Limit" under Custom Metadata Type "DR Application Configuration".

The Batch Scope size is specified in the Metadata Record "Recurring\_Payment\_Batch\_Size" under Custom Metadata Type "DR Application Configuration".

The Subscription Retry Count is specified in the Metadata Record "Subscription\_Retry\_Count" under Custom Metadata Type "DR Application Configuration"
{% endhint %}

## Sequence diagram

The following sequence diagram explains the Recurring Installment Subscription Payment Process supported by the connector.

{% file src="../.gitbook/assets/subscription_flow_phase-2.1.1B.png" %}

