---
description: Learn how to record a customer's request to be forgotten.
---

# Recording a customer's request to be forgotten

You must establish a process to allow a customer to request to be forgotten where required by [EU law](https://gdpr.eu/right-to-be-forgotten/). Digital River will remove a customer's information in accordance with [our data deletion process](https://help.digitalriver.com/legal/Legal.htm#PaymentsRisk) if you initiate a request to be forgotten on behalf of your customer.

The `requestToBeForgotten` is a boolean parameter that indicates whether or not a customer asked to be forgotten.

When a customer asks to be forgotten, Digital River logs the request to remove personally identifiable information (PII) from our system. PII is any information that someone could use to uniquely identify, contact, or locate an individual.

If you receive a request to be forgotten from a customer, you can programmatically set `requestToBeForgotten` to `true` on the Customer resource. If you receive a request to be forgotten from a guest user who has placed an order and for whom you have not created a Customer resource, you can set `requestToBeForgotten`to `true` on the Order resource.

See [https://www.digitalriver.com/corporate-policies](https://www.digitalriver.com/corporate-policies) for more information on Digital River Privacy Policy.

You choose to record a customer's request to be forgotten from the [Digital River Dashboard ](recording-a-request-to-be-forgotten.md#example-record-request-from-the-dashboard)or [programmatically](recording-a-request-to-be-forgotten.md#example-record-request-and-response).

## Example record request from the Digital River Dashboard

To record the customer's request to be forgotten from the Dashboard.

1. Sign in to the [Dashboard](https://dashboard.digitalriver.com/login).
2. Click **All orders**.
3. Click an identifier link under the **ID** column.
4. Under **Customer**, click the **Request removal of personal information** link.
5. Click **Confirm**.
6. [Send an email](recording-a-request-to-be-forgotten.md#example-email) to the customer to confirm the change.

## Example record request and response

Update a Customer object for a specific customer that sets the `requestToBeForgotten` parameter to `true` with a `POST` request.

{% tabs %}
{% tab title="cURL" %}
```
curl https://api.digitalriver.com/customers/5823594808 \
     -u sk_test_db9682a2-b04a-4e94-8e11-35fe8ec0b324: \
     -d requestToBeForgotten=true
```
{% endtab %}
{% endtabs %}

A `200 OK` response returns a [Customer](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Customers) object:

{% tabs %}
{% tab title="JSON" %}
```javascript
{
    "name": "John Smith",
    "phone": "952-111-1111",
    "email": "jsmith@digitalriver.com",
    "organization": "Digital River"
  },
  "defaultSourceId": "src_fd74a5c5-0163-469a-ae8e-031f0259b576",
  "requestToBeForgotten": true,
  "enabled": true
}
```
{% endtab %}
{% endtabs %}

Digital River will send a webhook to you that indicates we received the customer's request to be forgotten. When you receive the `customer.updated` webhook with this change, [send an email](recording-a-request-to-be-forgotten.md#example-email) to the customer to confirm the change.

## Example email

You can use the following text as a template when you send an email to a customer stating that you received and processed their request. Replace the variables with the appropriate information.

{% tabs %}
{% tab title="Plain Text" %}
```
Subject: <%YOUR_SITE_NAME%> - Request for personal data removal has been received

Dear <%CUSTOMER_NAME%>,

Thank you for contacting <%YOUR_SITE_NAME%>. We have received your request to remove your personal data from our records. 

E-commerce services are provided by Digital River. Your personal information will be removed once legal and business obligations for retention of this data have been satisfied. For questions regarding this request, please refer to Digital River’s Privacy Policy: https://www.digitalriver.com/corporate-policies. 

Please note: This email message was sent from a notification-only address that cannot accept incoming emails. Please do not reply to this message.

Sincerely,
<%YOUR_SITE_NAME%> Customer Service
<%YOUR_CUST_SERVICE_URL%>
```
{% endtab %}
{% endtabs %}
