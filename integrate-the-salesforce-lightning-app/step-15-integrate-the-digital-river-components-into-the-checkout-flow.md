---
description: Learn how to integrate the Digital River components into the checkout flow.
---

# Step 15: Integrate the Digital River components into the checkout flow

The Salesforce Lightning application comes with a completely functional checkout flow out-of the-box (OOTB). However, many clients will choose to customize their checkout flow to suit their particular needs. This section describes how you can use the Salesforce Lightning components provided by the application in your storefront.&#x20;

## Custom components used in the checkout subflows

| Custom subflow name | Custom component(s) used                                             | Description                                                                                  |
| ------------------- | -------------------------------------------------------------------- | -------------------------------------------------------------------------------------------- |
| DR Shipping Address | drb2b\_BuyerInfo                                                     | This custom subflow will be used in the place of OOTB subflow – Shipping Address.            |
| DR Delivery Method  | drb2b\_DRUtil                                                        | This custom subflow will be used in the place of OOTB subflow – Delivery Method.             |
| DR Checkout Summary | <p>drb2b_DRUtil </p><p>drb2b_DrTermsElement drb2b_taxIdentifier</p>  | This custom subflow will be used in the place of OOTB subflow – Checkout Summary.            |
| DR Payments         | <p>drb2b_Order Summary </p><p>drb2b_DRUtil </p><p>drb2b_Payments</p> | This custom subflow will be used in the place of OOTB subflow – Payment and Billing Address. |

## Subflow configuration

### Configure the shipping address subflow

This subflow will be used to capture buyer information such as `Bill To`, `Ship To`, and `Email`.

1. Go to **Setup** and search **flows** in the **Search** field.\
   ![](<../.gitbook/assets/Shipping address subflow 1 (1).png>)&#x20;
2. Click **Subflow - Shipping Address**. \
   ![](<../.gitbook/assets/Shipping address subflow 2.png>)&#x20;
3. Click the **Shipping Address** screen. \
   &#x20;![](<../.gitbook/assets/Shipping address subflow 3.png>)&#x20;
4. Click the screen in the flow and drag the **Buyer Info** component. \
   ![](<../.gitbook/assets/Shipping address subflow 4.png>)&#x20;
5. Enter the **API Name**, **Cart Id**, **Enable Tax Certificate**, and **Shipping Address ID** (in the **Advanced** section and only visible by selecting **Manually assign variables** check box).
   * **API Name**: BuyerInfo or any other name with no restriction
   * **Cart Id** - ({!cartId})
   * **Enable Tax Certificates**: ({!$GlobalConstant.True}) OR ({!$GlobalConstant.False})
   * **Shipping Address ID**: ({!contactPointAddressId}) \
     ![](<../.gitbook/assets/Shipping address subflow 5.png>)&#x20;
6. Click **Done**.&#x20;
7. Click **Save As**. \
   ![](<../.gitbook/assets/Shipping address subflow 6.png>)&#x20;
8. Enter the name of the custom subflow (for example, DR Shipping Address) and click **Save**. \
   ![](<../.gitbook/assets/Shipping address subflow 1.png>)&#x20;
9. Click **Activate**.

### Configure the delivery method subflow

To configure the Delivery Method subflow:

1. Go to **Setup** and search flows in the **Search** field.
2. Click **Subflow - Delivery Method**. \
   ![](<../.gitbook/assets/Delivery method subflow 1.png>)&#x20;
3. Click the **Delivery Method** screen. \
   ![](<../.gitbook/assets/Delivery method subflow 2.png>)&#x20;
4. Add the `drb2b_DRUtil` component to the screen and enter the API name (drb2b\_Util or any name).
5. Click **Done**. \
   ![](<../.gitbook/assets/Delivery method subflow 3.png>)&#x20;
6. Click **Save As**. \
   ![](<../.gitbook/assets/Delivery method subflow 4.png>)&#x20;
7. Enter the Delivery Method subflow name (for example, DR Delivery Method).
8. Click **Save**, then click **Activate**. \
   ![](<../.gitbook/assets/Delivery method subflow 5.png>)&#x20;

### Configure the checkout summary subflow

This subflow will be customized to add US Tax Certificate and Tax Identifier support.&#x20;

#### Create a variable

To create a variable:

