---
description: Learn how to edit the Payment Method screen.
---

# Edit the Payment Method screen

To edit the Payment Method screen:

1. Double-click the **paymentMethodScreen** screen.
2. Delete all OOTB components from the subflow.
3. Type `drb2b_payments` in the **Search components** field and click **drb2b\_payments**.![](<../../../../.gitbook/assets/Search components drb2b\_drUtil (1).png>)
4.  Enter the following values in the fields:

    * **API Name**: Type `drPayments` or any other name with no restrictions.
    * **Dropin Config**: Provide data for this designer attribute in JSON format. For example:\
      `{"options.button.type": custom, "options.button.buttonText": 'test', "test": "test3"}`
    * **Record Id**: Type `{!cartId}`.

    See [Designer attributes](../../../../extend-the-salesforce-lightning-app/customizing-the-lightning-web-components/designer-attributes.md) for additional information.
5. Click **Done**.
