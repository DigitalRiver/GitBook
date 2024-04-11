---
description: Learn how to use the Amazon Pay element.
---

# Amazon Pay element

With DigitalRiver.js, you can create an Amazon Pay collection element that will automatically retrieve and build a select drop-down that can be styled and placed on your page like other DigitalRiver.js elements.

## Creating an Amazon Pay element

To create an Amazon Pay element, use the `createElement` function exposed through the DigitalRiver Object. This object follows the same pattern and allows for the same [custom classes](./#custom-classes) and [styles ](./#custom-styles)as other elements.

{% tabs %}
{% tab title="Example" %}
{% code overflow="wrap" %}
```javascript
var options = {
    style: {
        color: 'DarkGray', // one of ['Gold', 'LightGray', 'DarkGray']
        height: '100px'
    },
    classes: {
        empty: 'DRElement',
        base: 'DRElement',
        invalid: 'DRElement',
        complete: 'DRElement',
    },
    sourceData: {
        type: 'amazonPay',
        sessionId: sessionId,
        country: 'US', // If your session does not contain shopper a country, a two-letter country code is required.
        amazonPay: {
            //Amazon Pay will redirect the shopper to this URL after the shopper signs in.
            returnUrl: 'https://return.com', 
            //After the shopper authorizes Amazon Pay, the shopper will be returned to this URL. 
            resultReturnUrl: 'https://resultreturn.com', 
            //Amazon Pay will redirect the shopper to this URL if the shopper cancels sign-in on the Amazon Pay hosted page.
            cancelUrl: 'https://cancel.com', 
            // The placement of the Amazon Pay button on your website. Your options are: ['Home', 'Cart', 'Product', 'Checkout', 'Other']
            placement: 'Product', 
             // Optional. Specify the checkout language. Your options are: ['en_US', 'en_GB', 'de_DE', 'fr_FR', 'it_IT', 'es_ES', 'ja_JP']
            checkoutLanguage: 'fr_FR'
        }
    }
};

var amazonpay = digitalriver.createElement('amazonpay', options);
amazonpay.mount('amazonpay');
```
{% endcode %}

| Attribute          | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `country`          | An optional string that represents an [ISO 3166-1 alpha-2](https://en.wikipedia.org/wiki/ISO\_3166-1\_alpha-2) country code. This is required when your session does not contain a shopper country.                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| `returnUrl`        | <p>A redirect to the Amazon Pay Sign in page. </p><p>When the shopper selects Amazon Pay as their payment method from the cart (see callout 1 in the image below), Digital River creates a payment session and source and redirects the shopper to the Amazon Pay Sign in page (see callout 2). The shopper must sign in to Amazon to access the order confirmation page. At this point, the payment information is attached to the Digital River payment source. The shopper must complete the verification process and place the order (see callout 3). Amazon Pay processes the payment (see callout 4) and the source is attached to the cart.</p> |
| `resultReturnUrl`  | <p>A redirect to your thank you page.</p><p>After Amazon Pay process the payment, the shopper is redirected to your thank you page (see callout 5).to the thank you page.</p>                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| `cancelUrl`        | <p>A redirect from the cancelled login page to a page specified by you.<br>Amazon will redirect the shopper to this cancellation URL if the shopper cancels their checkout on the Amazon Pay hosted page.</p>                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| `placement`        | <p>The location where you placed the Amazon Pay button on your website. Your options are <code>Home</code>, <code>Cart</code>, <code>Product</code>, <code>Checkout</code>, or <code>Other</code>.<br><strong>Note</strong>: If you place the Amazon Pay button on the <code>Checkout</code> page, it is a standard checkout. If you place it on <code>Home</code>, <code>Cart</code>, <code>Product</code>, or <code>Other</code> page, it is an express checkout.</p>                                                                                                                                                                                |
| `checkoutLanguage` | The language used on the checkout page. Your options are `en_US`, `en_GB`, `de_DE`, `fr_FR`, `it_IT`, `es_ES`, or `ja_JP`.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
{% endtab %}
{% endtabs %}

### amazonPay.mount();

Call this function to place the created Amazon Pay element on your page. This argument you specify in the HTML element will place the Amazon Pay button on the page.

{% tabs %}
{% tab title="Example" %}
{% code overflow="wrap" %}
```javascript
<div id="amazon-pay-button"></div>

amazonpay.mount('amazon-pay-button');
```
{% endcode %}
{% endtab %}
{% endtabs %}

### amazonPay.unmount();

Call this function to remove the Amazon Pay element from your page. The element may be re-added to your page by calling `mount()`.

{% tabs %}
{% tab title="Example" %}
{% code overflow="wrap" %}
```javascript
amazonPay.unmount();
```
{% endcode %}
{% endtab %}
{% endtabs %}

### amazonPay.destroy();

Call this function to remove the Amazon Pay element from your page and remove its functionality. You cannot re-add the destroyed element to your page via `mount()`.

{% tabs %}
{% tab title="Example" %}
{% code overflow="wrap" %}
```javascript
amazonPay.destroy();
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Amazon Pay events — amazonPay.on('event', handler);

The Amazon Pay element can receive the following events by creating an event listener. Use this function to listen to events that can be used to build and enhance your purchase flow.

| Event                                  | Triggered When                                                       |
| -------------------------------------- | -------------------------------------------------------------------- |
| [ready](broken-reference)              | The created element is loaded and ready to accept an update request. |
| [source](amazon-pay-element.md#source) | The payment source has been created.                                 |

### Ready

{% tabs %}
{% tab title="Ready example" %}
The Ready event triggers when the Amazon Pay element has been mounted.

{% code overflow="wrap" %}
```javascript
amazonpay.on('ready', function (event) {
    addContentToLog( event.elementType + ' ready received \n' + JSON.stringify(event, null, 4));
});
```
{% endcode %}
{% endtab %}

{% tab title="Successful ready event example" %}
The following example indicates the element mounted successfully:

{% code overflow="wrap" %}
```json
{
    "elementType": "amazonpay"
}
```
{% endcode %}
{% endtab %}

{% tab title="Unsuccessful ready even example" %}
The following example indicates the attempt to mount the element was unsuccessful because the country was not in session or options, or the specified country was not supported.

{% code overflow="wrap" %}
```json
{
    "error": {
        "liveMode": false,
        "type": "bad_request",
        "errors": [
            {
                "code": "missing_parameter",
                "parameter": "country",
                "message": "Country must be specified in session or in options"
            }
        ]
    },
    "elementType": "amazonpay"
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Source

When the shopper clicks the Amazon Pay button, DigitalRiver.js will generate a payment source and redirect the shopper to the Amazon Pay Sign In page. DigitalRiver.js will trigger the source event. At this point, the source state is still `pending_redirect` because we created it before we opened the Amazon Pay Sign In page.&#x20;

Once the shopper logs in, Amazon Pay will redirect the shopper to the Amazon Pay site. After the shopper authorizes Amazon Pay, Amazon redirects the shopper to the  `returnUrl` you provided in the [Amazon Pay element](amazon-pay-element.md#creating-an-amazon-pay-element). When the shopper submits their order, they get a response with a `pending_redirect` session state. A second redirect is needed. You need to redirect the shopper to Amazon Pay for a second authentication via the `redirect_url` from the order response. Once authentication completes, Amazon Pay will redirect the shopper from the Amazon Pay site to the `resultReturnUrl` and provide the correct authentication from the Amazon Pay side while doing so.

If the shopper cancels their sign in on the Amazon Pay-hosted page, Amazon Pay will redirect the user to the `cancelUrl`.

{% tabs %}
{% tab title="Source example" %}
{% code overflow="wrap" %}
```json
amazonpay.on('source', function (event) {
    addContentToLog(event.elementType + ' source received \n' + JSON.stringify(event, null, 4));
});
```
{% endcode %}
{% endtab %}

{% tab title="Response object" %}
{% code overflow="wrap" %}
```json
{
    "error": null,
    "source": {
        "clientId": "gc",
        "channelId": "paylive",
        "liveMode": false,
        "id": "a88fcc44-546e-44f3-a057-d144b33fdc00",
        "sessionId": "fd6cda0b-c20b-428c-a068-adc5c9f9218b",
        "clientSecret": "a88fcc44-546e-44f3-a057-d144b33fdc00_e9bbf504-f770-49e7-a147-f6ce7be1113e",
        "type": "amazonPay",
        "reusable": false,
        "owner": {
            "firstName": "US",
            "lastName": "Tester",
            "customerId": "502283345689",
            "email": "usTester@digitalriver.com",
            "phoneNumber": "9522251234",
            "upstreamId": "123456789",
            "organization": "Digital River",
            "address": {
                "line1": "10380 Bren Rd W",
                "city": "Minnetonka",
                "state": "MN",
                "country": "US",
                "postalCode": "55343"
            }
        },
        "amount": "100.00",
        "currency": "USD",
        "state": "pending_redirect",
        "creationIp": "209.87.180.27",
        "createdTime": "2022-10-12T14:58:11.632Z",
        "updatedTime": "2022-10-12T14:58:11.632Z",
        "flow": "redirect",
        "redirect": {
            "offline": false
        },
        "language": "en",
        "amazonPay": {
            "payload": "{\"merchantMetadata\":{\"merchantReferenceId\":\"76a4a202-bd8c-449b-b909-89c8f8955521\",\"merchantStoreName\":\"paylive\"},\"chargePermissionType\":\"OneTime\",\"scopes\":[\"name\",\"email\",\"phoneNumber\",\"billingAddress\"],\"storeId\":\"amzn1.application-oa2-client.a71c43abb93e482eb1f4bb6c08c00561\",\"paymentDetails\":{\"presentmentCurrency\":\"USD\",\"paymentIntent\":\"Authorize\",\"chargeAmount\":{\"amount\":\"100.00\",\"currencyCode\":\"USD\"},\"canHandlePendingAuthorization\":false},\"webCheckoutDetails\":{\"checkoutReviewReturnUrl\":\"https://api.digitalriver.com:443/payments/providers/amazonPayExpress/redirects/20eaa79e-5c73-4e15-ba33-1ccb86814350?apiKey=pk_sys_c2608001bba7477eae22808e1eb138db\",\"checkoutCancelUrl\":\"https://api.digitalriver.com:443/payments/providers/amazonPayExpress/redirects/9a499dc8-7756-418e-953a-102c86aa4acb?apiKey=pk_sys_c2608001bba7477eae22808e1eb138db\",\"checkoutResultReturnUrl\":\"https://api.digitalriver.com:443/payments/providers/amazonPayExpressConfirm/redirects/e2083178-bd35-4433-aa63-6492942828dd?apiKey=pk_sys_c2608001bba7477eae22808e1eb138db\"}}",
            "signature": "zkRZGLhdcEs0hY3PAphTKQOQOT2OOAZ8o//Lm/ktv8HycEAmBAPVbqx8hz6FVM7tQtiwj/fc7yWV1MjzVz+64AQO90q6JyHV96a+INl/CJ9iXGMN6m4yuDIYl61LFJD/P0MCU6kFZsL8hqmxkjGc1udf2kcsHYdKSYRKzrwH0PMKrHvHNFc49VjxPMyEYkYntzpIuwhDtqzWdbAB+9u1LBuDH2UW3H2/a5BPjxJg24B2CfxARctkSg53TZivQL2L3AvScpZfVgHBfWsRcaDqhLNtHtv0lIGFN0TB5l90OQnJHB77OrsIkMa3dHNuL/JeLGqGfiLiSzG4XGOWAoSTlQ==",
            "merchantId": "AXFH8Q1EVKKEH",
            "publicKeyId": "SANDBOX-AG2HJOMSWDGRHE56UFMJLRBF",
            "buttonUrl": "https://h010081013200.cpg-pmt-sys.aws-ue1-a.vdc3.npcloud.zone:44444/cpg_web/test/amazon.7615419205.html",
            "productType": "PayOnly",
            "ledgerCurrency": "USD"
        }
    },
    "elementType": "amazonpay"
}
```
{% endcode %}
{% endtab %}
{% endtabs %}
