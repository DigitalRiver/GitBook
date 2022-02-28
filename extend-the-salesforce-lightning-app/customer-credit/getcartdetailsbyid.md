---
description: Learn how to validate whether the cart contains a subscription product.
---

# getCartDetailsById

Use this global method to verify whether the cart contains a subscription product.  If the cart contains a subscription product, do not allow customer credit as the payment method since subscription renewals require a primary payment method. If your store sells subscriptions, use this method to verify whether the cart contains subscription products before allowing the user to select the customer credit as a payment method.&#x20;

## Sending a request

This method accepts parameters in JSON string format. You need to pass the `cartId` to this method.&#x20;

| Parameter | Required/Optional | Description                              |
| --------- | ----------------- | ---------------------------------------- |
| `cartId`  | Required          | The Salesforce ID for the `cart` object. |

{% code title="Request body example" %}
```json
“{
    "cartId":CartId
}”
```
{% endcode %}

## Receiving a response

You'll see the following parameters in the response.

| Parameter | Description                                                                                                                                                                                                                               |
| --------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `return`  | <p>This global method returns a Boolean value where:</p><ul><li> <code>true</code>–indicates the cart contains a subscription product. </li><li><code>false</code>–indicates the cart does not contain a subscription product. </li></ul> |

{% code title="Response body example" %}
```json
return true;
```
{% endcode %}

## Calling the global method from a custom component

Import the `getCartDetailsById`method into your custom component javascript  file with `digialriverv3` as the namespace as shown below.

{% code title="Import example" %}
```javascript
import getCartDetailsById from 
"@salesforce/apex/digitalriverv3.DRB2B_CustomerCreditService.getCartDetailsById";
```
{% endcode %}

Call the global method from a custom JavaScript file by passing the `cartId` as shown below.

```javascript
getCartDetails() {
        getCartDetailsById({cartId:this.webcartId })
            .then((result) => { 
              // implement here logic in case of success      
            })
            .catch((error) => {
             // implement here logic in case of error
            });
        }
```
