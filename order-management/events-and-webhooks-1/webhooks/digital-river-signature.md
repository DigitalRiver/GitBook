---
description: Understand the purpose of the DigitalRiver-signature.
---

# Digital River signature

You can include the Digital River signature if you want Digital River to sign the webhook events it sends to your endpoints. The signature will appear in each event's `DigitalRiver-Signature` header. You can use the signature to verify that Digital River sent the events, rather than a third party. You can use our libraries to verify signatures, or you can manually verify signatures.

The DigitalRiver-Signature is a header containing request signatures that is part of a webhook callback request. Each callback request generates a request signature based on the active "signing secrets" associated with a webhook. A _signing secret_, or signature key, or token, is a unique key associated with a webhook. When you rotate a key, the old key for the signing secret may stay around for a short time (12 hours).

Each token associated with an endpoint is unique. If you associate a test API key and a live API key with an endpoint, the token for each key is unique. If you use multiple endpoints, you must get the token for each one. When you apply the tokens, Digital River can sign each webhook it sends to the endpoint.

To prevent replay attacks, Digital River includes a timestamp in the `DigitalRiver-Signature` header. The signed payload has a timestamp that is verified by the signature, so an attacker cannot change the timestamp without invalidating the signature. If the signature is valid, but the timestamp is too old, you can have your application reject the payload.

Each time Digital River sends an event to your endpoint, we generate the timestamp and signature. When your endpoint replied with a non-2xx status code, Digital River will retry the event with a new signature and timestamp.
