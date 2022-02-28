---
description: Learn how to register external services.
---

# Step 3: Register external services

Register external services for Tax Calculation and Payment Services. You can run these scripts from the Developer Console in an Execute Anonymous window or by the method of your choice when you register other services as part of the site setup before starting the connector setup.

## Tax integration service

If you **have** **not** registered the external service for tax integration:

1.  Use the following script to insert the Tax Calculation Apex class that comes with the package into `RegisteredExternalService`.  To use the script, simply modify the `<<storeName>>` variable before running.

    ```
    // WebStore query values
    String webstoreName = <<storeName>>; // Enter your webstore name
     
    // ApexClass query values
    String apexClassname = 'DRB2B_CartTaxCalculations';
    String status = 'Active';
    Double ApiVersion = 51.0;
     
    // RegisteredExternalService insert values
    String registeredProviderType = 'Tax';
    String registeredDevName = 'COMPUTE_TAXES';
    String registeredLabel = registeredDevName;
     
    // StoreIntegratedService insert values
    String devname = registeredDevName;
    String prefix = registeredProviderType;
    String prefixedName = prefix + '__' + devname;
     
    // locate webstore
    WebStore webStore = Database.query('SELECT Id FROM WebStore 
    WHERE Name = :webstoreName LIMIT 1');
    String webStoreId = webStore.Id;
    System.debug('webStoreId:' + webStoreId);
     
    // locate apex class Id
    ApexClass apexClass = Database.query('SELECT Id FROM ApexClass 
    WHERE Status=:status AND ApiVersion=:apiVersion AND 
    Name=:apexClassname LIMIT 1');
    String apexClassId = apexClass.Id;
    System.debug('apexClassId:' + apexClassId);
     
     
    // locate apex in RegisteredExternalService
    String registeredIntegrationId = null;
    try {
        RegisteredExternalService registeredExternalService = 
        Database.query('SELECT Id FROM RegisteredExternalService 
        WHERE ExternalServiceProviderId=:apexClassId AND 
        DeveloperName=:registeredDevName AND 
        ExternalServiceProviderType=:registeredProviderType LIMIT 1');
        registeredIntegrationId = registeredExternalService.Id;
        System.debug('apex class registration: FOUND ' 
        + registeredIntegrationId);
        //delete registeredExternalService; // optionally remove 
        if needed
        
    } 
    catch (QueryException q) {
        System.debug('apex class registration: MISSING ' + apexClassId);
        insert new RegisteredExternalService(DeveloperName = 
        registeredDevName, MasterLabel = registeredLabel, 
        ExternalServiceProviderId = apexClassId, 
        ExternalServiceProviderType = registeredProviderType);
        RegisteredExternalService registeredExternalService = 
        Database.query('SELECT Id FROM RegisteredExternalService WHERE 
        ExternalServiceProviderId = :apexClassId  LIMIT 1');
        registeredIntegrationId = registeredExternalService.Id;
        System.debug('apex class registration: INSERTED ' + 
        registeredIntegrationId);
    }
    ```
2.  Verify that the `Tax Calculation Apex class ID` is registered with the`soql`query below. The `ExternalServiceProviderId` should match the Tax Calculation Apex Class `DRB2B_CartTaxCalculations` ID in the org.&#x20;

    ```
    Select Id, ExternalServiceProviderId, ExternalServiceProviderType, 
    DeveloperName From RegisteredExternalService Where 
    ExternalServiceProviderType = 'Tax'
    ```

If you **have** already registered the external service for tax integration:

1.  Run the following script to update the Tax Integration service to point to the Tax Calculation integration class from the Salesforce Lightning app.&#x20;

    ```
    // Configure Tax Calculation Service
    RegisteredExternalService taxServiceRegistration = [
            SELECT Id
            FROM RegisteredExternalService
            WHERE ExternalServiceProviderType = 'Tax'
            LIMIT 1
    ];

    ApexClass taxCalculationService = [
            SELECT Id
            FROM ApexClass
            WHERE Name = 'DRB2B_CartTaxCalculations'
            LIMIT 1
    ];


    taxServiceRegistration.ExternalServiceProviderId = 
    taxCalculationService.Id;update taxServiceRegistration;

    ```
2.  Verify that the `Tax Calculation Apex class ID` is registered by making the below `soql` query. The `ExternalServiceProviderId` should match the Tax Calculation Apex Class `DRB2B_CartTaxCalculations` ID in the org.

    ```
    Select Id, ExternalServiceProviderId, ExternalServiceProviderType, 
    DeveloperName  From RegisteredExternalService Where 
    ExternalServiceProviderType = 'Tax'
    ```

## Payment Service

Register Payment Service by the following steps:

1. Capture the `WebStore Id`. This will be used in the script in step 4.
2. Create a Named Credential for Digital River with the following details:
   * **Label**: Digital River API
   * **Name**: Digital\_River\_API
   * **URL**: https://api.digitalriver.com
   * **Identity Type**: Named Principal
   * **Authentication Protocol**: No Authentication
   * **Generate Authorization Header**: false \
     ![](<../.gitbook/assets/Named Credential.jpg>)&#x20;
3. Create a **Payment Gateway Provider**:
   * Sign in to Workbench from your commerce org.
   * Go to the **Data** tab and select **Insert**.
   * Go to the **Object Type** and select **PaymentGatewayProvider**.
   * Select **Single Record** and click **Next**.
   *   Fill in the fields using your Payment Gateway Adapter information.

       | Field name           | Example                                                                 |
       | -------------------- | ----------------------------------------------------------------------- |
       | ApexAdapterId        | ID of Payment Gateway Adapter Apex class  `DRB2B_PaymentGatewayAdapter` |
       | DeveloperName        | DR\_PaymentGateway                                                      |
       | IdempotencySupported | Yes                                                                     |
       | MasterLabel          | DR Payment Gateway                                                      |
       | Comments             | Digital River Payment Gateway Provider                                  |
   * Click **Confirm Insert**. \
     ![](<../.gitbook/assets/Payment gateway provider.png>)&#x20;
4. Set up Payment Gateway and insert a `StoreIntegratedService` record for payment by executing the below script:

```
PaymentGatewayProvider paymentGatewayProvider = 
[SELECT Id FROM PaymentGatewayProvider Where DeveloperName = 
'DR_PaymentGateway' LIMIT 1]; 
NamedCredential namedCredential = [SELECT Id FROM NamedCredential 
WHERE DeveloperName = 'Digital_River_API' LIMIT 1]; 
PaymentGateway paymentGateway = new PaymentGateway( 
        PaymentGatewayName = 'Digital River Payment Gateway', 
        MerchantCredentialId = namedCredential.Id, 
        PaymentGatewayProviderId = paymentGatewayProvider.Id, 
        Status = 'Active' 
); 
insert paymentGateway; 
List<StoreIntegratedService> storeIntegratedServiceList = 
[SELECT Id FROM StoreIntegratedService WHERE ServiceProviderType = 
'Payment' Limit 1]; 
if(null != storeIntegratedServiceList && 
storeIntegratedServiceList.size() > 0) { 
    StoreIntegratedService storeIntegratedService = 
    storeIntegratedServiceList.get(0); 
    storeIntegratedService.Integration = paymentGateway.Id; 
    update storeIntegratedServiceList; 
} 
else { 
    StoreIntegratedService storeIntegratedService = new 
    StoreIntegratedService( 
        StoreId = 'WebStoreId', 
        Integration = paymentGateway.Id, 
        ServiceProviderType = 'Payment' 
    ); 
    insert storeIntegratedService; 
} 
```

