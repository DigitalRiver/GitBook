---
description: Learn how to add custom components to pages
---

# Add custom components to pages

You can quickly and easily add Salesforce Lightning components to a record page and immediately view the information.

To use the custom Lightning component in your pages, you must assign your component to a theme layout in the Experience Builder.

After completion, drag and drop a custom component onto a particular page or flow based on the business requirements.

## List of custom components

The custom components listed here are either available in the Experience Builder or used in various flows.

If you do not drop an optional custom component onto the relevant Salesforce UI pages, the fields associated with that custom component (for example, Digital River custom fields) will not be visible on those UI pages.

Additionally, you can drop a given custom component on one or more UI pages based on what the custom component does. For example, you can place the Compliance footer custom component on multiple pages that require compliance footers.

We provide the custom components listed below as part of the app installation. However, you must place them on the pages within the flows and subflows as described in the table below.

You can use some of the custom components on pages such as **Tax Certificates**, **Tax Identifiers**, **My Wallet**, and **Stored Payments**. Separate tabs are available for these pages. You can directly drag and drop the following custom components onto a particular page based on your needs.

| Custom Component                      | Page/Flow                                                                       | Description                                                                                                                                                                                                                                                                                                                                                 |
| ------------------------------------- | ------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| drb2b\_cartContents                   | Checkout Page                                                                   | <p>Use this component to display cart item details such as item name, SKU, price per unit, total price, and so on. </p><p>You can configure this component in the Experience Builder.</p>                                                                                                                                                                   |
| drb2b\_addressDetails                 | Checkout Page or Subflow                                                        | <p>Use this component to display address details such as Bill To and Ship To. <br></p><p></p><p>You can configure this component in the Experience Builder or flow.</p>                                                                                                                                                                                  |
| drb2b\_drCompliance                   | All Checkout Pages                                                              | <p>Use this component to show the Digital River compliance links.<br></p><p></p><p>You can configure this component in the Experience Builder.</p>                                                                                                                                                                                                        |
| drb2b\_drTermsElement                 | Sub Flow-(For Example, Digital River Checkout Summary)                          | <p>Use the checkbox in this component for the active acceptance of terms and conditions by the user.</p><p></p><p></p><p>You can configure this component in the flow.</p>                                                                                                                                                                               |
| drb2b\_myWallet                       | My Wallet                                                                       | <p>Use this component to show and add new payment sources in the wallet. </p><p><code>dRB2B_MyWallet</code> is a wrapper component. </p><p></p><p>Its constituent components are <code>drb2b_StoredPayments</code> and <code>drb2bNewPayments</code>.</p><p>You can configure this component in the Experience Builder.</p>                             |
| drb2b\_paymentDetails                 | Pages: Order Summary Detail, Order Confirmation Subflow: Digital River Payments | <p>This component shows payment details. </p><p>You can configure this component in the sub flow.</p>                                                                                                                                                                                                                                                       |
| drb2b\_vatCreditMemo                  | Order Summary Detail                                                            | <p>Use this component to show invoices and credit memos to the user. It should appear on the Order Summary Detail page two times: one refers to the invoice and the other refers to the credit memo. </p><p>You can configure this component in the Experience Builder.</p>                                                                                |
| drb2b\_productDetail                  | Order Confirmation                                                              | <p>Use this component to show the product details. </p><p></p><p>You can configure this component in the Experience Builder.</p>                                                                                                                                                                                                                         |
| drb2b\_buyerInfo                      | Sub Flow-Digital River Shipping Address                                         | <p>Use this component to display user information such as Name, Email, Bill to and Ship to, and so on. </p><p></p><p></p><p><code>drb2b_Buyer Info</code> is a wrapper component. </p><p></p><p>Its constituent component is <code>drb2bUsersTaxCertificates</code>.</p><p></p><p></p><p>You can configure this component in the flow.</p>           |
| drb2b\_usersTaxCertificates           | User Tax Certificate                                                            | <p>Use this component to upload tax certificates. <br><code>drb2b_usersTaxCertificates</code> is a wrapper component.<br></p><p></p><p>Its constituent component is <code>drb2b_addTaxCertificate</code>.<br></p><p></p><p>You can configure this component in the Experience Builder.</p>                                                            |
| drb2b\_orderSummary                   | Order Confirmation and Digital River Payments Subflow                           | <p>Use this component to display Sub Total, Shipping, Tax, and Grand Total, and so on. <br><code>drb2b_orderSummary</code> is a wrapper component. </p><p></p><p>Its constituent component is <code>drb2b_checkoutSummary</code>.<br></p><p></p><p>You can configure this component in the Experience Builder or flow.</p>                            |
| drb2b\_checkoutSummary                | Checkout Page or subflow                                                        | <p>Use this component to display Sub Total, Shipping, Tax, and Grand Total, IOR Tax Regulatory Fee, and so on. </p><p></p><p>You can configure this component in the Experience Builder or flow.</p>                                                                                                                                                     |
| drb2b\_drUtil                         | Sub Flow-Digital River Checkout Summary and Delivery Method subflow             | <p>This component tells the Order Summary to get taxes and the subtotal from the cart.</p><p></p><p>You can configure this component in the flow.</p>                                                                                                                                                                                                     |
| drb2b\_taxIdentifier                  | Sub Flow-Digital River Checkout Summary                                         | <p>Use this component to add a tax identifier in the checkout flow. <br><br></p><p></p><p><code>drb2b_taxIdentifier</code> is a wrapper component</p><p></p><p>Its constituent component is <code>drb2b_myTaxIdentifier</code>.<br><br></p><p></p><p>You can configure this component in the flow.</p>                                              |
| drb2b\_myTaxIdentifier                | My Tax Identifier                                                               | <p>Use this component for the Tax Identifier functionality. </p><p></p><p></p><p><code>drb2b_myTaxIdentifier</code> is a wrapper component.<br>Its constituent component is <code>drb2b_CountryPicklist.</code> </p><p>You can configure this component in the Experience Builder.</p>                                                                  |
| <p>drb2b_payments</p><p></p><p></p> | Sub Flow-Digital River Payments                                                 | <p>Use this component for payment sources (for example, Drop-in and Stored Payments).<br></p><p></p><p><code>drb2b_payments</code> is a wrapper component.<br></p><p></p><p>Its constituent components are <code>drb2b_dropin</code> and </p><p><code>drb2b_myWalletPayment</code>. </p><p></p><p>You can configure this component in the flow.</p> |
| drb2b\_placeOrder (optional)          | Checkout Page                                                                   | <p>Use this component to add the Place Order button to the Checkout Page.<br>Use this component in conjunction with the <code>drb2b_orderSummary</code> component for the Place Order button to appear.<br>You can configure this component in the Experience Builder.</p>                                                                                  |
| drb2b\_taxCertificateCheckout         | Sub Flow-Digital River Shipping Address                                         | <p>Use this component t display the tax certificate and add the tax certificate.<br>You can configure this component in the flow.</p>                                                                                                                                                                                                                       |
| drb2b\_hideCheckoutSummary            | Sub flow - per business requirements                                            | <p>Use this component to hid the <code>drb2b_checkoutSummary</code> component. <br>You can configure this component in the flow.</p>                                                                                                                                                                                                                        |
| drb2b\_wireTransferInstructions       | Checkout Page                                                                   | <p>Use this component to display the Wire Transfer instructions.<br>You can configure this component in the flow.</p>                                                                                                                                                                                                                                       |

See [Customizing the Lightning web components](../../../extend-the-salesforce-lightning-app/customizing-the-lightning-web-components/) for additional information.

The following screenshots show a mocked-up version of each of the pages mentioned in the table above. The screenshots demonstrate the components that are recommended to be added to each page in the Experience Builder.

### Checkout&#x20;

![](<../../../.gitbook/assets/Checkout flow\_installation.png>)

### Order confirmation &#x20;

![](<../../../.gitbook/assets/Order confirmation\_1.png>)

### Order summary detail&#x20;

![](<../../../.gitbook/assets/Order summary detail\_installation.png>)

### My Wallet (custom page)

![](<../../../.gitbook/assets/My Wallet\_custom page.png>)

### My Tax Certificates (custom page)

![](<../../../.gitbook/assets/My Tax Certificates\_custom page.png>)

### My Tax Identifiers (custom page)&#x20;

![](<../../../.gitbook/assets/My Tax Identifiers\_custom page.png>)

##
