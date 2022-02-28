---
description: Understand the order-level satisfaction refund.
---

# Order-level satisfaction refund

{% tabs %}
{% tab title="Request body" %}
```markup
<?xml version="1.0" encoding="UTF-8"?>
<ns1:SalesOrderActivityInfoArray 
xmlns:ns1="http://integration.digitalriver.com/salesOrderActivityInfoArray/1.0">
 <reportBeginDate xsi:type="xsd:dateTime" 
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">
2005-12-20T06:00:00.209Z</reportBeginDate>
 <reportEndDate xsi:type="xsd:dateTime" 
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">
2005-12-20T06:00:00.209Z</reportEndDate>
 <reportRunDate xsi:type="xsd:dateTime" 
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"
>2005-12-21T10:06:11.209Z</reportRunDate>
 <salesOrderActivity xsi:type="ns1:SalesOrderActivityInfo" 
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <orderID xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">1111222223</orderID>
  <saleDate xsi:type="xsd:dateTime" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">2005-12-20T06:00:00.731Z</saleDate>
  <orderDate xsi:type="xsd:dateTime" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">2005-12-19T18:09:59.731Z</orderDate>
  <site xsi:type="ns2:SiteInfo" 
xmlns:ns2="http://integration.digitalriver.com/Common/1.0">
   <siteID xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">cageeks</siteID>
   <siteAddress xsi:type="ns2:AddressInfo">
    <addressID xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
    <city xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">Eden Praire</city>
    <countryA2 xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">US</countryA2>
    <country xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">US</country>
    <countryName xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">United States</countryName>
    <line1 xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">1234 Happy Street</line1>
    <line2 xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"> </line2>
    <line3 xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"> </line3>
    <locationCode xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
    <name1 xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">Digital</name1>
    <name2 xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">River</name2>
    <phoneNumber xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"> </phoneNumber>
    <postalCode xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">55555</postalCode>
    <state xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">MN</state>
    <email xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"> </email>
    <faxPhone xsi:type="xsd:string" 
              xmlns:xsd="http://www.w3.org/2001/XMLSchema"> </faxPhone>
    <companyName xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"> </companyName>
    <phoneNumber2 xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"> </phoneNumber2>
    <countyName xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
    <extendedAttributes xsi:type="ns2:ExtendedAttributesInfoArray" 
xsi:nil="true"/>
   </siteAddress>
   <siteURL xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
  </site>
  <pricing xsi:type="ns3:OrderPriceInfo" 
xmlns:ns3="http://integration.digitalriver.com/commonRequisition/1.0">
   <total xsi:type="ns4:MoneyInfo" 
xmlns:ns4="http://integration.digitalriver.com/Common/1.0">
    <currencyCode xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">USD</currencyCode>
    <amount xsi:type="xsd:decimal" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">-38.00</amount>
   </total>
   <subtotal xsi:type="ns5:MoneyInfo" 
xmlns:ns5="http://integration.digitalriver.com/Common/1.0">
    <currencyCode xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">USD</currencyCode>
    <amount xsi:type="xsd:decimal" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">-38.00</amount>
   </subtotal>
   <tax xsi:type="ns6:MoneyInfo" 
xmlns:ns6="http://integration.digitalriver.com/Common/1.0">
    <currencyCode xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">USD</currencyCode>
    <amount xsi:type="xsd:decimal" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">0.00</amount>
   </tax>
   <shipping xsi:type="ns7:MoneyInfo" 
xmlns:ns7="http://integration.digitalriver.com/Common/1.0">
    <currencyCode xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">USD</currencyCode>
    <amount xsi:type="xsd:decimal" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">0.00</amount>
   </shipping>
   <incentive xsi:type="ns8:MoneyInfo" 
xmlns:ns8="http://integration.digitalriver.com/Common/1.0">
    <currencyCode xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">USD</currencyCode>
    <amount xsi:type="xsd:decimal" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">0.00</amount>
   </incentive>
   <shippingIncentive xsi:type="ns9:MoneyInfo" xsi:nil="true" 
xmlns:ns9="http://integration.digitalriver.com/Common/1.0"/>
   <nonTaxableFees xsi:type="ns10:MoneyInfo" xsi:nil="true" 
xmlns:ns10="http://integration.digitalriver.com/Common/1.0"/>
   <taxableFees xsi:type="ns11:MoneyInfo" xsi:nil="true" 
xmlns:ns11="http://integration.digitalriver.com/Common/1.0"/>
   <taxOnTaxableFees xsi:type="ns12:MoneyInfo" xsi:nil="true" 
xmlns:ns12="http://integration.digitalriver.com/Common/1.0"/>
   <exchangeRate xsi:type="ns13:MoneyInfo" 
xmlns:ns13="http://integration.digitalriver.com/Common/1.0">
    <currencyCode xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">USD</currencyCode>
    <amount xsi:type="xsd:decimal" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">1</amount>
   </exchangeRate>
  </pricing>
  <paymentInfos xsi:type="ns14:PaymentInformationInfoArray" 
xmlns:ns14="http://integration.digitalriver.com/commonRequisition/1.0">
   <paymentInfo xsi:type="ns14:PaymentInformationInfo">
    <authorizationID xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
    <cardType xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">visa</cardType>
    <customerEmail xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">john.doe@gmail.com</customerEmail>
    <cardNumber xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
    <cardExpirationMonth xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
    <cardExpirationYear xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
    <customerPO xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
    <ccIssueCode xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
    <ccIssueMonth xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
    <ccIssueYear xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
    <securityIndicator xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
    <routingNumber xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
    <vatNumber xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"> </vatNumber>
    <customerLastName xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">Doe</customerLastName>
    <customerFirstName xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">John</customerFirstName>
    <paymentAmount xsi:type="ns15:MoneyInfo" 
xmlns:ns15="http://integration.digitalriver.com/Common/1.0">
     <currencyCode xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">USD</currencyCode>
     <amount xsi:type="xsd:decimal" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">-38.00</amount>
    </paymentAmount>
    <paymentMethodName xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
    <billingAddress xsi:type="ns16:AddressInfo" 
xmlns:ns16="http://integration.digitalriver.com/Common/1.0">
     <addressID xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
     <city xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">Eden Prairie</city>
     <countryA2 xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">US</countryA2>
     <country xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">US</country>
     <countryName xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">United States</countryName>
     <line1 xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">1234 Happy Lane</line1>
     <line2 xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"> </line2>
     <line3 xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"> </line3>
     <locationCode xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
     <name1 xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">John</name1>
     <name2 xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">Doe</name2>
     <phoneNumber xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">6122223333</phoneNumber>
     <postalCode xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">55555</postalCode>
     <state xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">mn</state>
     <email xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">john.doe@gmail.com</email>
     <faxPhone xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"> </faxPhone>
     <companyName xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"> </companyName>
     <phoneNumber2 xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"> </phoneNumber2>
     <countyName xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
     <extendedAttributes xsi:type="ns16:ExtendedAttributesInfoArray" xsi:nil="true"/>
    </billingAddress>
   </paymentInfo>
  </paymentInfos>
  <lineItems xsi:type="ns1:LineItemInfoArray">
   <item xsi:type="ns1:LineItemInfo">
    <lineItemID xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">1804676800</lineItemID>
    <transactionDescription xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">
RETURN_RECEIPT</transactionDescription>
    <quantity xsi:type="xsd:integer" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">0</quantity>
    <product xsi:type="ns17:ProductKey" 
xmlns:ns17="http://integration.digitalriver.com/Common/1.0">
     <productID xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">36229900</productID>
     <externalReferenceID xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">S3IP</externalReferenceID>
     <companyID xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">ca</companyID>
     <locale xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
    </product>
    <productInfo xsi:type="ns1:ProductDataInfo">
     <productDataID xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">149635200</productDataID>
     <sku xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">XXXXXXXXXXXX</sku>
     <mfrPartNumber xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"> </mfrPartNumber>
     <shipperPartNumber xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"> </shipperPartNumber>
     <name xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"
>eTrustÂ® PestPatrolÂ® Anti-Spyware 3- User Electronic Delivery</name>
     <platform xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">N/A - not available</platform>
     <companyID xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">ca</companyID>
     <year xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"> </year>
     <seats xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"> </seats>
     <productOwningCompanyName xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">
Computer Associates International, Inc. Master</productOwningCompanyName>
     <extendedAttributes xsi:type="ns18:ExtendedAttributesInfoArray" 
xmlns:ns18="http://integration.digitalriver.com/Common/1.0">
      <item xsi:type="ns18:ExtendedAttributesInfo">
       <name xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">Fireclick Family</name>
       <value xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">PestPatrol</value>
       <valueDataType xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">string</valueDataType>
      </item>
      <item xsi:type="ns18:ExtendedAttributesInfo">
       <name xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">fileSize</name>
       <value xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">21987</value>
       <valueDataType xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">string</valueDataType>
      </item>
      <item xsi:type="ns18:ExtendedAttributesInfo">
       <name xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">numberOfIPAddresses</name>
       <value xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">100</value>
       <valueDataType xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">string</valueDataType>
      </item>
      <item xsi:type="ns18:ExtendedAttributesInfo">
       <name xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">catNameImage</name>
       <value xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">pestpatrol_bannerimg.gif</value>
       <valueDataType xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">string</valueDataType>
      </item>
      <item xsi:type="ns18:ExtendedAttributesInfo">
       <name xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">Incrementor</name>
       <value xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">1</value>
       <valueDataType xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">string</valueDataType>
      </item>
      <item xsi:type="ns18:ExtendedAttributesInfo">
       <name xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">pdNameImage</name>
       <value xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">pp_watermark2.gif</value>
       <valueDataType xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">string</valueDataType>
      </item>
      <item xsi:type="ns18:ExtendedAttributesInfo">
       <name xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">pdRelatedProducts</name>
       <value xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"></value>
       <valueDataType xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">string</valueDataType>
      </item>
      <item xsi:type="ns18:ExtendedAttributesInfo">
       <name xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">userLicenses</name>
       <value xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">10-User</value>
       <valueDataType xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">string</valueDataType>
      </item>
      <item xsi:type="ns18:ExtendedAttributesInfo">
       <name xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">licenseOnly</name>
       <value xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">false</value>
       <valueDataType xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">string</valueDataType>
      </item>
      <item xsi:type="ns18:ExtendedAttributesInfo">
       <name xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">fulfiller</name>
       <value xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">DSS</value>
       <valueDataType xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">string</valueDataType>
      </item>
      <item xsi:type="ns18:ExtendedAttributesInfo">
       <name xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">downloadType</name>
       <value xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">HTTP</value>
       <valueDataType xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">string</valueDataType>
      </item>
      <item xsi:type="ns18:ExtendedAttributesInfo">
       <name xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">userType</name>
       <value xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">New</value>
       <valueDataType xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">string</valueDataType>
      </item>
      <item xsi:type="ns18:ExtendedAttributesInfo">
       <name xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">gameRating</name>
       <value xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">Teen</value>
       <valueDataType xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">string</valueDataType>
      </item>
      <item xsi:type="ns18:ExtendedAttributesInfo">
       <name xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">platform</name>
       <value xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">Windows</value>
       <valueDataType xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">string</valueDataType>
      </item>
      <item xsi:type="ns18:ExtendedAttributesInfo">
       <name xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">timeFrame</name>
       <value xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">60</value>
       <valueDataType xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">string</valueDataType>
      </item>
      <item xsi:type="ns18:ExtendedAttributesInfo">
       <name xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">pdSpecifications</name>
       <value xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"></value>
       <valueDataType xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">string</valueDataType>
      </item>
      <item xsi:type="ns18:ExtendedAttributesInfo">
       <name xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">downloadAction</name>
       <value xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">GET</value>
       <valueDataType xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">string</valueDataType>
      </item>
      <item xsi:type="ns18:ExtendedAttributesInfo">
       <name xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">pdPageTitleText</name>
       <value xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">Anti-Spyware</value>
       <valueDataType xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">string</valueDataType>
      </item>
      <item xsi:type="ns18:ExtendedAttributesInfo">
       <name xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">applicationFile</name>
       <value xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">
PestPatrolv5FullVersion.exe</value>
       <valueDataType xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">string</valueDataType>
      </item>
      <item xsi:type="ns18:ExtendedAttributesInfo">
       <name xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">numberOfDownloads</name>
       <value xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">100</value>
       <valueDataType xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">string</valueDataType>
      </item>
      <item xsi:type="ns18:ExtendedAttributesInfo">
       <name xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">downloadAdapter</name>
       <value xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">
com.digitalriver.downloads.adapters.DRHDownloadAdapter</value>
       <valueDataType xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">string</valueDataType>
      </item>
      <item xsi:type="ns18:ExtendedAttributesInfo">
       <name xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">serverLocation</name>
       <value xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">wgt.digitalriver.com</value>
       <valueDataType xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">string</valueDataType>
      </item>
      <item xsi:type="ns18:ExtendedAttributesInfo">
       <name xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">packageID</name>
       <value xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">36229800</value>
       <valueDataType xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">string</valueDataType>
      </item>
      <item xsi:type="ns18:ExtendedAttributesInfo">
       <name xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">pdHeaderText</name>
       <value xsi:type="xsd:string" xmlns:xsd="http://www.w3.org/2001/XMLSchema">
Remove spyware that leads to identity theft and slow PC performance</value>
       <valueDataType xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">string</valueDataType>
      </item>
     </extendedAttributes>
    </productInfo>
    <lineItemDigitalInfoList xsi:type="ns19:LineItemDigitalInfoArray" 
xmlns:ns19="http://integration.digitalriver.com/commonRequisition/1.0">
     <digitalInfo xsi:type="ns19:LineItemDigitalInfo">
      <serialNumber xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"> </serialNumber>
      <unlockCode xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">KXXTY-ECXXL-XMWKL-RIRL1</unlockCode>
     </digitalInfo>
    </lineItemDigitalInfoList>
    <shipping xsi:type="ns1:ShipmentInfo">
     <shipToAddress xsi:type="ns20:AddressInfo" 
xmlns:ns20="http://integration.digitalriver.com/Common/1.0">
      <addressID xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
      <city xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">Eden Prairie</city>
      <countryA2 xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">US</countryA2>
      <country xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">US</country>
      <countryName xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">United States</countryName>
      <line1 xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">1234 Happy Lane</line1>
      <line2 xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"> </line2>
      <line3 xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"> </line3>
      <locationCode xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
      <name1 xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">John</name1>
      <name2 xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">Doe</name2>
      <phoneNumber xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">6121112222</phoneNumber>
      <postalCode xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">55555</postalCode>
      <state xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">TX</state>
      <email xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"> </email>
      <faxPhone xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"> </faxPhone>
      <companyName xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"> </companyName>
      <phoneNumber2 xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"> </phoneNumber2>
      <countyName xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
      <extendedAttributes xsi:type="ns20:ExtendedAttributesInfoArray" 
xsi:nil="true"/>
     </shipToAddress>
     <shippingMethodName xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"> </shippingMethodName>
     <carrierName xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">United Parcel Service</carrierName>
     <shipmentDate xsi:type="xsd:date" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">2005-12-20</shipmentDate>
     <isReship xsi:type="soapenc:boolean" xsi:nil="true" 
xmlns:soapenc="http://schemas.xmlsoap.org/soap/encoding/"/>
     <fulfillerID xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">ca</fulfillerID>
     <fulfillerName xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">
Computer Associates International, Inc. Master</fulfillerName>
    </shipping>
    <returnInfo xsi:type="ns1:ReturnInfo">
     <returnType xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">
OrderLevelSatisfactionRefund</returnType>
     <returnReason xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">DUPLICATE_ORDER</returnReason>
     <returnDate xsi:type="xsd:date" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">2005-12-20</returnDate>
     <serialNumber xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"> </serialNumber>
     <returnID xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">3104109</returnID>
     <returnLineItemID xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">3841109</returnLineItemID>
    </returnInfo>
    <pricing xsi:type="ns1:LineItemPriceInfo">
     <unitPrice xsi:type="ns21:MoneyInfo" 
xmlns:ns21="http://integration.digitalriver.com/Common/1.0">
      <currencyCode xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">USD</currencyCode>
      <amount xsi:type="xsd:decimal" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">0</amount>
     </unitPrice>
     <listPrice xsi:type="ns22:MoneyInfo" 
xmlns:ns22="http://integration.digitalriver.com/Common/1.0">
      <currencyCode xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">USD</currencyCode>
      <amount xsi:type="xsd:decimal" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">0</amount>
     </listPrice>
     <pricePerQty xsi:type="ns23:MoneyInfo" 
xmlns:ns23="http://integration.digitalriver.com/Common/1.0">
      <currencyCode xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">USD</currencyCode>
      <amount xsi:type="xsd:decimal" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">0</amount>
     </pricePerQty>
     <saleAmount xsi:type="ns24:MoneyInfo" 
xmlns:ns24="http://integration.digitalriver.com/Common/1.0">
      <currencyCode xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">USD</currencyCode>
      <amount xsi:type="xsd:decimal" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">-26.38</amount>
     </saleAmount>
     <shipping xsi:type="ns25:MoneyInfo" 
xmlns:ns25="http://integration.digitalriver.com/Common/1.0">
      <currencyCode xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">USD</currencyCode>
      <amount xsi:type="xsd:decimal" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">0</amount>
     </shipping>
     <shopperShippingCostPerQty xsi:type="ns26:MoneyInfo" 
xmlns:ns26="http://integration.digitalriver.com/Common/1.0">
      <currencyCode xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">USD</currencyCode>
      <amount xsi:type="xsd:decimal" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">0</amount>
     </shopperShippingCostPerQty>
     <handling xsi:type="ns27:MoneyInfo" 
xmlns:ns27="http://integration.digitalriver.com/Common/1.0">
      <currencyCode xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">USD</currencyCode>
      <amount xsi:type="xsd:decimal" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">0</amount>
     </handling>
     <incentive xsi:type="ns28:MoneyInfo" 
xmlns:ns28="http://integration.digitalriver.com/Common/1.0">
      <currencyCode xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">USD</currencyCode>
      <amount xsi:type="xsd:decimal" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">0</amount>
     </incentive>
     <reqLevelIncentivePerQuantity xsi:type="ns29:MoneyInfo" 
xmlns:ns29="http://integration.digitalriver.com/Common/1.0">
      <currencyCode xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">USD</currencyCode>
      <amount xsi:type="xsd:decimal" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">0</amount>
     </reqLevelIncentivePerQuantity>
     <lineItemLevelIncentivePerQuantity xsi:type="ns30:MoneyInfo" 
xmlns:ns30="http://integration.digitalriver.com/Common/1.0">
      <currencyCode xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">USD</currencyCode>
      <amount xsi:type="xsd:decimal" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">0</amount>
     </lineItemLevelIncentivePerQuantity>
     <taxableFeesPerQuantity xsi:type="ns31:MoneyInfo" 
xmlns:ns31="http://integration.digitalriver.com/Common/1.0">
      <currencyCode xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">USD</currencyCode>
      <amount xsi:type="xsd:decimal" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">0</amount>
     </taxableFeesPerQuantity>
    </pricing>
    <lineItemTaxList xsi:type="ns32:LineItemTaxListInfo" 
xmlns:ns32="http://integration.digitalriver.com/commonRequisition/1.0">
     <typeOfTax xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
     <primaryCurrencyCode xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
     <federalTaxType xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
     <territoryTaxType xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
     <stateTaxType xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
     <countyTaxType xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
     <cityTaxType xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
     <secondaryStateTaxType xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
     <secondaryCountyTaxType xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
     <secondaryCityTaxType xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
     <districtTaxType xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
     <zeroRateIndicator xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
     <jurisdictionType xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
     <countryOfJurisdictionCode xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
     <territoryOfJurisdictionCode xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
     <stateOfJurisdiction xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
     <countyCodeOfJurisdiction xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
     <countyNameOfJurisdiction xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
     <cityOfJurisdiction xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
     <zipCodeOfJurisdiction xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
     <zipCodeExtensionOfJurisdiction xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
     <geoCodeOfJurisdiction xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
     <secStateOfJurisdiction xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
     <secCountyCodeOfJurisdiction xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
     <secCountyNameOfJurisdiction xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
     <secCityOfJurisdiction xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
     <secZipCodeOfJurisdiction xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
     <secZipCodeExtensionOfJurisdiction xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
     <secGeoCodeOfJurisdiction xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
     <calculatedTaxAmountTotal xsi:type="ns33:MoneyInfo" 
xmlns:ns33="http://integration.digitalriver.com/Common/1.0">
      <currencyCode xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">USD</currencyCode>
      <amount xsi:type="xsd:decimal" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">0</amount>
     </calculatedTaxAmountTotal>
     <calculatedTaxAmountCountry xsi:type="ns34:MoneyInfo" xsi:nil="true" 
xmlns:ns34="http://integration.digitalriver.com/Common/1.0"/>
     <calculatedTaxAmountTerritory xsi:type="ns35:MoneyInfo" xsi:nil="true" 
xmlns:ns35="http://integration.digitalriver.com/Common/1.0"/>
     <calculatedTaxAmountState xsi:type="ns36:MoneyInfo" xsi:nil="true" 
xmlns:ns36="http://integration.digitalriver.com/Common/1.0"/>
     <calculatedTaxAmountCounty xsi:type="ns37:MoneyInfo" xsi:nil="true" 
xmlns:ns37="http://integration.digitalriver.com/Common/1.0"/>
     <calculatedTaxAmountCity xsi:type="ns38:MoneyInfo" xsi:nil="true" 
xmlns:ns38="http://integration.digitalriver.com/Common/1.0"/>
     <calculatedTaxAmountSecState xsi:type="ns39:MoneyInfo" xsi:nil="true" 
xmlns:ns39="http://integration.digitalriver.com/Common/1.0"/>
     <calculatedTaxAmountSecCounty xsi:type="ns40:MoneyInfo" xsi:nil="true" 
xmlns:ns40="http://integration.digitalriver.com/Common/1.0"/>
     <calculatedTaxAmountSecCity xsi:type="ns41:MoneyInfo" xsi:nil="true" 
xmlns:ns41="http://integration.digitalriver.com/Common/1.0"/>
     <calculatedTaxAmountDistrict xsi:type="ns42:MoneyInfo" xsi:nil="true" 
xmlns:ns42="http://integration.digitalriver.com/Common/1.0"/>
     <sellerVatNumber xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
     <buyerVatNumber xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
     <commodityCode xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
     <taxCompanyID xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
     <stateTaxRate xsi:type="xsd:decimal" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
     <secStateTaxRate xsi:type="xsd:decimal" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
     <countyTaxRate xsi:type="xsd:decimal" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
     <secCountyTaxRate xsi:type="xsd:decimal" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
     <cityTaxRate xsi:type="xsd:decimal" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
     <secCityTaxRate xsi:type="xsd:decimal" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
     <countryTaxRate xsi:type="xsd:decimal" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
     <taxDate xsi:type="xsd:date" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
    </lineItemTaxList>
    <offerID xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"> </offerID>
    <extendedAttributes xsi:type="ns43:ExtendedAttributesInfoArray" 
xmlns:ns43="http://integration.digitalriver.com/Common/1.0">
     <item xsi:type="ns43:ExtendedAttributesInfo">
      <name xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">KEYRESPRETURNCODE</name>
      <value xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">0</value>
      <valueDataType xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">string</valueDataType>
     </item>
     <item xsi:type="ns43:ExtendedAttributesInfo">
      <name xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">CustomerNumber1</name>
      <value xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">00482A0303</value>
      <valueDataType xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">string</valueDataType>
     </item>
     <item xsi:type="ns43:ExtendedAttributesInfo">
      <name xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">
clientPartnerExternalReferenceID</name>
      <value xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">geeksoncall</value>
      <valueDataType xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">string</valueDataType>
     </item>
     <item xsi:type="ns43:ExtendedAttributesInfo">
      <name xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">companyProgramID</name>
      <value xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">1234</value>
      <valueDataType xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">string</valueDataType>
     </item>
     <item xsi:type="ns43:ExtendedAttributesInfo">
      <name xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">CustomerNumber3</name>
      <value xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">00482A0305</value>
      <valueDataType xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">string</valueDataType>
     </item>
     <item xsi:type="ns43:ExtendedAttributesInfo">
      <name xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">CustomerNumber2</name>
      <value xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">00482A0304</value>
      <valueDataType xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">string</valueDataType>
     </item>
     <item xsi:type="ns43:ExtendedAttributesInfo">
      <name xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">expirationDate</name>
      <value xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">12/19/2006 1:09:58 PM</value>
      <valueDataType xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">string</valueDataType>
     </item>
     <item xsi:type="ns43:ExtendedAttributesInfo">
      <name xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">verificationString</name>
      <value xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">
612a76cdb73878e734437e6601b50e32</value>
      <valueDataType xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">string</valueDataType>
     </item>
    </extendedAttributes>
   </item>
   <item xsi:type="ns1:LineItemInfo">
    <lineItemID xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">1804679600</lineItemID>
    <transactionDescription xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">
RETURN_RECEIPT</transactionDescription>
    <quantity xsi:type="xsd:integer" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">0</quantity>
    <product xsi:type="ns44:ProductKey" 
xmlns:ns44="http://integration.digitalriver.com/Common/1.0">
     <productID xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">35184000</productID>
     <externalReferenceID xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">PPIP</externalReferenceID>
     <companyID xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">ca</companyID>
     <locale xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
    </product>
    <productInfo xsi:type="ns1:ProductDataInfo">
     <productDataID xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">150008400</productDataID>
     <sku xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">ETRPP50EDL01</sku>
     <mfrPartNumber xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"> </mfrPartNumber>
     <shipperPartNumber xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"> </shipperPartNumber>
     <name xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">
eTrustÂ® PestPatrolÂ® Anti-Spyware Electronic Delivery</name>
     <platform xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">N/A - not available</platform>
     <companyID xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">ca</companyID>
     <year xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"> </year>
     <seats xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"> </seats>
     <productOwningCompanyName xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">
Computer Associates International, Inc. Master</productOwningCompanyName>
     <extendedAttributes xsi:type="ns45:ExtendedAttributesInfoArray" 
xmlns:ns45="http://integration.digitalriver.com/Common/1.0">
      <item xsi:type="ns45:ExtendedAttributesInfo">
       <name xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">longGeeks</name>
       <value xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"></value>
       <valueDataType xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">string</valueDataType>
      </item>
      <item xsi:type="ns45:ExtendedAttributesInfo">
       <name xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">numberOfIPAddresses</name>
       <value xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">100</value>
       <valueDataType xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">string</valueDataType>
      </item>
      <item xsi:type="ns45:ExtendedAttributesInfo">
       <name xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">catNameImage</name>
       <value xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">pestpatrol_bannerimg.gif</value>
       <valueDataType xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">string</valueDataType>
      </item>
      <item xsi:type="ns45:ExtendedAttributesInfo">
       <name xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">longOmni</name>
       <value xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"> </value>
       <valueDataType xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">string</valueDataType>
      </item>
      <item xsi:type="ns45:ExtendedAttributesInfo">
       <name xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">userLicenses</name>
       <value xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">Single User</value>
       <valueDataType xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">string</valueDataType>
      </item>
      <item xsi:type="ns45:ExtendedAttributesInfo">
       <name xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">licenseOnly</name>
       <value xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">false</value>
       <valueDataType xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">string</valueDataType>
      </item>
      <item xsi:type="ns45:ExtendedAttributesInfo">
       <name xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">downloadType</name>
       <value xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">HTTP</value>
       <valueDataType xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">string</valueDataType>
      </item>
      <item xsi:type="ns45:ExtendedAttributesInfo">
       <name xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">fulfiller</name>
       <value xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">DSS</value>
       <valueDataType xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">string</valueDataType>
      </item>
      <item xsi:type="ns45:ExtendedAttributesInfo">
       <name xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">userType</name>
       <value xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">New</value>
       <valueDataType xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">string</valueDataType>
      </item>
      <item xsi:type="ns45:ExtendedAttributesInfo">
       <name xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">gameRating</name>
       <value xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">Teen</value>
       <valueDataType xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">string</valueDataType>
      </item>
      <item xsi:type="ns45:ExtendedAttributesInfo">
       <name xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">platform</name>
       <value xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">Windows</value>
       <valueDataType xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">string</valueDataType>
      </item>
      <item xsi:type="ns45:ExtendedAttributesInfo">
       <name xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">multiPacks</name>
       <value xsi:type="xsd:string" xmlns:xsd="http://www.w3.org/2001/XMLSchema"></value>
       <valueDataType xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">string</valueDataType>
      </item>
      <item xsi:type="ns45:ExtendedAttributesInfo">
       <name xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">numberOfDownloads</name>
       <value xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">100</value>
       <valueDataType xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">string</valueDataType>
      </item>
      <item xsi:type="ns45:ExtendedAttributesInfo">
       <name xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">downloadAdapter</name>
       <value xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">
com.digitalriver.downloads.adapters.DRHDownloadAdapter</value>
       <valueDataType xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">string</valueDataType>
      </item>
      <item xsi:type="ns45:ExtendedAttributesInfo">
       <name xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">serverLocation</name>
       <value xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">wgt.digitalriver.com</value>
       <valueDataType xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">string</valueDataType>
      </item>
      <item xsi:type="ns45:ExtendedAttributesInfo">
       <name xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">packageID</name>
       <value xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">36245100</value>
       <valueDataType xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">string</valueDataType>
      </item>
      <item xsi:type="ns45:ExtendedAttributesInfo">
       <name xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">pdHeaderText</name>
       <value xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">
Remove spyware that leads to identity theft and slow PC performance</value>
       <valueDataType xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">string</valueDataType>
      </item>
      <item xsi:type="ns45:ExtendedAttributesInfo">
       <name xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">longMicro</name>
       <value xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"></value>
       <valueDataType xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">string</valueDataType>
      </item>
      <item xsi:type="ns45:ExtendedAttributesInfo">
       <name xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">weight</name>
       <value xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">2.59 lb</value>
       <valueDataType xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">string</valueDataType>
      </item>
     </extendedAttributes>
    </productInfo>
    <lineItemDigitalInfoList xsi:type="ns46:LineItemDigitalInfoArray" 
xmlns:ns46="http://integration.digitalriver.com/commonRequisition/1.0">
     <digitalInfo xsi:type="ns46:LineItemDigitalInfo">
      <serialNumber xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"> </serialNumber>
      <unlockCode xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">WXXTY-ECXXL-XMWKL-RIREM</unlockCode>
     </digitalInfo>
    </lineItemDigitalInfoList>
    <shipping xsi:type="ns1:ShipmentInfo">
     <shipToAddress xsi:type="ns47:AddressInfo" 
xmlns:ns47="http://integration.digitalriver.com/Common/1.0">
      <addressID xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
      <city xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">Eden Prairie</city>
      <countryA2 xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">US</countryA2>
      <country xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">US</country>
      <countryName xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">United States</countryName>
      <line1 xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">11303 Prestige Dr</line1>
      <line2 xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"> </line2>
      <line3 xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"> </line3>
      <locationCode xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
      <name1 xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">John</name1>
      <name2 xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">Doe</name2>
      <phoneNumber xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">6121113333</phoneNumber>
      <postalCode xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">55555</postalCode>
      <state xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">MN</state>
      <email xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"> </email>
      <faxPhone xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"> </faxPhone>
      <companyName xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"> </companyName>
      <phoneNumber2 xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"> </phoneNumber2>
      <countyName xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
      <extendedAttributes xsi:type="ns47:ExtendedAttributesInfoArray" 
xsi:nil="true"/>
     </shipToAddress>
     <shippingMethodName xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"> </shippingMethodName>
     <carrierName xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">United Parcel Service</carrierName>
     <shipmentDate xsi:type="xsd:date" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">2005-12-20</shipmentDate>
     <isReship xsi:type="soapenc:boolean" xsi:nil="true" 
xmlns:soapenc="http://schemas.xmlsoap.org/soap/encoding/"/>
     <fulfillerID xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">ca</fulfillerID>
     <fulfillerName xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">
Computer Associates International, Inc. Master</fulfillerName>
    </shipping>
    <returnInfo xsi:type="ns1:ReturnInfo">
     <returnType xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">
OrderLevelSatisfactionRefund</returnType>
     <returnReason xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">DUPLICATE_ORDER</returnReason>
     <returnDate xsi:type="xsd:date" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">2005-12-20</returnDate>
     <serialNumber xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"> </serialNumber>
     <returnID xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">3104109</returnID>
     <returnLineItemID xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">3841209</returnLineItemID>
    </returnInfo>
    <pricing xsi:type="ns1:LineItemPriceInfo">
     <unitPrice xsi:type="ns48:MoneyInfo" 
xmlns:ns48="http://integration.digitalriver.com/Common/1.0">
      <currencyCode xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">USD</currencyCode>
      <amount xsi:type="xsd:decimal" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">0</amount>
     </unitPrice>
     <listPrice xsi:type="ns49:MoneyInfo" 
xmlns:ns49="http://integration.digitalriver.com/Common/1.0">
      <currencyCode xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">USD</currencyCode>
      <amount xsi:type="xsd:decimal" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">0</amount>
     </listPrice>
     <pricePerQty xsi:type="ns50:MoneyInfo" 
xmlns:ns50="http://integration.digitalriver.com/Common/1.0">
      <currencyCode xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">USD</currencyCode>
      <amount xsi:type="xsd:decimal" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">0</amount>
     </pricePerQty>
     <saleAmount xsi:type="ns51:MoneyInfo" 
xmlns:ns51="http://integration.digitalriver.com/Common/1.0">
      <currencyCode xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">USD</currencyCode>
      <amount xsi:type="xsd:decimal" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">-11.62</amount>
     </saleAmount>
     <shipping xsi:type="ns52:MoneyInfo" 
xmlns:ns52="http://integration.digitalriver.com/Common/1.0">
      <currencyCode xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">USD</currencyCode>
      <amount xsi:type="xsd:decimal" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">0</amount>
     </shipping>
     <shopperShippingCostPerQty xsi:type="ns53:MoneyInfo" 
xmlns:ns53="http://integration.digitalriver.com/Common/1.0">
      <currencyCode xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">USD</currencyCode>
      <amount xsi:type="xsd:decimal" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">0</amount>
     </shopperShippingCostPerQty>
     <handling xsi:type="ns54:MoneyInfo" 
xmlns:ns54="http://integration.digitalriver.com/Common/1.0">
      <currencyCode xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">USD</currencyCode>
      <amount xsi:type="xsd:decimal" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">0</amount>
     </handling>
     <incentive xsi:type="ns55:MoneyInfo" 
xmlns:ns55="http://integration.digitalriver.com/Common/1.0">
      <currencyCode xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">USD</currencyCode>
      <amount xsi:type="xsd:decimal" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">0</amount>
     </incentive>
     <reqLevelIncentivePerQuantity xsi:type="ns56:MoneyInfo" 
xmlns:ns56="http://integration.digitalriver.com/Common/1.0">
      <currencyCode xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">USD</currencyCode>
      <amount xsi:type="xsd:decimal" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">0</amount>
     </reqLevelIncentivePerQuantity>
     <lineItemLevelIncentivePerQuantity xsi:type="ns57:MoneyInfo" 
xmlns:ns57="http://integration.digitalriver.com/Common/1.0">
      <currencyCode xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">USD</currencyCode>
      <amount xsi:type="xsd:decimal" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">0</amount>
     </lineItemLevelIncentivePerQuantity>
     <taxableFeesPerQuantity xsi:type="ns58:MoneyInfo" 
xmlns:ns58="http://integration.digitalriver.com/Common/1.0">
      <currencyCode xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">USD</currencyCode>
      <amount xsi:type="xsd:decimal" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">0</amount>
     </taxableFeesPerQuantity>
    </pricing>
    <lineItemTaxList xsi:type="ns59:LineItemTaxListInfo" 
xmlns:ns59="http://integration.digitalriver.com/commonRequisition/1.0">
     <typeOfTax xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
     <primaryCurrencyCode xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
     <federalTaxType xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
     <territoryTaxType xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
     <stateTaxType xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
     <countyTaxType xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
     <cityTaxType xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
     <secondaryStateTaxType xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
     <secondaryCountyTaxType xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
     <secondaryCityTaxType xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
     <districtTaxType xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
     <zeroRateIndicator xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
     <jurisdictionType xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
     <countryOfJurisdictionCode xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
     <territoryOfJurisdictionCode xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
     <stateOfJurisdiction xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
     <countyCodeOfJurisdiction xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
     <countyNameOfJurisdiction xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
     <cityOfJurisdiction xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
     <zipCodeOfJurisdiction xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
     <zipCodeExtensionOfJurisdiction xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
     <geoCodeOfJurisdiction xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
     <secStateOfJurisdiction xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
     <secCountyCodeOfJurisdiction xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
     <secCountyNameOfJurisdiction xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
     <secCityOfJurisdiction xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
     <secZipCodeOfJurisdiction xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
     <secZipCodeExtensionOfJurisdiction xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
     <secGeoCodeOfJurisdiction xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
     <calculatedTaxAmountTotal xsi:type="ns60:MoneyInfo" 
xmlns:ns60="http://integration.digitalriver.com/Common/1.0">
      <currencyCode xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">USD</currencyCode>
      <amount xsi:type="xsd:decimal" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">0</amount>
     </calculatedTaxAmountTotal>
     <calculatedTaxAmountCountry xsi:type="ns61:MoneyInfo" xsi:nil="true" 
xmlns:ns61="http://integration.digitalriver.com/Common/1.0"/>
     <calculatedTaxAmountTerritory xsi:type="ns62:MoneyInfo" xsi:nil="true" 
xmlns:ns62="http://integration.digitalriver.com/Common/1.0"/>
     <calculatedTaxAmountState xsi:type="ns63:MoneyInfo" xsi:nil="true" 
xmlns:ns63="http://integration.digitalriver.com/Common/1.0"/>
     <calculatedTaxAmountCounty xsi:type="ns64:MoneyInfo" xsi:nil="true" 
xmlns:ns64="http://integration.digitalriver.com/Common/1.0"/>
     <calculatedTaxAmountCity xsi:type="ns65:MoneyInfo" xsi:nil="true" 
xmlns:ns65="http://integration.digitalriver.com/Common/1.0"/>
     <calculatedTaxAmountSecState xsi:type="ns66:MoneyInfo" xsi:nil="true" 
xmlns:ns66="http://integration.digitalriver.com/Common/1.0"/>
     <calculatedTaxAmountSecCounty xsi:type="ns67:MoneyInfo" xsi:nil="true" 
xmlns:ns67="http://integration.digitalriver.com/Common/1.0"/>
     <calculatedTaxAmountSecCity xsi:type="ns68:MoneyInfo" xsi:nil="true" 
xmlns:ns68="http://integration.digitalriver.com/Common/1.0"/>
     <calculatedTaxAmountDistrict xsi:type="ns69:MoneyInfo" xsi:nil="true" 
xmlns:ns69="http://integration.digitalriver.com/Common/1.0"/>
     <sellerVatNumber xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
     <buyerVatNumber xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
     <commodityCode xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
     <taxCompanyID xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
     <stateTaxRate xsi:type="xsd:decimal" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
     <secStateTaxRate xsi:type="xsd:decimal" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
     <countyTaxRate xsi:type="xsd:decimal" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
     <secCountyTaxRate xsi:type="xsd:decimal" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
     <cityTaxRate xsi:type="xsd:decimal" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
     <secCityTaxRate xsi:type="xsd:decimal" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
     <countryTaxRate xsi:type="xsd:decimal" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
     <taxDate xsi:type="xsd:date" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
    </lineItemTaxList>
    <offerID xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"> </offerID>
    <extendedAttributes xsi:type="ns70:ExtendedAttributesInfoArray" 
xmlns:ns70="http://integration.digitalriver.com/Common/1.0">
     <item xsi:type="ns70:ExtendedAttributesInfo">
      <name xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">KEYRESPRETURNCODE</name>
      <value xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">0</value>
      <valueDataType xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">string</valueDataType>
     </item>
     <item xsi:type="ns70:ExtendedAttributesInfo">
      <name xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">companyProgramID</name>
      <value xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">1234</value>
      <valueDataType xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">string</valueDataType>
     </item>
     <item xsi:type="ns70:ExtendedAttributesInfo">
      <name xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">
clientPartnerExternalReferenceID</name>
      <value xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">geeksoncall</value>
      <valueDataType xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">string</valueDataType>
     </item>
     <item xsi:type="ns70:ExtendedAttributesInfo">
      <name xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">CustomerNumber1</name>
      <value xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">00482A0306</value>
      <valueDataType xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">string</valueDataType>
     </item>
     <item xsi:type="ns70:ExtendedAttributesInfo">
      <name xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">expirationDate</name>
      <value xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">12/19/2006 1:09:59 PM</value>
      <valueDataType xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">string</valueDataType>
     </item>
     <item xsi:type="ns70:ExtendedAttributesInfo">
      <name xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">verificationString</name>
      <value xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">
07a8272a8f59c60a7b43349370721c4c</value>
      <valueDataType xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">string</valueDataType>
     </item>
    </extendedAttributes>
   </item>
  </lineItems>
  <offerID xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">15111009</offerID>
  <programID xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"> </programID>
  <customerID xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">10616862409</customerID>
  <loginID xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">john.doe@gmail.com</loginID>
  <optIn xsi:type="soapenc:boolean" 
xmlns:soapenc="http://schemas.xmlsoap.org/soap/encoding/">false</optIn>
  <currencyCodeAlpha xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">USD</currencyCodeAlpha>
  <currencyCodeNumeric xsi:type="xsd:string" xsi:nil="true" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"/>
  <locale xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">en_US</locale>
  <extendedAttributes xsi:type="ns71:ExtendedAttributesInfoArray" 
xmlns:ns71="http://integration.digitalriver.com/Common/1.0">
   <item xsi:type="ns71:ExtendedAttributesInfo">
    <name xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">EndUserCity</name>
    <value xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">Minneapolis</value>
    <valueDataType xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">string</valueDataType>
   </item>
   <item xsi:type="ns71:ExtendedAttributesInfo">
    <name xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">EndUserAddress2</name>
    <value xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"></value>
    <valueDataType xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">string</valueDataType>
   </item>
   <item xsi:type="ns71:ExtendedAttributesInfo">
    <name xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">EndUserEmail</name>
    <value xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">janedoe@gmail.com</value>
    <valueDataType xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">string</valueDataType>
   </item>
   <item xsi:type="ns71:ExtendedAttributesInfo">
    <name xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">EndUserCountry</name>
    <value xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">US</value>
    <valueDataType xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">string</valueDataType>
   </item>
   <item xsi:type="ns71:ExtendedAttributesInfo">
    <name xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">EndUserPwd</name>
    <value xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">geek11</value>
    <valueDataType xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">string</valueDataType>
   </item>
   <item xsi:type="ns71:ExtendedAttributesInfo">
    <name xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">TechnicianID</name>
    <value xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">WE3994GE00</value>
    <valueDataType xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">string</valueDataType>
   </item>
   <item xsi:type="ns71:ExtendedAttributesInfo">
    <name xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">EndUserZipCode</name>
    <value xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">55555</value>
    <valueDataType xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">string</valueDataType>
   </item>
   <item xsi:type="ns71:ExtendedAttributesInfo">
    <name xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">FranchiseID</name>
    <value xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">ME5482GE00</value>
    <valueDataType xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">string</valueDataType>
   </item>
   <item xsi:type="ns71:ExtendedAttributesInfo">
    <name xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">EndUserFName</name>
    <value xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">Jane</value>
    <valueDataType xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">string</valueDataType>
   </item>
   <item xsi:type="ns71:ExtendedAttributesInfo">
    <name xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">EndUserState</name>
    <value xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">MN</value>
    <valueDataType xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">string</valueDataType>
   </item>
   <item xsi:type="ns71:ExtendedAttributesInfo">
    <name xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">EndUserAddress1</name>
    <value xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">12345 Happy Street</value>
    <valueDataType xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">string</valueDataType>
   </item>
   <item xsi:type="ns71:ExtendedAttributesInfo">
    <name xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">EndUserLName</name>
    <value xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">Doe</value>
    <valueDataType xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">string</valueDataType>
   </item>
   <item xsi:type="ns71:ExtendedAttributesInfo">
    <name xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">EndUserCompName</name>
    <value xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"></value>
    <valueDataType xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">string</valueDataType>
   </item>
   <item xsi:type="ns71:ExtendedAttributesInfo">
    <name xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">DPLResult</name>
    <value xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">Accept</value>
    <valueDataType xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">string</valueDataType>
   </item>
   <item xsi:type="ns71:ExtendedAttributesInfo">
    <name xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">EndUserPhone</name>
    <value xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema"></value>
    <valueDataType xsi:type="xsd:string" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema">string</valueDataType>
   </item>
  </extendedAttributes>
 </salesOrderActivity>
</ns1:SalesOrderActivityInfoArray>
```
{% endtab %}
{% endtabs %}
