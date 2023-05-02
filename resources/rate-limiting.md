---
description: Understand rate limiting.
---

# Rate limiting

The rate limits for calling the Digital River Commerce API depend on your service profile level. The service profile level limits the rates on a per-key basis.

The default limits noted in the following table are sufficient in most cases. If you need to increase these rate limits and environment type, contact your Digital River Account Manager or Professional Services Consultant. If you hit the rate limit, an error message indicates you exceeded the rate limit quota, and you need to reduce the number of calls or spread them out accordingly.

| Environment type         | The rate Limit for Default Calls |
| ------------------------ | -------------------------------- |
| Evaluation (test orders) | 10/second                        |
| Production (live orders) | 100/second                       |
