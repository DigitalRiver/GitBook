---
description: Learn more about the Order Management module.
---

# Order Management module

The `OrderManagement`module keeps the Digital River orders and WooCommerce orders in sync by managing the state of the orders.

### Specifications

This module is responsible for handling different order lifecycle states. It will also enable users to download and view order invoices for their purchases.&#x20;

### Order Management methods

#### Order Manager class

This class is the module's entry point.

| Method        | Args, Returns, and Descriptions                                                                                                                                                                                                                                                                              |
| ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| \_\_construct | <p><strong>Arg</strong>: <code>ApiInstance</code> $api_instance<code>OrderContainer</code> $container</p><p><strong>Return</strong>: string</p><p><strong>Description</strong>: Constructs the object by passing its dependencies</p>                                                                        |
| name          | <p><strong>Arg</strong>: -</p><p><strong>Return</strong>: string</p><p><strong>Description</strong>: Returns the name of the module</p>                                                                                                                                                                      |
| init          | <p><strong>Arg</strong>: -</p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Initializes the module, register necessary hooks, and initialize <code>StateManager</code></p>                                                                                                            |
| create        | <p><strong>Arg</strong>: int $order_id</p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Syncs the <code>WC_Order</code> with id <code>$order_id</code> to <code>digitalriver</code>, and stores the <code>digitalriver</code> order details in the <code>WC_Order</code> metadata</p> |
| get           | <p><strong>Arg</strong>: String $order_id</p><p><strong>Return</strong>: <code>Order</code>/null</p><p><strong>Description</strong>: Gets a <code>digitalriver Order</code> whose ID is <code>$order_id</code>, return <code>null</code> if no match found</p>                                               |
| is\_dr\_order | <p><strong>Arg</strong>: <code>WC_Order</code> $order/int $order_id</p><p><strong>Return</strong>: bool</p><p><strong>Description</strong>: Checks if a WooCommerce order has a <code>digitalriver</code> order associated with it</p>                                                                       |
| checkout\_id  | <p><strong>Arg</strong>: int $order_id</p><p><strong>Return</strong>: string</p><p><strong>Description</strong>: Returns the ID of the checkout corresponding to the order which has its ID <code>$order_id</code></p>                                                                                       |

#### Order Container class

This class acts as a Dependency Injection container for providing dependencies to classes present in the `OrderManagement` module.

| Method           | Args, Returns, and Descriptions                                                                                                                                                                                                   |
| ---------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| \_\_construct    | <p><strong>Arg</strong>: <code>PimpleContainer</code></p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Accepts a Dependency Injection container as an argument and assigns it to a container attribute</p> |
| define\_services | <p><strong>Arg</strong>: -</p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Defines all the classes present within the module</p>                                                                          |
| get              | <p><strong>Arg</strong>: String $service_name</p><p><strong>Return</strong>: object</p><p><strong>Description</strong>: Retrieves a service from the container</p>                                                                |

#### State Manager class

This class updates the `WC_Order` status to reflect the corresponding Digital River order status.

| Method                     | Args, Returns, and Descriptions                                                                                                                                                                                                                             |
| -------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| \_\_construct              | <p><strong>Arg</strong>: <code>OrderManager</code> $order_manager</p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Stores the <code>OrderManager</code> object as a property</p>                                                     |
| init                       | <p><strong>Arg</strong>: -</p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Initializes the object and register necessary hooks</p>                                                                                                  |
| statuses                   | <p><strong>Arg</strong>: array $order_statuses</p><p><strong>Return</strong>: array</p><p><strong>Description</strong>: Add statuses to the <code>WC_Order</code></p>                                                                                       |
| register\_statuses         | <p><strong>Arg</strong>: array $statuses</p><p><strong>Return</strong>: array</p><p><strong>Description</strong>: Add statuses to the <code>WC_Order</code></p>                                                                                             |
| transit                    | <p><strong>Arg</strong>: String $event, array $event_data</p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Uses<code>statuses()</code> as a method to register custom WooCommerce order statuses</p>                                 |
| handle\_status\_transition | <p><strong>Arg</strong>: int $order_id, string $status_from, string $status_to, \WC_Order $order</p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Handles status change for an order and is useful for a cancellation and refund</p> |

#### Fulfiller class

This class handles automatic order fulfillment.

