---
description: Learn how to submit an order for a Private Store.
---

# Submitting an order for a private store

{% hint style="info" %}
**Prerequisite**: A user with the role of a Private Store Manager in Global Commerce must enable Private Stores in Site Settings. See [Private Stores](https://help.digitalriver.com/help/gc/Administration/Site/Configuring-site-settings.htm) under [Configuring site settings](https://help.digitalriver.com/help/gc/Administration/Site/Configuring-site-settings.htm) in the Global Commerce Help for more information.
{% endhint %}

The following information describes how to submit an order to a Public Store, Private Store, or Friends and Family.

To submit an order for a Private Store:

* [Step 1: Get a limited access token](submitting-an-order-for-a-private-store.md#step-1-get-a-limited-access-token)
* [Step 2: Enable the Private Store](submitting-an-order-for-a-private-store.md#step-2-enable-the-private-store)
* [Step 3: Buy a product](submitting-an-order-for-a-private-store.md#step-3-buy-a-product)
* [Step 4: Update the billing and shipping address](submitting-an-order-for-a-private-store.md#step-4-update-the-billing-and-shipping-address)
* [Step 5: Submit the cart](submitting-an-order-for-a-private-store.md#step-5-submit-the-cart)

## Step 1: Get a limited access token

{% tabs %}
{% tab title="Request" %}
{% code overflow="wrap" %}
```http
POST /oauth20/token?grant_type=password&sessionToken={{session_token}}
Authorization: {{apikey_secret_authr}}
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Step 2: Enable the private store

You can apply a Private Store to either a limited access token or a full access token.

An access method determines how a shopper can access the pricing for a purchase plan. The following list describes the available access methods from most restrictive to least restrictive:

* **Email Address**—The shopper must use their email address to access the Private Store.
* **Email Domain**—The shopper’s email address must use one of the domains you specified entered for the Private Store. A domain is the end of the email address, such as the "digitalriver.com" in "jane.doe@digitalriver.com."
* **Email Invitation**—The shopper can join the Private Store through an email forwarded to them from someone they know. The person who sent the invitation has to approve invite if the shopper places an order. A Private Store that uses this access method is also called "friends and family" plan.
* **Generic Identifier**—The shopper must enter a name and a PIN created for the Private Store. Private Stores can have multiple names and PIN combinations used to access the plan.
* **IP Address**—The shopper must be on a network using a specific IP address or an IP address within a defined range.
* **Referral URL**—The shopper must click a link to access the Private Store.
* **Bypass Access Method**—Use this option when you don't want to specify the access method parameter. The `bypassAccessRuleType` can be any within `EmailAddress`, `EmailDomain`, `EmailInvitation`,  or `IpAddress`.

You can use one of the following options as the authorization method in the request body for a Private Store:

{% tabs %}
{% tab title="Email address example" %}
```javascript
{
    "purchasePlanAuthorize": {
        "id": "126668174",
        "targetMarketId": "126690174",
        "emailAddress": "chiliu@digitalriver.com"
    }
}
```
{% endtab %}

{% tab title="Email domain example" %}
```javascript
{
    "purchasePlanAuthorize": {
        "id": "101558174",
        "targetMarketId": "101580174",
        "emailDomain": "digitalriver.com"
    }
}
```
{% endtab %}

{% tab title="IP address example" %}
```javascript
{
    "purchasePlanAuthorize": {
        "id": "101558174",
        "targetMarketId": "101580174",
        "ipAddress": "1.2.3.4"
    }
}
```
{% endtab %}

{% tab title="Email invitation example" %}
```
{
    "purchasePlanAuthorize": {
        "id": "126668274",
        "targetMarketId": "126690274",
        "emailInvitationAddress": "chiliu@digitalriver.com",
        "emailInvitationPin": "I2wbfVSg"
    }
}
```
{% endtab %}

{% tab title="Return URL example" %}
```javascript
{
    "purchasePlanAuthorize": {
        "id": "101558174",
        "targetMarketId": "101580174",
        "referralUrl": "http://aaa.bbb.ccc.ddd"
         
    }
}
```
{% endtab %}

{% tab title="Bypass access method example" %}
```javascript
{
    "purchasePlanAuthorize": {
        "id": "101558174",
        "targetMarketId": "101580174",
        "bypassAccessRuleType": "EmailAddress"
    }
}
```
{% endtab %}
{% endtabs %}

If you view the session, you will see the extended attributes for `marketID` and `purchasePlanID`.

## Step 3: Buy a product

Once you've added a product to a cart, notice the discounts under `pricing` and the `PURCHASEPLAN_INCENTIVE_TOTAL` value under extended attributes.

{% tabs %}
{% tab title="Request" %}
{% code overflow="wrap" %}
```http
POST /shoppers/me/carts/active?productId=107845474&quantity=2
Authorization: bearer {{access_token}}
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Step 4: Update the billing and shipping address

{% tabs %}
{% tab title="Request" %}
```javascript
POST /shoppers/me/carts/active.json
Authorization: bearer {{access_token}}
```
{% endtab %}

{% tab title="Payload" %}
{% code overflow="wrap" %}
```json
{
    "cart": {
        "billingAddress": {
            "firstName": "Anita",
            "lastName": "Liu",
            "emailAddress":"chiliu@digitalriver.com",
            "companyName": null,
            "line1": "10380 Bren Rd",
            "line2": null,
            "line3": null,
            "city": "Taipei",
            "countrySubdivision": "MN",
            "postalCode": "10682",
            "country": "US"
        },
        "shippingAddress": {
            "firstName": "Anita",
            "lastName": "Liu",
            "emailAddress":"chiliu@digitalriver.com",
            "companyName": null,
            "line1": "10380 Bren Rd",
            "line2": null,
            "line3": null,
            "city": "Taipei",
            "countrySubdivision": "MN",
            "postalCode": "10682",
            "country": "US"
        }
    }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Step 5: Submit the cart

{% tabs %}
{% tab title="Request" %}
```http
POST /shoppers/me/carts/active/submit-cart.json
Authorization: bearer {{access_token}}
```
{% endtab %}
{% endtabs %}
