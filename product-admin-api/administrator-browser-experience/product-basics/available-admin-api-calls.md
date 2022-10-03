---
description: Learn about the available Admin API calls.
---

# Available Admin API calls

The following table list the available Admin API calls.

| Path                                             |                                                                                                            Action                                                                                                            |       ERID Support       |              Mode             |  Deployment Validation  |         Webhook         |
| ------------------------------------------------ | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: | :----------------------: | :---------------------------: | :---------------------: | :---------------------: |
| `/products/{productId}`                          |                            <p><a href="broken-reference">GET</a><br><a href="../../asynchronous-product-api/creating-or-updating-a-product.md#updating-an-individual-or-base-product">POST</a></p>                           |     <p>Yes<br>Yes</p>    |      <p>Sync<br>Async</p>     |    <p>Yes<br>Yes</p>    |     <p>No<br>Yes</p>    |
| `/products/{productId}/locales/locale}`          |                                                                    [DEL](../../asynchronous-product-api/deleting-a-base-or-individual-products-locale.md)                                                                    |            Yes           |             Async             |            No           |           Yes           |
| `/products/{productId}/deploy`                   |                                                                                 [POST](../../asynchronous-product-api/deploying-a-product.md)                                                                                |            Yes           |             Async             |           Yes           |           Yes           |
| `/products/{productId}/retire`                   |                                                                                 [POST](../../asynchronous-product-api/retiring-a-product.md)                                                                                 |            Yes           |             Async             |            No           |           Yes           |
| `/products/{productId}/variations/{variationId}` | <p><a href="broken-reference">GET</a><br><a href="../../asynchronous-product-api/adding-or-updating-a-product-variation.md">POST</a><br><a href="../../asynchronous-product-api/deleting-a-product-variation.md">DEL</a></p> | <p>Yes<br>Yes<br>Yes</p> | <p>Sync<br>Async<br>Async</p> | <p>Yes<br>Yes<br>No</p> | <p>No<br>Yes<br>Yes</p> |
| `/products/product/variation/{variationId}`      | <p><a href="broken-reference">GET</a><br><a href="../../asynchronous-product-api/adding-or-updating-a-product-variation.md">POST</a><br><a href="../../asynchronous-product-api/deleting-a-product-variation.md">DEL</a></p> | <p>Yes<br>Yes<br>Yes</p> | <p>Sync<br>Async<br>Async</p> | <p>Yes<br>Yes<br>No</p> | <p>No<br>Yes<br>Yes</p> |
| `/products/tasks`                                |                                                                   [GET](../../asynchronous-product-api/verifying-the-successful-completion-of-a-request.md)                                                                  |             -            |              Sync             |            -            |            -            |

##
