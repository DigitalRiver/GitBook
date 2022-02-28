---
description: Learn how to create SKUs and run Cron jobs.
---

# Step 5: Create SKUs and run Cron jobs

## SKU creation&#x20;

{% hint style="info" %}
Before performing this step, complete the [Digital River Configuration](step-1-open-or-update-the-digital-river-configuration-page.md), [Base Store Configuration](step-2-attach-the-base-store-configuration.md), [Digital River Tax Group](step-3-load-the-digital-river-tax-groups.md), and [Product Configuration](step-4-configure-the-product.md) steps.&#x20;
{% endhint %}

To create SKUs for the Digital River system, use the `ImpEx` below to create the Cron job at the merchant application after updating the product catalog ID and store ID.

```
$siteUid=electronics
$storeUid=electronics
$productCatalog=electronicsProductCatalog
INSERT_UPDATE CreateSKUCronJob;code[unique=true];job(code)[default=createSKUJob];
sessionLanguage(isoCode)[default=en];productCatalog;baseStore(uid)
;$siteUid-CreateSKUCronJob;;;$productCatalog;$storeUid


INSERT_UPDATE Trigger;cronJob(code)[unique=true];cronExpression
;$siteUid-CreateSKUCronJob;0 0/5 * 1/1 * ? *
```

![](<../.gitbook/assets/SKU creation.png>)

## Fee creation

Use the `ImpEx` below to create the fee.

```
$siteUid=electronics
$storeUid=electronics
$productCatalog=electronicsProductCatalog
INSERT_UPDATE CreateFeeCronJob;code[unique=true];job(code)
[default=createRegulatoryFeeJob];sessionLanguage(isoCode)[default=en];
baseStore(uid)
;$siteUid-CreateFeeCronJob;;;$storeUid


INSERT_UPDATE Trigger;cronJob(code)[unique=true];cronExpression
;$siteUid-CreateFeeCronJob;0 0/5 * 1/1 * ? *
```

![](<../.gitbook/assets/Fee job.png>)

### Fulfillment retry job

This Cron job gets the pending consignment list and creates a Digital River fulfillment.

#### Fulfillment retry job impex

```
$siteUid=electronics
$storeUid=electronics
$productCatalog=electronicsProductCatalog
INSERT_UPDATE  FulfillmentRetryJob;code[unique=true];job(code)
[default=createFulfillmentRetryJob];sessionLanguage(isoCode)[default=en];
baseStore(uid)
;$siteUid-FulfillmentRetryJob;;;$storeUid
```

![](<../.gitbook/assets/Fulfillment retry job.png>)

