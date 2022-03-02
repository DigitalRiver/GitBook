---
description: Learn how to run the installation command.
---

# Step 3: Run the installation command

To run the installation command:

1. Stop the Hybris server if it is already running. Depending on the server's `start` mode, use one of the following methods to stop the Hybris server:
   * If you started the Hybris server using `embedded` mode, press **Ctrl+C** to stop the Hybris server.
   * If you started the Hybris server with `service` mode, use the command appropriate for your system to stop it:\
     **Windows**: `hybrisserver.bat stop`\
     **Unix**: `./hybrisserver.sh stop`
2. Go to `<HYBRIS_HOME>/bin/platform` and run the following command if it was not applied in this terminal:
   * **Windows**: `setantenv.bat`
   * **Unix**: `./setantenv.sh`
3. Go to `<HYBRIS_HOME>/bin/platform` and run the installation add-on with the following commands:

```
ant addoninstall -Daddonnames="digitalriveraddon" -DaddonStorefront.yacceleratorstorefront="yacceleratorstorefront"
ant addoninstall -Daddonnames="digitalriverb2baddon" -DaddonStorefront.yacceleratorstorefront="yb2bacceleratorstorefront"
```

{% hint style="info" %}
The storefront name may differ from the default Hybris storefront name based on the project.
{% endhint %}

