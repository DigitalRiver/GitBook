---
description: Understand deployment error objects.
---

# Deployment objects

When Product Admin API detects a deployment error, it returns the `deploymentErrors` object in the response. This object will return the [code](../product-admin-api-error-codes/deployment-error-codes.md) and description.

{% code title="deploymentErrors response example" overflow="wrap" %}
```json
"deploymentErrors": [
    {
        "code": "SUBSCRIPTION_TRIAL_DAYS_VALUE_INVALID",
        "description": "Product 1234567800, en_US: Trial Days (freeTrialPeriod) cannot be less than 1 or larger than 1095."
    },
    {
        "code": "SUBSCRIPTION_COMBINED_RENEWAL_DAYS_VALUE_INVALID",
        "description": "Product 1234567800, en_US: Combined Renewal days (combinedRenewalPeriod) cannot be less than 0."
    }
]
```
{% endcode %}

