---
description: Learn how to enable or disable US tax certificates.
---

# Enable or disable US tax certificates

In the Salesforce Lightning app, you can enable or disable US tax certificates.&#x20;

1. To enable or disable US Tax Certificates on the **My Account** page, add or remove the **Tax Certificates** menu item.&#x20;
2. To enable or disable US Tax Certificates on the **Checkout process/flow**, adjust the **DR Shipping Address** for the `drb2b_BuyerInfo` component and configure it to include (or not include) US Tax Certificates as part of the flow.

## Main flow and subflow details

| Flow type | Description                                                                                                                                                                                         |
| --------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Main flow | DR checkout flow                                                                                                                                                                                    |
| Subflow   | <p>DR Shipping Address Custom component: <code>drb2b_BuyerInfo</code><br>Design variable: Enable Tax Certificates<br>Design variable values: {!$GlobalConstant.True} / {!$GlobalConstant.False}</p> |

## Enable tax certificates in the subflow

If the design variable's value is `!$GlobalConstant.True`, the tax certificates' functionality in the checkout flow will be enabled.

![](<../.gitbook/assets/Enable tax certificate in subflow.png>)

## Disable tax certificates in the subflow

If the design variable's value is `!$GlobalConstant.false`,  the tax certificates' functionality in the checkout flow will be disabled.

![](<../.gitbook/assets/Disable tax certificate in subflow.png>)

Once the design variable is configured, save and activate the checkout flow.
