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

1. Digital River will provide the following items:
   * A PGP key
   * The endpoint information to post the PGP encrypted information
2. Request XML generation from the client. The client will:
   * The client generates an XML request conforming to a schema.
   * The client encrypts the message above as a PGP armored (ASCII based) message using the key provided in step 1.
   * The client exposes a simple HTML form to the end-user. This form would contain a single hidden HTML parameter named "message," assign the results obtained in step 2b as its value. When the user clicks submit, it does an HTTP form Post to an endpoint provided by Digital River in step 2.

## HGOP2 schemas

| Version      | Scheme Components Table                                                        | Raw Schema                                                         | Sample Schema                                                              |
| ------------ | ------------------------------------------------------------------------------ | ------------------------------------------------------------------ | -------------------------------------------------------------------------- |
| 11 (Current) | [View](https://drhadmin.digitalriver.com/integration/isg/schematable/HGOP2/11) | [View](https://drhadmin.digitalriver.com/integration/xsd/HGOP2/11) | [View](https://drhadmin.digitalriver.com/integration/isg/example/HGOP2/11) |
| 10           | [View](https://drhadmin.digitalriver.com/integration/isg/schematable/HGOP2/10) | [View](https://drhadmin.digitalriver.com/integration/xsd/HGOP2/10) | [View](https://drhadmin.digitalriver.com/integration/isg/example/HGOP2/10) |
| 9            | [View](https://drhadmin.digitalriver.com/integration/isg/schematable/HGOP2/9)  | [View](https://drhadmin.digitalriver.com/integration/xsd/HGOP2/9)  | [View](https://drhadmin.digitalriver.com/integration/isg/example/HGOP2/9)  |
