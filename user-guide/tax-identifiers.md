---
description: Learn how to add and delete tax identifiers.
---

# Tax identifiers

Use the Salesforce Lightning app to add or delete tax identifiers. Tax identifiers can be added from the My Account page or during checkout on the Order Review screen.

## Using tax identifiers on the My Account page <a href="#using-tax-identifiers-on-the-my-account-page" id="using-tax-identifiers-on-the-my-account-page"></a>

The My Account page has options to either add a new tax identifier or delete existing tax identifiers. Tax identifiers can be added from either the My Account page or during checkout on the Order Review screen.

### Add the tax identifier <a href="#add-the-tax-identifier" id="add-the-tax-identifier"></a>

To add a tax identifier:

1. Sign in to the store.
2. Click **My Profile**.
3.  Click **New Tax identifier**.

    ![](https://files.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-MS-2crEBZIcuq\_A3pl1%2F-MbMjbiEWxAyUl3uj36R%2F-MbMkGSIJK7PAYgSe0SB%2FTax%20identifier%20tab.PNG?alt=media\&token=3a092cd8-3f0d-4d87-96af-b6655fd41d53)
4.  Choose a **Country** from the dropdown menu. If a tax identifier is applicable for that country, a text field will appear. Enter the value of the tax identifier into the field.

    ![](https://files.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-MS-2crEBZIcuq\_A3pl1%2F-MbMkL7Tyqr46VYAktuZ%2F-MbMkeWDjyescSOAZC97%2FNew%20tax%20identifier.PNG?alt=media\&token=0383b69a-af5d-4d89-8d96-e042c9874349)
5. Click Save. A message about the added tax identifier appears.![](https://files.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-MS-2crEBZIcuq\_A3pl1%2F-MbMkL7Tyqr46VYAktuZ%2F-MbMlCoyWsm8Fpy31Fpc%2FTax%20identifier%20saved%20successfully.PNG?alt=media\&token=9513871d-cf03-454f-b8b7-f194c58ae200)

{% hint style="info" %}
A single tax identifier of each type is permitted. If a tax identifier already exists, the following message appears:

![](https://files.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-MS-2crEBZIcuq\_A3pl1%2F-MbMlG2Ggei4RMh9gMy9%2F-MbMlMQpv3cjED3SqMTk%2FTax%20identifier%20already%20exists.PNG?alt=media\&token=ab48d1a8-c3e8-4de7-8c04-ff53db17821a)
{% endhint %}

## Delete the tax identifier <a href="#delete-the-tax-identifier" id="delete-the-tax-identifier"></a>

To delete a tax identifier:

1. Click **Delete** next to the tax identifier you want to remove.
2. Click **Confirm**.

![](https://files.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-MS-2crEBZIcuq\_A3pl1%2F-M\_N6GcqiKYiNjreHKpr%2F-M\_N7sQ5FoprDS0EbA4I%2FDelete%20tax%20identifier%203.PNG?alt=media\&token=53da85c0-14e1-4ffa-a9a9-656c5fe18b55)

## Using tax identifiers within checkout <a href="#using-tax-identifiers-within-checkout" id="using-tax-identifiers-within-checkout"></a>

You can save new tax identifiers, delete existing tax identifiers, or apply saved tax identifiers on the order review page as part of the checkout process.

To use tax identifiers during checkout:

1. Sign in to the store.
2.  Add the items to the cart and proceed through the checkout flow until you get to the **Order Review** page.

    ![](https://files.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-MS-2crEBZIcuq\_A3pl1%2F-MfYo-fkCnoG0Ayu95Gn%2F-MfYpDB7gMRbczEnluIS%2FTax%20identifier%20options.png?alt=media\&token=edc6b630-1268-4894-b304-ef7b73475ec7)

    The Tax identifier section will only appear when you are buying:|

    * **Physical** products and the **shipping address** is a non-US address
    * **Digital** products **** and the billing address is a non-US address
    * **Mixed** products (**physical and digital**) and the **shipping address** is a non-US address
3.  On the **Order Review** page, the shopper can select the existing tax identifier from the **Saved Tax Identifiers** section or can apply the tax identifier from the **Other tax identifiers** section.![](https://files.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-MS-2crEBZIcuq\_A3pl1%2F-MfiGSWLZdkisHt3iO5h%2F-MfiLRBBG6SeHreqjqZ7%2FTax%20identifier%20on%20order%20review%20page.png?alt=media\&token=8145c64e-a7b1-459a-b712-87b0b88ce9fb)

    **Note**: Steps for adding or deleting existing tax identifiers are the same as those on the My Account page.
4. Click **Apply Tax Identifier**. The page will refresh the amount and the tax identifier ID will be stamped in the **DR Tax Identifiers** field of the Cart object.
5. Click **Next** to navigate to the **Payment** page.

## Global tax identifier sequence diagram <a href="#global-tax-identifier-sequence-diagram" id="global-tax-identifier-sequence-diagram"></a>

{% file src="../.gitbook/assets/DR_TaxIdentifier_Flow_v3_1.0.png" %}
