---
description: Learn how to enable the B2B features.
---

# Step 8: Enable the B2B feature

If you enabled enabled Reorder for your B2B storefront, update the custom storefront `cms-content.impex` with code in the following example.

{% code title="Enable B2B code sample" %}
```javascript
ReorderAction;$contentCV[unique=true];uid[unique=true];url;name;&actionRef
;;ReorderAction;/checkout/summary/dr/reorder;Reorder Action;ReorderAction
```
{% endcode %}
