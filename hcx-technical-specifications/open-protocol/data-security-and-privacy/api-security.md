---
description: Details of API security to ensure authenticated and authorised access to APIs
---

# API Security

The protocol defines an API key-based security for authentication and authorization of the API calls between the participating systems and the HCX gateway. HCX instances have to generate the API keys in the form of JWT tokens ([RFC7519](https://datatracker.ietf.org/doc/html/rfc7519)) and shall mandatorily set an expiry time for all the generated tokens.

In future versions, HCX instances may support JWTs issued by other system identity providers, e.g. Health Facility Registry’s IDP.

## **Securing HCX Gateway APIs**

All participant systems (e.g.: providers, payers) should obtain an API key from the HCX gateway with which it identifies itself to the gateway. When calling any API on the HCX gateway, the participant system should pass the API key as part of the 'Authorization' http header.

### **Steps to obtain the API key:**

After a successful verification and onboarding of a participant system onto the participant registry, the HCX instance managing the registry shall share the following details via email, SMS, or both with the participant system:

* _client\_id_: this is the identifier of the participant in the participant registry.
* _client\_secret_: a unique secret is generated for the participant by the HCX instance. The client\_secret value shall be stored in the participant registry in an encrypted format and shall not be sent in the registry APIs.

The participant system can call ‘_/token/generate_’ API along with the client\_id and client\_secret they have received to obtain the API key.

```
POST /token/generate
Content-Type: application/json
Request-Body:
 {
   "client_id": "client_id received by the participant",
   "client_secret": "client_secret received by the participant"
 }
```

HCX instance would respond with the API token upon successful validation of the client\_id and client\_secret values:

```
HTTP/1.1 200 OK
Content-Type: application/json
Cache-Control: no-cache, no-store
Response-Body:
 {
   "access_token": "the API key, a JWT access token",
   "issued_token_type": "urn:ietf:params:oauth:token-type:access_token",
   "token_type": "Bearer",
   "expires_in": 300
 }
```

### **JWT Token Structure:**

API keys are expected to be in JWT format and signed as per JSON web signature ([RFC7515](https://datatracker.ietf.org/doc/html/rfc7515)). The API key should have three elements separated by periods (.): BASE64URL(UTF8(JOSE Header)), BASE64URL(JWS Payload), and BASE64URL(JWS Signature).

* JOSE Header should be a JSON with the following values:

```
{
  "typ":"JWT",
  "alg":"HS256"
}
```

* JWS Payload should be a claim set containing the mandatory claims _**jti**_, _**iss**_, _**sub**_, _**iat**_ and _**exp**_.
  * jti - unique identifier for the JWT
  * iss - HCX instance identifier
  * sub - client\_id of the participant
  * iat - unix timestamp at which the JWT is issued
  * exp - the expiration time after which the JWT must not be accepted for processing
* JWS Signature must be computed in the manner defined for HS256 algorithm over the input ASCII(BASE64URL(UTF8(JOSE Header)) || '.' || BASE64URL(JWS Payload)) using the client\_secret value of the participant.

### **Revoking API Keys**

HCX instances can revoke the API key of a participant by generating a new client\_secret and updating it in the participant registry. The participant system has to generate a new API key by calling the ‘/token/generate’ API with the new client\_secret value.

## **Securing Participant System APIs**

HCX instances while making the calls to the participant system will use a self-generated JWT token with the following elements:

* JOSE Header should be a JSON with the following values:

```
{
  "typ":"JWT",
  "alg":"RS256"
}
```

* JWS Payload should be a claim set containing the mandatory claims _**jti**_, _**iss**_, _**sub**_, _**iat**_ and _**exp**_.
  * jti - unique identifier for the JWT
  * iss - HCX instance identifier
  * sub - same as iss claim, HCX instance identifier
  * iat - unix timestamp at which the JWT is issued
  * exp - the expiration time after which the JWT must not be accepted for processing
* JWS Signature must be computed in the manner defined for RS256 algorithm over the input ASCII(BASE64URL(UTF8(JOSE Header)) || '.' || BASE64URL(JWS Payload)) using the private key of the HCX instance.

Participant systems should validate the API key signature using the public key of the HCX instance.
