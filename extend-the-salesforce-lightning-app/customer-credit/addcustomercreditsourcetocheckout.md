---
description: Learn how to add a Customer Credit source to checkout.
---

# addCustomerCreditSourceToCheckout

Use this global method to create a customer credit payment source and attach it to checkout.

The [payment session](https://docs.digitalriver.com/digital-river-api/integration-options/checkouts/creating-checkouts#payment-session) identifier and [currency code](https://docs.digitalriver.com/digital-river-api/integration-options/checkouts/creating-checkouts/selecting-a-currency#how-currency-is-prioritized) will be derived from the cart if multicurrency is enabled in org. Otherwise, the currency code will be derived from the user’s default currency.

Before creating a payment source, use this method to verify that the `amount` specified by the shopper is less than or equal to the `amountRemainingToBeContributed`. If the amount passed into the method is greater than `amountRemainingToBeContributed`, it will throw an error.

This global method will set the `amountContributed` and `amountRemainingToBeContributed` values in the [`Cart` object](../../appendix/custom-fields-and-objects.md#cart-standard-object).

## Sending a request

This method accepts parameters in JSON string format and can be called outside the managed package. You need to pass the `cartId` and the `amount` applied to this method.

| Parameter     | Required/Optional | Determine                                                                                                                                                                                                                                                                                                                                                                                           |
| ------------- | ----------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `cartId`      | Required          | The Salesforce ID for the `cart` object.                                                                                                                                                                                                                                                                                                                                                            |
| `amount`      | Required          | The amount specified by the shopper to use for the customer credit source.                                                                                                                                                                                                                                                                                                                          |
| `paymentName` | Optional          | <p>You can pass the <code>paymentName</code> if you want to provide a different label (for example, <code>GiftCard123</code>) for the payment on the payment detail component. The <code>paymentName</code> appears in the Display Name field for a <code>DR_Transaction_Payment__c</code> object.</p><p>If this parameter is not provided, the label "CustomerCredit" will be used by default.</p> |

{% code title="Request body example" %}
```json
“{
                 "cartId":CartId, 
                 "paymentName": "GiftCard123",
                 "amount”: "50", 
}”
```
{% endcode %}

## Receiving a response

You'll see the following parameters in the response.

| Parameter      | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| -------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `isSuccess`    | <p>This global method returns a Boolean value where:</p><ul><li><code>true</code>–indicates the source was successfully created and applied to checkout.</li><li><code>false</code>–indicates an error occurred while creating or attaching the source to checkout. The system returns an error message when an error occurs, and the Boolean value is <code>false</code>.</li></ul>                                                                                                                     |
| `errorMessage` | <p>If the system returns an error and the value for <code>isSuccess</code> is <code>false</code>, this parameter displays one of the following error messages:</p><ul><li><strong>Missing or invalid input parameters specified</strong>: One of the input parameters are missing or invalid.</li><li><strong>Invalid amount specified</strong>: The value specified for the amount is invalid.</li><li><strong>DR API error</strong>: An error message that comes from the Digital River API.</li></ul> |
| `sourceId`     | The unique identifier of the customer credit source.                                                                                                                                                                                                                                                                                                                                                                                                                                                     |

{% code title="Response body example" %}
```json
{
    "isSuccess":{{boolean_value}},
    "errorMessage": {{error_msg}}, //in case of error
    "sourceId":{{sourceId}}   //in case of success
}
```
{% endcode %}

## Calling the global method from a custom component

Import the `addCustomerChreditSourceToCheckout` method into your custom component javascript file with `digialriverv3` as the namespace as shown below.

{% code title="Import example" %}
```javascript
import addCustomerCreditSourceToCheckout from 
"@salesforce/apex/digitalriverv3.DRB2B_CustomerCreditService.addCustomerCreditSourceToCheckout";
```
{% endcode %}

Call the global method from a custom JavaScript file by passing the `cartId`, `amount`, and (optionally) `paymentName` arguments as shown below.

```javascript
handleAddCustomerCredit(event){
        addCustomerCreditSourceToCheckout({
            inputData : JSON.stringify({
                cartId : this.webcartId,//cart Id
                amount: amount 
            })
          }).then((result) => {
               // implement logic here in case of success
            })
            .catch((error) => {
               // implement logic here in case of error
            });
    }
```
