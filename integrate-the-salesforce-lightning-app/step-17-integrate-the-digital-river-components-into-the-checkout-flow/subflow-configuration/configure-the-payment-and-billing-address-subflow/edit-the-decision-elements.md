---
description: Learn how to edit the decision elements
---

# Edit the decision elements

To edit decision boxes:

1. Double-click the **Which payment type is selected** decision element. \
   ![](<../../../../.gitbook/assets/Which payment type is selected decision element.png>)&#x20;
2. From the Edit Decision dialog, click **+** next to **Outcome Order** to add a new outcome.\
   ![](<../../../../.gitbook/assets/Outcome order.png>)
3. From the **New Outcome** tab, enter the following values in the fields:
   * **Label**:  Type `Digital River`.
   * **Outcome API Name**: The field automatically populates the **Digital\_River** value.
   * **Resource**: Type `paymentType` and click the **paymentType** variable.
   * **Value**: Type `DigitalRiver`.\
     ![](<../../../../.gitbook/assets/Which payment type is selected edit decision.png>)
4. Click **Done**.
5. Double-click the **Update address if changed** decision element. \
   ![](<../../../../.gitbook/assets/Update address if changed decision element.png>)&#x20;
6. From the **Edit Decision** dialog, click **+** next to **Outcome Order** to add a new outcome.\
   ![](<../../../../.gitbook/assets/Outcome order - Update address if changed.png>)
7. From the **New Outcome** tab, enter the following values in the fields:
   * **Label**:  Type `Payment Equal DR`.
   * **Outcome API Name**: The field automatically populates the **Payment\_Equal\_DR** value.
   * **Resource**: Type `paymentType` and click the **paymentType** variable.
   * **Operator**: Select **Equals** from the dropdown list.
   * **Value**: Type `DigitalRiver`.\
     &#x20;![](<../../../../.gitbook/assets/Edit Decision - update address if changed.png>)
8. Click **Done**.
