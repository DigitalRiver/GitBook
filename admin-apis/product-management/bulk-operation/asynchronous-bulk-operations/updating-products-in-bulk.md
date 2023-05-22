---
description: Learn how to update products in bulk asynchronously.
---

# Updating products in bulk

To update products in bulk asynchronously, follow the instructions for [updating an individual or base product](../../manage-products-asynchronous-api/creating-or-updating-a-product.md#updating-an-individual-or-base-product) for each product and [product variation](../../manage-products-asynchronous-api/adding-or-updating-a-product-variation.md#updating-a-specific-product-variation). For example, to update 100 products, [send 100 update product requests](../../manage-products-asynchronous-api/creating-or-updating-a-product.md#updating-an-individual-or-base-product).

After creating the products in bulk, [retrieve the tasks for all products](../../get-the-task-status-for-a-product-synchronous-api/retrieving-the-tasks-for-products.md#retrieving-the-tasks-for-all-products) to verify the status of the requests. You can also verify the successful completion of the task by [checking the product history](updating-products-in-bulk.md#product-history-attributes) in [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do). Note that there may be a delay before these changes appear in Global Commerce.&#x20;