1. Go to **Setup** and search flows in the **Search** field.
2. Click **Subflow - Checkout Summary**. \
   ![](<../.gitbook/assets/Checkout summary subflow 1.png>)&#x20;
3. Click the **Manager** tab and then click **New Resource**. \
   ![](<../.gitbook/assets/Checkout summary subflow 2.png>)&#x20;
4. Complete the following fields:
   * **Resource Type**: Variable
   * **API Name**: Saved\_Tax\_Identifier (or other name as desired)
   * **Data Type**: Text
5. Check the **Available for input** and **Available for output** checkboxes.
6. Click **Done**. \
   ![](<../.gitbook/assets/Checkout summary subflow 3.png>)&#x20;

{% hint style="info" %}
This variable will be used to display payment information in a later step.
{% endhint %}

#### Add custom components to the checkout summary subflow

To add custom components for this subflow:

1. Click into the **Cart to Order Summary** screen. &#x20;
2. Remove all OOTB components from the subflow except the **Shipping Address** and **Delivery Method** components.
3. Add the `drb2b_DRutil` component and define the name. \
   ![](<../.gitbook/assets/Add custom components to checkout summary 1.png>)&#x20;
4. Add the `drb2b_taxIdentifier` and enter the **API Name**, **Cart Id**, **Selected Tax Identifier**, and **Selected Tax Identifier**. \
   ![](<../.gitbook/assets/Add custom components to checkout summary 2.png>)&#x20;
   * **API Name**: (Tax\_Identifier or any name)
   * **Cart Id**: ({!cartId})
   * **Selected Tax Identifier**: ({!Saved\_Tax\_Identifier})
   * **Selected Tax Identifier in the Advanced section**: ({!Saved\_Tax\_Identifier})
5. Add the `drB2B_DrTermsElement` and enter the **API Name** and **Cart Id**. \
   ![](<../.gitbook/assets/Add custom components to checkout summary 3.png>)&#x20;
   * **API Name**: `DR_Terms` or any name
   * **Cart Id**: ({!cartId})
6. Click **Done**.
7. Click **Save As**. \
   ![](<../.gitbook/assets/Add custom components to checkout summary 4.png>)&#x20;
8. Enter the custom subflow name (for example, DR Checkout Summary) and click **Save**. \
   ![](<../.gitbook/assets/Add custom components to checkout summary 5.png>)&#x20;
9. Click **Activate**. \
   ![](<../.gitbook/assets/Add custom components to checkout summary 6.png>)&#x20;

### Configure the payment subflow

This subflow must be customized to add **My Wallet** and **Digital River Payment Details** support. To configure the payment subflow:

1. Go to **Setup** and search **flows** in the **Search** field. \
   ![](<../.gitbook/assets/Payment subflow 1.png>)&#x20;
2. Click **Subflow - Payment and Billing Address**. \
   ![](<../.gitbook/assets/Payment subflow 2.png>)&#x20;
3. Click the **Manager** tab, then click **New Resource**. \
   ![](<../.gitbook/assets/Payment subflow 3.png>)&#x20;
4. Complete the following fields:
   * **Resource Type**: Variable
   * **API Name**: Payment\_Details (or other name as desired)
   * **Data Type**: Text\
     ![](<../.gitbook/assets/Payment subflow 4.png>)&#x20;
5. Click **Done**.

#### Add custom components to a screen

To add custom components to a screen:

1. Drag the screen element showing on the left panel to create a new screen and name the new screen (for example, **placeOrderConfirmation**).\
   &#x20;![](<../.gitbook/assets/New screen 1.png>)&#x20;
2. Click the custom screen **placeOrderConfirmation**.  \
   **Note**: See [Link screen components](step-15-integrate-the-digital-river-components-into-the-checkout-flow.md) for instructions on linking the screen. \
   ![](<../.gitbook/assets/New screen 2.png>)&#x20;
3. Drag **Display Text** from the left panel to screen and enter the **API Name** (for example, **Payment\_Information**) and insert **Resource Payment\_Details**. This is the variable resource created in the previous section.\
   ![](<../.gitbook/assets/New screen 3.png>)&#x20;
