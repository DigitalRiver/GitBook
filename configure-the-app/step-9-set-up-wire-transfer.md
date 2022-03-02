---
description: Learn how to set up Wire Transfer
---

# Step 9: Set up Wire Transfer

To handle refunds for Wire Transfer orders, we created the following items:

* A new storefront page where the shopper can provide their refund bank details
* A Wire Transfer pending information email notification

SAP Hybris sends a refund request to Digital River. When SAP Hybris receives a `refund.pending_information` event from Digital River,  it generates a Wire Transfer pending information email notification. This email notification provides a link to a storefront page where the shopper can provide their bank account details.

You need to import the following CMS ImpEx scripts to set up the Refund Information page.

{% code title="Send Wire Transfer Refund Email ImPex" %}
```
# -----------------------------------------------------------------------
# [y] hybris Platform
#
# Copyright (c) 2018 SAP SE or an SAP affiliate company.  All rights reserved.
#
# This software is the confidential and proprietary information of SAP
# ('Confidential Information'). You shall not disclose such Confidential
# Information and shall use it only in accordance with the terms of the
# license agreement you entered into with SAP.
# -----------------------------------------------------------------------
INSERT_UPDATE DynamicProcessDefinition;code[unique=true];active;content
;sendWireTransferRefundEmail-process;true;"<process xmlns='http://www.hybris.de/xsd/processdefinition' start='generateWireTransferEmail' name='sendWireTransferRefundEmail-process'
		processClass='de.hybris.platform.returns.model.ReturnProcessModel' onError='error'>

<action id='generateWireTransferEmail' bean='generateWireTransferEmail'>
    <transition name='OK' to='sendEmail'/>
    <transition name='NOK' to='error'/>
</action>

<action id='sendEmail' bean='sendEmail'>
    <transition name='OK' to='removeSentEmail'/>
    <transition name='NOK' to='failed'/>
</action>

<action id='removeSentEmail' bean='removeSentEmail'>
    <transition name='OK' to='success'/>
    <transition name='NOK' to='error'/>
</action>

<end id='error' state='ERROR'>Something went wrong.</end>
<end id='failed' state='FAILED'>Could not send return label email.</end>
<end id='success' state='SUCCEEDED'>Sent return label email.</end>

</process>"

```
{% endcode %}

{% code title="Import the Responsive CMS content for the Electronics site" %}
```
# -----------------------------------------------------------------------
# Copyright (c) 2019 SAP SE or an SAP affiliate company. All rights reserved.
# -----------------------------------------------------------------------
#
# Import the Responsive CMS content for the Electronics site
#
$contentCatalog=electronicsContentCatalog
$contentCV=catalogVersion(CatalogVersion.catalog(Catalog.id[default=$contentCatalog]),CatalogVersion.version[default=Online])[default=$contentCatalog:Online]

# Import modulegen config properties into impex macros
UPDATE GenericItem[processor=de.hybris.platform.commerceservices.impex.impl.ConfigPropertyImportProcessor];pk[unique=true]
$jarResourceCms=$config-jarResourceCmsValue
$lang=en


INSERT_UPDATE ContentPage;$contentCV[unique=true];uid[unique=true];name;masterTemplate(uid,$contentCV);label;defaultPage[default='true'];approvalStatus(code)[default='approved'];homepage[default='false'];
;;wiretransfer;Wire Transfer Details Page;AccountPageTemplate;wiretransfer


UPDATE ContentPage;$contentCV[unique=true];uid[unique=true];title[lang=$lang]
 ;;wiretransfer;"Wire Transfer Details"
```
{% endcode %}

