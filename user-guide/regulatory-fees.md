---
description: Learn more about regulatory fees.
---

# Regulatory fees

[Regulatory fee](https://docs.digitalriver.com/digital-river-api/regulatory-fees) creation and management are outside the scope of the Salesforce Lightning app. Work with your Digital River project manager on the management of regulatory fees.&#x20;

Once the fees are configured, the app will display any applicable fees to the shopper in the checkout flow.

![](<../.gitbook/assets/Regulatory fee 1.png>)

The total of the fees is added to the **Cart** and **Order** and stored in the **DR Total Regulatory Fee** field.

![](<../.gitbook/assets/Regulatory fee 2.png>)

Additionally, any fees will be stored in the `CartItem` and `OrderItem` objects in the **DR Regulatory Fee**, which stores the sum of the regulatory fees for that line item.

![](<../.gitbook/assets/Regulatory fee 3.png>)

The breakdown of each fee is stored in the **Digital River Regulatory Fee** object, which is linked to the **Cart Item**.

![](<../.gitbook/assets/Regulatory fee 4.png>)