4. Drag  the `drb2b_OrderSummary` component from the left panel and enter the **API Name**, **Record Id**, **Show Duty**,  **Show IOR tax**, **Show Regulatory Fee**, **Show Shipping**, and **Show Tax**. \
   ![](<../.gitbook/assets/New screen 4.png>)&#x20;
   * **API Name**: OrderSummary or any name&#x20;
   * **Record Id**: ({!cartId})
   * **Show Duty**: **** ({!$GlobalConstant.True})
   * **Show IOR Tax**: ({!$GlobalConstant.True})
   * **Show Regulatory Fee**: ({!$GlobalConstant.True})
   * **Show Shipping**: ({!$GlobalConstant.True})
   * **Show Tax**: ({!$GlobalConstant.True})
5. Drag the `drb2b_DRUtil` component from the left panel and enter the **API Name** (`drb2b_Util` or other desired name).\
   ![](<../.gitbook/assets/New screen 5.png>)&#x20;
6. Click **Done**.

#### Edit the paymentMethodScreen screen

To edit the **paymentMethodScreen** screen:

1. Click the **paymentMethodScreen** screen.
2. Delete the OOTB components and add the `drb2b_Payments` component. \
   ![](<../.gitbook/assets/Edit payment method screen 1.png>)&#x20;
3. Enter the **API Name**, **Record Id**, **Payment Detail**, **Payment Type**, **Payment Detail**, and **Payment Type** that is under the **Advanced** section, which will be visible by selecting the **Manually assign variables** check box. \
   ![](<../.gitbook/assets/Edit payment method screen 2.png>)&#x20;
   * **API Name**: (DR\_Payments or any other name with no restriction)
   * **Record Id**: ({!cartId})
   * **Payment Detail**: ({!Payment\_Detail})
   * **Payment Type**: ({!paymentType})
4. Click **Done**.

#### Edit decision boxes

To edit decision boxes:

1. Click the **Decision** box (which payment type is selected). \
   ![](<../.gitbook/assets/Decision box 1.png>)&#x20;
2. Add the new **Outcome** and enter the **Label**, **Outcome API Name**, and **Condition Requirements to Execute Outcome** (for example, **Resource** `paymentType` equals `DigitalRiver`). \
   ![](<../.gitbook/assets/Decision box 2.png>)&#x20;
3. Click **Done**, then click the **Update address if changed** decision box. \
   ![](<../.gitbook/assets/Decision box 3.png>)&#x20;
4. Add the new **Outcome** and enter the **Label**, **Outcome API Name**, and **Condition Requirements to Execute Outcome** (for example, **Resource** `paymentType` equals `DigitalRiver`).\
   &#x20;![](<../.gitbook/assets/Decision box 4.png>)&#x20;
5. Click **Done**.

#### Link screen components

{% hint style="info" %}
To delete the existing link, click the link and press the **Delete** button on your keyboard.&#x20;
{% endhint %}

1. Link **PaymentMethodScreen** to the **placeOrderConfirmation** screen (custom screen).
2. Link **placeOrderConfirmation** (custom screen) to subflow (Validate Checkout State).
3. Link **Decision** box (which payment type is selected) element to **Assignment** (Assign PO to null) element when the paymentType is Digital River.
4. Link from **Decision** box (Update Address if changed) to Subflow (Set State).\
   &#x20;![](<../.gitbook/assets/Link screen component 1.png>)&#x20;
5. Click **Save** **As** and enter a name for the custom subflow (for example, DR payments). \
   ![](<../.gitbook/assets/Link screen component 2.png>)&#x20;
6. Click **Activate**. \
   ![](<../.gitbook/assets/Link screen component 3.png>)&#x20;

## Configure main checkout flow

To configure the main checkout flow:

1. Click the **Checkout Flow Template** (OOTB flow). ****&#x20;
2.  Create the subflow element for all the custom subflows (for example, DR Shipping Address, DR Payment, DR Checkout Summary, DR Shipping Address, and DR Delivery Method) which were created in the above steps.

    * Drag the subflow from the left panel and enter the **Referenced Flow**, **Label**, **cardID**, **currentState**, **** and **nextState**. \
      ![](<../.gitbook/assets/New subflow.png>)&#x20;
    * Repeat the same steps for all custom subflows.

    | Subflow             | Cart Id   | Current state                | Next state     | Order Id                                  |
    | ------------------- | --------- | ---------------------------- | -------------- | ----------------------------------------- |
    | DR Shipping Address | {!cartId} | {!mainCheckoutSession.State} | Inventory      | NA                                        |
    | DR Delivery Method  | {!cartId} | {!mainCheckoutSession.State} | Taxes          | NA                                        |
    | DR Checkout Summary | {!cartId} | {!mainCheckoutSession.State} | Cart To Order  | NA                                        |
    | DR Payment          | {!cartId} | {!mainCheckoutSession.State} | Activate Order | <p>{!mainCheckout<br>Session.OrderId}</p> |
