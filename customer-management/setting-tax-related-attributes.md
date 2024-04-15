---
description: Learn how to set the customer type, tax certificates, and tax identifiers.
---

# Setting up tax exemptions

As part of the process of configuring tax exemptions, you can set a customer's [type](setting-tax-related-attributes.md#customer-type), along with arrays of [tax identifiers](setting-tax-related-attributes.md#tax-identifiers) and [tax certificates](setting-tax-related-attributes.md#tax-certificates)

## Customer type

For details on how a[ customer's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Customers) `type` is used to calculate taxes, refer to the [Setting the customer type](../integration-options/checkouts/creating-checkouts/setting-the-customer-type.md) page.

## Tax identifiers (legacy) <a href="#tax-identifiers" id="tax-identifiers"></a>

{% hint style="warning" %}
In versions `2020-12-17` and earlier, use the legacy features described in this section to manage tax identifiers. If you're on versions `2021-02-23` and later, refer to the [Tax identifiers](../integration-options/checkouts/creating-checkouts/tax-identifiers.md) page.
{% endhint %}

Some customers have tax identifiers that allow them to purchase zero-rated goods. If you want to allow customers to apply tax identifiers to their purchases, your integration must first [add the tax identifier to the customer's record](setting-tax-related-attributes.md#adding-tax-identifiers-to-customers). Once that operation is successfully completed, Digital River automatically attaches the tax identifier to the transaction whenever the customer creates an applicable [registered checkout](../integration-options/checkouts/creating-checkouts/using-the-checkout-identifier.md#registered-checkouts-or-invoices).

### Adding tax identifiers to customers

When you [create](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createCustomers) or [update](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/updateCustomers) a [customer](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Customers), you can add one or more `taxIdentifiers[]`. For each tax identifier you want to add, specify a `type` and a `value`. The [enumerated `type` values](../integration-options/checkouts/creating-checkouts/tax-identifiers.md#supported-tax-identifiers) typically consist of a lowercase, two-letter country code. This `value` is dependent on the format used in each country.

{% hint style="info" %}
You can use the [tax identifier element](../developer-resources/reference/elements/tax-identifier-element.md) to validate customer-supplied data.
{% endhint %}

The following shows how to add multiple tax identifiers in a [`POST/customers/{id}`](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Customers/operation/updateCustomers) request:

{% tabs %}
{% tab title="POST/customers/{id}" %}
```
curl --location --request POST 'https://api.digitalriver.com/customers/987654321' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer <API_key>' \
--data-raw '{
    "taxIdentifiers": [
        {
            "type": "uk",
            "value": "GB243609761"
        },
        {
            "type": "nl",
            "value": "NL002458380B62"
        }
    ]
}'
```
{% endtab %}
{% endtabs %}

The response returns `taxIdentifiers[]` that are now saved to the customer's record:

{% tabs %}
{% tab title="Customer" %}
```javascript
{
    "id": "987654321",
...
    "taxIdentifiers": [
        {
            "type": "uk",
            "value": "GB243609761"
        },        
        {
            "type": "nl",
            "value": "NL002458380B62"
        }
    ],
...
}
```
{% endtab %}
{% endtabs %}

### Replacing a tax identifier

A [customer](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Customers) can't have multiple `taxIdentifiers[]` of the same `type`. So, if you'd like to attach a new tax identifier to a [customer](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Customers) and it has the same `type` as a saved tax identifier, you must first delete the existing object.

To do this, submit a `POST/customers/{id}` request and set the `value` you'd like to replace to `""`.

{% hint style="success" %}
&#x20;Make sure you format `value` without white spaces.
{% endhint %}

{% tabs %}
{% tab title="POST/customers/{id}" %}
```
curl --location --request POST 'https://api.digitalriver.com/customers/987654321' \
--header 'Authorization: Bearer <API_key>' \
--header 'Content-Type: application/json' \
--data-raw '{
    "taxIdentifiers": [
        {
            "type": "nl",
            "value": ""
        }
      ]
}'
```
{% endtab %}
{% endtabs %}

Then submit another `POST/customers/{id}` request with the original `type` and an updated `value`:

{% tabs %}
{% tab title="POST/customers/{id}" %}
```
curl --location --request POST 'https://api.digitalriver.com/customers/987654321' \
--header 'Authorization: Bearer <API_key>' \
--header 'Content-Type: application/json' \
--data-raw '{
    "taxIdentifiers": [
        {
            "type": "nl",
            "value": "NL001868214B01"
        }
      ]
}'
```
{% endtab %}
{% endtabs %}

### Supported tax identifiers

For a complete list, refer to the [supported tax identifiers](../integration-options/checkouts/creating-checkouts/tax-identifiers.md#supported-tax-identifiers) section on the [Tax identifiers](../integration-options/checkouts/creating-checkouts/tax-identifiers.md) page

## Tax certificates

You can build your integration so [eligible customers](setting-tax-related-attributes.md#what-customers-are-eligible) with [valid tax certificates](setting-tax-related-attributes.md#how-we-validate-tax-certificates) can make tax-exempt purchases.

To configure certificates for use in [eligible transactions](setting-tax-related-attributes.md#what-transactions-are-eligible), you must:

* [Collect tax exemption information from customers](setting-tax-related-attributes.md#collecting-tax-certificate-information)
* [Create a tax certificate file](setting-tax-related-attributes.md#creating-tax-certificate-files)&#x20;
* [Add the certificate to the customer](setting-tax-related-attributes.md#adding-a-tax-certificate)&#x20;

Digital River also allows you to [associate multiple tax certificates with a single customer](setting-tax-related-attributes.md#adding-multiple-tax-certificates-to-a-customer).

### What customers are eligible

Usually, customers who want to use a tax certificate must be a government agency, non-profit organization, or a product reseller based in the United States.

In the US, almost all end users of a product are taxed. The primary exceptions are government agencies and not-for-profits. Businesses are typically only tax-exempt when reselling a product.

### What transactions are eligible

In the Digital River APIs, tax certificates can only be used in [registered checkouts](../integration-options/checkouts/creating-checkouts/using-the-checkout-identifier.md#registered-checkouts-or-invoices) and [registered checkout-sessions](../developer-resources/digital-river-api-reference/checkout-sessions.md#registered-customers). Additionally, the [customer's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Customers) record must contain a valid `taxCertificates[]` whose [`taxAuthority`](setting-tax-related-attributes.md#tax-authority) matches the transaction's `shipTo.address.state` or `billTo.address.state`. If the purchase contains [physical products](../product-management/creating-and-updating-skus.md#how-products-are-specified-as-physical-or-digital), Digital River compares `taxAuthority` to [`shipTo.address.state`](../integration-options/checkouts/creating-checkouts/providing-address-information.md#ship-to-address). In transactions that only contain [digital goods](../product-management/creating-and-updating-skus.md#how-products-are-specified-as-physical-or-digital), we compare `taxAuthority` to [`billTo.address.state`](../integration-options/checkouts/creating-checkouts/providing-address-information.md#bill-to-address).

For example, the following [customer](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Customers) has [multiple tax certificates](setting-tax-related-attributes.md#adding-multiple-tax-certificates-to-a-customer). Since the `taxAuthority` of one is `MN` and the other is `WI`, if this customer requests to have physical products shipped to Minnesota or Wisconsin, that transaction is tax-exempt. However, if the customer specifies a shipping address other than these two states, Digital River applies taxes.

{% tabs %}
{% tab title="Customer" %}
```javascript
{
    "id": "543790170336",
    ...
    "taxCertificates": [
        {
            "companyName": "Acme Inc",
            "taxAuthority": "MN",
            "startDate": "2021-04-07T00:00:00Z",
            "endDate": "2022-04-07T00:00:00Z",
            "fileId": "b87c6b64-e919-45d6-bf49-016bed76134a"
        },
        {
            "companyName": "Beta Inc",
            "taxAuthority": "WI",
            "startDate": "2021-04-07T00:00:00Z",
            "endDate": "2022-02-07T00:00:00Z",
            "fileId": "542d9a68-8eb4-4bda-b3fb-67b68e9f6846"
        }
    ],
    ...
}
```
{% endtab %}

{% tab title="Checkout (tax exempt)" %}
```javascript
{
    "id": "a3977c4e-948a-4ae8-b5c2-b5c5b052b0bd",
    ...
    "customerId": "543790170336",
    "currency": "USD",
    ...
    "shipTo": {
        "address": {
            "line1": "10380 Bren Road W",
            "city": "Minnetonka",
            "postalCode": "55343",
            "state": "MN",
            "country": "US"
        },
        ...
    },
    ...
    "totalAmount": 25.0,
    "subtotal": 25.0,
    "totalFees": 0.0,
    "totalTax": 0.0,
    "totalImporterTax": 0.0,
    "totalDuty": 0.0,
    "totalDiscount": 0.0,
    "totalShipping": 5.0,
    ...
}
```
{% endtab %}

{% tab title="Checkout (non-tax exempt)" %}
```javascript
{
    "id": "885ed72a-2237-496f-a6ef-4f1050053324",
    ...
    "customerId": "543790170336",
    "currency": "USD",
    ...
    "shipTo": {
        "address": {
            "line1": "2300 Southern Blvd",
            "city": "New York",
            "postalCode": "10460",
            "state": "NY",
            "country": "US"
        },
        ...
    },
    ...
    "totalAmount": 27.22,
    "subtotal": 25.0,
    "totalFees": 0.0,
    "totalTax": 2.22,
    "totalImporterTax": 0.0,
    "totalDuty": 0.0,
    "totalDiscount": 0.0,
    "totalShipping": 5.0,
    ...
}
```
{% endtab %}
{% endtabs %}

### How we validate tax certificates

Since Digital River is the [reseller of record](../general-resources/glossary.md#merchant-of-record-seller-of-record-mor-sor), we subject a [customer's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Customers) `taxCertificates[]` to a verification process. When customers supply their certificate during a checkout, we issue a temporary exemption for that individual transaction.

If we determine that a customer's document isn't a valid, state-accepted exemption certificate, we mark the account as in review. While in this state, certificates can't be used to make tax-exempt purchases.

We then email the customer to request additional documentation. If the customer fails to provide a valid certificate, we send another follow-up email. If that request doesn't produce the necessary documentation, we move the certificate into an unapproved state. This means it won't be applied to future transactions.

{% hint style="info" %}
On your site, we recommend that you inform customers that they might receive a follow-up email from Digital River requesting more information about their tax certificate.
{% endhint %}

On the other hand, if our review determines that a certificate is valid, we automatically apply a tax exemption to all future [eligible transactions](setting-tax-related-attributes.md#what-transactions-are-eligible). However, once the tax certificate's [`endDate`](setting-tax-related-attributes.md#start-and-end-dates) elapses, that exemption no longer applies.

No methods currently exist to query the APIs and determine the status of a tax certificate. Additionally, at this time, you can't subscribe to [webhook events](../order-management/events-and-webhooks-1/events-1/) that notify you when a certificate's state has been updated.

### Collecting tax certificate information

If your site intends to offer tax-exempt purchases, provide a form for customers to enter their certificate information. The form must contain fields that collect:

* The name of the company/organization/agency that was issued the tax exemption
* The name of the tax authority (i.e., the US state) that issued the certificate&#x20;
* The start and end dates of the tax exemption

You'll also need to give customers a way to upload a copy of their certificate. Restrict the format of the uploaded file to PDF, JPG, or PNG and its size to 10 MB or less.

<figure><img src="../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>

Certificates of exemption must be addressed to Digital River. This is because we act as the [reseller of record](../general-resources/glossary.md#merchant-of-record-seller-of-record-mor-sor). The correct address depends on the [selling entity](../integration-options/checkouts/creating-checkouts/selling-entities.md) that is facilitating the transaction. So, during the checkout process, use `sellingEntity.id` or `sellingEntity.name` to determine the appropriate address disclosure to display to customers:

| `sellingEntity.id` | `sellingEntity.name`  | Address disclosure                                                                                                               |
| ------------------ | --------------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| `DR_INC-ENTITY`    | `Digital River, Inc.` | <p>Please address exemption certificates to:</p><p>Digital River, Inc.</p><p>10380 Bren Road West</p><p>Minnetonka, MN 55343</p> |
| `C5_INC-ENTITY`    | `DR globalTech Inc.`  | <p>Please address exemption certificates to:</p><p>DR globalTech, Inc.</p><p>10380 Bren Road West</p><p>Minnetonka, MN 55343</p> |

After you collect the document, use it to [create a tax certificate file](setting-tax-related-attributes.md#creating-tax-certificate-files).

### Creating tax certificate files

Once customers upload their tax certificate, submit a [`POST /files`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createFiles) request to create a [file](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Files) in Digital River's system. In the request, make sure you define [`file`](../order-management/files-and-file-links-1/files.md#file-and-purpose) and set [`purpose`](../order-management/files-and-file-links-1/files.md#file-and-purpose) to `tax_document_customer_upload`.

From the response, retrieve `id` and use it to [add the tax certificate to the customer](setting-tax-related-attributes.md#adding-a-tax-certificate).

{% tabs %}
{% tab title="Request" %}
```json
curl --location --request POST 'https://api.digitalriver.com/files' \
--header 'Authorization: Bearer <Secret API key>' \
--header 'Cookie: incap_ses_1326_1638494=4ge4JL7HAx4pSa+KgOZmEkYOhWMAAAAAWIAkzLY4az9RKmTc8wx7Gg==; nlbi_1638494_2412637=cJ4AarfeUj2bpwP2iXZ5LAAAAAABc9D7iTv2m9SVHn69MYyb; visid_incap_1638494=a3up5REJQh+kLGuEgzmHj4ZpK2MAAAAAQUIPAAAAAABqxJXXizaCb2KT7rDTLZAM; visid_incap_2137235=YibR5HAMTw28J10M4p6Omyb+vWEAAAAAQUIPAAAAAADLOejzH/0oGlmJVXjAkh4Q' \
--data-raw '{
    "purpose": "tax_document_customer_upload",
    "fileName": "tax_certficate_John_Doe.pdf",
    "file": "JVBERi0xLjQKJeLjz9MKNCAwIG9iago8PC9Db2xvclNwYWNlWy9JbmRleGVkL0RldmljZVJHQiAyNTUoAAAAXGJcYlxiHBwcXClcKVwpQUFBXl5eh4eHra2twcHBzs7O1tbW3t7e5+fn7+/v9/f3AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAKV0vTWFzayBbMTUgMTUgXS9TdWJ0eXBlL0ltYWdlL0hlaWdodCAzOC9GaWx0ZXIvRmxhdGVEZWNvZGUvVHlwZS9YT2JqZWN0L1dpZHRoIDE1MC9MZW5ndGggNzI2L0JpdHNQZXJDb21wb25lbnQgOD4+c3RyZWFtCnic7VfJluMwCHy2WHTzJ/PrA2ixlUaJW37T04fhkDixDKUCSvg4/psa/2sAXwwRiCQvPUuEX/8EkYeQDgDnSVbYggKJhj8pHyzpESaC4nJld9BCXyEwGOmwP8DEdbMHTqligfhGPm9cVvDujvYHdQrNHQtNlohamA3ezkdOVIRenmnm7rN1ojT2xAuLchgm97qPs95xK18Tem+B6l03q03PXsgjnn8yddQJqudlUMcF1KQ0s7GUo7ssnR+UDhALPA604qblcz/TLjZQHOXvSl/qC6iBWlO+Y9jPjKk5qEOubLRrKm38IH0IXHfLU1BGyARUqG0N1DJTqghc6ZZpEWhsCu9iDMo5YlwWKmvcsl+a6pTi5RgUhycmSAG1zhS2ypwrusFONScv0EKtz772QfeReXWORtXOhXwjkfRDpIDa2kVHGzl1qLgOyntkAxcaQaqTCNkPqzVVH7t2YA3FFUgO6fVSg/Xuc6bMSVdn3gU2g2gdr19glyzS2mHsiGn/ZVo/kNmGqZcJDx1QSZob5WSMVRL3AUhY6rqU1ptPWdZn8zhm6LmSbXo02woZXkmWSCdOVNyw8pViquhBSalTtLNmUAMbC1CS0uN6uitTUglxSFj5a/EDryh1+hjpukueD4+jCLFHzpWfytTUAcdUFVmQa7fmDaQfG9pSCICI0Z7c53gWFzoOZQqOBupNMkJZl6p9uzFdvSdxUbTjh04wjEGmbeXQvq4H+pF2d6ypY5ZtDqoq+GAsVfsKTQhImdovAoAPFWdUXaZEraYXmVb/2zumIlQatcpuN1Jc75FcLUmmzmWS1/g6eJLMz8US8AWVr9/x02PvDOU8O+mLG8uEfHxVHbYCZX1OT2ThremcBTdeLal3GadPFfPcikDcWahqx5Rkf/LG9x1QN8OwCdF6Hd03B/UDcb5leDN7P2p4P3s/Z78xe1ZTy28Af9F+XfK+a38AgKXFTgplbmRzdHJlYW0KZW5kb2JqCjUgMCBvYmoKPDwvRmlsdGVyL0ZsYXRlRGVjb2RlL0xlbmd0aCA4MTE3Pj5zdHJlYW0KeJzNnVFzHNdxhd/xK6bKeZCrwuXee2dmd/NGk7Qkx6YlEYoriVMpCFgSawNYerEQxfz6zMydwRxKQM8503CV4sjhShie3q/7dt8eqk7+cfK705NUF6uqLk4vTl6fnnx7Eos/tH83FMvmP+1/rzaxOL0+ef77UIRlcfru5Ivfnv6t/dnxR5bF+TU+lJabYrWsF9UqPxmLdftg8/scTpaLWNf1qvjY/Koshr+++/Kzj4f3J1+83N/c7t7fbLfFm7Prbau5LN43f7W/R/Flo/XxgSD++3+a/3vRfYnHw4vhSaI7np0fi2+2h9v9zVNG18GLzvBe7A7FX84+/bC7uire3F3/sD08NUBvhG8vdx8+bA9PntyySkXtze7p/nh2Vfym2L8rvtltz7e3Tx6hF9/p9mr74XJ/s/0npLcLsHQG+M3+tmX4cn/xpOltT8cTpffLw/72tvjLdvf+8ljsbop/313tnzTRXazeRL/c390cD5+ePC5vfl/ujk8aVKgrf2Jf//Rhfzjubt4XL88Oh93THosuQve5Pfup+PpV8dcvXn/95q+/ffLwfqWnthkY/kP7T+x4bXy/woPahvVrO6dd81h7h//xsN0eixcXF4ft7ZP23BbZrze61Fy0681qsfrZlXrZ/fNW+w9//upN8Yc/v3n9dtD9pVTzRar2WzRS+cHmO/TyaVkt1utiFcri+qTalIuQug9XJ2/tx+r2x9qfvu4+1JvU/j6Tj3Vq9QbU2g8TjzU/Oaq1H0CNwlivJyiebm+b/J2ft0dyFsewGjE2PEiMYT1+r7AmIWapzLCXIhhaGaNLcRUsiCFWq7oKzQ+6SjFhKSbuiyX4YqsglKJa+F0pJihFUGNL0ab46rvi5dVue3MsSk8lJqzEaYphPX6trir5SlSL3koYv/B6x9zXNz/ud+fb4jdPved6A3t1dtwWedm9eOpRUplNMC7mVdzQ1bs6KKtl15G4OqixI1XKDKk2oFZN97/mJ0e19kM1p/8ls/8tl6laLZvffLmOz5bB1QUr7EsVd6gqPFRJ6YJiz+0aX4VdMGkwG0QTxTiPXlluxlIcLhjTpWgVx7RahdcZohS7GwxeZ9RSbOnV5hBJ9epZjPFZmaIPJBZGPV0YHcgEIGtqkMxMWwcSh3EtTpIOpHmmv0r/VcT/XLkY4lGup49yh61ChtRRnpmxDhse5Vo8yt2KYhbjyxeusZJwrHD3wRqvF1wJzhxiVsHz+MwS/NOf35x+9/rFH10QK/xa3DipcZxwNTgzZVbFk/euOAFxXdbLmffpOowEh31rmmCo4/idug8UwUENr+9s0T+SL56gvd3Vz0Jdbtbl2oVR/GKZHGLkNpNeDVcT9kr6SO+gMdr3mldfzTvIM79RRgb8uJtNr1bhSwbiZmNd6dnt2MZXVdWz/q/KsR5njA0PFuMaKK5ZiKuRYS9FMLQyRr/sMk/y9/NeFfbkEpKjXizU8GKBPL7zkmT0CpqcOUXenl0diz+e/X1b4FvyORQr/GrENFnDMFmzs2RewozBRVNc2e8JU/Fid2j/5K34bn924eEovgXtXrICx0rgKF4A8jtWnCWV/qbQft8Qn4f187icueL1b+/waxEvGsJ63Py7l4bCi0LxnaT1ToO/W9uluHzWVmN4Hos/vfj6TfG2uWm/Pi3e/MV12Rb/eMOqFPZqz6+X+c9PcOFj6jK0f2DcIgt5osXlunjWaBy2J+8Q+aruZt5qvVgl8yXoENWYi5f76+v9RdNXi1fb2/PD7sNxR/+LUuQUjpG9yeSvOQ78es0P/HoDUs2Hiaeanxy1ug+jGJGQsi67L1QvH0xIuaoWKc3LyPc3u2PxzWF3zv7ZvrXj1QnelUX2XVn/7frVsP1AZWJQ61IxqE2novnJUa37IKWiz2TbuR9KRYybRSiqdVqkjZiJr07fFm/PL7cXd1fb4nf+bMQIL9Ej/ebSKlVCLR+MDZuNuIFsdB+kbPTJLFYPH4wqrRdVNe9g5H8f7IlORhXxZPBvkY1aJdTyyaBzUWEuKjkX7U1h1Ty0qptcLH95MtJmsW6HfXNAqiEXzYV/TEZpz43t4XzXZKT/Qz0yJ+HxNl514WZA+dftF330ge7bNT+Yr0TNPK3sn+8EKhCobIGujHuF/GcvgwQzIEI+B9UjAyLGxWrmyP727uzmyP/7QlbDDnAImj7PjoeA4yHQ4yHAIRjUpg+BNYyIRKTKnNSpmVltIubMh/7fJSv27x5MxSjR/C6xyXW5WHZ/Rj39O//p7Obu3dn58e7wBK0uVZjlwGa5B9dfkCs2y4NaznKgs2zUFHMJ2JhZjpvN7OP2/eLNQvuXGc3pCrlIFX0FMIYyodblYlCbzoWVeXJZaUS6ZSX0Y0feHMTrfNYcN4dK2BwqlKq4zWHQ6j5U8nW13nTXVZ3O3EudETOhVqEaQagr0A1Uq0YoP96d5RmE5tW8FTOhVqHaNKF8qDZwwiRC/eMzCc3s0FbMhFqFatOE8gjYwDyQCPWPd9cvndDcm4oRM6FWoRpBqEa1WiZUe2po5qpvxUyoVag2TSjvZxtY1iRC/ePdKqsTmrvyGTETahWqEYSw61Vyp87xeQmpMWdRIFQqhEpUKzlCFRIq5VNWeU+ZWPe9KJwyitCgVqIaQcjIB9upK2+nVntnQEKBJhSA0KA2TcjKBzvtZ9fQzPnbi8K0pwgNaiWqEYSMfLA3xtmEZt7hInaGuGEJDWolqk0TsvLBbh2Vd+tQ94AsClsHR6hXK1FtmpCVD3Jrrbxbq7hKZs1xa6Xw9FIlShF0jFyQdEovHTHkrDnSSQKdhFKJo1MinSSfrtJ7utR6N2Im1BKqEYS6A4WnSyOUH3d2aLFnWjETagnVpgnlpowdWiLUP+6c8uLctWIm1BKqTRPKgx2nvESof9x5U1TvbkbMhFpCNYJQjWq1TKj21NDM+78VM6GWUG2aUF4wcNuQCPWPOzdWdYc0YibUEqoRhLDrVXKnzvF5CakxZ1EgFBVCEdUiRyghoSifsuQ9ZWLd96JwyihCg1pENYKQkQ+2Uydvp1Z7Z0BCgSYUgNCgNk3Iygc77WfX0Mz524vCtKcIDWoR1QhCRj7YG+NsQjPvcBE7Q9ywhAa1iGrThKx8sFtH8m4d6h6QRWHr4Aj1ahHVpglZ+SC31uTdWsVVMmuOWyuFp5eKKEXQMXJB0oleOmLIWXOkEwQ6AaUCRycinSCfrug9XWq9GzETagHVCELdgcLTpRHKjzs7tNgzrZgJtYBq04RyU8YOLRHqH3dOeXHuWjETagHVpgnlwY5TXiLUP+68Kap3NyNmQi2gGkGoRrVaJlR7amjm/d+KmVALqDZNKC8YuG1IhPrHnRurukMaMRNqAdUIQtj1KrlT5/i8hNSYsygQWiqElqi25AgFJLSUT1nwnjKx7ntROGUUoUFtiWoEISMfbKcO3k6t9s6AhAJNKAChQW2akJUPdtrPrqGZ87cXhWlPERrUlqhGEDLywd4YZxOaeYeL2BnihiU0qC1RbZqQlQ926wjerUPdA7IobB0coV5tiWrThKx8kFtr8G6t4iqZNcetlcLTSy1RiqBj5IKks/TSEUPOmvd0yg1Pp9yAVPuBobMEOiDGnq6l93Sp9W7EPK3WE8pqDKHuQMHpEgnlx50dWuyZVszTaplQr0YQyk0ZOrRGqH/cOeXFuWvFPK2WCfVqBKE82GHKa4T6x503RfXuZsQ8rdYTqmlCNarVMqHaU0Mz7/9WzNNqmVCvRhDKCwZsGxqh/nHnxqrukEbM02o9IbpTV9j1KrlT5/ichOSYsygQWiuE1qi2pgiNapvP1MhT1n4n1ylT674XhVNGERrU1qhGEDLyQXbq9ju5OrXcOwMSCjShAIQGtWlCVj7IaT+/hmbO314Upj1FaFBboxpByMgHeWOcT2jmHS5iZ4gbltCgtka1aUJWPsitoyPk2TrkPSCLwtbBEerV1qg2TcjKB7e1tl/JtbWqq2TWHLdWCk8vtUYpgo6RC5LO2ktHDDlrjnRWAp0VSq04Omuks5JP19p7utR6N2Im1FaoRhDqDhSeLo1QftzZocWeacVMqK1QbZpQbsrYoSVC/ePOKS/OXStmQm2FatOE8mDHKS8R6h933hTVu5sRM6G2QjWCUI1qtUyo9tTQzPu/FTOhtkK1aUJ5wcBtQyLUP+7cWNUd0oiZUFuhGkEIu14ld+ocn5eQGnMWBUKKpV2J/gYlZ2k3qm0+U2NP2cp7ysS670XhlCl2mCV6ZDCEjHywnXrl7dRq7wxIKNCEAhAa1DgXkcfywU772TU0c/72ojDtFTe1Er16GEJGPtgb42xCM+9wETtD3LCEBjX0eyIIWflgt46Vd+tQ94AsCluHYgRbomcYQcjKB7m1rrxbq7hKZs1xaxX8o0s0nGPoGLkg6Xg98tSQs+ZIR/DIK9HYoOScH0r0mytlj7zS65En17sRM6GG3hgMoe5A4emSPfJKr0ee2jOtmAk19FchCOWmjB1a9sibT2jm3LViJtTQo4cglAc7TnnZI6/0euTJdzcjZkINfZ4YQjWq1TKh2lNDM+//VsyEGnqFEYTygoHbhuwAV3o98uQd0oiZUEO/OYYQdr1K7tQ5Pi8hNeYsCoQUj7wS/Q1KziOvRI+8UvbIK70eeWrd96JwyhSPvBI9MhhCRj7YTu31yJN7Z0BCgSYUgNCgxrmIPJYPdtp7PfLU+duLwrRXPPJK9OphCBn5YG+MXo889Q4XsTPEDUtoUEO/J4KQlQ926/B65Ml7QBaFrUPxyCvRM4wgZOWD3Fq9HnnqKpk1x61V8Mgr0XCOoWPkgqTj9chTQ86aIx3BI69EY4OSc34o0W+ulD3ySq9HnlzvRsyEGnpjMIS6A4WnS/bIK70eeWrPtGIm1NBfhSCUmzJ2aNkjbz6hmXPXiplQQ48eglAe7DjlZY+80uuRJ9/djJgJNfR5YgjVqFbLhGpPDc28/1sxE2roFUYQygsGbhuyA1zp9ciTd0gjZkIN/eYYQtj1KrlT5/i8hNSYsygQUjzySvQ3KDmPvBI98krZI6/0euSpdd+LwilTPPJK9MhgCBn5YDu11yNP7p0BCQWaUABCgxrnIvJYPthp7/XIU+dvLwrTXvHIK9GrhyFk5IO9MXo98tQ7XMTOEDcsoUEN/Z4IQlY+2K3D65En7wFZFLYOxSOvRM8wgpCVD3Jr9Xrkqatk1hy3VsEjr0TDOYaOkQuSjtcjTw05a450BI+8Eo0NSs75oUS/uVL2yCu9HnlyvRsxE2rojcEQ6g4Uni7ZI6/0euSpPdOKmVBDfxWCUG7K2KFlj7z5hGbOXStmQg09eghCebDjlJc98kqvR558dzNiJtTQ54khVKNaLROqPTU08/5vxUyooVcYQSgvGLhtyA5wpdcjT94hjZgJNfSbYwhh16vkTp3j8xJSY86iQEjxyCvR36DkPPJK9MgrZY+80uuRp9Z9LwqnTPHIK9EjgyFk5IPt1F6PPLl3BiQUaEIBCA1qnIvIY/lgp73XI0+dv70oTHvFI69Erx6GkJEP9sbo9chT73ARO0PcsIQGNfR7IghZ+WC3Dq9HnrwHZFHYOhSPvBI9wwhCVj7IrdXrkaeukllz3FoFj7wSDecYOkYuSDpejzw15Kx5TycJHnkJjQ0S6fyAfnNJ9sgrvR55cr0bMU+rJfTGYAh1BwpOl0goP+7s0GLPtGKeVkvor0IQyk0ZOrRGqH/cOeXFuWvFPK2W0KOHIJQHO0x5jVD/uPOmqN7djJin1RL6PDGEalSrZUK1p4Zm3v+tmKfVEnqFEYTyggHbhkaof9y5sao7pBHztFpCvzmGEHa9Su7UOT4nITnmLAqEFI+8hP4GifPIS+iRl2SPvOT1yFPrvheFU6Z45CX0yGAIGfkgO3XyeuTJvTMgoUATCkBoUONcRB7LBznt59fQzPnbi8K0VzzyEnr1MISMfJA3xvmEZt7hInaGuGEJDWro90QQsvJBbh3J65En7wFZFLYOxSMvoWcYQcjKB7e1Jq9HnrpKZs1xaxU88hIazjF0jFyQdLweeWrIWXOkI3jkJTQ2SJzzQ0K/uSR75CWvR55c70bMhBp6YzCEugOFp0v2yEtejzy1Z1oxE2ror0IQyk0ZO7TskTef0My5a8VMqKFHD0EoD3ac8rJHXvJ65Ml3NyNmQg19nhhCNarVMqHaU0Mz7/9WzIQaeoURhPKCgduG7ACXvB558g5pxEyood8cQwi7XiV36hyfl5AacxYFQopHXkJ/g8R55CX0yEuyR17yeuSpdd+LwilTPPISemQwhIx8sJ3a65En986AhAJNKAChQY1zEXksH+y093rkqfO3F4Vpr3jkJfTqYQgZ+WBvjF6PPPUOF7EzxA1LaFBDvyeCkJUPduvweuTJe0AWha1D8chL6BlGELLyQW6tXo88dZXMmuPWKnjkJTScY+gYuSDpeD3y1JCz5khH8MhLaGyQOOeHhH5zSfbIS16PPLnejZgJNfTGYAh1BwpPl+yRl7weeWrPtGIm1NBfhSCUmzJ2aNkjbz6hmXPXiplQQ48eglAe7DjlZY+85PXIk+9uRsyEGvo8MYRqVKtlQrWnhmbe/62YCTX0CiMI5QUDtw3ZAS55PfLkHdKImVBDvzmGEHa9Su7UOT4vITXmLAqEFI+8hP4GifPIS+iRl2SPvOT1yFPrvheFU6Z45CX0yGAIGflgO7XXI0/unQEJBZpQAEKDGuci8lg+2Gnv9chT528vCtNe8chL6NXDEDLywd4YvR556h0uYmeIG5bQoIZ+TwQhKx/s1uH1yJP3gCwKW4fikZfQM4wgZOWD3Fq9HnnqKpk1x61V8MhLaDjH0DFyQdLxeuSpIWfNkY7gkZfQ2CBxzg8J/eaS7JGXvB55cr0bMRNq6I3BEOoOFJ4u2SMveT3y1J5pxUyoob8KQSg3ZezQskfefEIz564VM6GGHj0EoTzYccrLHnnJ65En392MmAk19HliCNWoVsuEak8Nzbz/WzETaugVRhDKCwZuG7IDXPJ65Mk7pBEzoYZ+cwwh7HqV3KlzfF5CasxZFAgpHnkJ/Q0S55GX0CMvyR55yeuRp9Z9LwqnTPHIS+iRwRAy8sF2aq9Hntw7AxIKNKEAhAY1zkXksXyw097rkafO314Upr3ikZfQq4chZOSDvTF6PfLUO1zEzhA3LKFBDf2eCEJWPtitw+uRJ+8BWRS2DsUjL6FnGEHIyge5tXo98tRVMmuOW6vgkZfQcI6hY+SCpOP1yFNDzpojHcEjL6GxQeKcHxL6zSXZIy95PfLkejdiJtTQG4Mh1B0oPF2yR17yeuSpPdOKmVBDfxWCUG7K2KFlj7z5hGbOXStmQg09eghCebDjlJc98pLXI0++uxkxE2ro88QQqlGtlgnVnhqaef+3YibU0CuMIJQXDNw2ZAe45PXIk3dII2ZCDf3mGELY9Sq5U+f4vITUmLMoEFI88hL6GyTOIy+hR16SPfKS1yNPrfteFE6Z4pGX0CODIWTkg+3UXo88uXcGJBRoQgEIDWqci8hj+WCnvdcjT52/vShMe8UjL6FXD0PIyAd7Y/R65Kl3uIidIW5YQoMa+j0RhKx8sFuH1yNP3gOyKGwdikdeQs8wgpCVD3Jr9Xrkqatk1hy3VsEjL6HhHEPHyAVJx+uRp4acNe/pRMEjL6KxQSSdH9BvLsoeecnrkSfXuxHztFpEbwyGUHeg4HSJhPLjzg4t9kwr5mm1iP4qBKHclKFDa4T6x51TXpy7VszTahE9eghCebDDlNcI9Y87b4rq3c2IeVotos8TQ6hGtVomVHtqaOb934p5Wi2iVxhBKC8YsG1ohPrHnRurukMaMU+rRfSbYwhh16vkTp3jcxKSY86iQEjxyIvobxA5j7yIHnlR9siLXo88te57UThlikdeRI8MhpCRD7JTR69Hntw7AxIKNKEAhAY1zkXksXyQ035+Dc2cv70oTHvFIy+iVw9DyMgHeWOcT2jmHS5iZ4gbltCghn5PBCErH+TWEb0eefIekEVh61A88iJ6hhGErHxwW2v0euSpq2TWHLdWwSMvouEcQ8fIBUnH65Gnhpw1RzqCR15EY4PIOT9E9JuLskde9HrkyfVuxEyooTcGQ6g7UHi6ZI+86PXIU3umFTOhhv4qBKHclLFDyx558wnNnLtWzIQaevQQhPJgxykve+RFr0eefHczYibU0OeJIVSjWi0Tqj01NPP+b8VMqKFXGEEoLxi4bcgOcNHrkSfvkEbMhBr6zTGEsOtVcqfO8XkJqTFnUSCkeORF9DeInEdeRI+8KHvkRa9Hnlr3vSicMsUjL6JHBkPIyAfbqb0eeXLvDEgo0IQCEBrUOBeRx/LBTnuvR546f3tRmPaKR15Erx6GkJEP9sbo9chT73ARO0PcsIQGNfR7IghZ+WC3Dq9HnrwHZFHYOhSPvIieYQQhKx/k1ur1yFNXyaw5bq2CR15EwzmGjpELko7XI08NOWuOdASPvIjGBpFzfojoNxdlj7zo9ciT692ImVBDbwyGUHeg8HTJHnnR65Gn9kwrZkIN/VUIQrkpY4eWPfLmE5o5d62YCTX06CEI5cGOU172yItejzz57mbETKihzxNDqEa1WiZUe2po5v3fiplQQ68wglBeMHDbkB3gotcjT94hjZgJNfSbYwhh16vkTp3j8xJSY86iQEjxyIvobxA5j7yIHnlR9siLXo88te57UThlikdeRI8MhpCRD7ZTez3y5N4ZkFCgCQUgNKhxLiKP5YOd9l6PPHX+9qIw7RWPvIhePQwhIx/sjdHrkafe4SJ2hrhhCQ1q6PdEELLywW4dXo88eQ/IorB1KB55ET3DCEJWPsit1euRp66SWXPcWgWPvIiGcwwdIxckHa9Hnhpy1hzpCB55EY0NIuf8ENFvLsoeedHrkSfXuxEzoYbeGAyh7kDh6ZI98qLXI0/tmVbMhBr6qxCEclPGDi175M0nNHPuWjETaujRQxDKgx2nvOyRF70eefLdzYiZUEOfJ4ZQjWq1TKj21NDM+78VM6GGXmEEobxg4LYhO8BFr0eevEMaMRNq6DfHEMKuV7Gd+nen938npqKqw6JaF6fXJ89/H4pVcfqul2kQfvHN5afb3fnZ1du/3/1vqNNmVW6WKf329G/Nz7w/eX0qXwwqfNlfUS/7K3jZXwkv+yu8oVXcFbbCF+cV94JEnP0Vvs8nCFhhEWp4j2cgNEVU4btxCgJUVPf/cKm0q+r7t7MqqB9FFb7MJgC2s67Cl9kcwEENl2kCYBlArfsgAiyrahGCDTDM4tcPqgpfdRP8rG9EqOHrGoZfjWr1DH7NlW5l4/uX9TItyvU8iDVA7GcZA9H4WoQavhUkILaDp8I3yyrEqv6nQuzHXYUvzAmI1tci1PDlMwMRW2HFtkJ506nwTy+ZeWB0aEIN33wREKzmyc2D5aYIqamjVa6jWKzbOorF6aHVret61UovymL4qxHHj22tvTo7bodCW3ZPFl82Ch8fqDru2hP8Mb3dvb85O94dtsX+XfHi7ni5P+z+b3tRfLM93O5vyGiR/Odyn11lQt5Pl91VJjxwL3z42e7B+7tTbiXck51q06XuRZtfU082Pz6Kth9GVa5cqub5GBerOLSd5ur++exbPw/xeVzGeUMwLauRaN8MHiL6i8ce/V7TYh3IXusBkA/0nYC2ziLC5k7frASPAzy93N5ui/P99fX+YnfcbW//tThuzy9v9lf795/+tdgfitv9u+PHs6ayP26b/9r+9GF/ODaV/e6wvy6Ol9vi+5td+/ntsTmWt135X28PzZpQvGsevrs67q6bf1BcbG+Pu+aI7PY3xcsXxe7+TECgzbqy7AbMGN7Z+fn+cHF2c97I746XvXxxdnG9u9ndHg/5Nzxs399ddb+8XRSvdj82h6792+f7m+YnDp+K4774fvF2UVydfbwtdrfFh8P+cvdDG/bCsb1oiWzPXHl//PLvQG0uzU+PtTk93toSKcdyGYXYcgm1deC+fv5xW1w2lfDDp+J8ezju3jV4L8+OXSnsbpqcX+ecNP97vGxY725+3O+a9DW/PB7utsXZzUWTmMNhe37sfn3/cJut7c2xK6HuydvL3Yfr5u8UbfGdNZ/bCrt4oG5CFX5ZOD/sf9wuihc3n4pXZzfvt4f93W3x5X5/cdv9drub4vVP59sPbeV+e3d2c+xq31MNYQXl0H6Yrofmp8aCEF5yq+0q1wEWhfhioKriYl0XMTYHtHysMiavgOHn4S0Xqf2f5m//4sVH808+e/fRfm7DbW+9y/xmoxnL7U+kxaYePjOvY5rfqxrexkSmbQ9BRchv+4F5GzOIbT4TI//YpfOar4tnocqvq3CtWZeLVHYJWSXz2nLP+j5Pb+9+OO6PZ1f/Rt5KptN2/0cvfdbiz7MW1p8nLQpJyyQ6jO0vqZT1AeWMRTpjj5cHmbF2CXksY821Ocbmrpn0jP3+sN29vzwWL/e3RzZrT04nf7/xD+UEu7CIpi6Rsyy51+o+MHZhP1tYN+sOttGvlovl0rOwyh3B+FqEGvq+MBA3qLYhIX5WzkujAZWpnQhhM6MBnbbdp/i6vxf8x9nV3fbpqlostfw1xym84dtL2MABaj8w6UcjHhBTpnDLfKjq2Fd1D33oyw9A/9l0ns95bjka335arWe9oVlvUG3zGOt/NFfH/Ghq/4XNYlU1X754vrt+vyxe7YtvP7sZd/+4oZ4fOb04eXb/q4eG5niO2nirVXOO4vIX56idN+WmuZ01sVb3OS0hp+XjB+nV9qrddYpXd8dPzRr24Wx38VTnSAWevyasN8I5Ei/OOZ2frTgP5fb/ATbFSQYKZW5kc3RyZWFtCmVuZG9iagoxIDAgb2JqCjw8L1RhYnMvUy9Hcm91cDw8L1MvVHJhbnNwYXJlbmN5L1R5cGUvR3JvdXAvQ1MvRGV2aWNlUkdCPj4vQ29udGVudHMgNSAwIFIvVHlwZS9QYWdlL1Jlc291cmNlczw8L0NvbG9yU3BhY2U8PC9DUy9EZXZpY2VSR0I+Pi9Qcm9jU2V0IFsvUERGIC9UZXh0IC9JbWFnZUIgL0ltYWdlQyAvSW1hZ2VJXS9Gb250PDwvRjEgMiAwIFIvRjIgMyAwIFI+Pi9YT2JqZWN0PDwvaW1nMCA0IDAgUj4+Pj4vUGFyZW50IDYgMCBSL01lZGlhQm94WzAgMCA2MTIgNzkyXT4+CmVuZG9iago3IDAgb2JqClsxIDAgUi9YWVogMCA4MDIgMF0KZW5kb2JqCjIgMCBvYmoKPDwvU3VidHlwZS9UeXBlMS9UeXBlL0ZvbnQvQmFzZUZvbnQvSGVsdmV0aWNhL0VuY29kaW5nL1dpbkFuc2lFbmNvZGluZz4+CmVuZG9iagozIDAgb2JqCjw8L1N1YnR5cGUvVHlwZTEvVHlwZS9Gb250L0Jhc2VGb250L0hlbHZldGljYS1Cb2xkL0VuY29kaW5nL1dpbkFuc2lFbmNvZGluZz4+CmVuZG9iago2IDAgb2JqCjw8L0tpZHNbMSAwIFJdL1R5cGUvUGFnZXMvQ291bnQgMS9JVFhUKDIuMS43KT4+CmVuZG9iago4IDAgb2JqCjw8L05hbWVzWyhKUl9QQUdFX0FOQ0hPUl8wXzEpIDcgMCBSXT4+CmVuZG9iago5IDAgb2JqCjw8L0Rlc3RzIDggMCBSPj4KZW5kb2JqCjEwIDAgb2JqCjw8L05hbWVzIDkgMCBSL1R5cGUvQ2F0YWxvZy9QYWdlcyA2IDAgUi9WaWV3ZXJQcmVmZXJlbmNlczw8L1ByaW50U2NhbGluZy9BcHBEZWZhdWx0Pj4+PgplbmRvYmoKMTEgMCBvYmoKPDwvTW9kRGF0ZShEOjIwMjExMjE4MDgyMzAwLTA3JzAwJykvQ3JlYXRvcihKYXNwZXJSZXBvcnRzIExpYnJhcnkgdmVyc2lvbiA2LjEuMCkvQ3JlYXRpb25EYXRlKEQ6MjAyMTEyMTgwODIzMDAtMDcnMDAnKS9Qcm9kdWNlcihpVGV4dCAyLjEuNyBieSAxVDNYVCk+PgplbmRvYmoKeHJlZgowIDEyCjAwMDAwMDAwMDAgNjU1MzUgZiAKMDAwMDAwOTg4NCAwMDAwMCBuIAowMDAwMDEwMTkyIDAwMDAwIG4gCjAwMDAwMTAyODAgMDAwMDAgbiAKMDAwMDAwMDAxNSAwMDAwMCBuIAowMDAwMDAxNjk5IDAwMDAwIG4gCjAwMDAwMTAzNzMgMDAwMDAgbiAKMDAwMDAxMDE1NyAwMDAwMCBuIAowMDAwMDEwNDM2IDAwMDAwIG4gCjAwMDAwMTA0OTAgMDAwMDAgbiAKMDAwMDAxMDUyMiAwMDAwMCBuIAowMDAwMDEwNjI2IDAwMDAwIG4gCnRyYWlsZXIKPDwvSW5mbyAxMSAwIFIvSUQgWzw0ODM0MmNlNGRiZDkyY2RhNTFjMThjYzAzYzExNDg0ZD48YTY5ODVhNzM0YzlmNmJlZmE4ZTI2MzA4NGZkNmQwYjA+XS9Sb290IDEwIDAgUi9TaXplIDEyPj4Kc3RhcnR4cmVmCjEwNzk0CiUlRU9GCg=="
}'
```
{% endtab %}

{% tab title="Response" %}
```json
{
    "id": "32ba91c6-3793-4a59-8b76-dfb468e0ec5b",
    "createdTime": "2022-11-28T19:38:46Z",
    "fileName": "tax_certficate_John_Doe.pdf",
    "purpose": "tax_document_customer_upload",
    "size": 11185,
    "type": "pdf",
    "url": "https://api.digitalriver.com/files/32ba91c6-3793-4a59-8b76-dfb468e0ec5b/content",
    "liveMode": false
}
```
{% endtab %}
{% endtabs %}

### Adding tax certificates to existing customers <a href="#adding-a-tax-certificate" id="adding-a-tax-certificate"></a>

After [creating a tax certificate file](setting-tax-related-attributes.md#creating-tax-certificate-files), pass the [customer's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Customers) unique identifier as a path parameter in a [`POST /customers/{id}`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/updateCustomers). In the body of the request, use `taxCertificate` to send the information your form collected, as well as the identifier of the file.

{% tabs %}
{% tab title="Update customer" %}
```
curl --location --request POST 'https://api.digitalriver.com/customers/541670080336' \
--header 'Content-Type: application/json' \
...
--data-raw '{
    "taxCertificate":{
        "companyName": "Acme Inc",
        "taxAuthority": "MN",
        "startDate":"2021-04-07T13:47:13Z",
        "endDate":"2025-04-07T13:47:13Z",
        "fileId": "9d149880-7306-49da-b37b-8440649ae9c2"
    }
}'
```
{% endtab %}
{% endtabs %}

#### Company name

The `companyName` should indicate the name of the company or organization that has been granted the tax exemption.

#### Tax authority

Since tax certificates only apply to US-based customers, `taxAuthority` corresponds to the issuing state. The value you assign should be formatted to conform to the [USPS two-letter state and possession abbreviation standard](https://pe.usps.com/text/pub28/28apb.htm). These are the same abbreviations used in the [ISO 3166-2 subdivision codes](https://www.iso.org/obp/ui/#iso:code:3166:US).

#### Start and end dates

The `startDate` and `endDate` values correspond to the issue and expiration dates of the tax certificate, respectively.

{% hint style="info" %}
In the request, make sure `startDate` and `endDate` adhere to the [date and time format used in the Digital River APIs](../developer-resources/api-structure.md#dates-and-times).
{% endhint %}

Tax certificates can be difficult to interpret. As a result, your customers might be unable to determine appropriate input dates. If this is the case, define `startDate` as the first date of the current month and `endDate` as the last date of the current month. This allows us time to review the certificate, determine its validity, and set the applicable dates.

#### File identifier

Retrieve the identifier of the [tax certificate file](setting-tax-related-attributes.md#creating-tax-certificate-files) that you created and use it to define `fileID`.

### Verifying the tax certificate exists

Once you [add a tax certificate to the customer's record](setting-tax-related-attributes.md#adding-a-tax-certificate), send a [`GET /customers/{id}`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/retrieveCustomers) request and parse the response to verify the object has been successfully added to `taxCertificates[]`.

{% tabs %}
{% tab title="Customer" %}
```javascript
{
    "id": "541670080336",
    "createdTime": "2021-08-23T20:30:06Z",
    "updatedTime": "2021-08-23T20:33:53Z",
    ...
    "taxCertificates": [
        {
            "companyName": "Acme Inc",
            "taxAuthority": "MN",
            "startDate": "2021-04-07T00:00:00Z",
            "endDate": "2025-04-07T00:00:00Z",
            "fileId": "9d149880-7306-49da-b37b-8440649ae9c2"
        }
    ],
    "locale": "en_US",
    "type": "business"
}
```
{% endtab %}
{% endtabs %}

### Adding multiple tax certificates to a customer

You can only send one `taxCertificate` in a [`POST /customers`](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Customers/operation/createCustomers) or [`POST /customers/{id}`](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Customers/operation/updateCustomers) request. But a [customer](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Customers) can have multiple `taxCertificates[]`.&#x20;

At checkout-time, Digital River determines which (if any) are [applicable](setting-tax-related-attributes.md#what-transactions-are-eligible).

{% tabs %}
{% tab title="Customer" %}
```javascript
{
    "id": "543790170336",
    "createdTime": "2021-09-08T20:58:15Z",
    "updatedTime": "2021-09-08T22:09:59Z",
    ...
    "taxCertificates": [
        {
            "companyName": "Acme Inc",
            "taxAuthority": "MN",
            "startDate": "2021-04-07T00:00:00Z",
            "endDate": "2022-04-07T00:00:00Z",
            "fileId": "b87c6b64-e919-45d6-bf49-016bed76134a"
        },
        {
            "companyName": "Beta Inc",
            "taxAuthority": "WI",
            "startDate": "2021-04-07T00:00:00Z",
            "endDate": "2022-02-07T00:00:00Z",
            "fileId": "542d9a68-8eb4-4bda-b3fb-67b68e9f6846"
        }
    ],
    "locale": "en_US",
    "type": "business"
}
```
{% endtab %}
{% endtabs %}
