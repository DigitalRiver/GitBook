---
description: >-
  Learn how to provide ship from and ship to information for products in your
  cart.
---

# Providing address information

The [Cart ](https://docs.digitalriver.com/commerce-api/cart)resource contains attributes that allow you to set the shopper's billing and shipping addresses. Digital River then uses the values to determine the correct business entity and process your order.&#x20;

## Basic address information

The following table describes each parameter in a `billingAddress`, and `shippingAddress` :

| Parameter            | Description                                                                                                                                                                     |
| -------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `nickName`           | The name the customer prefers.                                                                                                                                                  |
| `firstName`          | The customer's first name.                                                                                                                                                      |
| `lastName`           | The customer's last name.                                                                                                                                                       |
| `companyName`        | The company's name.                                                                                                                                                             |
| `line1`              | The first line of the address.                                                                                                                                                  |
| `line2`              | The second line of the address.                                                                                                                                                 |
| `line3`              | The third line of the address.                                                                                                                                                  |
| `city`               | The city of the address.                                                                                                                                                        |
| `countrySubdivision` | The [state](providing-address-information.md#us-states-and-territories), county, province, or region.                                                                           |
| `postalCode`         | <p>The country's <a href="providing-address-information.md#postal-codes">postal code</a>. </p><p></p>                                                                           |
| `country`            | A two-letter [Alpha-2 country code](https://www.iban.com/country-codes) as described in the [ISO 3166](https://www.iso.org/iso-3166-country-codes.html) international standard. |
| `countryName`        | The country's name.                                                                                                                                                             |
| `phoneNumber`        | The customer's phone number.                                                                                                                                                    |
| `countyName`         | The name of the county.                                                                                                                                                         |
| `emailAddress`       | The customer's email address.                                                                                                                                                   |
| `phoneticFirstName`  | The [phonetic spelling of the customer's first name](providing-address-information.md#japanese-phonetics-and-divisions) in Katakana.                                            |
| `phoneticLastName`   | The[ phonetic spelling of the customer's last name](providing-address-information.md#japanese-phonetics-and-divisions) in Katakana.                                             |
| `division`           | The name of the [division within the organization](providing-address-information.md#japanese-phonetics-and-divisions) within a Japanese company.                                |

{% tabs %}
{% tab title="Billing address example" %}
{% code overflow="wrap" %}
```json
 {
  "cart": {
        "billingAddress": {
            "uri": "http://dispatch-test.digitalriver.com/v1/shoppers/me/carts/active/billing-address",
            "id": "billingAddress",
            "firstName": "e2000699-72a7-4f39-ba6d-2e5a1c913b5d",
            "lastName": "DR",
            "companyName": null,
            "line1": "8251 Flying Cloud Drive",
            "line2": "Suite 100",
            "line3": null,
            "city": "London",
            "countrySubdivision": "AL",
            "postalCode": "SE5 9JH",
            "country": "GB",
            "countryName": "Great Britain",
            "phoneNumber": "+44 20 7274 9987",
            "countyName": null,
            "emailAddress": "shopxTest@digitalriver.com",
            "phoneticFirstName": null,
            "phoneticLastName": null,
            "division": null,
            "suggestions": {
                "uri": "http://dispatch-test.digitalriver.com/v1/shoppers/me/carts/active/billing-address/suggestions",
                "address": [
                    {
                        "uri": "http://dispatch-test.digitalriver.com/v1/shoppers/me/carts/active/billing-address/suggestions/1",
                        "applyAddress": {
                            "uri": "http://dispatch-test.digitalriver.com/v1/shoppers/me/carts/active/apply-billing-address?suggestionid=1"
                        },
                        "id": 1,
                        "firstName": "null",
                        "lastName": "null",
                        "line1": "8251 Flying Cloud Drive Suite 100",
                        "line2": "Suite 100",
                        "city": "Al",
                        "countrySubdivision": null,
                        "postalCode": "SE5 9JH",
                        "country": "GB",
                        "phoneNumber": "null"
                    }
                ]
            }
        },
    }
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Japanese phonetics and divisions

For Japanese addresses, customers can provide their division within their organization (for example, the sales department). Additionally, a customer can enter their name in two scripting styles: Hiragana and Katakana. Hiragana is the traditional script, while Katakana is the phonetic spelling. Customer and courier services often want phonetic spelling so they can correctly pronounce the customer's name when making a delivery. Katakana is also used by foreigners living in the country who don't have a Japanese name.

Digital River provides the ability to enter a phonetic name for a Japanese customer and a division in the `billingAddress` and `shippingAddress` objects.

Phonetic names stored in the required billing address will appear on the Order Summary page.

#### Add phonetics and divisions

To add phonetics to your billing and shipping addresses, add the following attributes:

`"phoneticFirstName": "タロ",`\
`"phoneticLastName": "ヤマダ",`\
`"division": "営業部"`

To the following resources:

* [`POST /shoppers/me/carts/active`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Carts/paths/\~1v1\~1shoppers\~1me\~1carts\~1active/post) – Update the billing address and shipping address in the cart.
* [`PUT /shoppers/me/carts/active/billing-address`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Billing-Address/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1billing-address/put) – Update billing address independently.
* [`PUT /shoppers/me/carts/active/shipping-address`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Shipping-Address/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1shipping-address/put) – Update shipping address independently.

After you implement phonetic names, you will see the new fields under the billing or shipping address in the response. For example:

* [`GET /shoppers/me/carts/active/billing-address`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Billing-Address/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1billing-address/get) – Get the billing address for a cart.
* [`GET /shoppers/me/carts/active/shipping-address`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Shipping-Address/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1shipping-address/get) – Get the shipping address for a cart.
* Submit cart response

{% tabs %}
{% tab title="Phonetics and division example" %}
{% code overflow="wrap" %}
```json
 {
  "cart": {
    "billingAddress": {
                             "nickname": "Home",
                              "firstName": "太郎",
                              "lastName":"山田",
                              "line1":"新宿区新宿1-1-1",
                              "line2":"新宿ビル203",
                              "line3":"line3",
                              "countrySubdivision":"愛知県",
                              "country":"JP",
                              "countryName":"Japan",
                              "phoneNumber":"03-1234-1234",
                              "city":"田原市",
                              "postalCode": "123-1234",
                              "companyName":"Digitalriver",
                              "emailAddress": "shopxTest@digitalriver.com",
                              "phoneticFirstName": "タロ",
                              "phoneticLastName":"ヤマダ",
                              "division": "営業部"
                                
    },
    "shippingAddress": {
                             "nickname": "Home",
                              "firstName": "太郎",
                              "lastName":"山田",
                              "line1":"新宿区新宿1-1-1",
                              "line2":"新宿ビル203",
                              "line3":"line3",
                              "countrySubdivision":"愛知県",
                              "country":"JP",
                              "countryName":"Japan",
                              "phoneNumber":"03-1234-1234",
                              "city":"田原市",
                              "postalCode": "123-1234",
                              "companyName":"Digitalriver",
                              "emailAddress": "shopxTest@digitalriver.com",
                              "phoneticFirstName": "タロ",
                              "phoneticLastName":"ヤマダ",
                              "division": "営業部"   
    }
  }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

## US states and territories

The following lists the enumerated two-letter `state` values. Digital River uses these values to represent [states](providing-address-information.md#us-states), [territories](providing-address-information.md#us-territories), [APO/FPO military addresses](providing-address-information.md#us-apo-fpo-military-addresses), and the [District of Columbia](providing-address-information.md#us-federal-district). When you specify one of these `state` enumerations in a request, you must also provide `US` as the `country` parameter.

### US  states

| Two-letter Abbreviation | State Name     |
| ----------------------- | -------------- |
| AK                      | Alaska         |
| AL                      | Alabama        |
| AR                      | Arkansas       |
| AZ                      | Arizona        |
| CA                      | California     |
| CO                      | Colorado       |
| CT                      | Connecticut    |
| DE                      | Delaware       |
| FL                      | Florida        |
| GA                      | Georgia        |
| HI                      | Hawaii         |
| IA                      | Iowa           |
| ID                      | Idaho          |
| IL                      | Illinois       |
| IN                      | Indiana        |
| KS                      | Kansas         |
| KY                      | Kentucky       |
| LA                      | Louisiana      |
| MA                      | Massachusetts  |
| MD                      | Maryland       |
| ME                      | Maine          |
| MI                      | Michigan       |
| MN                      | Minnesota      |
| MO                      | Missouri       |
| MS                      | Mississippi    |
| MT                      | Montana        |
| NC                      | North Carolina |
| ND                      | North Dakota   |
| NE                      | Nebraska       |
| NH                      | New Hampshire  |
| NJ                      | New Jersey     |
| NM                      | New Mexico     |
| NV                      | Nevada         |
| NY                      | New York       |
| OH                      | Ohio           |
| OK                      | Oklahoma       |
| OR                      | Oregon         |
| PA                      | Pennsylvania   |
| RI                      | Rhode Island   |
| SC                      | South Carolina |
| TN                      | Tennessee      |
| TX                      | Texas          |
| UT                      | Utah           |
| VT                      | Vermont        |
| WA                      | Washington     |
| WV                      | West Virginia  |
| WY                      | Wyoming        |

### US federal district

| Two-letter Abbreviation | Federal District     |
| ----------------------- | -------------------- |
| DC                      | District of Columbia |

### US territories

| Two-letter Abbreviation | Territories              |
| ----------------------- | ------------------------ |
| AS                      | American Samoa           |
| GU                      | Guam                     |
| MP                      | Northern Mariana Islands |
| PR                      | Puerto Rico              |
| VI                      | U.S. Virgin Islands      |

### US APO/FPO military addresses

| Two-letter Abbreviation | APO/FPO Military Addresses |
| ----------------------- | -------------------------- |
| AE                      | Armed Forces               |
| AP                      | Armed Forces Pacific       |
| AA                      | Armed Forces America       |

## Postal codes

A postal code is a series of letters, digits, or both, sometimes including spaces or punctuation, in a postal address. The postal code format varies by country. Countries throughout the world use postal codes for sorting mail. The [US ZIP Code](providing-address-information.md#us-zip-code-and-geocode) is a type of postal code.

### US ZIP Code and geocode

A ZIP Code is a group of five or nine numbers added to a postal address to assist in the sorting of mail. The five-digit ZIP Code represents the US's destination post office or delivery area. The geocode consists of the last four digits of a full nine-digit ZIP Code representing a specific delivery route within that overall delivery area. Some US states use ZIP Codes and geocodes to determine taxes. This enhancement caters to states' tax calculation requirements relying on geocodes and ZIP Codes. It will greatly benefit users in states where both ZIP Codes and geocodes are crucial for accurate tax calculation.

#### How it works

To enable the postalCode feature, enter the [ZIP Code and geocode](https://tools.usps.com/zip-code-lookup.htm) in the following format: "xxxxx-yyyy," where the first five-digits represent the ZIP Code and the last four digits represent the geocode. Digital River uses this format when calculating taxes, resulting in more precise results.

{% tabs %}
{% tab title="Request body/response body" %}
{% code overflow="wrap" %}
```javascript
"billingAddress": {
  "postalCode": “12345-6789”,
  "country": "US"
}

"shippingAddress": {
  "postalCode": “12345-6789”,
  "country": "US"
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

{% hint style="info" %}
A US shopper can provide just their five-digit ZIP Code without impact. However, we recommend providing the ZIP Code and geocode to ensure the correct tax calculation.
{% endhint %}

#### Validation for US locales

If a shopper tries to enter their ZIP Code and geocode using the wrong format, such as entering the nine digits without a dash (123456789) or with a misplaced dash (for example, 1-23456789), Digital River will throw a 409 Conflict [`invalid-postal-code`](../../../common-shopper-and-admin-apis/error-codes/error-codes-for-shopper-apis/409-conflict.md#invalid-postal-code) that shows the correct format.

#### Validation for non-US locales

No changes or validations are introduced for non-US locales so that this update won't disrupt or alter the behavior of users operating in non-US regions.
