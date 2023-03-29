---
description: Learn about the file upload integration processes.
---

# File uploads

## Bulk Product Upload (BPU)

Use the Bulk Product Upload (BPU) process to add, update, or remove multiple products. The BPU process creates categories based on the provided category path. The BPU process is an inbound event.

The BPU uses the Bulk Import process to add, update, or remove products.

### Bulk import XML file

The following example shows the smallest possible Bulk Import XML file:

{% tabs %}
{% tab title="Bulk Import XML file" %}
{% code overflow="wrap" %}
```xml
<?xml version="1.0" encoding="utf-8"?>
<loader xmlns="urn:com.digitalriver.bulkloader">
    <loaderType>incremental</loaderType>
    <ownerCompanyID>myCompanyID</ownerCompanyID>
    <catalogID>858100</catalogID>
    <noOverwriteIfEmpty>true</noOverwriteIfEmpty>
    <items>
        <product>
            <productID>42716000</productID>
            <action>UPDATE</action>
            <companyID>myCompanyID</companyID>
        </product>
    </items>
</loader>
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Bulk import XML file with category import

The following example shows a Bulk Import XML file with Category Import:

{% tabs %}
{% tab title="Bulk Import XML file with Category Import file" %}
{% code overflow="wrap" %}
```xml
<?xml version="1.0" encoding="utf-8"?>
<loader xmlns="urn:com.digitalriver.bulkloader">
    <loaderType>incremental</loaderType>
    <ownerCompanyID>myCompanyID</ownerCompanyID>
    <catalogID>858100</catalogID>
    <noOverwriteIfEmpty>true</noOverwriteIfEmpty>
    <items>
      <productCategory>
          <categoryPath>
            <categoryName>Accessories1</categoryName>
            <categoryName>Cameras1</categoryName>
          </categoryPath>
          <categoryData>
            <locale>en_GB</locale>
            <categoryDisplayName>Cameras1</categoryDisplayName>
            <categoryImageURI></categoryImageURI>
            <isViewable>true</isViewable>
            <shortDescription></shortDescription>
            <longDescription>Camera Type</longDescription>
            <attributes/>
          </categoryData>
    </productCategory>
        <product>
            <productID>42716000</productID>
            <action>UPDATE</action>
            <companyID>myCompanyID</companyID>
        </product>
    </items>
</loader>
```
{% endcode %}
{% endtab %}
{% endtabs %}

{% hint style="info" %}
**Note**: BPU is non-interactive. When the BPU process finishes, there is no required notification response. When the BPU process finishes, the presence of a BulkImportResponse file indicates the bulk file upload has finished.
{% endhint %}

When using Bulk Import to import categories, consider the following tips:

* Ensure all categories are listed in the file before products. Follow the sequence in the schema.
* A category path cannot be empty.
* Define the `loaderType` to Add or Update the category, if the n`oOverwriteIfEmptyData` flag is not set.
* If you run an incremental upload and the category action is REMOVE, then categories with subcategories or products in a predeployed state will not be deleted.
* If you run a full catalog upload, all categories that are not in the import file will be removed.

### Bulk import response XML file

The BPU Import process creates the Bulk Import Response file after the Bulk Import process completes. The Bulk Import Response file reports when the BPU Import process successfully adds, updates, or retires a product. If an error occurs during the import, The BPU Import process adds the error and `stackTrace` elements to provide more information.

{% tabs %}
{% tab title="Bulk Import Response XML file" %}
{% code overflow="wrap" %}
```xml
<?xml version="1.0" encoding="utf-8"?>
<loader xmlns="urn:com.digitalriver.bulkloader">
    <loaderType>incremental</loaderType>
    <ownerCompanyID>myCompanyID</ownerCompanyID>
    <catalogID>858100</catalogID>
    <noOverwriteIfEmpty>true</noOverwriteIfEmpty>
    <items>
      <productCategory>
          <categoryPath>
            <categoryName>Accessories1</categoryName>
            <categoryName>Cameras1</categoryName>
          </categoryPath>
          <categoryData>
            <locale>en_GB</locale>
            <categoryDisplayName>Cameras1</categoryDisplayName>
            <categoryImageURI></categoryImageURI>
            <isViewable>true</isViewable>
            <shortDescription></shortDescription>
            <longDescription>Camera Type</longDescription>
            <attributes/>
          </categoryData>
    </productCategory>
        <product>
            <productID>42716000</productID>
            <action>UPDATE</action>
            <companyID>myCompanyID</companyID>
        </product>
    </items>
</loader>
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Terminology

#### `externalReferenceId`

The BPU process uses `externalReferenceId` to identify products. It frees clients from the need to consume and store Digital River product IDs. When using this field to identify products, ensure the `externalReferenceId` is unique across the product-owning company.

#### locale in prices

The locale in the price node is not tied to the locale of the enclosing product node. To use locale-specific prices, specify the locale at the price level.

#### `noOverwriteIfEmpty`

This value should be set to true. Setting this value to false can result in undesired side effects.

#### `productConfigType`

This complex type, while appearing in the schema, is not consumed by the BPU process. It does not affect the BPU process when you include it in the XML.

#### retiring products

