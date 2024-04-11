---
description: >-
  Understand the rate limits in the Digital River API and learn how to handle
  and avoid reaching these limits
---

# Rate Limiting

Based on the API key that you include in a request, the Digital River APIs limit the number of calls that you can make within a given time period.

We use this rate limiting to maintain system stability and to ensure that all Digital River API clients experience efficient, secure, and reliable service. Rate limiting also helps us mitigate the damage caused by malicious actors and faulty integrations.

If you exceed the [designated rate limit](rate-limiting.md#how-we-rate-limit), then your integration should temporarily stop making requests. This is because these requests will fail until a certain amount of time has passed. You can usually avoid hitting this ceiling by following our [rate limiting best practices](rate-limiting.md#rate-limiting-best-practices). But, in the event the request limit is breached, your integration should have logic in place to [handle rate limiting](rate-limiting.md#handling-rate-limiting).

## How we rate limit

The [secret (confidential) API](api-structure.md#confidential-keys) key you are using determines the maximum number of requests you can make per unit of time. In [live mode](api-structure.md#test-and-production-environments), your integration can send up to 250 requests per second. In [test mode](api-structure.md#test-and-production-environments), you can make up to 25 requests per second.

When a request exceeds these rate limits, we block that call from reaching our backend servers. We then send you a response with a `429 Too Many Requests` status code and a standardized `Retry-After` header. The header value is an integer, representing the number of seconds you should wait before making another request. You can use this value when building your mechanism to [handle rate limiting](rate-limiting.md#handling-rate-limiting).

The following example shows a partial response to an API request that exceeded the rate limit. The `Retry-After` response header indicates that your integration should delay 2 minutes before sending any more requests.

{% tabs %}
{% tab title="429 Too Many Requests" %}
```
...
Retry-After: 120
...
```
{% endtab %}
{% endtabs %}

## Causes of rate limiting

Here are some of the more common reasons you might exceed your request rate limit:

* Making a large number of requests within a small amount of time. This might be because you're performing analytics or [building/updating a SKU product catalog](../product-management/creating-and-updating-skus.md). In these scenarios, you could attempt to reduce your request rate or employ a [delta encoding](https://en.wikipedia.org/wiki/Delta\_encoding) strategy.
* Your ecommerce store might be conducting a flash sale (in which deep product discounts are offered for a short period of time) and this event results in a sudden spike in traffic. In almost all cases, our [standard rate limits](rate-limiting.md#how-we-rate-limit) are high enough so that legitimate traffic is never throttled. However, if you believe that an upcoming event might cause you to hit your request ceiling, then you should contact your Digital River representative and inquire about temporarily increasing your rate limit.
* Making unnecessary requests to the APIs that retrieve data items from the response but then fail to use that data in your application.

Your integration should always have a mechanism for [handling rate limiting](rate-limiting.md#handling-rate-limiting). But, in most cases, you can avoid triggering our request rate restrictions by following some [rate limiting best practices](rate-limiting.md#rate-limiting-best-practices).

## Handling rate limiting

In addition to following our [best practices](rate-limiting.md#rate-limiting-best-practices), you should have a built-in retry mechanism to handle rate limiting.

The simplest, most straightforward approach is to just build a delay into your code. This means that, whenever you catch a `429` error, you should delay the execution of your next API call. The exact number of seconds to delay that call is determined by the value of the `Retry-After` response header. We recommend that you don't make any additional requests until this specified time has elapsed. If you do, those requests will be blocked.

If you're seeking a more sophisticated solution to handling rate limits, you could implement an [exponential backoff](https://en.wikipedia.org/wiki/Exponential\_backoff) algorithm. With this approach, after the wait period has expired, you periodically retry a failed request. The wait time between each retry request increases exponentially, up to a designated maximum backoff time. At this point, the time between retries does not need to continue increasing. If you use this approach, we also recommend you code some random behavior, or [jitter](https://en.wikipedia.org/wiki/Jitter), into your algorithm's wait times. This helps to avoid scenarios in which many client requests have become synchronized by a blocking event and retry requests are sent in synchronous waves (i.e., the [thundering herd problem](https://en.wikipedia.org/wiki/Thundering\_herd\_problem)).

At an even more advanced level, you could implement a [token bucket](https://en.wikipedia.org/wiki/Token\_bucket) algorithm (sometimes known as a "[leaky bucket](https://medium.com/smyte/rate-limiter-df3408325846)") to manage traffic to the Digital River APIs.

## Rate limiting best practices

Your integration should always be set up to [handle rate limiting](rate-limiting.md#handling-rate-limiting). But we also recommend that you attempt to minimize the probability of hitting your request ceiling. In most cases, you can accomplish this by adhering to the following best practices:

* Instead of frequently calling the APIs, your integration should make extensive use of [webhook events](../order-management/events-and-webhooks-1/).
* Optimize your code to eliminate unnecessary API calls. For example, ensure that all of your requests are retrieving data and that data is then used by your application.
* When updating product catalogs, implement [delta encoding](https://en.wikipedia.org/wiki/Delta\_encoding) strategies to minimize the number of `POST/skus/{id}` and `PUT/skus/{id}` requests you make.
* Avoid making multiple concurrent requests.
* When you're making a large number of `POST`, `PUT`, or `DELETE` requests for a single user, you should implement a delay between each request.