3. Replace the OOTB flows with custom flows. &#x20;
   * **Shipping Address**: DR Shipping Address
   * **Delivery Method**: DR Delivery Method
   * **CheckoutSummary**: DR Checkout Summary
   * **Payment and Billing Address**: DR Payment \
     ![](<../.gitbook/assets/Replace OOTB flow with custom flow.png>)&#x20;
4. Click **Save As** and enter a name for the main checkout flow. \
   ![](<../.gitbook/assets/Name for main checkout flow.png>)&#x20;
5. Click **Save**, then click **Activate**.

## Add custom components to pages

Salesforce Lightning components can be quickly and easily added to a record page to have an immediate view of information.

To use the custom Lightning component in your pages, you must assign your component to a theme layout in the Experience Builder.

After completion, drag and drop a custom component onto a particular page based on the business requirements.

### List of custom components

The custom components listed here are either available in the Experience Builder or used in various flows.

If an optional custom component is NOT dropped onto relevant standard Salesforce UI pages, the downside is that custom fields (for example, Digital River custom fields) will not be visible on those UI pages.

Additionally, a given custom component can be dropped on one or more UI pages based on what the custom component does (for example, the Compliance footer custom component can be placed on multiple pages that require compliance footers).

The custom components listed in this section are provided as part of the app installation. However, they must be placed on the page(s) within the flows and subflows as described in the table below.&#x20;

Some of the custom components are used on pages such as **Tax Certificates**, **Tax Identifiers**, **My Wallet**, and **Stored Payments**. Separate tabs are available for these pages. You can directly drag and drop the following custom components onto a particular page based on the user’s needs.