| Method         | Args, Returns, and Descriptions                                                                                                                                                                                                                          |
| -------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| \_\_construct  | <p><strong>Arg</strong>: <code>OrderManager</code> $order_manager</p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Constructs the object by passing its dependencies</p>                                                          |
| init           | <p><strong>Arg</strong>: -</p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Registers necessary hooks if <code>Automatic fulfillment</code> is enabled</p>                                                                        |
| order          | <p><strong>Arg</strong>: <code>WC_Product</code></p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Updates the <code>$order</code> attribute</p>                                                                                   |
| fulfill        | <p><strong>Arg</strong>: int $order_id, string $status_from, String $status_to, <code>WC_Order</code> $order</p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Fulfills the order by calling the Digital River fulfillment API</p> |
| prepare\_items | <p><strong>Arg</strong>: array $items</p><p><strong>Return</strong>: array</p><p><strong>Description</strong>: Prepares items before passing them to the Digital River fulfillment API</p>                                                               |

#### Invoice Manager class

This class manages order invoices.

| Method                    | Args, Returns, and Descriptions                                                                                                                                                                                                               |
| ------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| \_\_construct             | <p><strong>Arg</strong>: <code>OrderManager</code> $order_manager</p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Constructs the object by passing its dependencies</p>                                               |
| init                      | <p><strong>Arg</strong>: -</p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Initializes the object and registers necessary hooks</p>                                                                                   |
| associate\_invoice        | <p><strong>Arg</strong>: <code>Order</code> $order</p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Associates invoice file ID to WooCommerce Order</p>                                                                |
| invoice\_event            | <p><strong>Arg</strong>: string $event_name, array $event_data</p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Handles an invoice created from <code>digitalriver</code></p>                                          |
| download\_invoice\_action | <p><strong>Arg</strong>: array $actions, <code>WC_Orde</code>r $order</p><p><strong>Return</strong>: array</p><p><strong>Description</strong>: Adds a <code>Download Invoice</code> call to action under <code>My Account > Orders</code></p> |
| download\_invoice         | <p><strong>Arg</strong>: -</p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Gets the invoice file link and redirects to it</p>                                                                                         |

#### State Transition Handler Classes

These three Handler classes are responsible for the order state transition.

| Class                                    | Description                                                                                                                                                                                                                                                                                                                                  |
| ---------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Fulfiller`                              | This Handler is responsible for fulfilling orders. It calls Digital River API for fulfillment so that the order can be fulfilled and eventually be completed.                                                                                                                                                                                |
| <p></p><p><code>Canceller</code></p>     | <p>This Handler is responsible for order cancellation. An order can only be cancelled if it is in <code>Ready for fulfilment</code> state in WooCommerce. </p><p><strong>Note:</strong> The order can only be cancelled as a whole, no partial cancellation is available. </p>                                                               |
| <p></p><p><code>RequestRefund</code></p> | <p>This Handler is responsible for order reversal. The refund can be generated only by the store admin by selecting <code>Request refund</code> status in WooCommerce. </p><p><strong>Note:</strong> Only completed orders can be refunded. The refund will be performed on order-level, line-item or partial refunds are not available.</p> |

State transition classes must implement the `StateTransition` interface. Optionally, they can also extend the`BaseTransition` class.&#x20;

**State Transition Interface**

```php
interface StateTransition {

    /**
     * Transition the status.
     * Also, perform any intermediate operations during transition.
     *
     * @param \WC_Order $order WC order object.
     *
     * @return void
     */
    public function transit( \WC_Order $order ): void;

    /**
     * Checks whether the current transition is valid or not.
     *
     * @param string    $status_to Status to which transition is happening.
     * @param string    $status_from Status from which transition is happening.
     * @param \WC_Order $order Order object.
     *
     * @return bool
     *
     * @throws Exception For non-accepted transitions.
     */
    public function valid( string $status_to, string $status_from, \WC_Order $order ): bool;
}
```

| Method  | Args, Returns, and Descriptions                                                                                                                                                                                |
| ------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| valid   | <p><strong>Arg</strong>: string $status_to, string $status_from, \WC_Order $order</p><p><strong>Return</strong>: bool</p><p><strong>Description</strong>: Checks if the current transition is valid or not</p> |
| transit | <p><strong>Arg</strong>: WC_Order $order</p><p><strong>Return</strong>: void</p><p><strong>Description</strong>: Performs any in-transition activity such as calling Digital River API</p>                     |
