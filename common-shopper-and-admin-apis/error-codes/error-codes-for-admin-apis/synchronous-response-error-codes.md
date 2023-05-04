---
description: Understand the synchronous response error codes for the Admin API.
---

# Synchronous response error codes

## `concurrent_process_conflict`

Cannot update or change a product state for one of the following reasons:

### `cannot_change_product_concurrently`

Digital River does not allow multiple users to change the same product concurrently. For example, two Global Commerce users cannot simultaneously apply and save changes to the same product.

* `Cannot change product [$baseProductId] concurrently.`

### `cannot_change_product_state_until_update_request_finished`

All product update requests must be completed before you can change the product state. For example:

* `Unable to change the product state for product [12345600] of [12345700], because there are [5] unfinished requests for [UPDATE_PRODUCT, UPDATE_PRODUCT_LIVE_CHANGE, CREATE_VARIATION].`

### Cannot retrieve order details because the order is still open or waiting for transfer. If queries continue to fail, the order may not exist.

The system cannot retrieve the order details because the order is still open or waiting for transfer. If queries continue to fail, the order may not exist.

### `cannot_update_product_until_state_change_request_finished`

All state change requests must be completed before you can change products. For example:

* `Unable to update product [65432100] of [65432200], because there are [3] unfinished requests for [DEPLOY_PRODUCT, RETIRE_PRODUCT].`&#x20;

## `internal_server_error`

An internal server error has occurred.

## `invalid-request`

The system cannot validate the request for one of the following reasons:

### `duration-begin-later-than-end`

The `beginReceivedTime` attribute's specified date and time values are later than the date and time value. Provide a date and time value for the `endReceivedTime` attribute later than the `beginReceivedTime` value.

* `The date and time for the [endReceivedTime] value [2023-04-01T00:00:00.000Z] must be later than the [beginReceivedTime] value [2023-06-01T00:00:00.000Z].`

### `duration-exceeds-max-value`

The  specified duration between `beginReceivedTime`  and `endReceivedTime`  exceeded the maximum value. Provide a value equal to or less than 30 days and try again.

* `The duration between [beginReceivedTime] [2023-04-01T00:00:00.000Z] and [endReceivedTime] [2023-06-01T00:00:00.000Z] must be equal to or less than [30] days.`

### `duration-in-the-future`

You cannot provide a future date and time for the `beginReceivedTime` value. Provide a past date and time value and try again.

* `The date and time for the [beginReceivedTime] value [2023-04-01T00:00:00.000Z] must be in the past.`

### `invalid-datetime-forma`t

The `endReceivedTime` value is not a valid date and time format. The expected format is `yyyy-MM-dd'T'HH:mm:ss.SSSZ`.

* `The [endReceivedTime] value [2023-06-01] is not a valid date and time format. The expected format is [yyyy-MM-dd'T'HH:mm:ss.SSSZ].`

### `invalid_limit`

The specified `limit` value is invalid. Provide a valid value and try again.

* `The [limit] value [51] is invalid. The value must be a number between [1] and [50].`

### `invalid_task_status`

The specified values for `taskStatus` are invalid. Provide the expected values and try again.

* `The values [ABC, DEF] for [taskStatus] are invalid. The expected values are [COMPLETED, FAILED, PROCESSING, PUBLISHED].`

### `startingAfter-and-endingBefore-cannot-be-both-provided`

You cannot include both `startingAfter` and `endingBefore` attributes in the request.

* `Cannot provide both [startingAfter] and [endingBefore] attributes in the request.`

## `resource-not-found`

### `invalid-product-id`

The specified product could not be found.

* `Cannot find the product [12345678]. The specified product IDs could not be found. Provide the correct product ID and try again.`

### `invalid-task-id`

The specified task (resource) could not be found.

* `The task cannot be found by id: [1234].`

## `validation-error`

The system could not validate the request.&#x20;

* `Variation [12345678] does not belong to the base product [87654321], try replacing the base product ID with 'product'.`
