---
description: Learn how to run the project data ImPex files.
---

# Step 7: Run project data ImPex files

Once you [update the system](step-6-update-the-system.md), run the `projectdata-dynamic-business-process-order.impex` and `projectdata-dynamic-business-process-return.impex`.&#x20;

{% code title="projectdata-dynamic-business-process-order.impex" %}
```javascript
# -----------------------------------------------------------------------
# [y] hybris Platform
#
# Copyright (c) 2018 SAP SE or an SAP affiliate company.  All rights reserved.
#
# This software is the confidential and proprietary information of SAP
# ("Confidential Information"). You shall not disclose such Confidential
# Information and shall use it only in accordance with the terms of the
# license agreement you entered into with SAP.
# -----------------------------------------------------------------------
INSERT_UPDATE DynamicProcessDefinition;code[unique=true];active;content
;order-process;true;"<process xmlns='http://www.hybris.de/xsd/processdefinition' start='checkOrder'
name='order-process' processClass='de.hybris.platform.orderprocessing.model.OrderProcessModel'>

<!-- Check Order -->
<action id='checkOrder' bean='checkOrderAction'>
   		<transition name='OK' to='checkAuthorizeOrderPayment'/>
		<transition name='NOK' to='error'/>
		<transition name='WAIT' to='waitForDRReview'/>
</action>

	<wait id='waitForDRReview' then='checkAuthorizeOrderPayment' prependProcessCode='false'>
  		<event>${process.order.code}_DRReviewDecision</event>
	</wait>
	
	<action id='checkAuthorizeOrderPayment' bean='checkAuthorizeOrderPaymentAction'>
		<transition name='OK' to='fraudCheck'/>
		<transition name='NOK' to='authorizationFailedNotification'/>
	</action>
	
	<action id='authorizationFailedNotification' bean='sendAuthorizationFailedNotificationAction'>
		<transition name='OK' to='failed'/>
	</action>

<!-- Fraud Check -->
<action id='fraudCheck' bean='fraudCheckOrderInternalAction'>
    <transition name='OK' to='sendOrderPlacedNotification'/>
    <transition name='POTENTIAL' to='manualOrderCheckCSA'/>
    <transition name='FRAUD' to='cancelOrder'/>
</action>

<!-- Fraud Check : OK -->
<action id='sendOrderPlacedNotification' bean='sendOrderPlacedNotificationAction'>
   		<transition name='OK' to='geocodeShippingAddress'/>
		<transition name='WAIT' to='fulfillDigital'/>
</action>

<action id='fulfillDigital' bean='fulFillDigitalAction'>
    <transition name='OK' to='verifyOrderCompletion'/>
    <transition name='WAIT' to='geocodeShippingAddress'/>
    <transition name='DONE' to='success'/>
</action>

<!-- Fraud Check : FRAUD -->
<action id='cancelOrder' bean='cancelOrderAction'>
    <transition name='OK' to='notifyCustomer'/>
</action>

<action id='notifyCustomer' bean='notifyCustomerAboutFraudAction'>
<transition name='OK' to='failed'/>
</action>

<!-- Fraud Check : POTENTIAL -->
<action id='manualOrderCheckCSA' bean='prepareOrderForManualCheckAction'>
    <transition name='OK' to='waitForManualOrderCheckCSA'/>
</action>

<wait id='waitForManualOrderCheckCSA' then='orderManualChecked' prependProcessCode='true'>
    <event>CSAOrderVerified</event>
</wait>

<action id='orderManualChecked' bean='orderManualCheckedAction'>
    <transition name='OK' to='sendOrderPlacedNotification'/>
    <transition name='NOK' to='cancelOrder'/>
    <transition name='CANCELLED' to='success'/>
</action>

<!-- Sourcing and Allocation -->
<action id='geocodeShippingAddress' bean='geocodeShippingAddressAction'>
    <transition name='OK' to='sourceOrder'/>
</action>

<action id='sourceOrder' bean='sourceOrderAction'>
    <transition name='OK' to='waitForOrderAction'/>
</action>

<!-- Wait to perform action on Order -->
<wait id='waitForOrderAction' prependProcessCode='true' then='failed'>
    <case event='OrderActionEvent'>
        <choice id='consignmentProcessEnded' then='verifyOrderCompletion'/>
        <choice id='cancelOrder' then='processOrderCancellation'/>
        <choice id='cancelled' then='success'/>
        <choice id='reSource' then='sourceOrder'/>
        <choice id='putOnHold' then='putOrderOnHold'/>
    </case>
</wait>

<!-- Wait for order cancellation to be completed -->
<action id='processOrderCancellation' bean='processOrderCancellationAction'>
    <transition name='OK' to='verifyOrderCompletion'/>
    <transition name='WAIT' to='waitForOrderAction'/>
    <transition name='SOURCING' to='sourceOrder'/>
</action>

<action id='verifyOrderCompletion' bean='verifyOrderCompletionAction'>
    <transition name='OK' to='waitForDRCapture'/>
    <transition name='WAIT' to='waitForOrderAction'/>
    <transition name='CANCELLED' to='success'/>
</action>

<wait id='waitForDRCapture' then='takePayment' prependProcessCode='false' >
		<event>${process.order.code}_DRCaptureProcessEnd</event>
</wait>
	
<action id='putOrderOnHold' bean='putOrderOnHoldAction'>
    <transition name='OK' to='waitForOrderAction'/>
</action>

<!-- Tax and Payment -->
<action id='postTaxes' bean='postTaxesAction'>
    <transition name='OK' to='takePayment'/>
</action>

<action id='takePayment' bean='takePaymentAction'>
    <transition name='OK' to='completeOrder'/>
    <transition name='NOK' to='sendPaymentFailedNotification'/>
</action>

<action id='completeOrder' bean='completeOrderAction'>
    <transition name='OK' to='success'/>
</action>

<action id='sendPaymentFailedNotification' bean='sendPaymentFailedNotificationAction'>
    <transition name='OK' to='failed'/>
</action>

<end id='error' state='ERROR'>Order process error.</end>
<end id='failed' state='FAILED'>Order process failed.</end>
<end id='success' state='SUCCEEDED'>Order process completed.</end>

</process>"

```
{% endcode %}

