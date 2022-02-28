---
description: Understand how customers upload tax certificates.
---

# Uploading tax certificates (US TEMS)

The Digital River Salesforce B2B Commerce App supports tax-exempt purchases on US storefronts. Authenticated customers will be able to add or upload one or more tax certificates to their profile from the User Info page and My Account page. The following list shows Digital River's Tax Certificate Validation once a shopper uploads a tax certificate.

1. Validation of the tax certificate is a manual process done by Digital River employees. It is not a real-time determination.
2. Pending that validation, the customer can place their order and that order will be treated as if there was a valid certificate (that is, tax-free).
3. If the shopper’s certificate fails validation, when that shopper places another order, their order will not be tax-free.

## Upload a tax certificate from the My account page <a href="#upload-a-tax-certificate-from-the-my-account-page" id="upload-a-tax-certificate-from-the-my-account-page"></a>

To upload a tax certificate from the My Account page:

1. Sign in to the storefront.
2. Go to **My Account**.
3. Click the **My Tax Certificates** link in the **My Account Navigation Bar** to open a window listing the customer’s uploaded tax certificates. \
   ![](<../.gitbook/assets/Install DR B2B API Connector95.png>)
4. Click **Manage Tax Exemption** and complete the details on the form (such as Company Name, Tax Authority, Start Date, Expiry Date, and the actual Tax Certificate file).\
   ![](<../.gitbook/assets/Install DR B2B API Connector96.png>)
5. Click **Submit** to upload the tax certificate to Digital River. \
   ![](<../.gitbook/assets/Install DR B2B API Connector97.png>) \
   After you successfully submit the tax certificate to Digital River, the page refreshes and the newly uploaded tax certificate will appear on the Existing Tax Certificates page. \
   ![](<../.gitbook/assets/Install DR B2B API Connector98.png>)
6. Click the close button (**X**) to close this window and return to the My Account page.\
   ![](<../.gitbook/assets/Install DR B2B API Connector99.png>) \
   If there is an issue while uploading the tax certificate, a generic error message will appear on the screen and the error information will be logged to the custom DCM Application Log object.

## Upload a tax certificate from the Order Review page <a href="#upload-a-tax-certificate-from-the-user-information-page" id="upload-a-tax-certificate-from-the-user-information-page"></a>

To upload a tax certificate from the Order Review page:

1. Sign in to the storefront.
2. Add products to your cart and click `Checkout`. The User Information page appears.
3. Click `Continue` to open the Shipping page.
4. On the Shipping page, click `Accept Terms and Proceed` to open the Order Review page.
5. The purchase type will be set to `individual` by default and the shopper can change it to business by clicking `Change to Business` . This information is stamped on the **DR Customer Type** field on the CC Cart object.\
   ![](../.gitbook/assets/order\_review2.png)
6. To make a tax-exempt purchase, click `Business` as the Purchase Type. The **Click here to Manage your Tax Certificates** link appears.\
   &#x20;![](../.gitbook/assets/tax\_certificate\_link2.png)&#x20;
7. Click the link. A window appears and lists previously uploaded tax certificates.
8. Repeat steps 4–6 under [**Upload a Tax Certificate from the My Account page**](uploading-tax-certificates-us-tems.md#upload-a-tax-certificate-from-the-my-account-page) to upload a new certificate from the User Info page.

**Notes**

* To make a tax-exempt purchase, you must select **Business** for Purchase Type on the Order Review page.
* Tax certificate files are not stored in Salesforce.
* Tax certificate information like the File Name, Digital River Tax Certificate File Id, Company Name, Tax Authority, Start Date, Expiry Date, Contact Id, and Account Id of the User who uploaded the tax certificate are captured in a custom object **DR US Tax Certificate (digitalriverv2\_\_DR\_US\_Tax\_Certificate\_\_c)** in Salesforce.&#x20;

![](<../.gitbook/assets/Install DR B2B API Connector101.png>)

## Sequence diagram

The following sequence diagram explains the Tax Exemption Subprocess flow supported by the connector.

{% file src="../.gitbook/assets/sfb2b_taxexemptflow-2.1.1B.png" %}

