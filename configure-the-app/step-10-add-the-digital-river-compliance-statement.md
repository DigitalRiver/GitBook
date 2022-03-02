---
description: Learn how to add the Digital River compliance statement.
---

# Step 10: Add the Digital River compliance statement

The merchant system must show a Digital River compliance statement in the footer section of every checkout step. We updated the OOB and created the following custom JSP files to display the Digital River compliance section in the footer.

* `addEditDeliveryAddressPage.jsp`
* `chooseDeliveryMethodPage.jsp`
* `silentOrderPostPage.jsp`
* `checkoutSummaryPage.jsp`
* `drTemsPage.jsp`
* `drAddPaymentPage.jsp`

You can use the following code on any page that requires the Digital River Compliance section for both B2C and B2B storefronts.

{% code title="Compliance footer code example" %}
```html
<div class="col-sm-12 col-lg-12">
    <cms:pageSlot position="SideContent" var="feaure" element="div" class="checkout-help">
        <div id="drComplianceFuooter"></div>
        <cms:component component="#{feature}"/>
    </cms:pageSlot>
</div>
```
{% endcode %}
