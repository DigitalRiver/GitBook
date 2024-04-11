---
description: Learn about payment objects that are common to all payment methods.
---

# Common payment objects

Understanding common payment objects is essential for developers and businesses in the digital payment ecosystem. These objects, often represented in structured formats like JSON, serve as the foundation for transactions, storing vital information such as buyer details, payment methods, transaction amounts, etc. Familiarizing yourself with these objects makes implementing, troubleshooting, and optimizing payment flows easier. This section delves into some of the most frequently encountered payment objects, illustrating their structure and explaining the significance of each field to ensure a smooth and secure payment experience.

## Owner object

An Owner object represents the individual or entity that owns the account or is making a purchase. It contains key information such as the individual's name, contact details (phone number and email), organization affiliation, and physical address. Below is an example of an Owner object and a detailed explanation of each field:

#### Example:

```json
{
  "firstName": "Otis",
  "lastName": "Lin",
  "email": "test@digitalriver.com",
  "phoneNumber": "01314532211",
  "organization": "DR",
  "address": {
    "line1": "东城区景山前街4号",
    "city": "北京市",
    "country": "CN",
    "postalCode": "100009"
  }
}
```

#### Fields:

* **`firstName`** (Required): The customer's first name as it appears on the payment instrument.
* **`lastName`** (Required): The customer's last name as it appears on the payment instrument.
* **`phoneNumber`** (Required): The customer's phone number.
* **`email`** (Required): The customer's email address.
* **`organization`** (Optional): The name of the organization the customer is associated with.
* **`address`** (Required): An Address object containing the customer's physical address. See the [Address object](common-payment-objects.md#address-object) and [Additional address information object](common-payment-objects.md#additional-address-information-object) sections for details.

## Address object

Address objects are crucial parts of an owner object, providing detailed information about the customer's location. Below is an example of an Address object and a detailed explanation of each field:

#### Example:

```json
  "address": {
    "line1": "1-16-24 Minami-gyotoku",
    "line2": "Ichikawa-shi",
    "city": "Chiba",
    "state": "Kyongsangnamdo",
    "postalCode": "272-0138",
    "country": "JP"
  }
```

#### Fields:

* **`line1`** & **`line2`** (Required): Address lines for detailed street information.
* **`city`** (Required): The city of the customer's billing address.
* **`state`** (Required): The state of the customer's billing address.
* **`postalCode`** (Required): The postal code of the customer's billing address.
* **`country`** (Required): The country of the customer's billing address.

## Additional address information object

The Additional Address Information object provides additional details that might be required for certain payment types or to ensure more accurate delivery of goods. Below is an example of an Additional Address information object and a detailed explanation of each field:

#### Example:

```json
    "additionalAddressInfo": {
            "neighborhood": "Centro",
            "phoneticFirstName": "John",
            "phoneticLastName": "Doe",
            "division": "Development"
            }
```

#### Fields:

* **`additionalAddressInfo`**:
  * **`neighborhood`** _(Optional)_: Specifies the neighborhood of the customer.
  * **`phoneticFirstName`** _(Optional)_: The phonetic spelling of the customer's first name is useful for ensuring correct pronunciation by customer service or delivery personnel.
  * **`phoneticLastName`** _(Optional)_: The phonetic spelling of the customer's last name.
  * **`countyName`** _(Optional)_: The county associated with the customer's address.
  * **`division`** _(Optional)_: The division applicable to the customer might be used for internal segmentation or routing of deliveries.
  * **`title`** _(Optional)_: The customer's title (e.g., `MR`, `MS`, `MISS`, `MRS`, `M`, `MME`, `MLLE`). This field is required for [Pay with Installments France](../../../supported-payment-methods/pay-with-installments-france.md).
