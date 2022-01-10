---
description: Building blocks of the Health Claims Data Exchange protocol
---

# Health Claims Exchange (HCX) Protocol

As indicated in the [**overall message flow diagram**](key-components-building-blocks.md#overall-message-flow-diagram), the exchange platform will be the routing engine that will be responsible for receiving the data from either participant (provider, payor, another HCX instance, ...), and performing necessary validations, and forwarding it to the intended recipients.

## **Terminology**

1. **Request** - Initiation of the flow by the sender by passing relevant payload in the message structure defined by this protocol. Requests may travel from Sender to the Receiver through a relay of HCX instances.
2. **Response** - Response/reply by the recipient of the request by passing relevant response payload defined by this protocol. Responses may also travel from the “original request message” recipient to the “original request message” sender through a relay of HCX instances. The key difference here is that a response is always sent as an earlier event received from the HCX instance.
3. **HCX instance** - A runtime of the HCX platform that performs the role of message receiving and forwarding on behalf of senders and receivers. Based on the use case, any participating party may act as the sender (thereby a requester), or a receiver (thereby a recipient). E.g. for the cashless claims use cases defined so far - Providers will be the senders in case of CheckEligibility, PreAuth and ClaimSubmission use cases (and the payers will be recipients), while Payers will be the sanders in case of PaymentNotice (and the providers will be recipients).
4. **Message** - HCX protocol transfers a Message that contains a transport envelope and the content as per the use case.
   1. Transport envelop is a set attribute that carries the transport information for HCX to reliably forward the message to the destination
   2. Content would have two parts:
      1. Business headers - any domain or use case specific information which may not be necessary for the transportation but allows more information about the payload, e.g. type of the payload
      2. Payload - Domain object defined for the pertinent use case. Usually, this data will be encrypted using the recipient's key to ensure that HCX instances cannot view this data.
5. **Senders and Receivers** - Two systems participating in the information exchange. They may also be referred to as client/server as per current industry terminology. E.g. Provider(s) are senders in claims flow use case, and Payor(s) are senders in Payment Notice use case in the flow diagram above.

## **Overall Message Flow Diagram**

![](<../../.gitbook/assets/0 (1).png>)

HCX protocol is designed for the exchanges to work in an asynchronous manner (like SMTP), therefore each use case will be completed in a cycle of messages as shown below:

## **Exchange Protocol**

**Sender to HCX (Leg 1)**

* **The sender** (originator of the communication) sends the initial message to its preferred HCX instance.
* HCX validates the status of the sender and the next intended recipient (maybe another HCX instance) on its registries.
* HCX then performs required signature verifications etc before responding with an acknowledgement to the sender.
* It then forwards it to either the end recipient (if registered with the same instance) or the next HCX in the chain.

Steps 1 and 7 in the above diagram as examples of this leg.

**HCX to Receiver (Leg 2)**

* Final HCX in the relay chain (could be the original HCX itself) checks the status of the recipient on its registries,
* performs needed verifications and forwards the message to the recipient.
* The recipient acknowledges the receipt of the message.

Steps 3 and 9 in the above diagram as examples of this leg.

**Receiver to HCX (Leg 3)**

* **The recipient** (receiver of the original request message) sends the response message to its preferred HCX instance.
* HCX validates the status of the recipient and original sender (maybe another HCX instance) on its registries.
* HCX then performs required signature verifications etc before responding with an acknowledgement to the recipient.
* It then forwards it to either the initial sender (if registered with the same instance) or the next HCX in the chain.

Steps 4 and 10 in the above diagram as examples of this leg.

**HCX to Sender (Leg 4)**

* Final HCX in the relay chain (could be the original HCX itself) checks the status of the original sender on its registries,
* Performs needed verifications and forwards the response message to the sender.
* The sender acknowledges the receipt of the response message.

Steps 6 and 12 in the above diagram as examples of this leg.

**Relays**

In case Sender and receiver are listed/registered on different HCX instances, there may be relays between the HCXs. Steps 2, 5, 8 and 11 in the above diagram may involve such relays. [Appendix A](../appendix-a-hcx-relay-example.md) provides an example of a provider-payor use case with a relay between two HCXs.

## Message Structure

To facilitate safe, secure, and reliable message exchanges through HCX, its message payload needs to be designed in a manner that separates the actual use case-specific information (payload) from transport and generic domain-specific information (headers). To achieve this, HCX messages can be structured in line with [JWE tokens](https://datatracker.ietf.org/doc/html/rfc7516) as below (value in bracket are the corresponding JSON keys as per JWE):

1. Protected headers (**protected**) - A set of attributes that provide transport, security, message integrity and summary information about the message being exchanged.
2. Encrypted Payload (**ciphertext**) - Payload containing the relevant domain entity (eObject) as prescribed for the use case by the domain specifications. This needs to be encrypted so that HCX cannot read this.
3. Signature (**tag**) - Digital signature on the protected header and the payload of the message to ensure its integrity.
4. Other JWE elements like **iv** (Initialisation Vector for the algorithm), **aad** (additional authentication data), and **encrypted\_key** (Content Encryption Key)

HCX expects the resulting JWE token to be JSON serialised. The following subsections detail each of these message elements:

### **Protected Headers**

Protected headers contain information that helps exchanges to identify senders, receivers of the message, perform integrity checks, audits and routing functionality. Header values are posted in clear and never contain any Personally Identifiable Information (PII) about the patient. HCX protocol uses JWE protected headers for such information to ensure these are not tampered with by the intermediate gateways. Protected Headers for HCX will be the union of the following three header categories:

#### **Registered JOSE Headers**

JSON Web encryption header as per [RFC7516](https://datatracker.ietf.org/doc/html/rfc7516). For HCX V1, this is proposed to be fixed to:

{"alg":"RSA-OAEP","enc":"A256GCM"}

#### **HCX Protocol Headers**

Used as private headers as per [RFC7516](https://datatracker.ietf.org/doc/html/rfc7516) section 4.3. Please note that all the parameter names are appended with “x-hcx-” to avoid a collision.

The following table provides the protocol related header elements in the claims exchange:

| Name                  | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                           | Type                                                                                                                 | Additional Properties       |
| --------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------- | --------------------------- |
| x-hcx-sender\_code    | Registry code of the sender (e.g. provider or payer)                                                                                                                                                                                                                                                                                                                                                                                                                                  | String                                                                                                               | <ul><li>Mandatory</li></ul> |
| x-hcx-recipient\_code | Registry code of the recipient (e.g. provider or payer)                                                                                                                                                                                                                                                                                                                                                                                                                               | String                                                                                                               | <ul><li>Mandatory</li></ul> |
| x-hcx-request\_id     | Sender generated unique id for each originating request.                                                                                                                                                                                                                                                                                                                                                                                                                              | String                                                                                                               | <ul><li>Mandatory</li></ul> |
| x-hcx-correlation\_id | Unique id of the conversation (a collection of related messages). It may be chosen as the message\_id of in the original sender’s (initiator’s) system. For return messages (asynchronous responses) responders are expected to populate with the one in the request.                                                                                                                                                                                                                 | String                                                                                                               | <ul><li>Mandatory</li></ul> |
| x-hcx-workflow\_id    | Unique id of workflow that may span over a series of message exchanges, e.g. an eligibility check, a preauth and then claims submission for a patient may be linked with such an id from the providers initiate a request on check eligibility                                                                                                                                                                                                                                        | String                                                                                                               | <ul><li>Optional</li></ul>  |
| x-hcx-timestamp       | Unix timestamp of the message while sending                                                                                                                                                                                                                                                                                                                                                                                                                                           | datetime                                                                                                             | <ul><li>Mandatory</li></ul> |
| x-hcx-debug\_flag     | Request to the server to include debug information. Useful in the time of integration testing and prod debugging. However, server(s) may choose to ignore this flag based on their policy.                                                                                                                                                                                                                                                                                            | <p>ENUM</p><p>- Error</p><p>- Info</p><p>- Debug</p>                                                                 | <ul><li>Optional</li></ul>  |
| x-hcx-status          | <p>Operational status of the message. Depending on the leg of the message it would be:</p><ul><li>request.initiate</li><li>request.retry</li><li>response.success</li><li>response.fail</li><li>response.sender_not_supported</li><li>response.unhandled</li><li>response.request_retry</li></ul>                                                                                                                                                                                     | String                                                                                                               | <ul><li>Mandatory</li></ul> |
| x-hcx-error\_details  | <p>Expected to be used for providing details of the status. It Will be especially useful in scenarios where Operational status indicates an irrecoverable error.</p><p>Key elements of this object are:</p><ul><li><strong>Code</strong>: error, info, debug code from the system - expected to be namespaced for better readability</li><li><strong>Message</strong>: Short description of the detail</li><li><strong>Trace</strong>: Long description supporting the Code</li></ul> | <p>JSON Object -</p><p>E.g.</p><p>{error.code: “bad.input”, error.message: “Provider code not found”, trace: “”}</p> | <ul><li>Optional</li></ul>  |
| x-hcx-debug\_details  | <p>Expected to be used for providing details of the status. It Will be especially useful in debugging scenarios</p><p>Key elements of this object are:</p><ul><li><strong>Code</strong>: error, info, debug code from the system - expected to be namespaced for better readability</li><li><strong>Message</strong>: Short description of the detail</li><li><strong>Trace</strong>: Long description supporting the Code</li></ul>                                                  | <p>JSON Object -</p><p>E.g.</p><p>{error.code: “bad.input”, error.message: “Provider code not found”, trace: “”}</p> | <ul><li>Optional</li></ul>  |

#### **HCX Domain Headers**

JSON object containing a map of domain-specific header values as proposed in domain data specifications. E.g. For claims use cases, domain specs may decide to populate the total claimed amount, list of diagnostics/procedures. Please note that all such parameter names must follow the naming convention x-hcx-\<use\_case\_name>-\<parameter\_name>, where

* use\_case\_name = short name (<16 chars) given to the use case by domain working group, it is advisable to keep it the same as the one in API’s URI path
* Parameter\_name = short name (<32 chars) given to the parameter

Therefore the protected headers will be:

Protected Headers = (Registered JOSE headers) U (HCX Protocol Headers) U (HCX Domain Headers)

### **Payload**

Use case-specific base64 encoded, encrypted payload as defined in [Domain Data specifications](../../hcx-domain-specifications/domain-data-specifications/). This can be thought of as a private claim in JWT terminology. JSON web encryption as defined in [RFC7516](https://datatracker.ietf.org/doc/html/rfc7516) to be used for encrypting the payload with “alg” and “enc” as defined in the JOSE header above.

E.g. In the current cashless claims scenario, domain working groups have decided the payload to be an FHIR bundle of the appropriate type. Therefore the payload will be an encrypted FHIR bundle as defined in the domain data specs.

### **Signatures**

As per [RFC7516](https://datatracker.ietf.org/doc/html/rfc7516), cryptographic mechanisms used in JWE encrypts and provides integrity protection to encrypted payload and protected headers using Authenticated Encryption with Associated Data (AEAD), hence additional signatures are not needed for message integrity protection.

## API Structure

Based on the above protocol definition and the message structure, each use case API in the HCP ecosystem is expected to follow the following pattern for the onward and return journey of the use case message:

\<transport\_protocol>://\<server\_address>/\<protocol\_version/>\<resource\_name>/\<action|on\_action>, where

* **transport\_protocol** - for HCX V1 purpose it will always be **https**
* **server\_address** is the address of the server on which the API is called (an HCX for payor/provider or a payor/provider/HCX for an HCX)
* **protocol\_version** - API version for the current protocol to help support protocol transitions
* **resource\_name** is the name of the domain resource that the API is serving. E.g. for cashless claims, it may be “claims”, “coverage eligibility”, etc. based on the use case.
* **action** is the action sought within the context of that resource
* **on\_action** represents the callback from the receiving system for responding to the original message

Keeping this pattern in mind, in the current cashless use case following APIs are expected to be supported.

Please note that search APIs are expected to support search parameters as detailed in the [domain data specifications](../../hcx-domain-specifications/domain-data-specifications/). For FHIR based entities this is expected to be clearly published in the corresponding implementation guides. Visibility and availability of the attributes in the search result payloads are also expected to be defined in domain data specifications.

### **CoverageEligibility**

* **Eligibility check**
  * /coverageeligibility/check (provider->HCX, HCX->payor)
  * /coverageeligibility/on\_check (payor->HCX, HCX->provider)

### **Claims**

* **PreAuth submission**
  * /preauth/submit (provider->HCX, HCX->payor)
  * /preauth/on\_submit (payor->HCX, HCX->provider)
* **PreAuth Search**
  * /preauth/search (provider->HCX, HCX->payor)
  * /preauth/on\_search (payor->HCX, HCX->provider)
* **Claim submission**
  * /claim/submit (provider->HCX, HCX->payor)
  * /claim/on\_submit (payor->HCX, HCX->provider)
* **Claims Search** (Also supports status search)
  * /claim/search (provider|regulator|auditor->HCX, HCX->payor)
  * /claim/on\_search (payor->HCX, HCX->provider|regulator|auditor)

### **Payments**

* **Payment notice and acknowledgement**
  * /paymentnotice/request (payor>HCX, HCX->provider-)
  * /paymentnotice/on\_request (provider->HCX, HCX->payor)
* **Payment Search** (Also supports status search)
  * /paymentnotice/search (provider->HCX, HCX->payor)
  * /paymentnotice/on\_search (payor->HCX, HCX->provider)

Following [OpenAPI 3.0 specification](https://raw.githubusercontent.com/Swasth-Digital-Health-Foundation/standards/main/API%20Definitions/openapi\_hcx.yaml) details these APIs in detail.

## Questions for Consultation&#x20;

#### Question 1

Please review the Exchange Protocol and provide comments/suggestions on its comprehensiveness. Kindly provide aspects of the protocol would you find challenging and suggestions to overcome those challenges.&#x20;

#### Question 2

While the consultation paper covers only interactions between the provider and payer, and the interactions with the beneficiary will be detailed post public consultation, what additional workflows do you think must be considered?

{% hint style="info" %}
Instructions to send responses to the consultation questions are available [here](../../how-to-submit-responses.md).
{% endhint %}
