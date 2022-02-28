---
description: Determine your approach to implementing SCA.
---

# How to ensure SCA compliance

For your integration to access our [Strong Customer Authentication (SCA)](https://info.digitalriver.com/rs/348-QUY-258/images/Digital\_River\_Guide\_to\_PSD2\_Compliance\_2020.pdf) solution, you must be using [payment sessions](../payment-sessions.md). These are embedded in both [Drop-in](../drop-in/) and [DigitalRiver.js with Elements](../digitalriver.js/reference/elements.md).&#x20;

Use the following flowchart to find your appropriate SCA integration scenario:

![](<../../.gitbook/assets/PSD2 test (3).png>)

| Integration scenario                     | Next steps                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| ---------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| I'm using Drop-in                        | <p>You're already using our recommended, out of the box solution for <a href="https://info.digitalriver.com/rs/348-QUY-258/images/Digital_River_Guide_to_PSD2_Compliance_2020.pdf">complying with SCA</a>. <br><br>To make sure you're using the tool correctly, review the <a href="../drop-in/drop-in-integration-guide.md">Drop-in</a> documentation, and then <a href="../building-your-workflows.md">build your workflow</a>.</p>                                                                           |
| I'm using payment sessions with elements | You're currently using DigitalRiver.js in a way that gives you access to SCA flow handling.  Your next steps involve [building your SCA workflow](../building-your-workflows.md).                                                                                                                                                                                                                                                                                                                                |
| I need to migrate to payment sessions    | <p>In order to access SCA handling and compliance, you'll need to be using <a href="../payment-sessions.md">payment sessions</a>.  <br><br><a href="../drop-in/">Drop-in</a> is the preferred method for performing this migration, but you can also migrate <a href="../payment-sessions.md#migrating-to-payment-sessions">directly to payment sessions</a> using DigitalRiver.js. Once you're done with the migration, you'll need to <a href="../building-your-workflows.md">build your SCA workflow</a>.</p> |
