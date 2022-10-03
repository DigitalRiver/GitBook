---
description: Understand refund error scenarios.
---

# Refund error scenarios

| Error Scenario                                                                       | Error Message Description                                                                               |
| ------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------- |
| API successfully executed                                                            | Operation Successful.                                                                                   |
| Cannot successfully resolve a site for a requisition                                 | Unable to resolve the site for the requisition.                                                         |
| The provided Site ID was invalid or unresolved                                       | It cannot resolve the requisition.                                                                      |
| Input requisition line item ID is invalid or unresolved                              | Cannot resolve the line item.                                                                           |
| Input refund type value is invalid                                                   | Invalid refund type.                                                                                    |
| Input refund reason value is invalid                                                 | Invalid refund reason.                                                                                  |
| Input refund category value is invalid                                               | Invalid refund category.                                                                                |
| Input currency type value is invalid                                                 | Currency in the request does not match with the requisition or lineItem.                                |
| Input currency code value is invalid                                                 | The currency code is invalid.                                                                           |
| Input session ID value is invalid                                                    | The user session ID is invalid.                                                                         |
| Input refund amount is 0 or less                                                     | Invalid refund amount.                                                                                  |
| Input refund amount is greater than the refundable amount                            | The requested refund amount is greater than the refundable amount.                                      |
| Input refund amount is in incorrect format                                           | The refund amount is not a valid currency amount. valid format is (####.##).                            |
| Input fee type is invalid for a product level return (category: product\_level\_fee) | Unable to resolve fee type for the line item.                                                           |
| Requisition ID is empty                                                              | Requisition ID can not be empty.                                                                        |
| Refund reason is empty                                                               | Refund Reason can not be empty.                                                                         |
| Refund category is empty                                                             | The Refund Category can not be empty.                                                                   |
| A product-level refund request fails to provide line item level details              | Requisition Line Items can not be empty.                                                                |
| A product-level fee return fails to provide fee details                              | Line Item's Fee List can not be empty.                                                                  |
| The site does not support satisfaction refund                                        | The site is not allowed to accept a satisfaction refund for the requisition.                            |
| A second refund is not allowed                                                       | This order does not allow a second refund. Additional refunds require that you perform a manual refund. |
| The user roles are invalid for this API                                              | The user is not a Customer Service Representative/ Director/Supervisor.                                 |
| The user roles are invalid for this API                                              | The user is not a Customer Service Representative/ Director/Supervisor/InternalUser/Owner of the Order. |
| An unforeseen exception occurred                                                     | An unhandled runtime exception has occurred.                                                            |

