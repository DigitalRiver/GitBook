---
description: >-
  Learn how to initiate a Prebuilt Checkout session and generate your own
  Prebuilt Checkout links.
---

# Generate Prebuilt Checkout links

You can [configure Prebuilt Checkout](../../settings/prebuilt-checkout.md) in the Digital River Dashboard to generate Prebuilt Checkout links. Share these links to connect customers to an upstream commerce system with Digital River's payment processing, fraud detection, tax exemption, and disclosure services.

To use this feature, you first [create and save a Prebuilt Checkout](../../settings/prebuilt-checkout.md). You can create, save, update, and manage Prebuilt Checkout scoped configurations if assigned an [Administrator](../../settings/users-and-roles/) role.

If you have an Administrator or [Customer Service](../../settings/users-and-roles/) role, you can go to the **Create Prebuilt Checkout link** page and initiate a session to generate Prebuilt Checkout links. Share these links with customers to access a UI checkout model that lets them complete a purchase.

For more information on creating a [Prebuilt Checkout configuration](../../settings/), refer to [Prebuilt Checkout](../../../../integration-options/low-code-checkouts/drop-in-checkout.md).

{% hint style="warning" %}
**Note:** You can access all or part of the Prebuilt Checkout feature based on your assigned role when using the Dashboard.

If assigned a **Customer Service** role, you can

