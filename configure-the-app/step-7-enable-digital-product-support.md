---
description: Learn how to enable support for digital products.
---

# Step 7: Enable support for digital products

To enable support for digital products, the checkout flow has been changed by extending the `MultiStepCheckoutController.java` and `addCheckoutStepsToModel()` methods in various checkout steps controllers. Digital River automatically fulfills digital products by default.

Include the following override methods in the `DefaultDigitalRiverFacade.java` file.

{% code title="" %}
```java
@Override
	public boolean isDigitalProduct(final String productCode)
	{
		return digitalRiverPaymentService.isDigitalProduct(productCode);
	}

	@Override
	public boolean isDigitalCart()
	{
		return digitalRiverPaymentService.isDigitalCart();
	}

	@Override
	public boolean isDigitalOrder(final OrderModel order)
	{
		return digitalRiverPaymentService.isDigitalOrder(order);
	}
@Override
	public boolean hasDigitalProduct(final OrderModel order)
	{
		return digitalRiverPaymentService.hasDigitalProduct(order);
	}

	@Override
	public String getDigitalEntryStatus(final String code, final OrderEntryData orderEntry)
	{
		return digitalRiverPaymentService.getDigitalEntryStatus(code, orderEntry);
	}
```
{% endcode %}

Products marked as `Digital` in the `DRProductType` attribute of the product configuration will be treated as a digital product in this extension.

See [Step 8: Run the confirmation email body template](step-8-run-the-confirmation-email-body-template.md) for digital product-related changes in the confirmation email.

See [Step 11: Customize the locale, OMS, and webhooks](step-11-customize-the-locale-oms-and-webhooks.md) section for OMS-related changes for digital products.

****
