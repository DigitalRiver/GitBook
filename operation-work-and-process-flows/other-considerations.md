---
description: Understand other considerations when working with Magento Extension.
---

# Other considerations

To upgrade to a new version of the DrPay module, replace the `DrPay` folder in your directory with the updated version, and execute the upgrade. Following the upgrade command, flush the Magento cache. No other action is required and configurations will remain in place.

To add the Digital River legal footer links on the payments and review page, create a new block by navigating to **Content**, then **Blocks**, and then **Add New Block**. Name the block `PrivacyBlock` and include the following content. (This is the legal default requirement for US sales. For EU and/or global stores, links may vary.)

```
<p style="text-align: center;">
  <a href="https://store.digitalriver.com/DRHM/store?Action=DisplayDRAboutDigitalRiverPage&amp;SiteID=defaults&amp;Locale=en_US&amp;ThemeID=22100&amp;Env=BASE&amp;eCommerceProvider=Digital%20River,%20Inc.">Digital River Inc.</a> is the authorized reseller and merchant of the products and services offered within this store.</p>
<p style="text-align: center;">
  <a href="https://store.digitalriver.com/DRHM/store?Action=DisplayDRTermsAndConditionsPage&amp;SiteID=defaults&amp;Locale=en_US&amp;ThemeID=22100&amp;Env=BASE&amp;eCommerceProvider=Digital%20River,%20Inc.">Terms of Sale</a>  <a href="https://store.digitalriver.com/DRHM/store?Action=DisplayDRPrivacyPolicyPage&amp;SiteID=defaults&amp;Locale=en_US&amp;ThemeID=22100&amp;Env=BASE&amp;eCommerceProvider=Digital%20River,%20Inc.">Privacy Policy</a>  <a href="https://store.digitalriver.com/DRHM/store?Action=DisplayDRPrivacyPolicyPage&amp;SiteID=defaults&amp;Locale=en_US&amp;ThemeID=22100&amp;Env=BASE&amp;eCommerceProvider=Digital%20River,%20Inc.#collection_of_information">Cookies</a>  <a href="https://store.digitalriver.com/store/defaults/en_US/DisplayCCPAPage">Your California Privacy Rights</a>
</p>
```

The following block will appear above the Magento footer at the bottom of the content container in the `checkout_index_index.xml` layout. &#x20;

![](../.gitbook/assets/FooterBlock.png)

On the final order review page add the following text should also along with a checkbox to explicitly accept the Digital River Terms of Sale and Privacy Policy prior to checkout:

_“By checking this box, I confirm that I have read and agree to the Digital River Inc. Terms of Sale and Privacy Policy.”_
