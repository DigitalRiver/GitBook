---
description: Learn about the limitations for the BigCommerce app.
---

# Limitations

* If you already have a transacting store with a non-Digital River payment integration, you must disable any non-Digital River payment and tax integrations before connecting with Digital River.
* This integration does not currently support the following features.
  * For SKU groups, there is only one `hsCode` per product
  * [Gift wrapping](https://support.bigcommerce.com/s/article/Gift-Wrapping?language=en\_US)
  * [Creating tax-exempt customers](https://support.bigcommerce.com/s/article/How-do-I-have-customers-with-a-tax-exempt-status?language=en\_US)
  * [Gift certificates](https://support.bigcommerce.com/s/article/Gift-Certificates?language=en\_US)
  * [Buy one get one free (BOGOF)](https://support.bigcommerce.com/s/article/Possible-Discounts-Offer?language=en\_US#promotions)
  * [Stored payment methods](https://support.bigcommerce.com/s/article/Enabling-Stored-Payment-Methods?language=en\_US)
  * Stored credit
* When the BigCommerce control panel triggers a refund and the refund fails, the order status will continue to display as refunded to the customer. The order timeline will reflect the failure correctly and you must use the Digital River [Dashboard ](https://dashboard.digitalriver.com/login)to [process the refund](https://docs.digitalriver.com/digital-river-api/administration/dashboard/order-management/orders/creating-a-refund).
* At this point, you must [refund the order](https://docs.digitalriver.com/digital-river-api/administration/dashboard/order-management/orders/creating-a-refund) from the [Digital River Dashboard](https://dashboard.digitalriver.com/login). See [Processing Refunds](https://support.bigcommerce.com/s/article/Processing-Refunds?language=en\_US) for more information.
