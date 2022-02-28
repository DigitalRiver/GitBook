---
description: Learn how to set up Regulatory Fees.
---

# Step 6: Set up regulatory fees

## Regulatory Fee setup

Set up the **Regulatory Fees** section in **Backoffice**:

1.  Expand **Digital River** and click the **Regulatory Fees** link. \
    If the Regulatory Fees link does not appear, see the [troubleshooting tips](step-8-set-up-the-regulatory-fee.md#troubleshooting-tips) for more information.\
    &#x20;![](<../.gitbook/assets/Regulatory fee (1).png>) \


    A configuration page with the following attributes will appear: &#x20;

    | Attribute   | Description                             |
    | ----------- | --------------------------------------- |
    | Code        | Regulatory Fee code                     |
    | Type        | Regulatory Fee type                     |
    | Product     | Product with the applied Regulatory Fee |
    | Amount      | Regulatory Fee amount                   |
    | Currency    | Regulatory Fee currency amount          |
    | Country     | Regulatory Fee country                  |
    | Subdivision | Regulatory Fee subdivision              |
2. Add or update the configuration details and click **Save**.&#x20;

![](<../.gitbook/assets/Regulatory fee 2.png>)

![](<../.gitbook/assets/Regulatory fee 3 (1).png>)

## Troubleshooting tips

If the **Regulatory Fees** section does not appear after the system update, following these steps in **Backoffice**:

1. Press **F4** once. A loading icon will appear and Backoffice will switch to `orchestrator`mode after two-three minutes.\
   &#x20;![](<../.gitbook/assets/Regulatory fee 4.png>)&#x20;
2. Click **Reset Everything** on the right-hand side and press **OK** to continue. Backoffice will reset the configuration and will return to `orchestrator` mode in 10-15 minutes. \
   ![](<../.gitbook/assets/Regulatory fee 5.png>)&#x20;
3. Click **F4** again and Backoffice will return to its original view.  \
   ![](<../.gitbook/assets/Regulatory fee 6.png>)&#x20;

#### Digital River regulatory fee impex

```
$productCatalog=electronicsProductCatalog
$productCatalogName=Electronics Product Catalog
$catalogVersion=catalogversion(catalog(id[default=$productCatalog]),
version[default='Online'])[unique=true,default=$productCatalog:Online]


INSERT_UPDATE DRRegulatoryFee;code[unique=true];rfType(code);rfProduct(code,$catalogVersion);rfAmount;rfCurrency(isocode);rfCountry(isocode);subdivision(isocode)
;TestImpex_1992693;battery;1992693;8;USD;US;US-PR
;1992693_UK;battery;1992693;7;GBP;GB;
```

#### Regulatory fee type impex

```
INSERT_UPDATE DRFeeType;code[unique = true];name;
; test; testfeetype
```

