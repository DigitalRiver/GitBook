---
description: Learn how to delete the customer credit payment source from checkout.
---

# deattachPaymentToCheckout

Use this global method to delete the customer credit payment source from checkout.

In addition to deleting the source from the checkout, this method will delete the Digital River Transition Payment Object corresponding to the `sourceId` and will update the values for `amountRemainingToBeContributed` and `amountContributed` in the `cart` object.

## Sending a request

This method accepts parameters in JSON string format. You need to pass the `cartId` and the `sourceId` with this method.

| Parameter  | Required/Optional | Description                                        |
| ---------- | ----------------- | -------------------------------------------------- |
| `cartId`   | Required          | The Salesforce ID for the `cart` object.           |
| `sourceId` | Required          | The unique identifier of the source to be removed. |

{% code title="Request body example" %}
```json
“{
      "cartId”:CartId, 
      “sourceId”: “sourceId”
}”
```
{% endcode %}

## Receiving a response

You'll see the following parameters in the response.

| Parameter      | Description                                                                                                                                                                                                                                                                                                                                                                                            |
| -------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `isSuccess`    | <p>This global method returns a Boolean value where:</p><ul><li><code>true</code>–indicates the source was successfully deleted.</li><li><code>false</code>–indicates an error occurred while deleting the source from checkout. The system returns an error message when an error occurs, and the Boolean value is <code>false</code>.</li></ul>                                                      |
| `errorMessage` | <p>If the system returns an error and the value for <code>isSuccess</code> is <code>false</code>, this parameter displays one of the following error messages:</p><ul><li><strong>Missing or invalid input parameters specified</strong>: One of the input parameters are missing or invalid.</li><li><strong>DR API error</strong>: An error message that comes from the Digital River API.</li></ul> |

{% code title="Response body example" %}
```json
{
   "isSuccess":{{Boolean_Value}},  
   "errorMessage":{{error_msg}} // In case of error
}
```
{% endcode %}

## Calling the global method from a custom component

Import the `deattachPaymentToCheck` method into your custom component javascript file with `digialriverv3` as the namespace as shown below.

{% code title="Import example" %}
```javascript
import deattachPaymentToCheckout from 
"@salesforce/apex/digitalriverv3.DRB2B_CustomerCreditService.deattachPaymentToCheckout";
```
{% endcode %}

Call the global method from a custom JavaScript file by passing the `cartId`, `amount` and () sourceId `arguments` as shown below.

```javascript
handleRemoveCustomerCredit(event){
        var sourceId = event.target.name;
        deattachPaymentToCheckout({
            inputData : JSON.stringify({
                cartId : this.webcartId, // Cart Id
                sourceId : sourceId  // source Id
            })
        }).then((result) => {
             // implement logic here in case of success
            })
            .catch((error) => {
            // implement logic here in case of error
            });
    }
```
