---
description: Understand rate limiting in the Commerce API.
---

# Rate limiting

The rate limits for making calls to the Digital River Commerce API depend on your service profile level. The service profile level limits the rates on a per-key basis.

The default limits noted in the following table are sufficient in most cases. If you need to increase these rate limits and environment type, contact your Digital River Customer Success Manager or Partner Enablement. If you happen to hit the rate limit, an error message indicates you exceeded the rate limit quota, and you need to reduce the number of calls or spread them out accordingly.

| Environment type         | The rate limit for default calls |
| ------------------------ | -------------------------------- |
| Evaluation (test orders) | 10/second                        |
| Production (live orders) | 100/second                       |
