---
description: Learn how to use Digital River's test and production environments.
---

# Test and production environments

In the test environment, you can test Digital River's features without affecting live data. The production environment allows you to perform actions that affect live data.

The test and production environments behave similarly with the following exceptions:

* You can only use test payment information in the test environment. Card networks and payment providers do not process payments in a test environment.
* The flow is different for some payment methods using the source resources in the production environment. They may require more steps when in the test environment.
* In the test environment, Digital River retries webhooks three times over a few hours (as opposed to 72 hours for the production environment) when it does not receive a successful acknowledgment.

You can tell which environment you are in by looking at the Test/Production toggle.

Test:\
\
![](<../../.gitbook/assets/image (257).png>)

Production:

<div align="left">

<img src="../../.gitbook/assets/ProductionDropdown (1).png" alt="">

</div>

Click the drop-down menu to toggle between the two environments.\
\
![](<../../.gitbook/assets/image (258).png>)

Only paid accounts can toggle to the Production environment.