| Custom Component                      | Page/Flow                                                                                                                                               | Description                                                                                                                                                                                                                                                                                                                                                                |
| ------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| B2B Sample Cart Contents              | Checkout Page                                                                                                                                           | <p>This component is used to display cart item details such as item name, SKU, price per unit. and total price. </p><p></p><p>This component is configured in the Experience Builder.</p>                                                                                                                                                                                  |
| dRB2B\_AddressDetails                 | Checkout Page                                                                                                                                           | <p>This component is used to display address details such as Bill To and Ship To. <br><br></p><p></p><p>This component is configured in the Experience Builder.</p>                                                                                                                                                                                                     |
| dRB2B\_DrCompliance                   | <p>All Checkout Pages</p><ul><li>Checkout</li><li>Order Confirmation</li><li>My Wallet</li><li>My Tax Certificates</li><li>My Tax Identifiers</li></ul> | <p>This component is used to show the DR compliance link.<br><br></p><p></p><p>This component is configured in the Experience Builder.</p>                                                                                                                                                                                                                              |
| dRB2B\_DrTermsElement                 | <p>Sub Flow<br>DR Checkout Summary</p>                                                                                                                  | <p>The checkbox in this component is used for the active acceptance of terms and conditions by the user.</p><p></p><p></p><p></p><p>This component is configured in the flow.</p>                                                                                                                                                                                       |
| dRB2B\_MyWallet                       | My Wallet                                                                                                                                               | <p>This component is used for showing and adding new payment sources in the wallet. </p><p></p><p><code>dRB2B_MyWallet</code> is a wrapper component. </p><p></p><p>Its constituent components are <code>drb2b_StoredPayments</code> and <code>drb2bNewPayments</code></p><p></p><p>This component is configured in the Experience Builder.</p>                        |
| drb2b\_PaymentDetails                 | <p>Order Summary Detail,</p><p>Order Confirmation</p>                                                                                                   | This component is used to show payment details and is configured in the Experience Builder.                                                                                                                                                                                                                                                                                |
| dRB2B\_VatCreditMemo                  | Order Summary Detail                                                                                                                                    | <p>This component is used to show invoices and credit memos to the user and should be dropped on the Order Summary Detail page two times: one refers to the invoice and the other refers to the credit memo (type = Invoices or type = Credit Memos). </p><p></p><p>This component is configured in the Experience Builder.</p>                                           |
| drb2b\_ProductDetail                  | Order Confirmation                                                                                                                                      | <p>This component is used to show product details. </p><p></p><p></p><p>This component is configured in Experience Builder.</p>                                                                                                                                                                                                                                         |
| drb2b\_BuyerInfo                      | Sub Flow-DR Shipping Address                                                                                                                            | <p>This component is used to display user information such as Name, Email, Bill to and Ship to, etc. </p><p></p><p></p><p></p><p><code>drb2b_Buyer Info</code> is a wrapper component. </p><p></p><p>Its constituent component is <code>drb2bUsersTaxCertificates</code>.<br></p><p></p><p></p><p>This component is configured in the flow.</p>                     |
| DRB2B User Tax Certificates           | My Tax Certificates                                                                                                                                     | <p>This component is used to upload tax certificates. </p><p></p><p>DRB2B User Tax Certificates is a wrapper component.<br>  <br></p><p></p><p>Its constituent component is <code>drb2bAddTaxCertificate</code>.<br><br></p><p></p><p>This component is configured in the Experience Builder.</p>                                                                   |
| drb2b\_OrderSummary                   | Order Confirmation                                                                                                                                      | <p>This component is used to display Sub Total, Shipping, Tax, and Grand Total, etc. </p><p></p><p><br><code>drb2b_OrderSummary</code> is a wrapper component. </p><p></p><p>Its constituent component is <code>drb2b_CheckoutSummary</code>.<br><br></p><p></p><p>This component is configured in the Experience Builder and in the flow.</p>                      |
| drb2b\_CheckoutSummary                | Checkout Page                                                                                                                                           | <p>This component is used to display Sub Total, Shipping, Tax, and Grand Total, IOR Tax Regulatory Fee, and so on. </p><p></p><p></p><p>This component is configured in the Experience Builder.</p>                                                                                                                                                                     |
| drb2b\_DRUtil                         | Sub Flow-DR Checkout Summary and Delivery Method subflow                                                                                                | <p>This component tells the Order Summary to get taxes and the subtotal from the cart.</p><p></p><p></p><p>This component is configured in the flow.</p>                                                                                                                                                                                                                 |
| drb2b\_taxIdentifier                  | Sub Flow-DR Checkout Summary                                                                                                                            | <p>This component is used to add a tax identifier in the checkout flow. <br><br></p><p></p><p><code>drb2b_taxIdentifier</code> is a wrapper component</p><p></p><p>Its constituent component is <code>drb2b_MyTaxIdentifier</code>.<br><br></p><p></p><p>This component is configured in the checkout flow.</p>                                                    |
| drb2b\_MyTaxIdentifier                | My Tax Identifiers                                                                                                                                      | <p>This component is used for Tax Identifier functionality. </p><p></p><p></p><p></p><p><code>drb2b_MyTaxIdentifier</code>is a wrapper component.</p><p></p><p><br>Its constituent component is <code>drb2b_CountryPicklist.</code> </p><p></p><p>This component is configured in the Experience Builder.</p>                                                         |
| <p>drb2b_Payments</p><p></p><p></p> | Sub Flow-DR Payments                                                                                                                                    | <p>This component is used for payment sources (for example, Drop-in and Stored Payments).<br><br></p><p></p><p><code>drb2b_Payments</code> is a wrapper component.<br><br></p><p></p><p>Its constituent components are <code>drb2b_Dropin</code> and </p><p><code>drb2b_MyWalletpayment</code>. </p><p></p><p></p><p>This component is configured in the flow.</p> |
| drb2b\_HideCheckoutSummary            | As required                                                                                                                                             | <p>This component is added inside the screens of the flow and allows the client to conditionally show and hide the drb2b_CheckoutSummary component.<br><br>This component is configured in the flow.</p>                                                                                                                                                                   |

The screenshots below show a mocked-up version of each of the pages mentioned in the table above. The screenshots demonstrate the components that are recommended to be added to each page in the Experience Builder.

#### Checkout&#x20;

![](<../.gitbook/assets/Checkout flow\_installation.png>)

#### Order confirmation &#x20;

![](<../.gitbook/assets/Order confirmation\_1.png>)

#### Order summary detail&#x20;

![](<../.gitbook/assets/Order summary detail\_installation.png>)

#### My Wallet (custom page)

![](<../.gitbook/assets/My Wallet\_custom page.png>)

