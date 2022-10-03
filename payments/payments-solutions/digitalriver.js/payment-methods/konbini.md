---
description: Learn how to configure Konbini for DigitalRiver.js with Elements.
---

# Configuring Konbini

If you're using[ DigitalRiver.js with Elements](../), you can create a [Konbini](../../../supported-payment-methods/konbini.md) payment method for your app or website in four easy steps:

* [Step 1: Build a Kobini source request object](konbini.md#step-1-build-a-kobini-source-request-object)
* [Step 2: Create a Konbini source using DigitalRiver.js](konbini.md#step-2-create-a-konbini-source-using-digitalriver-js)
* [Step 3: Use the Konbini source](konbini.md#step-3-use-the-konbini-source)
* [Step 4: After submitting the order](konbini.md#step-4-after-submitting-the-order)

## Step 1: Build a Kobini source request object

Build a Kobini source request object. A Konbini Source Request object requires the following fields.

| Field       | Value                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| ----------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `type`      | `konbini`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| `sessionId` | The payment session identifier.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| `owner`     | <p>An <a href="common-payment-objects.md#owner-object">Owner object</a>. When the <code>storeId</code> is<code>040</code> (Lawson), use double-byte Kanji without <a href="https://developer.mozilla.org/en-US/docs/Glossary/Whitespace">whitespace </a>for the <code>owner.firstName</code> and <code>owner.lastName</code> to ensure successful payment source creation. You also need to ensure that the <code>lastName</code> precedes the <code>firstName</code>.<br><strong>Example</strong>: </p><p><code>{</code> <br>  <code>"lastName": "山田",</code> <br>  <code>"firstName": "太郎", "email":</code>  <br><code>}</code> <br>If you use a single-byte string, the payment source creation will fail.<br>The <code>address</code> object must contain <a href="broken-reference">postal code</a> and <a href="broken-reference">state/province</a> data that <a href="broken-reference">adheres to a standardized format</a>.</p> |
| `konbini`   | A [Konbini Source Details object](konbini.md#konbini-source-details-object).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |

### Konbini Source Details object

{% tabs %}
{% tab title="Source Details object" %}
{% code overflow="wrap" %}
```
{
    "storeId": "010"
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

| Field     | Required/Optional | Description                                                                                                                                                                                                                                |
| --------- | ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `storeId` | Required          | The identifier of the store where the Customer chose to pay. **If you use the DigitalRiver.js Konbini Element, Digital River automatically populates the value for you. If you construct the request yourself, this is a required field.** |

## Step 2: Create a Konbini source using DigitalRiver.js

Use the DigitalRiver.js library to create and mount elements to the HTML container. If you are using the DigitalRiver.js element ([option 1](konbini.md#option-1-create-a-konbini-element-using-digitalriver-js-functionality)), the `storeId` value is automatically populated based on the customer's selected store. If you are not using the DigitalRiver.js element ([option 2](konbini.md#option-2-using-digitalriver-js-to-create-your-own-konbini-display)), you must construct the request to include the `storeId` parameter.

### Option 1: Create a Konbini element using DigitalRiver.js functionality

The pattern for creating the Konbini element follows the same pattern as other elements and exposes the same c[ustomization and events](../../../../general-resources/reference/elements/). You can customize the look and feel through [options ](../../../../general-resources/reference/elements/#custom-classes)and then place it on the page.

{% tabs %}
{% tab title="Example" %}
{% code overflow="wrap" %}
```javascript
var konbiniOptions = {
    classes: {
        base: "DRElement",
        complete: "konbini-complete",
        empty: "konbini-empty",
        focus: "konbini-focus"
    },
    style: {
        base: {
            color: '#495057',
            height: '35px',
            fontSize: '1rem',
            fontFamily: 'apple-system,BlinkMacSystemFont,Segoe UI,Roboto,Helvetica Neue,Arial,sans-serif',
            ':hover': {
                color: '#ccc',
            },
            '::placeholder': {
                color: '#495057'
            }
        },
        focus: {
            ':hover': {
                color: '#495057',
            },
        },
        empty: {
            ':hover': {
                color: '#495057',
            },
        },
        complete: {
            ':hover': {
                color: '#495057',
            },
        }
    }
};
 
//Create the element
var konbiniElement = digitalriver.createElement('konbini', konbiniOptions);
 
 
//Place it on the page
konbiniElement .mount('konbini-selector');
```
{% endcode %}
{% endtab %}
{% endtabs %}

DigitalRiver.js will create and render a select element that populates with the store logo and localized store name of the available stores where the customer can pay using this payment method.

![](../../../../.gitbook/assets/konbini\_drjs\_render.png)

The same [events and structures](../../../../general-resources/reference/elements/#element-on) appear in the Konbini element, and you should listen to the [Change event](../../../../general-resources/reference/elements/konbini-elements.md#change) to determine when the user has made a selection. When the change event response contains `"complete": true`, the shopper has selected a store.

{% tabs %}
{% tab title="Example" %}
{% code overflow="wrap" %}
```javascript
konbiniElement.on('blur', function (event) {
    console.log('konbini blur', event);
});
             
konbiniElement.on('focus', function (event) {
    console.log('konbini focus', event);
});
             
konbiniElement.on('ready', function (event) {
    console.log('konbini ready', event);
});
         
konbiniElement.on('change', function (event) {
    console.log('konbini change', event);
 
    if (event.complete) {
        //the user has selected a store, you may create the source
    } else if(event.error) {
        //do something with the error message
    }
});
```
{% endcode %}
{% endtab %}
{% endtabs %}

To create a Konbini source, reference the created element and the supplemental data in your [createSource ](../../../../general-resources/reference/digitalriver-object.md#digitalriver-createsource-element-sourcedata)request. DigitalRiver.js will retrieve and assemble the request on your behalf.

{% hint style="info" %}
The `address` object must contain postal code and state/province data that **** [adheres to a standardized format](../../../../cart/creating-or-updating-a-cart/providing-address-information.md) using the `state` attribute. Note that the `state` attribute listed below corresponds to the `countrySubdivision` attribute used when providing address information. The payment session manages the correct field name on the backend.
{% endhint %}

{% tabs %}
{% tab title="Example" %}
{% code overflow="wrap" %}
```javascript
var data = {
    "type": "konbini",
    "sessionId": "ea03bf6f-84ef-4993-b1e7-b7d5ecf71d1f",
    "owner": {
         "firstName": "John",
            "lastName": "Doe",
            "email": "john.doe@digitalriver.com",
            "phoneNumber": "000-000-0000",
            "address": {
                "line1": "6 Chome-10-1 Roppongi, Minato",
                "state": "Tokyo",
                "postalCode": "106-0032",
                "country": "JP"
            }
        },
        "konbini": {
            "storeId": "010"
        }
}
 
  
digitalriver.createSource(data).then(function(result) {
    if (result.error) {
        //handle errors
    } else {
        var source = result.source;
        //send source to back end
        sendToBackend(source);
    }
});
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Option 2. Using DigitalRiver.js to create your own Konbini display

If you decide that you do not want to use the out of the box functionality provided with the Konbini element, you may also use the `digitalriver.retrieveKonbiniStores()` method which will allow you to build your own experience.

### Retrieving available stores

DigitalRiver.js exposes a method that allows you to retrieve the available stores where Konbini is accepted. If stores are available, the response returns an array of objects. If stores are not available, the response returns an empty array.

{% tabs %}
{% tab title="Example" %}
{% code overflow="wrap" %}
```javascript
digitalriver.retrieveKonbiniStores().then(function(response) {
    //use the returned values to create your own display
});
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Retrieved stores

{% tabs %}
{% tab title="Example" %}
{% code overflow="wrap" %}
```javascript
[{
    "storeId": "010",
    "storeName": "Seven Eleven",
    "localizedStoreName": "セブン‐イレブン",
    "storeLogoUrl": "https://ui1.img.digitalrivercontent.net/Storefront/images/Konbini/pmt_seven11.gif"
}, {
    "storeId": "030",
    "storeName": "Family Mart",
    "localizedStoreName": "ファミリーマート",
    "storeLogoUrl": "https://ui1.img.digitalrivercontent.net/Storefront/images/Konbini/pmt_familymart.gif"
}, {
    "storeId": "060",
    "storeName": "Lawson",
    "localizedStoreName": "ローソン／ミニストップ",
    "storeLogoUrl": "https://ui1.img.digitalrivercontent.net/Storefront/images/Konbini/pmt_lawson3.gif"
}, {
    "storeId": "080",
    "storeName": "Daily Store",
    "localizedStoreName": "デイリーヤマザキ／ヤマザキデイリーストアー",
    "storeLogoUrl": "https://ui1.img.digitalrivercontent.net/Storefront/images/Konbini/pmt_dailystore4.gif"
}]
```
{% endcode %}
{% endtab %}
{% endtabs %}

You can use the retrieved stores to build an experience suitable for your needs.

{% tabs %}
{% tab title="Example" %}
{% code overflow="wrap" %}
```javascript
<select>
    <option value="010">セブン‐イレブン</option>
    <option value="030">ファミリーマート</option>
    <option value="060">ローソン／ミニストップ</option>
    <option value="080">デイリーヤマザキ／ヤマザキデイリーストアー</option>
</select>
```
{% endcode %}
{% endtab %}
{% endtabs %}

Once you reached a point in your flow where the customer has selected a store, you can use the `createSource` function to assemble and pass the data to Digital River to create your payment.

{% hint style="info" %}
**Additional Fields Required**: If you are creating a Konbini source without using the DigitalRiver.js Konbini element, you are required to pass an additional field `storeId`.
{% endhint %}

| Key       | Value Description                                                         |
| --------- | ------------------------------------------------------------------------- |
| `storeId` | The identifier of the store where the customer will submit their payment. |

{% tabs %}
{% tab title="Example" %}
{% code overflow="wrap" %}
```javascript
var sourceData = {
        "type": "konbini",
        "sessionId": "ea03bf6f-84ef-4993-b1e7-b7d5ecf71d1f",
        "owner": {
            "firstName": "John",
            "lastName": "Doe",
            "email": "john.doe@digitalriver.com",
            "phoneNumber": "000-000-0000",
            "address": {
                "line1": "6 Chome-10-1 Roppongi, Minato",
                "state": "Tokyo",
                "postalCode": "106-0032",
                "country": "JP"
            }
        },
        "konbini": {
            "storeId": "010"
        }
 
        digitalriver.createSource(sourceData).then(function(result) {
            if (result.error) {
                //handle errors
            } else {
                var source = result.source;
                //send source to back end
                sendToBackend(source);
            }
        });
```
{% endcode %}
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Source example" %}
{% code overflow="wrap" %}
```javascript
{
    "clientId": "gc",
    "channelId": "drdod15",
    "liveMode": false,
    "id": "6900dc7e-1860-46bf-a353-0a6c82092ee9",
    "sessionId": "ea03bf6f-84ef-4993-b1e7-b7d5ecf71d1f",    
    "clientSecret": "6900dc7e-1860-46bf-a353-0a6c82092ee9_4ddc9a11-fd91-46e4-b572-d5727ffb5e2a",
    "type": "konbini",
    "reusable": false,
    "owner": {
        "firstName": "John",
        "lastName": "Doe",
        "email": "john.doe@digitalriver.com",
        "phoneNumber": "000-000-0000",
        "address": {
            "line1": "6 Chome-10-1 Roppongi, Minato",
            "state": "Tokyo",
            "country": "JP",
            "postalCode": "106-0032"
        }
    },
    "amount": "217.72",
    "currency": "JPY",
    "state": "pending_funds",
    "creationIp": "209.87.180.5",
    "createdTime": "2020-01-08T17:37:04.562Z",
    "updatedTime": "2020-01-08T17:37:04.64Z",
    "expirationTime": "2020-02-07T17:37:04.562Z",
    "flow": "receiver",
    "konbini": {
        "storeId": "010",
        "receiptNumber": "7210246313380",
        "printableInvoiceUrl": "http://payment.sej.co.jp:580/od/hi.asp?50100210246313380cf550a4fde12162",
        "storeName": "Seven Eleven",
        "localizedStoreName": "セブン‐イレブン",
        "storeLogoUrl": "https://ui1.img.digitalrivercontent.net/Storefront/images/Konbini/pmt_seven11.gif"
    }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Step 3: Use the Konbini source

Once created, the Konbini source will be in a `pending_funds` state.  Attach the source to a cart.  Once attached, you may submit your order.&#x20;

The following example shows how to [attach a payment method to an order or cart](../../../sources/#attaching-a-payment-method-to-an-order-or-cart).

{% tabs %}
{% tab title="POST /v1/shoppers/me/carts/active/apply-payment-method" %}
{% code overflow="wrap" %}
```javascript
{
  "paymentMethod": {
    "sourceId": "e7ba0595-059c-460c-bad8-2812123b9313"
  }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Step 4: After submitting the order

Once the order has been submitted, the source remains in a `pending_funds` state. At this point, direct your customer to go to the store they chose and pay the invoice. These details are reflected in the `konbini` block of the payment source.

| Field                 | Description                                                                              |
| --------------------- | ---------------------------------------------------------------------------------------- |
| `receiptNumber`       | The customer's receipt number.                                                           |
| `printableInvoiceUrl` | A URL that links to a printable invoice that can be brought into the store while paying. |
| `storeName`           | The name of the store where the customer will submit their payment.                      |
| `localizedStoreName`  | The localized name of the store where the customer will submit their payment.            |
| `storeLogoUrl`        | The logo of the store where the customer will submit their payment.                      |
