---
description: Learn how to run cron jobs.
---

# Step 5: Run cron jobs

## Create a SKU

{% hint style="info" %}
Before performing this step, complete the [Digital River Configuration](step-1-open-or-update-the-digital-river-configuration-page.md), [Base Store Configuration](step-2-attach-the-base-store-configuration.md), [Digital River Tax Group](step-3-load-the-digital-river-tax-groups.md), and [Product Configuration](step-4-configure-the-product.md) steps.&#x20;
{% endhint %}

To create a SKU for the Digital River system, run the `ImpEx` script below to create the cron job at the merchant application after updating the product catalog ID and store ID. The cron job runs every 5 minutes and uploads all approved products that were added or updated within that timeframe.

{% code title="ImpEx for SKU cron job" %}
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
{% endcode %}

![](<../.gitbook/assets/SKU creation.png>)

## Create a SKU group job

You can fetch the Digital River SKU groups and store them in SAP Hybris by running the SKUGroupConJob. This cron job will be created against the Digital River API key.

{% code title="ImPex for SKU grop cron job" %}
```javascript
INSERT_UPDATE ServicelayerJob ;code[unique=true];springId
;skuGroupJob;skuGroupJob


$drConfig=DRConfig

INSERT_UPDATE SKUGroupCronJob;code[unique=true];job(code)[default=skuGroupJob];sessionLanguage(isoCode)[default=en];drConfig(code)
;SKUGroupCronJob;skuGroupJob;en;$drConfig


INSERT_UPDATE Trigger;cronJob(code)[unique=true];cronExpression
;SKUGroupCronJob$siteUid-SKUGroupCronJob;0 0/5 * 1/1 * ? *Ce
```
{% endcode %}

You can later map the SKU groups stored in SAP Hybris to the respective products using the Digital **River SKU Group** attribute.

![](<../.gitbook/assets/DigitalRiver SKU Group attribute.png>)

## Create a fee job

Use the `ImpEx` script below to create the fee. The cron job runs every 5 minutes and uploads syncs the fee attribues that were added or updated within that timeframe.

{% code title="ImpEx for fee cron job " %}
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
{% endcode %}

![](<../.gitbook/assets/Fee job.png>)

## Retry fulfillment job

This cron job gets the pending consignment list and creates a Digital River fulfillment.

{% code title="ImpEx for retry fulfillment cron job" %}
```
$siteUid=electronics
$storeUid=electronics
$productCatalog=electronicsProductCatalog
INSERT_UPDATE  FulfillmentRetryJob;code[unique=true];job(code)
[default=createFulfillmentRetryJob];sessionLanguage(isoCode)[default=en];
baseStore(uid)
;$siteUid-FulfillmentRetryJob;;;$storeUid
```
{% endcode %}

![](<../.gitbook/assets/Fulfillment retry job.png>)

