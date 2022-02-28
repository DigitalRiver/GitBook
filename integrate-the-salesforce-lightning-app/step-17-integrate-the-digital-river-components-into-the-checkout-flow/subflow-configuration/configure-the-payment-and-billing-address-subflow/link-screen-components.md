---
description: Learn how to link screen components on a subflow.
---

# Link screen components

{% hint style="info" %}
To delete an existing link, click the link line between two elements and press the **Delete** key on your keyboard.
{% endhint %}

1. Click the circle below the **paymentMethodScreen** and drag it to the **placeOrderConfirmation** screen.\
   ![](<../../../../.gitbook/assets/paymentMethodScreen to Validate Checkout State.png>)
2. Click the circle below **placeOrderConfirmation** custom screen) and drag it to the **Validate Checkout State** subflow.\
   ![](<../../../../.gitbook/assets/placeOrdersConfirmation to Validate Checkout State.png>)
3. Click the circle below the **Which payment type is selected** decision element and drag it to the **Assign PO to null** when the payment type is Digital River.\
   ![](<../../../../.gitbook/assets/Which payment type to Assign PO to null.png>)
4. Click the circle below the **Update Address if change**d decision element and drag it to the Set **State** subflow.\
   ![](<../../../../.gitbook/assets/Update address if changed to Set States.png>)
5. Click **Save as** and enter a name for the custom subflow (for example, `DR payments`).
6. Click **Activate**.
