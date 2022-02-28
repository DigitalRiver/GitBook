---
description: Learn how to add and delete tax identifiers.
---

# Tax identifiers

Use the Salesforce Lightning app to add or delete tax identifiers. Tax identifiers can be added from the **My Account** page or during checkout on the **Order Review** screen.

## Using tax identifiers on the My Account page

{% hint style="info" %}
The **My Account** page has options to either add a new tax identifier or delete existing tax identifiers. Tax identifiers can be added from either the **My Account** page or during checkout on the **Order Review** screen.
{% endhint %}

### Add the tax identifier

To add a tax identifier:

1. Log in to the store.
2. Click **My Profile**.
3. Click **New Tax identifier**. \
   ![](<../.gitbook/assets/Tax identifier tab (2).PNG>) &#x20;
4. Click **New Tax Identifier**.
5. Choose a **Country** from the dropdown menu. If a tax identifier is applicable for that country, a text field will appear. Enter the value of the tax identifier into the field.\
   &#x20;![](<../.gitbook/assets/New tax identifier (2).PNG>)&#x20;
6. Click **Save**. A message about the added tax identifier appears.\
   ![](<../.gitbook/assets/Tax identifier saved successfully (3).PNG>)&#x20;

{% hint style="info" %}
A single tax identifier of each type is permitted. If a tax identifier already exists, the following message appears: ![](<../.gitbook/assets/Tax identifier already exists (1).PNG>)&#x20;
{% endhint %}

## Delete the tax identifier

To delete a tax identifier:

1. Click **Delete** for the tax identifier you wish to remove.
2. Click **Confirm.** \
   ****![](<../.gitbook/assets/Delete tax identifier 2 (1).PNG>) \
   ![](<../.gitbook/assets/Delete tax identifier 3 (1).PNG>)&#x20;

## Using tax identifiers within checkout

You can save new tax identifiers, delete existing tax identifiers, or apply saved tax identifiers on the order review page as part of the checkout process. &#x20;

To use tax identifiers during checkout:

1. Log in to the store.&#x20;
2. Add item(s) to the cart and proceed through the checkout flow until you get to the **Order Review** page.\
   &#x20;![](<../.gitbook/assets/Tax identifier options (2).png>) \
   The Tax identifier section will only appear when you are buying:
   * **Physical** products and the **shipping address** is a non-US address
   * **Digital** products **** and the billing address is a non-US address
   * **Mixed** products (**physical and digital**) and the **shipping address** is a non-US address
3. On the **Order Review** page, the shopper can select the existing tax identifier from the **Saved Tax Identifiers** section or can apply the tax identifier from the **Other tax identifiers** section. \
   ![](<../.gitbook/assets/Tax identifier on order review page.png>) \
   **Note**: Steps for adding or deleting existing tax identifiers are the same as those on the **My Account** page.
4. Click **Apply Tax Identifier**. The page will refresh the amount and the tax identifier ID will be stamped in the **DR Tax Identifiers** field of the `Cart` object.&#x20;
5. Click **Next** to navigate to the **Payment** page.

## Global tax identifier sequence diagram

{% file src="../.gitbook/assets/DR_TaxIdentifier_Flow_v3_1.0 (3).png" %}
Global tax identifier flow
{% endfile %}