* [Create a Prebuilt Checkout link session.](generate-prebuilt-checkout-links.md#create-a-drop-in-checkout-session-and-links)
* [Generate a one-time Prebuilt Checkout link ](generate-prebuilt-checkout-links.md#generate-a-one-time-use-drop-in-checkout-link-administrator-or-customer-service-role-required)that expires in 24 hours.
* [Generate ](generate-prebuilt-checkout-links.md)a reusable Prebuilt Checkout link with no expiration.
* [Add an existing customer to the Create Prebuilt Checkout links page during a session.](add-a-customer-during-prebuilt-checkout.md)
* [Add a current product to the Create Prebuilt Checkout links page during a session.](add-a-product-during-prebuilt-checkout.md)

If assigned an **Administrator** role, you can do the following with this feature:

* [Create, save, update, and manage Prebuilt Checkout scoped configurations](../../settings/prebuilt-checkout.md).
* [Create a Prebuilt Checkout link session.](generate-prebuilt-checkout-links.md#create-a-drop-in-checkout-session-and-links)
* [Generate a one-time Prebuilt Checkout link that expires in 24 hours.](generate-prebuilt-checkout-links.md#generate-a-one-time-use-drop-in-checkout-link-administrator-or-customer-service-role-required)
* [Generate a _reusable_ Prebuilt Checkout link with no expiration period.](generate-prebuilt-checkout-links.md#generate-a-reusable-drop-in-checkout-link-administrator-role-required)
* [Delete any reusable Prebuilt Checkout link you no longer wish to be active.](generate-prebuilt-checkout-links.md#delete-an-existing-checkout-link)
* [Add a new or an existing customer to the Create Prebuilt Checkout links page during a session.](add-a-customer-during-prebuilt-checkout.md)
* [Add a new or current product to the Create Prebuilt Checkout links page during a session.](add-a-product-during-prebuilt-checkout.md)

For more information on roles, refer to [Users and roles](../../settings/users-and-roles/).
{% endhint %}

## Create a Prebuilt Checkout session and generate links

Use the **Create Prebuilt Checkout link** page to

* Create and initiate a Prebuilt Checkout link session.
* Generate one-time use and reusable checkout links. These links can be shared with customers to access a UI checkout modal that lets them complete their purchase.
* Delete existing links that need to be taken out of circulation. You must be assigned an [administrator role ](../../settings/users-and-roles/)to do this.
* [Add a new or an existing customer to the Create Prebuilt Checkout links page during a session.](add-a-customer-during-prebuilt-checkout.md) Users with an Administrator role can add new or existing customers. Users with a Customer service can only add existing customers.
* [Add a new or current product to the Create Prebuilt Checkout links page during a session.](add-a-product-during-prebuilt-checkout.md) Users with an Administrator role can add new or existing products. Users with a Customer service can only add existing products.

To create a Prebuilt Checkout link session that lets you generate one-time use and reusable checkout links, do the following:

1. Go to the [**Order Management**](../) section in the left navigation of the Dashboard.
2.  Click **Prebuilt Checkout links** to go to the **Prebuilt Checkout links** page.

    <figure><img src="../../../../.gitbook/assets/1 pbco links list.png" alt=""><figcaption></figcaption></figure>
3.  Click the **Add link** button at the top of the page. The **Create Prebuilt Checkout link** page appears.

    <figure><img src="../../../../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>
4. [Provide the Prebuilt Checkout session information](generate-prebuilt-checkout-links.md#provide-the-prebuilt-checkout-session-information).

### Provide the Prebuilt Checkout session information

Use the following steps to provide checkout session information (required and optional) on the **Create Prebuilt Checkout link** page.

1. Click **Order Management** in the Dashboard left navigation. Click **Prebuilt Checkout links** to go to the **Prebuilt Checkout links** page. Click **Add link**.
2. Under **Required information**, enter the\
   three-character currency code in the **Currency** field of the **Product** subsection. Refer to the [ISO-4217 Standard](https://www.iso.org/iso-4217-currency-codes.html) for more information on currency codes.
3. Under **Required information**, click **Add Product** to display the **Add product** modal and [add a new or current product](add-a-product-during-prebuilt-checkout.md) to your Prebuilt Checkout session. Follow the modal instructions to add a new product or choose from existing products.
4. Under this page's **Default shipping methods** subsection, default shipping method information is pulled from the saved Prebuilt Checkout configuration to populate this page section with the configured information. None will be displayed if you have not initially configured default shipping methods. You are then given an alert message and a link to the [**Configure Prebuilt Checkout**](../../settings/prebuilt-checkout.md) page to configure the required shipping methods.
5. Under **Optional information**, add your **Shopping country** by specifying its two-character country code.\
   **Note:** The country choice you provide here overrides the[ Default shopping country choice](../../settings/prebuilt-checkout.md#create-a-drop-in-checkout-configuration) set in the [original Prebuilt Checkout](../../settings/prebuilt-checkout.md) configuration if it is a different country choice. If you enter nothing in this field, the session uses the value specified in the [Prebuilt Checkout configuration](../../settings/prebuilt-checkout.md).
6. Under **Optional information**, add your checkout session's **Language** setting. Digital River uses the [checkout-session's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions) `language` to set the [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) `language`, which, once the [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) is successfully created, determines [how purchase invoices and credit memos are localized](../../../../integration-options/checkouts/creating-checkouts/designating-a-locale.md). Refer to [Supported languages](https://docs.digitalriver.com/digital-river-api/developer-resources/supported-languages) for more information.
7. Under **Optional information**, select the tax-inclusive option you want in the **Tax inclusive** subsection. Click the correct radio button to select your desired option (**Not selected**, **True**, or **False)**. Refer to [Tax calculations](../../../../integration-options/checkouts/creating-checkouts/tax-calculations.md) and [Configuring Taxes](https://docs.digitalriver.com/digital-river-api/integration-options/checkouts/creating-checkouts/configuring-taxes#setting-tax-inclusive-prices) for more information on these options. The option you choose is later displayed on the Checkout link details page.
8. Under **Optional information**, click **Add Customer** to display the **Add customers** modal. From this modal, you can either:
   1. Select **Create new customer** to add a new customer to the page. Add the requested customer info. Click **Continue** to add the new customer to the **Create Prebuilt Checkout link** page.\
      \
      **Note:** When creating a new customer, you must select either **Individual** or **Business** as a customer Type, or you cannot add the customer information to the Create Prebuilt Checkout link page.
   2. Select **Choose from current customers** to add an existing customer to the page. Provide the existing Customer ID or email address in the Search field to search for and display that customer's information. Click **Continue** to add the customer to the page.\
      \
      **Note**: For complete details on adding or changing a customer, refer to [Add a customer during Prebuilt Checkout](add-a-customer-during-prebuilt-checkout.md).
9. Add optional [order-level](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) metadata to the Prebuilt checkout session. Provide additional [metadata ](https://www.digitalriver.com/docs/digital-river-api-reference/#section/Metadata)that may be useful for Sales or a client brand. You can add metadata on this page that is integrated into the [order](../../../../order-management/creating-and-updating-an-order.md) object and is visible in all order-related [webhooks](../../../../order-management/events-and-webhooks-1/webhooks/). For instance, if a client system captures an [`order.accepted` event](../../../../order-management/events-and-webhooks-1/events-1/event-types.md), you could include metadata in the accepted order. Metadata can be helpful for a client setting a specific value, such as a number or code, as information for a particular checkout. They could easily include metadata to identify that order when it comes through.\
   \
   In the Optional information **Metadata** subsection, enter the following information in the row:
   * Name: Provide a descriptive name (for example, subscriberID or coupon\_Program) for the metadata you add.
   * String: Select the correct datatype for the metadata from the drop-down list. Choose either **String**, **Integer**, or **Boolean**. The default setting is String.
   * Value: Provide the metadata value you passed with the prebuilt checkout session.
10. Click **Add metadata** to add another metadata and repeat Step 8.
11. Click the **Delete** icon <img src="../../../../.gitbook/assets/image (78).png" alt="" data-size="original">to delete a metadata row.
12. Under **Optional information**, enter the JSON script in the field of **Customize style** subsection. This script customizes the style of the checkout modal presented to a customer when a checkout link is clicked. In this subsection, you also have a link to click to go to the information assisting with the coding of the modal script. You are also provided with a "starter" template version of a script (on the right side of the subsection) that you can copy into the field and modify as needed.

{% hint style="info" %}
**Note:** An error message appears if you enter incorrect or invalid information on this page. A link will be generated once the incorrect data has been fixed or removed. This could include entering incorrect JSON XML, data of the wrong type for a field, invalid currency code, and so on.
{% endhint %}

### Generate a one-time use Prebuilt Checkout link (Administrator or Customer Service [role ](../../settings/users-and-roles/)required)

Once Required and Optional information has been entered, if you have an Administrator or Customer Service role, you can generate a one-time use Prebuilt Checkout link to share with a customer.

Use the following steps to generate a one-time use Prebuilt Checkout link:

1.  Click **Generate reusable link** button on the **Create Prebuilt Checkout links** page. This action launches a **Prebuilt Checkout link details** page with the one-time-use link information in the **Prebuilt Checkout session link** section. This link expires in 24 hours and is NOT reusable. The link can be shared with customers to access a UI checkout modal that lets them complete a purchase.\
    \
    **Note:** If you use the one-time-use (single session) link at all during this Prebuilt Checkout session, you will not be able to generate a reusable link.

    <figure><img src="../../../../.gitbook/assets/2 generate pbco checkout links.png" alt=""><figcaption></figcaption></figure>
2. Click the copy icon next to the generated link information to copy the link URL to the Clipboard.
3. Share the copied link with a customer as desired.

{% hint style="info" %}
**Note:** An error message appears if you enter incorrect or invalid information. A link will not be generated until the incorrect data has been fixed or removed. This could include entering incorrect JSON XML, data of an incorrect type for a field, invalid currency code, and so on.
{% endhint %}

### Generate a reusable Prebuilt Checkout link

Once **Required** and **Optional information** has been entered, you can generate a reusable Prebuilt Checkout link to share with a customer if assigned an Administrator or Customer service role.

Use the following steps to generate a reusable Prebuilt Checkout link:

1. Click the **Generate reusable link** button on the **Create Prebuilt Checkout links** page. This action launches a **Checkout link details page** with the one-time-use link information and an option in the middle of the page to create a reusable link by clicking the **Generate reusable link** button.
2. Confirm all information displayed on the **Checkout link details page** before generating the reusable link.
3.  Click the **Generate reusable link** button to create the reusable Prebuilt Checkout link. This action again launches an updated **Checkout link details page,** but this time, it also displays the reusable link URL in the **Re-usable link** portion of the page. This link is reusable and _does not_ expire. This link can be shared with customers to access a UI checkout modal that lets them complete a purchase.\
    \
    **Note:** You cannot generate the reusable link if you use the one-time-use (single session) during this Prebuilt Checkout session.

    <figure><img src="../../../../.gitbook/assets/3 generate pbco checkcout links reusable.png" alt=""><figcaption></figcaption></figure>
4. Click the copy icon next to the generated reusable link to copy the reusable link URL to the Clipboard.
5. Share the copied link with a customer as desired.

{% hint style="info" %}
**Note:** An error message appears if you enter incorrect or invalid information on this page. A link will not be generated until the wrong data has been fixed or removed. This could include entering incorrect JSON XML, data of an incorrect type for a field, and so on.
{% endhint %}

### Understand the checkout modal

When you generate either a one-time or reusable link, you can share it with a customer to allow that customer access to a UI checkout modal that lets them complete a purchase.

The style and appearance of the checkout modal interface can differ depending on the information provided in the **Optional information** section of the **Prebuilt Checkout links** page. This would include providing the modal style script.

After a customer receives a shared Prebuilt Checkout link and clicks it, they are presented with a purchase checkout flow of checkout modals. Following the modals and providing any remaining information, they can complete their purchase without needing a storefront user interface.

An example of a checkout modal flow might look like the following. In the first example, the customer is purchasing a SAAS service, which is not taxed since it is a digital product (as opposed to a physical). Also, if a customer ID had been provided in the initial session settings, all name and address information would have populated the related fields:

<div align="left">

<img src="../../../../.gitbook/assets/dig checkout order modal match 1.png" alt="">

</div>

<div align="left">

<img src="../../../../.gitbook/assets/dig checkout order modal match 2.png" alt="">

</div>

The following modal screen flow example shows the modals received with the purchase of a physical product with taxes included:

<div align="left">

<img src="../../../../.gitbook/assets/phys checkout order modal 1.png" alt="">

</div>

<div align="left">

<img src="../../../../.gitbook/assets/phys checkout order modal 2.png" alt="">

</div>

When the customer is presented with these checkout modals, they can complete their purchase without needing an actual storefront user interface.

### Delete an existing checkout link

If you have an Administrator role, you can delete reusable or one-time-use Prebuilt Checkout links to remove them from circulation.

Use the following procedure to delete a reusable or one-time-use Prebuilt Checkout link while on the **Prebuilt Checkout links** page.

1. Go to the [**Order Management**](../) section in the left navigation of the Dashboard. Click **Prebuilt Checkout links** to go to the **Prebuilt Checkout links** page. This page lists all permanent links you have created and provides an ID link to each link's details page.
2.  Click the **More** icon (vertical ellipses) at the link row's end.

    <figure><img src="../../../../.gitbook/assets/4 pbco links delete list.png" alt=""><figcaption></figcaption></figure>
3.  Click **Delete** to delete that Prebuilt Checkout link and its information.\
    **Note:** Only users with an **Administrator** role can delete a link. The following modal appears:

    <figure><img src="../../../../.gitbook/assets/5 dlete2 pbco checkout links.png" alt=""><figcaption></figcaption></figure>
4. Click **Confirm** to delete the link.

You can also delete a link from the **Prebuilt checkout link details** page by doing the following:

1. Go to the **Order Management** section in the left navigation of the Dashboard.
2. Click **Prebuilt Checkout links** to go to the **Prebuilt Checkout links** page.
3. Use the Search link ID feature or scroll to find the link whose details you want to view. Click **ID.** The **Prebuilt Checkout link details** page appears with all the link information.
4.  Click **Delete link** at the top of the page.

    <figure><img src="../../../../.gitbook/assets/6 delete pbc checkout.png" alt=""><figcaption></figcaption></figure>
5.  Click **Confirm**. A green "Checkout link deleted" message appears if the link is successfully removed. A red "Checkout link not deleted" message appears if invalid data is entered.\


    <div align="left">

    <figure><img src="../../../../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

    </div>

{% hint style="info" %}
**Note:** An error message appears if you enter and submit an invalid or typed checkout link. Ensure all link data is valid and free of typos or copying mistakes before submitting it.
{% endhint %}
