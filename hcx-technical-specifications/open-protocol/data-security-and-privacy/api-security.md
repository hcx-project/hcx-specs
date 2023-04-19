---
description: Details of API security to ensure authenticated and authorised access to APIs
---

# API Security

The protocol defines an API key-based security for authentication and authorization of the API calls between the participating systems and the HCX gateway. HCX instances have to generate the API keys in the form of JWT tokens ([RFC7519](https://datatracker.ietf.org/doc/html/rfc7519)) and shall mandatorily set an expiry time for all the generated tokens.

In future versions, HCX instances may support JWTs issued by other system identity providers, e.g. Health Facility Registry’s IDP.

## **Securing HCX Gateway APIs**

All participant systems (e.g.: providers, payers) should obtain an API key from the HCX gateway with which it identifies itself to the gateway. When calling any API on the HCX gateway, the participant system should pass the API key as part of the 'Authorization' http header.

### **Steps to obtain the API key:**

After a successful verification and onboarding of a participant system onto the participant registry, use the following details to generate a API key:

* _username_: This is the primary email address of the participant in the registry.
* _password_: This is the password that is set during the onboarding onto the registry.  

The participant system can call ‘_/auth/realms/{realm-name}/protocol/openid-connect/token_’ API along with the username and password to obtain the API key.

```
POST /auth/realms/{realm-name}/protocol/openid-connect/token
Content-Type: application/x-www-form-urlencoded
Request-Body:
 {
   "client_id": "", // The client id of the authentication provider.
   "username": "", // This is the primary email of the participant who is attempting to authenticate.
   "password": "", // This is the password of the participant.
   "grant_type": "password", // This field specifies the grant type that is being used to obtain the token.
 }
```

HCX instance would respond with the API token upon successful validation of the username and password values:

```
HTTP/1.1 200 OK
Content-Type: application/json
Cache-Control: no-cache, no-store
Response-Body:
 {
   "access_token": "", // This is the token that the client can use to access protected resources on the server. The token is a JSON Web Token (JWT) that contains claims about the user and the client
   "expires_in": 6000, // The number of seconds until the access token expires. After this time, the client must obtain a new access token.
   "refresh_expires_in": 300, // The number of seconds until the refresh token expires. After this time, the client must obtain a new refresh token. 
   "refresh_token": "", // A token that the client can use to obtain a new access token after the current access token expires. The refresh token is also a JWT that contains claims about the user and the client. 
   "token_type": "Bearer", // The type of token, which is usually "bearer".
   "not-before-policy": 1607576887, // The time before which the token is not valid.
   "session_state": "a1415249-c4eb-49e1-97ea-42c7c91db874", // A unique identifier for the user's session.
   "scope": "profile email" // The scopes that the client has requested access to.
 }
```

### **JWT Token Structure:**

API keys are expected to be in JWT format and signed as per JSON web signature ([RFC7515](https://datatracker.ietf.org/doc/html/rfc7515)). The API key should have three elements separated by periods (.): BASE64URL(UTF8(JOSE Header)), BASE64URL(JWS Payload), and BASE64URL(JWS Signature).

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
  * sub - authentication provider id of the participant in the registry.
  * iat - unix timestamp at which the JWT is issued
  * exp - the expiration time after which the JWT must not be accepted for processing
* JWS Signature must be computed in the manner defined for RS256 algorithm over the input ASCII(BASE64URL(UTF8(JOSE Header)) || '.' || BASE64URL(JWS Payload)) using the private key of the authentication provider.

### **Revoking API Keys**

HCX instances can revoke the API key of a participant by updating a new password in the participant registry. The participant system has to generate a new API key by calling the ‘auth/realms/swasth-health-claim-exchange/protocol/openid-connect/token’ API with the new password value.

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
