---
description: Details of various exchange scenarios and steps involved
---

# Exchange Protocol

## **Key Terms**

1. **Request** - Initiation of the flow by the sender by passing relevant payload in the message structure defined by this protocol. Requests may travel from Sender to the Receiver through a relay of HCX instances.
2. **Response** - Response/reply by the recipient of the request by passing relevant response payload defined by the protocol. The key difference here is that it is always in response to an earlier event received from the HCX instance and needs to carry the correlation\_id from the original event. Responses may also travel from the “original request message” recipient to the “original request message” sender through a relay of HCX instances.
3. **HCX instance** - A runtime of the HCX platform that performs the role of message receiving and forwarding on behalf of senders and receivers. Based on the use case, any participating party may act as the sender (thereby a requester), or a receiver (thereby a recipient). E.g. for the cashless claims use cases defined so far - Providers will be the senders in case of CheckEligibility, PreAuth and ClaimSubmission use cases (and the payers will be recipients), while Payers will be the sanders in case of PaymentNotice (and the providers will be recipients).
4. **Message** - HCX protocol transfers a Message that contains a transport envelope and the content as per the use case.
   1. Transport envelope is a set attribute that carries the transport information for HCX to reliably forward the message to the destination
   2. Content would have two parts:
      1. Business headers - any domain or use case specific information which may not be necessary for the transportation but allows more information about the payload, e.g. type of the payload
      2. Payload - Domain object defined for the pertinent use case. Usually, this data will be encrypted using the recipient's key to ensure that HCX instances cannot view this data.
5. **Senders and Receivers** - Two systems participating in the information exchange. They may also be referred to as client/server as per current industry terminology. E.g. Provider(s) are senders in claims flow use case, and Payor(s) are senders in Payment Notice use case in the flow diagram above.

Following sub-sections provide details on the primary and alternate flows on the data exchange.
