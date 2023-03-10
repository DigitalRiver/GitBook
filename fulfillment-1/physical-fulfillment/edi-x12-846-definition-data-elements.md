---
description: Understand the EDI X12 846 definition data elements.
---

# EDI X12 846 definition data elements

| Position      | Element ID | Description                                                                                                                                                               |
| ------------- | ---------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Envelope**  |            |                                                                                                                                                                           |
| **ISA**       |            | <p><strong>Interchange Control Header</strong><br><strong>Min/Max</strong>: 1<br><strong>Required</strong>: Y</p>                                                         |
| ISA01         | I01        | <p>Authorization Information Qualifier<br><strong>Type</strong>: ID<br><strong>Min/Max</strong>: 2/2<br><strong>Required</strong>: Y<br><strong>Comments</strong>: 00</p> |
| ISA02         | I02        | <p>Authorization Information<br><strong>Type</strong>: AN<br><strong>Min/Max</strong>: 10/10<br><strong>Required</strong>: Y</p>                                          |
| ISA03         | I03        | <p>Security Information Qualifier<br>Type: ID<br><strong>Min/Max</strong>: 2/2<br><strong>Required</strong>: Y<br><strong>Comments</strong>: 00</p>                       |
| ISA04         | I04        | <p>Security Information<br><strong>Type</strong>: AN<br><strong>Required</strong>: </p>                                                                                   |
| ISA05         | I05        | <p>Interchange ID Qualifier<br><strong>Type</strong>: ID<br><strong>Min/Max</strong>: 2/2<br><strong>Required</strong>: Y<br><strong>Comments</strong>: 01</p>            |
| ISA06         | I06        | <p>Interchange Sender ID<br><strong>Type</strong>: AN<br><strong>Required</strong>: Y</p>                                                                                 |
| ISA07         | I05        | <p>Interchange ID Qualifier<br><strong>Type</strong>: ID<br><strong>Min/Max</strong>: 2/2<br><strong>Required</strong>: Y<br><strong>Comments</strong>: 01</p>            |
| ISA08         | I07        | <p>Interchange Receiver ID<br><strong>Type</strong>: AN<br><strong>Min/Max</strong>: 15/15<br><strong>Required</strong>: Y</p>                                            |
| ISA09         | I08        | <p>Interchange Date<br><strong>Type</strong>: DT<br><strong>Required</strong>: Y</p>                                                                                      |
| ISA10         | I09        | <p>Interchange Time<br><strong>Type</strong>: TM<br><strong>Required</strong>: Y</p>                                                                                      |
| ISA11         | I10        | <p>Interchange Control Standards ID<br><strong>Type</strong>: ID<br><strong>Min/Max</strong>: ID<br><strong>Required</strong>: Y</p>                                      |
| ISA12         | I11        | <p>Interchange Control Version Number<br><strong>Type</strong>: ID<br><strong>Min/Max</strong>: 5/5<br><strong>Required</strong>: Y</p>                                   |
| ISA13         | I12        | <p>Interchange Control Number<br><strong>Type</strong>: N0<br><strong>Min/Max</strong>: 9/9<br><strong>Required</strong>: Y</p>                                           |
| ISA14         | I13        | <p>Acknowledgment Requested<br><strong>Type</strong>: ID<br><strong>Min/Max</strong>: 1/1<br><strong>Required</strong>: Y</p>                                             |
| ISA15         | I14        | <p>Usage Indicator<br><strong>Type</strong>: ID<br><strong>Min/Max</strong>: 1/1<br><strong>Required</strong>: Y<br><strong>Comments</strong>: P=Production, T=Test</p>   |
| ISA16         | I15        | <p>Component Element Separator<br><strong>Min/Max</strong>: 1/1<br><strong>Required</strong>: Y</p>                                                                       |
| GS            |            | <p><strong>Functional Group Header</strong><br><strong>Min/Max</strong>: 1<br><strong>Required</strong>: Y</p>                                                            |
| GS01          | 479        | <p>Functional Identifier Code<br><strong>Type</strong>: ID<br><strong>Min/Max</strong>: 2/2<br><strong>Required</strong>: Y</p>                                           |
| GS02          | 142        | <p>Application Sender's Code<br><strong>Type</strong>: An<br><strong>Min/Max</strong>: 2/15<br><strong>Required</strong>: Y</p>                                           |
| GS03          | 124        | <p>Application Receiver's Code<br><strong>Type</strong>: AN<br><strong>Min/Max</strong>: 2/15<br><strong>Required</strong>: Y</p>                                         |
| GS04          | 373        | <p>Date<br><strong>Type</strong>: DT<br><strong>Min/Max</strong>:8/8<br><strong>Required</strong>: Y</p>                                                                  |
| GS05          | 337        | <p>Time<br><strong>Type</strong>: TM<br><strong>Min/Max</strong>: 4/8<br><strong>Required</strong>: Y</p>                                                                 |
| GS06          | 28         | <p>Group Control Number<br><strong>Type</strong>: N0<br><strong>Min/Max</strong>: 1/9<br><strong>Required</strong>: Y</p>                                                 |
| GS07          | 455        | <p>Responsible Agency Code<br><strong>Type</strong>: ID<br><strong>Min/Max</strong>: 1/2<br><strong>Required</strong>: Y</p>                                              |
| GS08          | 480        | <p>Version / Release / Industry ID<br><strong>Type</strong>: AN<br><strong>Min/Max</strong>: 1/12<br><strong>Required</strong>: Y<br><strong>Comments</strong>: 4010</p>  |
| **Heading**   |            |                                                                                                                                                                           |
|  **ST**       |            | <p><strong>Transaction Set Header</strong><br><strong>Min/Max</strong>: 1<br><strong>Required</strong>: Y</p>                                                             |
| ST01          | 143        | <p>Transaction Set Identifier Code<br><strong>Type</strong>: ID<br><strong>Min/Max</strong>: 3/3<br><strong>Required</strong>: Y<br><strong>Comments</strong>: 846</p>    |
| ST02          | 329        | <p>Transaction Set Control Number<br><strong>Type</strong>: AN<br><strong>Min/Max</strong>: 4/9<br><strong>Required</strong>: Y</p>                                       |
| **BIA**       |            | <p><strong>Beginning Segment for Inventory Inquiry</strong><br><strong>Min/Max</strong>: 1<br><strong>Required</strong>: Y</p>                                            |
| BIA01         | 353        | <p>Transaction Set Purpose Code<br><strong>Type</strong>: ID<br><strong>Min/Max</strong>: 2/2<br><strong>Required</strong>: Y<br><strong>Comments</strong>: 00</p>        |
|               |            |  _00–Original_                                                                                                                                                            |
|               |            |  _25—Incremental_                                                                                                                                                         |
| BIA02         | 755        | <p>Report Type Code<br><strong>Type</strong>: ID<br><strong>Min/Max</strong>: 2/2<br><strong>Required</strong>: Y</p>                                                     |
|               |            | <p><em>DD–Distributor Inventory</em><br><strong>ReportType</strong>: AN<br><strong>Min/Max</strong>: 1/15<br><strong>Required</strong>: Y</p>                             |
| BIA03         | 127        | <p>Reference Identification<br><strong>Type</strong>: AN<br><strong>Min/Max</strong>:1/30<br><strong>Required</strong>: Y</p>                                             |
| BIA04         | 373        | <p>Date<br><strong>Type</strong>: DT<br><strong>Min/Max</strong>: 8/8<br><strong>Required</strong>: Y</p>                                                                 |
| **Detail**    |            |                                                                                                                                                                           |
| **LIN**       |            | <p><strong>Line Item Description</strong><br><strong>Min/Max</strong>: 1<br><strong>Required</strong>: Y</p>                                                              |
| LIN01         | 350        | <p>Assigned Identification<br><strong>Type</strong>: AN<br><strong>Min/Max</strong>: 2/20<br><strong>Required</strong>: N</p>                                             |
| LIN02         | 235        | <p>Product/Service ID Qualifier<br><strong>Type</strong>: ID<br><strong>Min/Max</strong>: 2<br><strong>Required</strong>: Y<br><strong>Comments</strong>: VP</p>          |
|               |            | <p><em>VP—Vendor/Seller Part Number</em><br><strong>Min/Max</strong>: 1/18</p>                                                                                            |
|               |            | <p><em>MG—Manufacturer Part Number</em><br><strong>Min/Max</strong>: 1/20</p>                                                                                             |
|               |            | <p><em>UP—UPC Consumer Package Code</em><br><strong>Min/Max</strong>: 1/20</p>                                                                                            |
| LIN03         | 234        | <p>Product Service ID<br><strong>Type</strong>: AN<br><strong>Required</strong>: Y</p>                                                                                    |
| **SDQ**       |            | <p><strong>Quantity</strong><br><strong>Required</strong>: N<br><strong>Comments</strong>: Requires either SDQ or QTY</p>                                                 |
| SDQ01         | 355        | <p>Unit or Basis for Measurement Code<br>Type: AN<br><strong>Min/Max</strong>: 2/2<br><strong>Required</strong>: N</p>                                                    |
|               |            | _EA–Each_                                                                                                                                                                 |
| SDQ02         | 66         | <p>Identification Code Qualifier<br><strong>Type</strong>: ID<br><strong>Min/Max</strong>: 2/2<br><strong>Required</strong>: N</p>                                        |
|               |            | _9—Assigned by Seller_                                                                                                                                                    |
| SDQ03         | 67         | <p>Identification Code<br><strong>Type</strong>: AN<br><strong>Min/Max</strong>: 1/20<br><strong>Required</strong>: N<br><strong>Comments</strong>: Warehouse ID</p>      |
| SDQ04         | 380        | <p>Quantity<br><strong>Type</strong>: AN<br><strong>Min/Max</strong>: 1/15<br><strong>Required</strong>: N</p>                                                            |
| **QTY**       |            | <p><strong>Quantity</strong><br><strong>Required</strong>: N<br><strong>Comments</strong>: Requires either SDQ or QTY</p>                                                 |
| QTY 01        | 673        | <p>Quantity Qualifier<br><strong>Type</strong>: ID<br><strong>Min/Max</strong>: 2/2<br><strong>Required</strong>: N</p>                                                   |
| QTY 02        | 380        | <p>Quantity<br><strong>Type</strong>: AN<br><strong>Min/Max</strong>: 1/15<br><strong>Required</strong>: N</p>                                                            |
| QTY 03        | 355        | <p>Unit of Measurement Code<br><strong>Type</strong>: AN<br><strong>Min/Max</strong>: 2/2<br><strong>Required</strong>: N</p>                                             |
|               |            | _EA–Each_                                                                                                                                                                 |
| **Summary**:  |            |                                                                                                                                                                           |
| **CTT**       |            | <p><strong>Transaction Totals</strong><br><strong>Min/Max</strong>: 1<br><strong>Required</strong>: Y<br><strong>Comments</strong>: Not mandatory</p>                     |
| CTT01         | 354        | <p>Number of Line Items<br><strong>Type</strong>: N0<br><strong>Min/Max</strong>: 1/6<br><strong>Required</strong>: Y</p>                                                 |
| **SE**        |            | <p><strong>Transaction Set Trailer</strong><br><strong>Min/Max</strong>: 1<br><strong>Required</strong>: Y</p>                                                            |
| SE01          | 96         | <p>Number of Included Segments<br><strong>Type</strong>: N0<br><strong>Min/Max</strong>: 1/10<br><strong>Required</strong>: Y</p>                                         |
| SE02          | 329        | <p>Transaction Set Control Number<br><strong>Type</strong>: AN<br><strong>Min/Max</strong>: 4/9<br><strong>Required</strong>: Y</p>                                       |
| **Envelope**: |            |                                                                                                                                                                           |
| **GE**        |            | <p><strong>Functional Group Trailer</strong><br><strong>Min/Max</strong>: 1<br><strong>Required</strong>: Y</p>                                                           |
| GE01          | 97         | <p>Number of Transaction Sets Included<br><strong>Type</strong>: N0<br><strong>Min/Max</strong>: 1/6<br><strong>Required</strong>: Y</p>                                  |
| GE02          | 28         | <p>Group Control Number<br><strong>Type</strong>: N0<br><strong>Min/Max</strong>: 1/9<br><strong>Required</strong>: Y</p>                                                 |
| **IEA**       |            | <p><strong>Interchange Control Trailer</strong><br><strong>Min/Max</strong>: 1<br><strong>Required</strong>: Y</p>                                                        |
| IEA01         | I16        | <p>Number of Included Functional Groups<br><strong>Type</strong>: N0<br><strong>Min/Max</strong>: 1/5<br><strong>Required</strong>: Y</p>                                 |
| IEA02         | I12        | <p>Interchange Control Number<br><strong>Type</strong>: N0<br><strong>Min/Max</strong>: 9/9<br><strong>Required</strong>: Y</p>                                           |
