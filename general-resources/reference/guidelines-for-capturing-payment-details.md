---
description: 'When creating a payment method, follow these guidelines:'
---

# Guidelines for capturing payment details

## **Immediate payment method (Credit Card)**

* You may create a credit card source at any point in your checkout flow.

## **One-Click buttons (Apple Pay, Google Pay, PayPal)**

* Do not allow customers to click the "One-Click" buttons until they agree to all the required terms.
* After authorization by the one-click provider, submit the order and direct the shopper to the Thank You page. You should not allow changes to the order at this point.

## **Redirect payment methods**

* Before creating a redirect payment source, your order should be in a final state for all amounts, including taxes, shipping, duties, and fees.
* Before following the redirect, the shopper must agree to all the required terms.
* Once the payment provider approves the payment, you should submit the order and direct the shopper to the Thank You page. You should not allow changes to the order at this point.

## **Delayed repayment methods**

* Before creating a delayed payment source, your order should be in a final state for all amounts, including taxes, shipping, duties, and fees.
* Once created, you should submit the order and direct the shopper to the Thank You page. You should not allow changes to the order at this point.
* On the Thank You page, you should display the details included in the source about how to pay. This may consist of wiring money or paying at a physical location such as a store.