{% code title="Import the CMS content for the Electronics site emails" %}
```
# -----------------------------------------------------------------------
# Copyright (c) 2019 SAP SE or an SAP affiliate company. All rights reserved.
# -----------------------------------------------------------------------
#
# Import the CMS content for the Electronics site emails
#
$contentCatalog=electronicsContentCatalog
$contentCV=catalogVersion(CatalogVersion.catalog(Catalog.id[default=$contentCatalog]),CatalogVersion.version[default=Online])[default=$contentCatalog:Online]
$wideContent=CMSImageComponent,BannerComponent,SimpleBannerComponent,CMSLinkComponent,CMSParagraphComponent

# Import config properties into impex macros for modulegen
INSERT_UPDATE GenericItem[processor=de.hybris.platform.commerceservices.impex.impl.ConfigPropertyImportProcessor];pk[unique=true]
$drEmailResourceValue=$config-drEmailResourceValue

# Import modulegen config properties into impex macros
UPDATE GenericItem[processor=de.hybris.platform.commerceservices.impex.impl.ConfigPropertyImportProcessor];pk[unique=true]
$drEmailPackageName=$config-drEmailPackageName

# Email page Template
INSERT_UPDATE EmailPageTemplate;$contentCV[unique=true];uid[unique=true];name;active;frontendTemplateName;subject(code);htmlTemplate(code);restrictedPageTypes(code)
;;WireTransferRefundEmailTemplate;Wire Transfer Refund Email Template;true;WireTransferRefundEmail;electronics_Email_WireTransfer_Refund_Subject;electronics_Email_WireTransfer_Refund_Body;EmailPage

# Templates for CMS Cockpit Page Edit
UPDATE EmailPageTemplate;$contentCV[unique=true];uid[unique=true];velocityTemplate[translator=de.hybris.platform.commerceservices.impex.impl.FileLoaderValueTranslator]
;;WireTransferRefundEmailTemplate;$drEmailResourceValue/structure_wireTransferReturnEmailTemplate.vm


INSERT_UPDATE ContentSlotName;name[unique=true];template(uid,$contentCV)[unique=true][default='WireTransferRefundEmailTemplate'];validComponentTypes(code)
;SiteLogo;;;logo
;TopContent;;$wideContent;
;BottomContent;;$wideContent;


INSERT_UPDATE ContentSlot;$contentCV[unique=true];uid[unique=true];name;active;cmsComponents(uid,$contentCV)
;;WireTransferRefundEmailTopSlot;Default WireTransferRefund Email Top Slot;true;EmailBannerSaleNowOnImage



# Bind Content Slots to Email Page Templates
INSERT_UPDATE ContentSlotForTemplate;$contentCV[unique=true];uid[unique=true];position[unique=true];pageTemplate(uid,$contentCV)[unique=true][default='WireTransferRefundEmailTemplate'];contentSlot(uid,$contentCV)[unique=true];allowOverwrite
;;SiteLogo-WireTransferRefundEmail;SiteLogo;;EmailSiteLogoSlot;true
;;TopContent-WireTransferRefundEmail;TopContent;;ReturnLabelEmailTopSlot;true
;;BottomContent-WireTransferRefundEmail;BottomContent;;EmailBottomSlot;true


# Email Pages
INSERT_UPDATE EmailPage;$contentCV[unique=true];uid[unique=true];name;masterTemplate(uid,$contentCV);defaultPage;approvalStatus(code)[default='approved']
;;WireTransferRefundEmail;Wire Transfer Refund Email;WireTransferRefundEmailTemplate;true;

# Email velocity templates
INSERT_UPDATE RendererTemplate;code[unique=true];contextClass;rendererType(code)[default='velocity']
;electronics_Email_Order_Confirmation_Body;$drEmailPackageName.DROrderNotificationEmailContext
;electronics_Email_Order_Confirmation_Subject;$drEmailPackageName.DROrderNotificationEmailContext
;electronics_Email_WireTransfer_Refund_Body;com.digitalriver.facade.process.email.context.WireTransferRefundEmailContext
;electronics_Email_WireTransfer_Refund_Subject;com.digitalriver.facade.process.email.context.WireTransferRefundEmailContext



INSERT_UPDATE ContentSlotName;name[unique=true];template(uid,$contentCV)[unique=true][default='WireTransferRefundEmailTemplate'];validComponentTypes(code)
;SiteLogo;;;logo
;TopContent;;$wideContent;
;BottomContent;;$wideContent;

INSERT_UPDATE ContentSlotForTemplate;$contentCV[unique=true];uid[unique=true];position[unique=true];pageTemplate(uid,$contentCV)[unique=true][default='WireTransferRefundEmailTemplate'];contentSlot(uid,$contentCV)[unique=true];allowOverwrite
;;SiteLogo-WireTransferRefundEmail;SiteLogo;;EmailSiteLogoSlot;true
;;TopContent-WireTransferRefundEmail;TopContent;;ReturnLabelEmailTopSlot;true
;;BottomContent-WireTransferRefundEmail;BottomContent;;EmailBottomSlot;true



```
{% endcode %}

{% code title="Email content (en_us)" %}
```
# -----------------------------------------------------------------------
# [y] hybris Platform
#
# Copyright (c) 2018 SAP SE or an SAP affiliate company.
# All rights reserved.
#
# This software is the confidential and proprietary information of SAP
# ("Confidential Information"). You shall not disclose such Confidential
# Information and shall use it only in accordance with the terms of the
# license agreement you entered into with SAP.
# -----------------------------------------------------------------------
# OMS velocity template for printing label

$contentCatalog=electronicsContentCatalog
$contentCV=catalogVersion(CatalogVersion.catalog(Catalog.id[default=$contentCatalog]),CatalogVersion.version[default=Online])[default=$contentCatalog:Online]
$lang=en
$picture=media(code, $contentCV);



# Import config properties into impex macros for modulegen
INSERT_UPDATE GenericItem[processor=de.hybris.platform.commerceservices.impex.impl.ConfigPropertyImportProcessor];pk[unique=true]
$drEmailResourceValue=$config-drEmailResourceValue

# CMS components and Email velocity templates
UPDATE RendererTemplate;code[unique=true];description[lang=$lang];templateScript[lang=$lang,translator=de.hybris.platform.commerceservices.impex.impl.FileLoaderValueTranslator]
 ;electronics_Email_WireTransfer_Refund_Body;"Return Wire Transfer Email Body";$drEmailResourceValue/email-wireTransferRefundBody.vm
 ;electronics_Email_WireTransfer_Refund_Subject;"Return Wire Transfer Email Subject";$drEmailResourceValue/email-wireTransferRefundSubject.vm

# Email Pages
UPDATE EmailPage;$contentCV[unique=true];uid[unique=true];fromEmail[lang=$lang];fromName[lang=$lang]
 ;;WireTransferRefundEmail;"customerservices@hybris.com";"Customer Services Team"

```
{% endcode %}
