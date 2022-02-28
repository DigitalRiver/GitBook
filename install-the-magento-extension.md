---
description: >-
  Learn how to install the Digital River Global Commerce v. 2.1.1 Extension for
  Magento.
---

# Install the Magento Extension

## Install using Composer

Use Composer to install the Digital River Extension for Magento.

1. Run the following Composer command in the root of Magento:\
   `composer require digitalriver/module-drpay`
2. Update Magento to execute the install and update scripts in the command line in the root of Magento by executing:\
   `bin/magento setup:upgrade`
3. In the Magento Admin panel click **System**, click **Cache Management**, and then click **Flush Cache Storage**.
4. Log out of Magento and then log back in.
