---
description: Learn how to create products in bulk asynchronously.
---

# Creating products in bulk

To create products in bulk asynchronously, follow the instructions for [creating an individual or base product](../../manage-products-asynchronous-api/creating-or-updating-a-product.md#creating-an-individual-or-base-product) for each product and [product variation](../../manage-products-asynchronous-api/adding-or-updating-a-product-variation.md#adding-a-product-variation-to-a-base-product). For example, to add 100 products, [send 100 create product requests](../../manage-products-asynchronous-api/creating-or-updating-a-product.md#creating-an-individual-or-base-product).&#x20;

After creating the products in bulk, [retrieve the tasks for all products](../../get-the-task-status-for-a-product-synchronous-api/retrieving-the-tasks-for-products.md#retrieving-the-tasks-for-all-products) to verify the status of the requests. You can also verify the successful completion of the task by [checking the product history](creating-products-in-bulk.md#product-history-attributes) in [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do). Note that there may be a delay before these changes appear in Global Commerce.&#x20;
