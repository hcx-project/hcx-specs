---
description: Building blocks of the Health Claims Data Exchange protocol
---

# Health Claims Exchange (HCX) Protocol

As indicated in the [**overall message flow diagram**](./#overall-message-flow-diagram), the exchange platform will be the routing engine that will be responsible for receiving the data from either participant (provider, payor, another HCX instance, ...), and performing necessary validations, and forwarding it to the intended recipients.

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

Please note that search APIs are expected to support search parameters as detailed in the [domain data specifications](../../../hcx-domain-specifications/domain-data-specifications/). For FHIR based entities this is expected to be clearly published in the corresponding implementation guides. Visibility and availability of the attributes in the search result payloads are also expected to be defined in domain data specifications.

### **CoverageEligibility**

* **Eligibility check**
  * /coverageeligibility/check (provider->HCX, HCX->payor)
  * /coverageeligibility/on\_check (payor->HCX, HCX->provider)

### **Claims**

* **PreDetermination submission**
  * /predetermination/submit (provider->HCX, HCX->payor)
  * /predetermintation/on\_submit (payor->HCX, HCX->provider)
* **PreAuth submission**
  * /preauth/submit (provider->HCX, HCX->payor)
  * /preauth/on\_submit (payor->HCX, HCX->provider)
* **Claim submission**
  * /claim/submit (provider->HCX, HCX->payor)
  * /claim/on\_submit (payor->HCX, HCX->provider)

### **Communications**

Communications API will be used for communications between the payors and providers within the claims cycle.

* /communication/request
* /communication/on\_request

### **Payments**

* **Payment notice and acknowledgement**
  * /paymentnotice/request (payor>HCX, HCX->provider-)
  * /paymentnotice/on\_request (provider->HCX, HCX->payor)

### **Operational APIs**

* **Entity Status API**: Status API can be used by providers to know the status of a request made by them. For example, a provider can query the status of a pre-auth request using the status API. HCX gateway shall return the protocol status synchronously and the recipient returns the status in the on\_status callback API asynchronously.
  * /hcx/status
  * /hcx/on\_status
* **Entity Search API**: Search API is for regulators/observers to fetch the details of claims for reconciliation and may be for grievance redressal (in future). For example, NHA can request for all claims processed by all payors in the last one week. The response to the search request will be via the callback API (/hcx/on\_search) containing a list of encrypted FHIR objects matching the search criteria.
  * /hcx/search
  * /hcx/on\_search

Following [OpenAPI 3.0 specification](https://raw.githubusercontent.com/Swasth-Digital-Health-Foundation/hcx-specs/v0.7/API%20Definitions/openapi\_hcx.yaml) details these APIs in detail.

## Questions for Consultation

#### Question 1

Please review the Exchange Protocol and provide comments/suggestions on its comprehensiveness. Kindly provide aspects of the protocol would you find challenging and suggestions to overcome those challenges.

#### Question 2

While the consultation paper covers only interactions between the provider and payer, and the interactions with the beneficiary will be detailed post public consultation, what additional workflows do you think must be considered?

{% hint style="info" %}
Instructions to send responses to the consultation questions are available [here](../../../how-to-submit-responses.md).
{% endhint %}
