---
description: Understand how transport works.
---

# Transport

### HTTP post

When Digital River posts XML, the XML appears in the body of the HTTP request.&#x20;

### Endpoints

Choose the type of endpoint you need based on what you want to do. Digital River provides the following types of endpoints:

* An FTP/SFTP endpoint for integrations that require an FTP/SFTP endpoint. You can use FTP/SFTP-based endpoints for sales reports. When Digital River assigns an FTP account to you (the client), Digital Rivers expects you to control your directory structure. You can create any directory structure you like, just let Digital River know where you want your files. Deleting files does not cause any issues.
* An endpoint to the client for inbound calls to Digital River.

The client provides an HTTP-based endpoint for real-time outbound calls from Digital River to the client.

Note that testing endpoints are different than production endpoints.

### Transport failures

If your servers go down while processing an HTTP post from Digital River and your endpoint does not respond, Digital River will try again at a configured interval. Digital River configures clients to retry transport failures once an hour for a maximum of 48 hours by default. Once the 48 retries are exhausted, different processes respond based on unique business rules. Generally, Digital River monitors the number of retries and looks into the issue when all retries are exhausted. You can configure the interval and number of retries.

Based on observation, only 0.5% of processes are affected due to transport failures.
