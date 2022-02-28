---
description: Learn how to get the remaining amount available for checkout.
---

# getAmountRemainingforCheckout

Use this global method to get the remaining customer credit amount that the shopper can contribute to the checkout.

## Sending a request

This method accepts parameters in JSON string format. You need to pass the `cartId` with this method.&#x20;

| Parameter | Required/Optional | Description                              |
| --------- | ----------------- | ---------------------------------------- |
| `cartId`  | Required          | The Salesforce ID for the `cart` object. |

{% code title="Request body example" %}
```json
"{
    "cartId":CartId
}"
```
{% endcode %}

## Receiving a response

You'll see the following parameters in the response.

| Parameter                        | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| -------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `isSuccess`                      | <p>This global method returns a Boolean value where:</p><ul><li> <code>true</code>–indicates the call to Digital River to get the remaining amount was successful. This global method will also return the amount remaining to be be contributed and the currency code when successful.</li><li><code>false</code>–indicates an error occurred while getting the remaining amount. The system returns an error message when an error occurs, and the Boolean value is <code>false</code>.</li></ul>                                                                                     |
| `amountRemainingToBeContributed` | The amount remaining to be contributed to the checkout.  A customer credit source can be created for an amount less than or equal to this value.                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `currencyCode`                   | The currency code of the checkout                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `errorMessage`                   | <p>If the system returns an error and the value for <code>isSuccess</code> is <code>false</code>, this parameter displays one of the following error messages:</p><ul><li><strong>Missing or invalid input parameters specified</strong>: One of the input parameters are missing or invalid.</li><li><strong>Unable to retrieve Remaining Amount for checkout</strong>: An <a href="https://docs.digitalriver.com/digital-river-api/payment-integrations-1/digitalriver.js/reference/error-types-codes-and-objects">error message</a> that comes from the Digital River API.</li></ul> |

{% code title="Response body example" %}
```json
{
   "isSuccess":{{Boolean_Value}},
   "amountRemainingToBeContributed":{{Remaining_Amount_To_Be_Contributed}},
   "currencyCode": {{Currency_Code}},
   "errorMessage": {{Error_Message}} // In case of error
}
```
{% endcode %}

## Calling the global method from a custom component

Import the `getAmountRemainingforCheckout` method into your custom component javascript  file with `digialriverv3` as the namespace as shown below.

{% code title="Import example" %}
```javascript
import getRemainingAmount from 
"@salesforce/apex/digitalriverv3.DRB2B_CustomerCreditService.getAmountRemainingforCheckout";
```
{% endcode %}

Call the global method from a custom JavaScript file by passing the `cartId` as shown below.

```javascript
getRemainingAmount(){
        let input = {
            cartId:this.recordId
        };
        getRemainingAmount({inputData:JSON.stringify(input)})
        .then((data)=>{
         // implement logic here in case of success
        })
        .catch((error)=>{
         // implement logic here in case of error
        })
    }
```
