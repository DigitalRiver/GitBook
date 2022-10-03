# HGOP2

The HGOP2 (Half GUI Order Processing version 2) service allows clients to host their cart and then post the information in their cart to Digital River at checkout time. A successful HGOP2 call consumes the information, creates a cart on the Digital River-side, and then redirects the user to the cart on the Digital River-side.

| Class             | Description                                                                                                  |
| ----------------- | ------------------------------------------------------------------------------------------------------------ |
| CreateCartRequest | Contains the client's cart information. Use this information to populate the cart on the Digital River-side. |

Digital River can provide interfaces to post PGP messages for testing purposes.

See [PGP coding examples](http://www.docjar.org/html/api/org/bouncycastle/openpgp/examples/KeyBasedFileProcessor.java.html) for more information.

## Using HGOP2 with PGP encryption

You can use PGP encryption with the HGOP2 service to encrypt the contents of the cart.

To integrate HGOP2 with PGP encryption:

1. Get the following items from your Digital River representative:
   * A PGP key
   * The endpoint information to post the PGP encrypted information
2. Generate an XML request that conforms to one of the [HGOP2 schemas](hgop2.md#hgop2-schemas).
3. Encrypt the message above as a PGP armored (ASCII-based) message using the key provided in step 1.
4.  Expose a simple HTML form to the end-user that contains a single hidden HTML `message` parameter.  Use the encrypted results obtained in step 3 as the value for the `message` parameter. When the user clicks submit, iXMt triggers an HTTP POST call with the encrypted key to the endpoint.



## Using HGOP2 with store credit

### Create a store credit source

When you create a store credit source using [`POST /sources`](https://www.digitalriver.com/docs/commerce-api-reference/#operation/createSources), the sources array will contain a source with a `type` of `customerCredit`.

{% code title="JSON" overflow="wrap" %}
```json
{
    "type": "customerCredit",
    "amount": 14,
    "currency": "USD",
    "customerCredit": {}
}
```
{% endcode %}

| Field            | Type   | Required/Optional | Description                                                                                               |
| ---------------- | ------ | ----------------- | --------------------------------------------------------------------------------------------------------- |
| `type`           | String | Required          | The payment type In this instance, the required value is `customerCredit`.                                |
| `amount`         | String | Required          | The amount of the source                                                                                  |
| `currency`       | String | Required          | The [three-letter currency code](https://www.iban.com/currency-codes) associated with the payment method. |
| `customerCredit` |        | Required          | The `customerCredit` instrument should be empty.                                                          |

### Add the store credit source to the cart

Accept the store credit source in the HGOP2 request body and create the payment information with the source.

{% code title="XML" overflow="wrap" %}
```xml
<?xml version="1.0" encoding="UTF-8"?>
<CreateCartRequest xmlns="http://integration.digitalriver.com/HGOP2">
    <!-- Omitted -->
    <payment>
        <sources>
            <source>
                <sourceID>9f3de26b-79f4-4918-888f-a90535271dcc</sourceID>  <!-- Stored credit source Id -->
            </source>
        </sources>
    </payment>
</CreateCartRequest>
```
{% endcode %}

## HGOP2 schemas

| Version      | Scheme Components Table                                                        | Raw Schema                                                         | Sample Schema                                                              |
| ------------ | ------------------------------------------------------------------------------ | ------------------------------------------------------------------ | -------------------------------------------------------------------------- |
| 12 (Current) | [View](https://drhadmin.digitalriver.com/integration/isg/schematable/HGOP2/12) | [View](https://drhadmin.digitalriver.com/integration/xsd/HGOP2/12) | [View](https://drhadmin.digitalriver.com/integration/isg/example/HGOP2/12) |
| 11           | [View](https://drhadmin.digitalriver.com/integration/isg/schematable/HGOP2/11) | [View](https://drhadmin.digitalriver.com/integration/xsd/HGOP2/11) | [View](https://drhadmin.digitalriver.com/integration/isg/example/HGOP2/11) |
| 10           | [View](https://drhadmin.digitalriver.com/integration/isg/schematable/HGOP2/10) | [View](https://drhadmin.digitalriver.com/integration/xsd/HGOP2/10) | [View](https://drhadmin.digitalriver.com/integration/isg/example/HGOP2/10) |