#### My Tax Certificates (custom page)

![](<../.gitbook/assets/My Tax Certificates\_custom page.png>)

#### My Tax Identifiers (custom page)&#x20;

![](<../.gitbook/assets/My Tax Identifiers\_custom page.png>)

## Drag and drop (custom) components &#x20;

After the custom component is added into the Experience Builder, drag and drop the custom component on the page.

### Custom pages and menu items

The app provides custom components for three custom pages: My Wallet, My Tax Certificates, and My Tax Identifiers. It is recommended that you create these custom pages as required.

To customize a page:

1. Go to **Setup** in the Experience Builder.
2. Search **All Sites** in the **Search** field. &#x20;
3. Click **Builder**.&#x20;
4. Click **Home** at the top left corner. \
   ![](<../.gitbook/assets/Customize a page\_Home.png>)&#x20;
5. Scroll down at the bottom and the **+New Page** option will be available to create the custom page. Once the page has been created, it will appear in the **Pages** section. \
   ![](<../.gitbook/assets/Pages section.png>) \
   The page will also appear on the **Menu Item**.\
   &#x20;![](<../.gitbook/assets/Menu item.png>)&#x20;

{% hint style="info" %}
If you want to add any page for the **Menu Item**, select the particular page from the page picklist under the **Menu Item**.
{% endhint %}

### Create a custom menu

To add a menu:

1. Go to **Setup**.
2. Search **All Sites** in the **Search** field.&#x20;
3. Click **Builder**.
4. Click the user profile dropdown at the top right.\
   &#x20;![](<../.gitbook/assets/Custom menu 1.png>)&#x20;
5. Click **Authenticated User Options**. \
   ![](<../.gitbook/assets/Custom menu 2.png>)&#x20;
6. Click the **Edit Default User** profile menu. \
   ![](<../.gitbook/assets/Custom menu 3.png>)&#x20;
7. Click **+Add Menu item**.\
   &#x20;![](<../.gitbook/assets/Custom menu 4 (2).png>)&#x20;
8. Select **Site Page** as the **Type**. The **Name** field will appear.&#x20;
   * Enter the desired name for the **Menu Item**.
   * Select the desired custom page as the **Page**.\
     ![](<../.gitbook/assets/Site Page\_type (2).png>)&#x20;
9. Click **Save Menu**.
10. Click **Publish**.

### Add a custom component to a page

To add a custom component to a page:

1. Go to **Setup**.&#x20;
2. Search **All Sites** in the **Search** field.&#x20;
3. Click **Builder**.
4. Click **Home** at the top left corner and select the desired page. The custom components will appear at the bottom of the dropdown.
5. Drag and drop the custom component on the page.
6. Click **Publish**.

### Add a custom component to a custom page

To add a custom component to a custom page:

1. Go to **Setup**.&#x20;
2. Search **All Sites** in the **Search** field.&#x20;
3. Click **Builder**.
4. Click **Home** at the top left corner.
5. Type the name for the custom page in the **Search** field.
6. Click the selected page.
7. Click the lightning icon on the upper left side to add the custom component. The custom component will appear at the bottom of the dropdown.&#x20;
8. Drag and drop the custom component on the custom page.
9. Click **Publish**.
10. Repeat the above steps for other custom components you want to add to various pages.

{% hint style="info" %}
This custom component can be placed on other UI pages.&#x20;
{% endhint %}

### Add Tax Certificates component on the My Account page

As an example of how to add a custom component to a page, here are the steps to place the Tax Certificates component on the **My Account** page.

To add a tax certificate component on the **My Account** page:

1. Go to **Setup**.
2. Search **All Sites** in the **Search** field.&#x20;
3. Click **Builder**.
4.  Click **Home** at the top left corner.

    ![](<../.gitbook/assets/My Account page 1.png>)&#x20;
5. Type **My Account** in the **Search** field. \
   ![](<../.gitbook/assets/My Account page 2.png>)&#x20;
6. Click the selected page and click the lightning icon to add the custom component. The custom component will appear at the bottom of the dropdown. \
   ![](<../.gitbook/assets/My Account page 3.png>)&#x20;
7. Drag and drop the custom component on the **My Account** page. \
   ![](<../.gitbook/assets/My Account page 4.png>)&#x20;
8. Click **Publish**.\
   &#x20;&#x20;