{% code title="projectdata-dynamic-business-process-return.impex" %}
```javascript
# -----------------------------------------------------------------------
# [y] hybris Platform
#
# Copyright (c) 2018 SAP SE or an SAP affiliate company.  All rights reserved.
#
# This software is the confidential and proprietary information of SAP
# ('Confidential Information'). You shall not disclose such Confidential
# Information and shall use it only in accordance with the terms of the
# license agreement you entered into with SAP.
# -----------------------------------------------------------------------
INSERT_UPDATE DynamicProcessDefinition;code[unique=true];active;content
;return-process;true;"<process xmlns='http://www.hybris.de/xsd/processdefinition' start='initialReturnAction'
         name='return-process' processClass='de.hybris.platform.returns.model.ReturnProcessModel'>

<action id='initialReturnAction' bean='initialReturnAction'>
    <transition name='ONLINE' to='waitForConfirmOrCancelReturnAction'/>
    <transition name='INSTORE' to='captureRefundAction'/>
</action>

<wait id='waitForConfirmOrCancelReturnAction' prependProcessCode='true' then='failed'>
    <case event='ConfirmOrCancelRefundEvent'>
        <choice id='cancelReturn' then='cancelReturnAction'/>
        <choice id='approveReturn' then='approveReturnAction'/>
    </case>
</wait>

<action id='cancelReturnAction' bean='cancelReturnAction'>
    <transition name='OK' to='success'/>
</action>

<action id='approveReturnAction' bean='approveReturnAction'>
    <transition name='OK' to='printReturnLabelAction'/>
</action>

<action id='printReturnLabelAction' bean='printReturnLabelAction'>
    <transition name='OK' to='printPackingLabelAction'/>
</action>

<action id='printPackingLabelAction' bean='printPackingLabelAction'>
    <transition name='OK' to='waitForGoodsAction'/>
</action>

<wait id='waitForGoodsAction' prependProcessCode='true' then='failed'>
    <case event='ApproveOrCancelGoodsEvent'>
        <choice id='cancelReturn' then='cancelReturnAction'/>
        <choice id='acceptGoods' then='acceptGoodsAction'/>
    </case>
</wait>

<action id='acceptGoodsAction' bean='acceptGoodsAction'>
    <transition name='OK' to='captureRefundAction'/>
</action>

<action id='captureRefundAction' bean='captureRefundAction'>
    <transition name='OK' to='waitForDRRefund'/>
    <transition name='NOK' to='waitForFailCaptureAction'/>
</action>

<wait id='waitForDRRefund' then='successCaptureAction' prependProcessCode='false' >
		<event>${process.returnRequest.order.code}_${process.returnRequest.RMA}_DRRefundProcessEnd</event>
</wait>

<wait id='waitForFailCaptureAction' prependProcessCode='true' then='failed'>
    <case event='FailCaptureActionEvent'>
        <choice id='bypassCapture' then='taxReverseAction'/>
        <choice id='cancelReturn' then='cancelReturnAction'/>
    </case>
</wait>

<action id='successCaptureAction' bean='successCaptureAction'>
    <transition name='OK' to='inventoryUpdateAction'/>
    <transition name='NOK' to='failed'/>
</action>

<action id='taxReverseAction' bean='taxReverseAction'>
    <transition name='OK' to='successTaxReverseAction'/>
    <transition name='NOK' to='waitForFailTaxReverseAction'/>
</action>

<wait id='waitForFailTaxReverseAction' then='inventoryUpdateAction' prependProcessCode='true'>
    <event>FailTaxReverseEvent</event>
</wait>

<action id='successTaxReverseAction' bean='successTaxReverseAction'>
    <transition name='OK' to='inventoryUpdateAction'/>
</action>

<action id='inventoryUpdateAction' bean='inventoryUpdateAction'>
    <transition name='OK' to='completeReturnAction'/>
</action>

<action id='completeReturnAction' bean='completeReturnAction'>
    <transition name='OK' to='success'/>
</action>

<end id='failed' state='FAILED'>Return issue detected.</end>
<end id='success' state='SUCCEEDED'>Return process ended as expected.</end>
</process>"
rojectdata-dynamic-business-proces-rejetdatje-dynamic-business-pro
```
{% endcode %}

If the `ImPex` fails when your run it, go to **Backoffice**, select **System**, then select **Business process**, select **Dynamic Processes Definitions**, and delete the `order-process` and `return-process` if present. Then run the `ImPex` files again.

![](<../.gitbook/assets/Dynamci Processes Definitions.png>)

When the ImPex files run successfully, click the order-process/return process and verify the content.
