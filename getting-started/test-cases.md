---
description: >-
  Tap into these use cases when developing and testing the Commerce API and your
  commerce connector.
---

# Test and use cases

Before and after any production deployment, we recommend that you run a series of regression tests similar to those outlined below on your site. These tests are a suggested baseline, and you can customize the test cases based on your implementation. Include additional tests such as reviewing the logged API response codes, browser compatibility, domain or TLS security, JavaScript errors, and so on, as required.&#x20;

Since "live changes" do not allow for testing in a DESIGN or TEST mode, we also recommended that you integrate your Stage or Test systems with Digital River’s Client Test Environment (CTE) whenever possible. This will help facilitate safe end-to-end testing of all changes before you deploy to production.

## Confirm parameters are passed as expected&#x20;

On pre-cart pages, ensure that the expected products, currency, pricing, and discounts appear on the Home page, Category pages, and Product pages. If your store supports multiple countries and regions, verify that locale language and currency changes as expected by country and region.

* Confirm the product IDs, category IDs, and locale parameters are passed as expected.
* Confirm the API responses are consumed as expected.

## Confirm changes to the cart and Checkout page

1.  Add two or three products to a cart:

    * Confirm an [anonymous shopper token](https://docs.digitalriver.com/commerce-api/getting-started/best-practices#creating-session-aware-access-tokens) or [authenticated shopper token](https://docs.digitalriver.com/commerce-api/getting-started/best-practices#creating-authenticated-shopper-tokens) was generated, and the Checkout pages and API requests use HTTPS.
    * Confirm the [products were added to the cart](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Carts/paths/\~1v1\~1shoppers\~1me\~1carts\~1active/post).

    See [Creating or updating a cart](../cart/creating-or-updating-a-cart.md) for more information.
2. Verify that the expected products, currency, pricing, and discounts [appear in the cart](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Shoppers/paths/\~1v1\~1shoppers\~1me/post) as expected. See [Local and currency](https://docs.digitalriver.com/commerce-api/consumer-browsing-experience-1/basic-information/locale-and-currency) for more information.
3. Adjust the product quantities and delete one line item from the cart.
   * Confirm the [line item updates](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Line-Items/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1line-items\~1{lineItemsId}/post) worked as expected.
   * Confirm the [deletion of a line item](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Line-Items/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1line-items\~1%7BlineItemsId%7D/delete) worked as expected.
4. **\[Required if you are using coupons.]** Submit a promo code (`promoCode`) that is either valid or invalid) and confirm the [application of the coupon](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Carts/paths/\~1v1\~1shoppers\~1me\~1carts\~1active/post) worked as expected. If the store supports promo codes that trigger order, line item, and shipping discounts, we recommend testing all promo code types from checkout to order completion. See [Applying a coupon code](../consumer-browsing-experience-1/common-use-cases/applying-a-coupon-code.md) for more information.
5. **\[Required for account creation.]** Create a new shopper and sign in as the shopper.
   * Confirm the [shopper was created](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Shoppers/paths/\~1v1\~1shoppers/post) as expected.
   * Confirm the [authentication or full access token](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Token) was generated as expected.
6. **\[Required for physical products.]**  Submit a shipping address from the Shipping Address page and confirm the [shipping address change](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Shipping-Address/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1apply-shipping-address/post) works as expected. We recommend that you manually enter the address without using the Form Filler. For more information, see [Providing address information](../cart/providing-address-information.md).
7. **\[Required for physical products.]** Confirm the available [shipping methods appear](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Shipping-Options/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1shipping-options/get) as expected and [change the shipping method](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Apply-Shipping-Option) on the Shipping Method page.
8.  From the Payment or Billing Address page, submit the payment information and billing address. We recommend that you manually enter the address without using the Form Filler and verify all required payment methods are available for the locale.

    * Confirm [payment method was applied](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Apply-Payment-Method) as expected and a [source was created](https://docs.digitalriver.com/commerce-api/payment-integrations-1/digitalriver.js/reference/digitalriver-object#creating-sources).
    * Confirm the [billing address was applied](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Billing-Address/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1apply-billing-address/post) as expected.

    See the following topics for more information:

    * [Sources](../cart/sources/)
    * [Testing scenarios](../payment-integrations-1/testing-scenarios.md)
    * [Providing address information](../cart/providing-address-information.md)
9. From the Review page, review the order details and confirm the previously submitted data is present and accurate, including:
   * The required legal text and disclosures (Terms of Sale, privacy policy, and so on) appear as expected and links to the accompanying legal pages are functioning.
   * The products (including pricing, discounts, and quantities)
   * The payment method (for example, the payment method type and last four digits of the card number)
   * The billing and shipping addresses
   * The selected shipping method
10. Submit the order and confirm the [cart submitted correctly](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Submit-Cart/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1submit-cart/post) by sending a test payment.

    * Verify the content in the Order Summary is accurately reflects the shopper's order and the order number appears (if required).
    * When using a test credit card and the Test Order flag (`testOrder`)  is set to `false` for a live order, confirm that you received an "Auth Failed" error message.&#x20;
    * When using a valid credit card and the Test Order flag (`testOrder`) is set to `false` for a live order, confirm you received a successful payment authorization and order submission.

    **Note**: Check the submitted order to confirm the Test Order flag (`testOrder`) is not present in a live order. Essentially, you need to confirm that the Test Order flag (`testOrder`) is not set to `true` when you go live.

## Submit a live order for production validation

When submitting a live order for production validation, verify the following information in the Submit Cart response or the platform used to look up order information (for example, [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do)).

* Verify that you received an order confirmation email.
* The Test Order flag (`testOrder`) is set to `false`.
* The submitted data is present in the order and accurate, including:
  * The products (including pricing, discounts, and quantities)
  * The payment method (for example, the payment method type and last four digits of the card number)
  * The billing and shipping addresses
  * The selected shipping method
* You captured the [shopper's IP address](https://docs.digitalriver.com/commerce-api/cart/shopper-ip-address).
* Confirm the [Terms of Sale](https://docs.digitalriver.com/commerce-api/cart/terms-of-sale-acceptance) (`termsOfSalesAcceptance`) works as expected. See [Checkout tab](https://help.digitalriver.com/help/gc/Administration/Site/Configuring-site-settings.htm#CheckoutTab) for more information on Terms of Sale Acceptance.