The “remove” action for products works a little differently for products with multiple locales as opposed to products with a single locale. For products with multiple locales, “remove” deletes that locale from the product. If there is only a single locale, the “remove” action will retire the product.

### Schemas

| Version     | Schema Components Table                                                             | Raw Schema                                                               | Sample XML                                                                      |
| ----------- | ----------------------------------------------------------------------------------- | ------------------------------------------------------------------------ | ------------------------------------------------------------------------------- |
| 7 (Current) |  [View](https://drhadmin.digitalriver.com/integration/isg/schematable/BulkLoader/7) |  [View](https://drhadmin.digitalriver.com/integration/xsd/BulkLoader/7)  | Not available                                                                   |
| 6           |  [View](https://drhadmin.digitalriver.com/integration/isg/schematable/BulkLoader/6) |  [View](https://drhadmin.digitalriver.com/integration/xsd/BulkLoader/6)  |  [View](https://drhadmin.digitalriver.com/integration/isg/example/BulkLoader/6) |
| 5           |  [View](https://drhadmin.digitalriver.com/integration/isg/schematable/BulkLoader/5) |  [View](https://drhadmin.digitalriver.com/integration/xsd/BulkLoader/5)  |  [View](https://drhadmin.digitalriver.com/integration/isg/example/BulkLoader/5) |

## Product association feed

Use the Product Association Feed to add, modify, or remove product associations. Product Associations allow users to associate one product with one or more other products. The Product Associations framework is generic.

The Product Association Feed is a webhook event.

### Details

The Product Association Feed Integration serves as the automated mechanism through which Digital River adds, modifies, and deletes product associations in an Association Group.

The following list describes when you cannot create an association.

* The owning product is not deployed. You can only create associations (via the feed) when the owning product is deployed.
* The associated product is not deployed. You can only create an association group when the product you want to associate with the owning product is deployed.
* The locale of the owning product in the feed is not a valid locale for that product.

{% hint style="info" %}
**Note**: If you create an association group that also includes deployed products in the association, the created association group will not include the undeployed products. The locale for the owning product in the feed is not a valid locale for that product.
{% endhint %}

The following table describes the request and response types for exporting and importing product association details.

| Task                                                                                       | Request Type                        | Response Type                        |
| ------------------------------------------------------------------------------------------ | ----------------------------------- | ------------------------------------ |
| View the existing product association details by exporting the product association details | ProductAssociationFeedExportRequest | ProductAssociationFeedExportResponse |
| View the existing product association details by exporting the product association details | ProductAssociationFeedImportRequest | ProductAssociationFeedImportResponse |

A Product Association Type defines the behavior of a specific type of product association. The behavior defined by the type includes but may not be limited to the following:

* Enforcement of cardinality between parent and child products.

{% hint style="info" %}
**Example**: one-to-one (1:1) or one-to-many (1:M)
{% endhint %}

* State-dependent behavior, including whether you can:
  * Display the association on a shopper site
  * Add the products to the association
  * Modify the association name
* State transition rules

Each Product Association Type is associated with a collection of one or more Categories specific to that type. The Categories are company-specific, and you must create them before you create specific Product Associations.

{% hint style="info" %}
**Example**: Categories that you could create for a Related Items Type include "Related Trial Ware" and "Related Products".
{% endhint %}

Each Category appears as a separate panel or container in an administrator interface. Associations of that Type and Category will be managed entirely within that panel.

Also, the Product Association Type and Category combine to allow site designers to display certain association Groups at certain locations on the shopper site.

A Product Association Group defines a relationship between a single Parent Product and a collection of Child Products. The Group links the Parent Product with the Child Products. Also, the Group inherits behavior defined by the Product Association Type, and to a lesser extent by the Category within that type. Groups can be sorted within a Category.

You can give the Product Association Group a localized Group Name. When you create a localized Group Name, you must:

* Associate each Group Name with a specific Locale.
* Define one Group Name as the default.

You can add additional Group Names for other locales. A Client may ask for the name of a Group by Locale. If a localized name matches the Locale in the request, that name is provided; otherwise, the default name is provided. Group Name may be optional for some Product Association Types.

The Parent Product is the Key Product in an Association Group. It drives the maintenance and display of Product Associations. You cannot remove a Parent Product from a Group.

A Group contains a collection of Associated Products with relative sort order. You can add or remove Associated Products from a Group if the group's state allows it.

The Product Association Tag is a display API that provides Product Association Group information that you can use in shopper-side views.

You can send a `productAssociationFeedImportRequest` and expect a  `productAssociationFeedImportResponse` in real-time.

You can send a `productAssociationFeedImportRequest` and expect a `productAssociationFeedImportResponse` at a later point.

The following example shows the request and response for adding an Associated Product and Associations.

{% tabs %}
{% tab title="Request sample" %}
{% code overflow="wrap" %}
```xml
<ProductAssociationFeedImportRequest 
xmlns="http://integration.digitalriver.com/ProductAssociationFeed">
  <companyID>mycompany</companyID>
  <reportingLevel>all</reportingLevel>
  <lenientCommit>true</lenientCommit>
  <productAssociation>
    <action>add</action>
    <associationInfo>
      <categoryName>Related Products</categoryName>
      <parentProduct>
        <externalReferenceID>111111</externalReferenceID>
        <companyID>mycompany</companyID>
        <locale>en_US</locale>
      </parentProduct>
    </associationInfo>
    <groupData>
      <groupDataInfo>
        <groupName>Inkjet Ink/Print Cartridge</groupName>
        <locale>en_US</locale>
        <isDefault>1</isDefault>
      </groupDataInfo>
    </groupData>
    <associatedProduct>
      <action>add</action>
      <associatedProductInfo>
        <productKey>
          <externalReferenceID>222222</externalReferenceID>
          <companyID>mycompany</companyID>
          <locale>en_US</locale>
        </productKey>
        <sortOrder>1</sortOrder>
      </associatedProductInfo>
    </associatedProduct>
    <associatedProduct>
      <action>add</action>
      <associatedProductInfo>
        <productKey>
          <externalReferenceID>333333</externalReferenceID>
          <companyID>mycompany</companyID>
          <locale>en_US</locale>
        </productKey>
        <sortOrder>2</sortOrder>
      </associatedProductInfo>
    </associatedProduct>
  </productAssociation>
</ProductAssociationFeedImportRequest>
```
{% endcode %}
{% endtab %}

{% tab title="Response sample" %}
{% code overflow="wrap" %}
```xml
<?xml version="1.0" encoding="utf-8"?>
<ProductAssociationFeedImportResponse 
xmlns="http://integration.digitalriver.com/ProductAssociationFeed">
	<companyID>mycompany</companyID>
	<importResult>
		<actionResult>
			<action>add
		<action>
			<resultCode>1
		</resultCode>
			<message>Product Association created.
		</message>
		</actionResult>
		<associationInfo>
			<categoryName>Related Products
</categoryName>
			<parentProduct>
				<externalReferenceID>111111
</externalReferenceID>
				<companyID>mycompany</companyID>
				<locale>en_US</locale>
			</parentProduct>
		</associationInfo>
		<groupData>
			<groupDataInfo>
				<groupName>Inkjet Ink/Print Cartridge
</groupName>
				<locale>en_US</locale>
				<isDefault>1</isDefault>
			</groupDataInfo>
		</groupData>
		<associatedProduct>
			<action>add</action>
			<associatedProductInfo>
				<productKey>
					<externalReferenceID>222222
</externalReferenceID>
					<companyID>mycompany</companyID>
					<locale>en_US</locale>
				</productKey>
				<sortOrder>1</sortOrder>
			</associatedProductInfo>
		</associatedProduct>
	</importResult>
</ProductAssociationFeedImportResponse>
```
{% endcode %}
{% endtab %}
{% endtabs %}

The following example shows the request and response for modifying an Associated Product and Associations.

{% tabs %}
{% tab title="Request sample" %}
{% code overflow="wrap" %}
```xml
<?xml version="1.0" encoding="utf-8"?>
<ProductAssociationFeedImportRequest 
xmlns="http://integration.digitalriver.com/ProductAssociationFeed">
  <companyID>mycompany</companyID>
  <reportingLevel>all</reportingLevel>
  <lenientCommit>true</lenientCommit>
  <productAssociation>
    <action>update</action>
    <associationInfo>
      <associationID>12345</associationID>
      <categoryName>Related Products</categoryName>
      <parentProduct>
        <externalReferenceID>111111</externalReferenceID>
        <companyID>mycompany</companyID>
        <locale>en_US</locale>
      </parentProduct>
    </associationInfo>
	<groupData>
      <groupDataInfo>
        <groupName>Inkjet Ink/Print Cartridge</groupName>
        <locale>en_US</locale>
        <isDefault>1</isDefault>
      </groupDataInfo>
    </groupData>
	<associatedProduct>
      <action>update</action>
      <associatedProductInfo>
        <productKey>
          <externalReferenceID>222222</externalReferenceID>
          <companyID>mycompany</companyID>
          <locale>en_US</locale>
        </productKey>
        <sortOrder>1</sortOrder>
      </associatedProductInfo>
    </associatedProduct>
    <associatedProduct>
      <action>update</action>
      <associatedProductInfo>
        <productKey>
          <externalReferenceID>333333</externalReferenceID>
          <companyID>mycompany</companyID>
          <locale>en_US</locale>
        </productKey>
        <sortOrder>2</sortOrder>
      </associatedProductInfo>
    </associatedProduct>
  </productAssociation>
</ProductAssociationFeedImportRequest>
```
{% endcode %}
{% endtab %}

{% tab title="Response sample" %}
{% code overflow="wrap" %}
```xml
<?xml version="1.0" encoding="utf-8"?>
<ProductAssociationFeedImportResponse 
xmlns="http://integration.digitalriver.com/ProductAssociationFeed">
	<companyID>mycompany</companyID>
	<importResult>
		<actionResult>
			<action>update
		<action>
			<resultCode>1
		</resultCode>
			<message>Product Association updated
		</message>
		</actionResult>
		 <associationInfo>
      <associationID>12345</associationID>
      <categoryName>Related Products</categoryName>
      <parentProduct>
        <externalReferenceID>111111</externalReferenceID>
        <companyID>mycompany</companyID>
        <locale>en_US</locale>
      </parentProduct>
    </associationInfo>
	<groupData>
      <groupDataInfo>
        <groupName>Inkjet Ink/Print Cartridge</groupName>
        <locale>en_US</locale>
        <isDefault>1</isDefault>
      </groupDataInfo>
    </groupData>
	<associatedProduct>
      <action>update</action>
      <associatedProductInfo>
        <productKey>
          <externalReferenceID>222222</externalReferenceID>
          <companyID>mycompany</companyID>
          <locale>en_US</locale>
        </productKey>
        <sortOrder>1</sortOrder>
      </associatedProductInfo>
    </associatedProduct>
    <associatedProduct>
      <action>update</action>
      <associatedProductInfo>
        <productKey>
          <externalReferenceID>333333</externalReferenceID>
          <companyID>mycompany</companyID>
          <locale>en_US</locale>
        </productKey>
        <sortOrder>2</sortOrder>
      </associatedProductInfo>
    </associatedProduct>
	</importResult>
</ProductAssociationFeedImportResponse>
```
{% endcode %}
{% endtab %}
{% endtabs %}

The following example shows the request and response for deleting an Associated Product and Associations.

{% tabs %}
{% tab title="Request sample" %}
{% code overflow="wrap" %}
```xml
<?xml version="1.0" encoding="utf-8"?>
<ProductAssociationFeedImportRequest 
xmlns="http://integration.digitalriver.com/ProductAssociationFeed">
	<companyID>mycompany</companyID>
	<reportingLevel>all</reportingLevel>
	<lenientCommit>true</lenientCommit>
	<productAssociation>
		<action>delete</action>
		<associationInfo>
			<associationID>12345</associationID>
			<categoryName>Related Products</categoryName>
			<parentProduct>
				<externalReferenceID>111111</externalReferenceID>
				<companyID>mycompany</companyID>
				<locale>en_US</locale>
			</parentProduct>
		</associationInfo>
		<groupData>
      <groupDataInfo>
        <groupName>Inkjet Ink/Print Cartridge</groupName>
        <locale>en_US</locale>
        <isDefault>1</isDefault>
      </groupDataInfo>
    </groupData>
	<associatedProduct>
      <action>update</action>
      <associatedProductInfo>
        <productKey>
          <externalReferenceID>222222</externalReferenceID>
          <companyID>mycompany</companyID>
          <locale>en_US</locale>
        </productKey>
        <sortOrder>1</sortOrder>
      </associatedProductInfo>
    </associatedProduct>
	</productAssociation>
</ProductAssociationFeedImportRequest>
```
{% endcode %}
{% endtab %}

{% tab title="Response sample" %}
{% code overflow="wrap" %}
```xml
<?xml version="1.0" encoding="utf-8"?>
<ProductAssociationFeedImportResponse 
xmlns="http://integration.digitalriver.com/ProductAssociationFeed">
	<companyID>mycompany</companyID>
	<importResult>
		<actionResult>
			<action>delete
		<action>
			<resultCode>1
		</resultCode>
			<message>Product Association deleted.
		</message>
		</actionResult>
		 <associationInfo>
			<associationID>12345</associationID>
			<categoryName>Related Products</categoryName>
			<parentProduct>
				<externalReferenceID>111111</externalReferenceID>
				<companyID>mycompany</companyID>
				<locale>en_US</locale>
			</parentProduct>
		</associationInfo>
	<groupData>
      <groupDataInfo>
        <groupName>Inkjet Ink/Print Cartridge</groupName>
        <locale>en_US</locale>
        <isDefault>1</isDefault>
      </groupDataInfo>
    </groupData>
	<associatedProduct>
      <action>update</action>
      <associatedProductInfo>
        <productKey>
          <externalReferenceID>222222</externalReferenceID>
          <companyID>mycompany</companyID>
          <locale>en_US</locale>
        </productKey>
        <sortOrder>1</sortOrder>
      </associatedProductInfo>
    </associatedProduct>
    <associatedProduct>
      <action>update</action>
      <associatedProductInfo>
        <productKey>
          <externalReferenceID>333333</externalReferenceID>
          <companyID>mycompany</companyID>
          <locale>en_US</locale>
        </productKey>
        <sortOrder>2</sortOrder>
      </associatedProductInfo>
    </associatedProduct>
	</importResult>
</ProductAssociationFeedImportResponse>
```
{% endcode %}
{% endtab %}
{% endtabs %}

The Action Result denotes whether or no the action succeeded. The possible results are as follows:

* SUCCESSFUL
* FAILED

If the request failed, the following table describes the possible response codes associated with the failure:

| Response Code | Error Name                | Message                                                                                    |
| ------------- | ------------------------- | ------------------------------------------------------------------------------------------ |
| 100           | ERR\_INVALID\_ACTION      | Unrecognized action. The association group was not created.                                |
| 110           | ERR\_NO\_GROUP\_FOUND     | The product does not contain an association.                                               |
| 120           | ERR\_INVALID\_CATEGORY    | The company has no category, and Product Association was not created (updated or deleted). |
| 130           | ERR\_ASSOCIATION\_PARTIAL | Association was created, but errors occurred.                                              |
| 140           | ERR\_NOT\_CREATED         | Errors occurred, the association was not created.                                          |
| 200           | ERR\_GROUPDATA\_ADD       | Error in adding `groupData`.                                                               |
| 210           | ERR\_NO\_GROUPDATA\_FOUND | The association does not contain locale.                                                   |
| 220           | ERR\_GROUP\_NOT\_EDITABLE | Association cannot be modified: Group is not tied to the latest parent version.            |
| 230           | ERR\_NO\_MODIFICATION     | Errors occurred, the association was not modified.                                         |
| 300           | ERR\_CHILD\_ADD           | Could not add the associated product: product could not be found.                          |
| 310           | ERR\_NO\_CHILD\_FOUND     | Association does not contain a child product.                                              |
| 320           | ERR\_INVALID\_CHILD       | The child product can not be found. The child was not removed/updated.                     |
| 400           | ERR\_INVALID\_PARENT      | Parent product can not be found. Product Association was not added/modified/deleted.       |

### Schemas

| Version     | Schema Components Table                                                                         | Raw Schema                                                                          | Sample XML                                                                                  |
| ----------- | ----------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- |
| 1 (Current) |  [View](https://drhadmin.digitalriver.com/integration/isg/schematable/ProductAssociationFeed/1) |  [View](https://drhadmin.digitalriver.com/integration/xsd/ProductAssociationFeed/1) |  [View](https://drhadmin.digitalriver.com/integration/isg/example/ProductAssociationFeed/1) |

## Channel bulk loader

Use the Channel Bulk Loader to import company information, payment details, and channel contract agreement details along with other product information.

* The Channel Bulk Loader process imports products, companies, contracts, payment disbursement, pricing, and other objects necessary to sell products in the marketStream business model of Digital River.
* You can use the Channel Bulk Loader to add, update, or remove companies, products, and payment disbursement.

The Channel Bulk Loader is an inbound event.

### Company examples

{% tabs %}
{% tab title="Request sample" %}
{% code overflow="wrap" %}
```xml
<?xml version="1.0" encoding="windows-1252"?>
<loader xmlns = "ns:test">
    <catalogName>Test Channel Catalog</catalogName>
    <loaderType>testLoader</loaderType>
    <ownerCompanyID>0</ownerCompanyID>
    <sourceID>Test</sourceID>
    <items>
        <company>
            <companyID>1234</companyID>
            <name><![CDATA[Test Software]]></name>
            <duns/>
            <contactName><![CDATA[Test Contact]]></contactName>
            <contactEmail><![CDATA[mail@test.com]]></contactEmail>
            <url><![CDATA[www.testcompany.com]]></url>
            <telephone>123-1234</telephone>
            <fax/>
            <taxID/>
            <companyShortName>testsoft</companyShortName>
        </company>
    </items>
</loader>
```
{% endcode %}
{% endtab %}

{% tab title="Response Sample" %}
{% code overflow="wrap" %}
```xml
<?xml version="1.0"?>
<loaderResponse>
    <importFileName>test.xml</importFileName>
    <message>ok</message>
    <results>
        <result>
            <dataType>ChannelCompany</dataType>
            <dataID>1234</dataID>
            <loadStatus>SUCCESSFUL</loadStatus>
        </result>
    </results>
</loaderResponse>
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Payment disbursement examples

{% tabs %}
{% tab title="Request sample" %}
{% code overflow="wrap" %}
```xml
<?xml version="1.0" encoding="windows-1252"?>
<loader xmlns ="ns:test">
    <catalogName>Test Channel Catalog</catalogName>
    <loaderType>testLoader</loaderType>
    <ownerCompanyID>0</ownerCompanyID>
    <sourceID>testSource</sourceID>
    <items>
        <paymentDisbursement>
            <companyID>1234</companyID>
            <companyName><![CDATA[Test Software]]></companyName>
            <payToVendorID>123123</payToVendorID>
            <minimumAmountToPay><![CDATA[0]]></minimumAmountToPay>
            <minimumAmountToPayCurrency><![CDATA[USD]]></minimumAmountToPayCurrency>
            <paymentType><![CDATA[CHECK]]></paymentType>
            <paymentCycle><![CDATA[0]]></paymentCycle>
            <name1><![CDATA[Test1 ]]></name1>
            <name2><![CDATA[Test2]]></name2>
            <payToName><![CDATA[Test Software]]></payToName>
            <paymentAddressLine1><![CDATA[EP]]></paymentAddressLine1>
            <paymentAddressLine2><![CDATA[11]]></paymentAddressLine2>
            <paymentAddressCity><![CDATA[Eden Prairie]]></paymentAddressCity>
            <paymentAddressState><![CDATA[MN]]></paymentAddressState>
            <paymentAddressZipCode><![CDATA[45567]]></paymentAddressZipCode>
            <paymentAddressCountry><![CDATA[US]]></paymentAddressCountry>
            <bankName/>
            <bankAddressLine1/>
            <bankAddressLine2/>
            <bankAddressCity/>
            <bankAddressState/>
            <bankAddressZipCode/>
            <bankAddressCountry/>
            <bankAccountNumber/>
            <swiftCode/>
            <beneficiaryName/>
            <beneficiaryAddressLine1/>
            <beneficiaryAddressLine2/>
            <beneficiaryAddressCity/>
            <beneficiaryAddressState/>
            <beneficiaryAddressZipCode/>
            <beneficiaryAddressCountry/>
            <intermediaryAddressLine1/>
            <intermediaryAddressLine2/>
            <intermediaryAddressLine3/>
            <specialInstructions/>
        </paymentDisbursement>
    </items>
</loader>
```
{% endcode %}
{% endtab %}

{% tab title="Response sample" %}
{% code overflow="wrap" %}
```xml
<?xml version="1.0"?>
<loaderResponse>
    <importFileName>Test.xml</importFileName>
    <message>ok</message>
    <results>
        <result>
            <dataType>paymentDisbursement</dataType>
            <dataID>companyID: 123, paymentType: CHECK</dataID>
            <loadStatus>SUCCESSFUL</loadStatus>
        </result>
    </results>
</loaderResponse>
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Add product example

{% tabs %}
{% tab title="Request sample" %}
{% code overflow="wrap" %}
```xml
<?xml version="1.0" encoding="utf-8"?>
<loader xmlns:xsi = "http://www.w3.org/2001/XMLSchema-instance" 
xmlns:bulk = "ns1:testBulkloader">
    <loaderType>testLoader</loaderType>
    <noOverwriteIfEmpty>true</noOverwriteIfEmpty>
    <noOverwriteExistingCategoryData>true</noOverwriteExistingCategoryData>
    <items>
        <product>
            <action>ADD</action>
            <externalReferenceID>123123</externalReferenceID>
            <locale>en_US</locale>
            <currencyCode>USD</currencyCode>
            <companyID>test</companyID>
            <catalogID>123123</catalogID>
            <productName>Test Product</productName>
            <displayName>Test Product</displayName>
            <shortDescription>Short Description</shortDescription>
            <longDescription><![CDATA[Long Description]]></longDescription>
            <thumbnailImageURI>http://images.com/1</thumbnailImageURI>
            <detailImageURI>http://images.com/2</detailImageURI>
            <manufacturer>Test</manufacturer>
            <mfrPartNumber>123123/12</mfrPartNumber>
            <sku>12312</sku>
            <upc>021212121</upc>
            <type></type>
            <keywords>123,123123,12312</keywords>
            <weight>1.00</weight>
            <weightUnits>lb</weightUnits>
            <taxableProductCode>989</taxableProductCode>
            <commodityCode>89910</commodityCode>
            <taxableUnspscCode>4000</taxableUnspscCode>
            <categories>
                <category>
                    <categoryPath>
                        <categoryName>ACC</categoryName>
                        <categoryName>ACC_TEST</categoryName>
                    </categoryPath>
                </category>
            </categories>
            <prices>
                <price>
                    <currencyCode>USD</currencyCode>
                    <type>LIST_PRICE</type>
                    <amount>12.99</amount>
                </price>
                <price>
                    <currencyCode>USD</currencyCode>
                    <type>MSRP_PRICE</type>
                    <amount>29.99</amount>
                </price>
            </prices>
            <attributes>
                <attribute>
                    <name>testDivision</name>
                    <value>testValue</value>
                    <familyName>testFamilyl</familyName>
                </attribute>
            </attributes>
            <more>
                <productFulfillment>
                    <fulfillerID>testComp</fulfillerID>
                    <fulfillerPartNumber>123123</fulfillerPartNumber>
                    <warehouseLocationID>4000</warehouseLocationID>
                </productFulfillment>
            </more>
            <isViewable>true</isViewable>
            <isOrderable>true</isOrderable>
            <limitedToSupportingLocales>true</limitedToSupportingLocales>
        </product>
    </items>
</loader>
```
{% endcode %}
{% endtab %}

{% tab title="Response sample" %}
{% code overflow="wrap" %}
```xml
<?xml version="1.0"?>
<loaderResponse>
    <importFileName>test.xml</importFileName>
    <message>ok</message>
    <results>
        <result>
            <dataType>Product</dataType>
            <dataID>123123</dataID>
            <externalReferenceID>12312</externalReferenceID>
            <loadStatus>SUCCESSFUL</loadStatus>
            <sku>12312</sku>
        </result>
    </results>
</loaderResponse>
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Remove product example

{% tabs %}
{% tab title="Request sample" %}
{% code overflow="wrap" %}
```xml
<?xml version="1.0" encoding="utf-8"?>
<loader xmlns:xsi = "http://www.w3.org/2001/XMLSchema-instance" 
xmlns:bulk = "ns1:testBulkloader">
    <catalogName>Test Channel Catalog</catalogName>
    <loaderType>itestLoader</loaderType>
    <ownerCompanyID>0</ownerCompanyID>
    <sourceID>testSource</sourceID>
    <items>
        <product>
            <action>REMOVE</action>
            <externalReferenceID>123123</externalReferenceID>
            <companyID>123</companyID>
        </product>
    </items>
</loader>
```
{% endcode %}
{% endtab %}

{% tab title="Response sample" %}
{% code overflow="wrap" %}
```xml
<?xml version="1.0"?>
<loaderResponse>
    <importFileName>test.xml</importFileName>
    <message>ok</message>
    <results>
        <result>
            <dataType>Product</dataType>
            <dataID>123123</dataID>
            <externalReferenceID>12312</externalReferenceID>
            <loadStatus>SUCCESSFUL</loadStatus>            
        </result>
    </results>
</loaderResponse>
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Additional company attributes

The following example shows additional company attributes. These attributes indicate the channel contract acceptance date and email address of the product owner.

{% tabs %}
{% tab title="Attributes example" %}
{% code overflow="wrap" %}
```xml
<attributes>
  <attribute>
       <name>AgreementDateTime</name>
       <value>2008-12-31 23:14:24</value>
  </attribute>
  <attribute>
       <name>emailSignature</name>
       <value>abc@abc.com</value>
  </attribute>
</attributes>
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Schemas

| Version     | Schema Components Table                                                                    | Raw Schema                                                                     | Sample XML                                                                             |
| ----------- | ------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------- |
| 1 (Current) |  [View](https://drhadmin.digitalriver.com/integration/isg/schematable/ChannelBulkLoader/1) |  [View](https://drhadmin.digitalriver.com/integration/xsd/ChannelBulkLoader/1) |  [View](https://drhadmin.digitalriver.com/integration/isg/example/ChannelBulkLoader/1) |

## Order create

Use the Order Create API to submit an order to Digital River for fulfillment. The business process uses XML and HTTPS since the APIs are real-time in nature.

### Details

After you import the product catalog into the client’s e-commerce system, you can enable the order to create a business process. For this business process, the client will process the following items implemented via their e-commerce solution:

* The transaction performing payment authorization
* The fraud check
* Other client-specific transaction processing functions

After processing these items, the client knows the customer and the order are acceptable. The client then uses the Order Create API to submit the order to Digital River for fulfillment. For a digital product, this fulfillment information consists of a Digital River-hosted download URL that the client delivers to the customer who placed the order. The customer uses this URL to download the product they purchased. Sometimes products require a serial number or unlock code in addition to the download URL so the customer can install the product properly. In this case, the Order Create business process returns this information to the client, and the client displays the information to the client on the customer service interface and also sends the information in an email notification to the customer.

The business process uses XML and HTTPS since the APIs are real-time in nature. Clients should consider coding in a timing feature so that, in the very rare case where the call to the Digital River servers takes over 10 seconds or so, they return a page to the customer that says they will send the information the customer requires to get the product they purchased later.

The following table shows the business process specifics.

| Characteristics         | Specification |
| ----------------------- | ------------- |
| Business process type   | Real-Time     |
| Communication protocols | HTTPS         |
| Available data formats  | XML           |

The following diagram shows an overview of the Order Create business process.

![System Architecture](https://files.readme.io/80c1925-order\_create\_system\_architecture.gif)

Multiple orders per request are not supported at this time.

If the Client inadvertently submits the same order twice (that is, the same external order ID and line items), Digital River will accept the request and return the same information via the Order Create Response that it did in the previous order submissions. If one or more of the line items has pending digital rights, Digital River will try to obtain the digital rights before sending the response.

Occasionally Digital River deactivates products as part of product catalog maintenance. If Digital River deactivates a product that appears in a Client's catalog, the return response contains an error code.

When Digital River receives a fulfillment request, Digital River provides an immediate response to this call. This response's XML format follows a specific XML schema.

The following table shows the values for status return codes. There are two types of return codes:

* Return code for the order fulfillment itself
* Return code for each line item quantity unit in the order

For unsuccessful orders with multiple products, the line item order status allows the client to pinpoint the product in the order that caused the failure. Line items in pending status will be resubmitted every hour for up to 30 days.

{% hint style="warning" %}
**Requirement**: The client is responsible for resubmitting any 202/503 status code combinations to verify the order fulfillment status.
{% endhint %}

| Code Types             | Codes                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Order Status Codes     | <p><strong>201 - Success</strong>: All line item units completely fulfilled</p><p><strong>202 - Partial success</strong>: Order was valid, but some line items could not currently be fulfilled</p><p><strong>400 - Bad request</strong>: The server could not understand the request due to malformed syntax</p><p><strong>401 - Unauthorized</strong>: See Error! Reference source not found.</p><p><strong>409 - Unfulfillable</strong>: One or more the line items cannot be fulfilled. Details are provided in corresponding line item status codes (404)</p><p><strong>500 - Temporary service outage</strong>: Retry later (we could set a Retry-After header)</p> |
| Line Item Status Codes | <p><strong>201 - Success</strong>: The unit will contain licenses, <code>actualPrice</code>, and <code>downloadUrl</code></p><p><strong>404 - Not Found</strong>: The requested product is permanently unavailable.</p><p><strong>503 - Unavailable</strong>: Not all of the licenses could be generated at this time, but some will become available in the future. The fulfillment/status/code will be 202.</p>                                                                                                                                                                                                                                                         |

The following example shows a return response for the example order request provided earlier in the document. The earlier request contained two copies of the same product. This fulfillment response shows a license and an unlock code for the first product and a pending digital rights response for the second product.

{% hint style="info" %}
**Note**: Each line item quantity has a fulfillment unit.
{% endhint %}

{% tabs %}
{% tab title="Response sample" %}
{% code overflow="wrap" %}
```xml
<rws:fulfillment
  uri="http://integration.digitalriver.com/integration/job/request/DRRWS
/fulfillment/123/"
  orderUri="http://dealer.acme.com/order/12345A6/"
  xmlns:rws="http://integration.digitalriver.com/2005/10/RetailWebService"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://integration.digitalriver.com/2005/10/RetailWebService 
C:\projects\x-stream\resources\ws\xsd\integration\rws\fulfill.xsd ">
  <status>
    <code>202</code>
    <message/>
  </status>
  <units>
    <unit uri="http://digitalriver.com/drws/fu/452455" 
lineItemUri="http://dealer.acme.com/lineItem/1">
      <status>
        <code>200</code>
        <message>OK</message>
      </status>
      <actualPrice>
        <amount>23.56</amount>
        <currencyCode>USD</currencyCode>
      </actualPrice>
      <downloadUrl>ftp://foo/baz/bar.exe</downloadUrl>
      <licenses>
        <license uri="http://digitalriver.com/drws/lic/42">
          <type>serialNo</type>
          <value>1120348MB67198749756</value>
        </license>
        <license uri="http://digitalriver.com/drws/lic/523">
          <type>unlockCode</type>
          <value>1120348MB67198749756</value>
        </license>
      </licenses>
    </unit>
    <unit uri="http://digitalriver.com/drws/fu/45246" 
lineItemUri="http://dealer.acme.com/lineItem/1">
      <status>
        <code>503</code>
        <message>pending fulfillment </message>
      </status>
      <actualPrice/>
      <downloadUrl/>
      <licenses/>
    </unit>
  </units>
</rws:fulfillment>
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Schemas

| Version     | Schema Components Table                                                                                | Raw Schema                                                                                 | Sample XML                                                                                         |
| ----------- | ------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------- |
| 1 (Current) |  [View](https://drhadmin.digitalriver.com/integration/isg/schematable/IntegratedRetailerOrderCreate/1) |  [View](https://drhadmin.digitalriver.com/integration/xsd/IntegratedRetailerOrderCreate/1) |  [View](https://drhadmin.digitalriver.com/integration/isg/example/IntegratedRetailerOrderCreate/1) |

## Order return

Use the Order Return API when a client needs to reverse the order for a customer based on a customer service issue. The business process uses XML and HTTPS since the APIs are real-time in nature.

### Details

You can use the Order Return API to reverse the transaction on the Digital River-side. The Order Return API notifies Digital River to disable the customer’s download URL.

{% hint style="info" %}
**Note**: If you send an `OrderReturn` for an order that previously resulted in a 202/503 error, Digital River will submit an order cancellation.
{% endhint %}

The Order Return business process works similarly to the Order Create business process in that it leverages XML and HTTPS and has a request and response message-passing sequence.

The following table shows the business process specifics.

| Characteristic          | Specification |
| ----------------------- | ------------- |
| Business process type   | Real-Time     |
| Communication protocols | HTTPS only    |
| Available data formats  | XML           |

The XML format for the Order Return's response follows a specific XML schema provided in the Order Return schemas. The following example shows the order return responses sent to a client.

{% tabs %}
{% tab title="Succesful response" %}
{% code overflow="wrap" %}
```xml
<?xml version="1.0" encoding="UTF-8"?>
<ns1:returnReceipt
   returnRequestUri="http://dealer.acme.com/order/1636395390/1”
   uri=" https://drh1sys.digitalriver.com/integration/job
/request/DRRWS?r=returnLiID/4562889"
   xmlns:rws="http://integration.digitalriver.com/2005/10/RetailWebService"
   xmlns:xsi=http://www.w3.org/2001/XMLSchema-instance>
    <status>
        <code>201</code>
        <message>The return unit request has been submitted successfully.</message>
    </status>
</ns1:returnReceipt>
```
{% endcode %}
{% endtab %}

{% tab title="Successful cancellation response" %}
{% code overflow="wrap" %}
```xml
<?xml version="1.0" encoding="UTF-8"?>
<ns1:returnReceipt
   returnRequestUri="http://dealer.acme.com/order/1636395390/1”
   uri=" https://drh1sys.digitalriver.com/integration/job/request
/DRRWS?r=unit/6353179490-0"
   xmlns:rws="http://integration.digitalriver.com/2005/10/RetailWebService"
   xmlns:xsi=http://www.w3.org/2001/XMLSchema-instance>
    <status>
        <code>201</code>
        <message>The return unit request has been submitted successfully.</message>
    </status>
</ns1:returnReceipt>
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Schemas

| Version     | Schema Components Table                                                                                | Raw Schema                                                                                 | Sample XML                                                                                         |
| ----------- | ------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------- |
| 1 (Current) |  [View](https://drhadmin.digitalriver.com/integration/isg/schematable/IntegratedRetailerOrderReturn/1) |  [View](https://drhadmin.digitalriver.com/integration/xsd/IntegratedRetailerOrderReturn/1) |  [View](https://drhadmin.digitalriver.com/integration/isg/example/IntegratedRetailerOrderReturn/1) |
