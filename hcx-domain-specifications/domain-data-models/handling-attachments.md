---
description: Exchanging supporting information using attachments
---

# Handling Attachments

In HCX context, sender's may need to include supporting information like required documents, checklists, answers to questionnaires, scans, Proof of Identity, Proof of presence, images, X-Rays, Prescriptions, etc.

As described in [section 13.0.10 of FHIR financial module](http://build.fhir.org/financial-module.html#attachments), supporting information may be provided, as a reference or the actual material to support claims cycle (predetermination, pre-auth, claim submission) in a variety of manners:

1. Included: in the {resource}.supportingInfo section; or
2. Unsolicited: in a Communication which refers to the Claim or Explanation of Benefit; or
3. Solicited: in a Communication in response to a CommunicationRequest from the insurer requesting more information; or
4. Input: in the input parameters of a FHIR operation or Task.input element if a Task resource is used.

This version of protocol supports the below listed mechanisms to share such supporting information as detailed below:

### “Included” in the “{resource}.supportingInfo”

Supporting documents can be included in the {resource}.supportingInfo section as below:

1. As a reference to an external system url, e.g. PHR systems, using supportingInfo.value\[x].valueAttachment.url (along with other needed details in the attachment profile). Please note that the receiving party (e.g. payor) may need to perform the needed access processes on the resource against the URL as needed, e.g. the consent process as per ABDM HIE-CM in case the url points to a PHR system URL.
2. As inline data blob inside the {resource} using supportingInfo.value\[x].valueAttachment.data (along with other needed details in the attachment profile).

### “Solicited” using “Communication.payload”

Using communication APIs provided as part of this version, supporting documents can be included in the communication.payload section in response to the CommunicationRequest as below:

1. As a reference to an external system url, e.g. PHR systems, using payload.content\[x].contentAttachment.url (along with other needed details in the attachment profile). Please note that the receiving party (e.g. payor) may need to perform the needed access processes on the resource against the URL as needed, e.g. the consent process as per ABDM HIE-CM in case the url points to a PHR system URL.
2. As inline data blob inside the {resource} using payload.content\[x].contentAttachment.data (along with other needed details in the attachment profile).

### Sender (Requested) managed DMS

Pre-signed URLs can be used to exchange documents between senders and receivers in a secure and efficient manner:

1. The sender generates pre-signed URLs for the documents they want to share. These URLs include a signed authorization token that specifies the permissions and expiration time for accessing the document.
2. The sender shares pre-signed URLs via HCX request resources ({reqeust\_resource}.supportingInfo or Communication.payload) to the receiver as detailed above.
3. The receiver accesses the documents using the pre-signed URLs. The authorization token embedded in the URLs verifies that the receiver has permission to access the document and that the URL has not expired.
4. Once the receiver has accessed the document, they can view it, download it, or save it to their own system.

Pre-signed URLs are a secure and tamper-proof method for exchanging documents between senders and receivers. The use of an authorization token ensures that only authorized individuals can access the document, and the sender can further enhance security by strategies like - limiting the number of times the document can be accessed, adding unique identifiers from the request, etc. This method is easily accessible and does not require any special software or infrastructure, as the documents can be stored in cloud-based storage services like Amazon S3 or Microsoft Azure. Additionally, pre-signed URLs can be set to expire after a specified time period, protecting the document's confidentiality and preventing access after it is no longer required. Given these benefits, pre-signed URLs are **highly recommended** for document sharing in HCX flows.

### Receiver manager DMS

When the receiver manages the Document Management System (DMS), one of the key challenges is to share the DMS details, such as the type of DMS (http, ftp), endpoint URL, and access credentials, with the sender in a manner that allows the receiver to change the DMS details as needed. There are two ways to achieve this:

**Out of band DMS details sharing:**

This leverages existing ways of sharing Payer’s DMS details with others (Providers, TPAs, etc.) and HCX protocol doesn’t have a role to play in such sharing of DMS details.

**Inline DMS details sharing through HCX**

This method enables the sharing of DMS details between the sender and receiver via HCX response resources in an inline manner. The organization.endpoint profiles available in various response resources such as CoverageEligibilityResponse and ClaimResponse are utilized for this purpose.

Here is an overview of how the inline DMS details sharing is intended to work:

1. Receiver receives one of the cycle request from sender
2. If the sender doesn't have its own DMS or can't create pre-signed URLs for some reason, the receiver decides to send its DMS details to the sender to use it as DMS. This can be done for various cycles in the protocol:
   1. **CoverageEligibility cycle**: Payer sends the DMS details as part of CoverageEligibilityResponse.insurer.endpoint.
   2. **Claim cycles (predetermination, pre-auth, claim)**: Payer can send the DMS details as part of ClaimResponse.insurer.endpoint. This would mainly be used if the CoverageEligibility cycle wasn't used for the episode.
   3. **CommunicationRequest cycle**: Receiver could also raise explicit (solicited) CommunicationRequest and send the DMS details in CommunicationRequest.requester(organisation).endpoint. The sender is expected to respond as described in 3c below.
3. The sender can then use the received DMS information to access the receiver's DMS, upload necessary documents, and provide the url reference to the document in subsequent requests/cycles as follows:
   1. As part of **supportingInfo** in predetermination, pre-auth, claim cycles.
   2. As part of proactive **CommunicationRequest payload** to send the information beyond the Claim request cycle, e.g. when DMS details were themselves received as part of a previous/current claim cycle (predetermination, pre-auth, claim cycles).
   3. Respond to a CommunicationRequest raised by the receiver using **Communication.payload\[]**.
4. Receivers are expected to communicate following DMS details using Organisation.endpoint attribute of resources listed in point 2 above:
   1. organisation.endpoint.connectionType should be one of “http” or “ftp”.
   2. Organisation.endpoint.address should be the respective url for the system
   3. Organisation.endpoint.header (array) should contain the protocol specific headers to access the DMS
      1. In the case of HTTP, the headers required would depend on the authentication scheme chosen by the DMS. You can refer to the list of authentication schemes and their respective RFCs [here](https://www.iana.org/assignments/http-authschemes/http-authschemes.xhtml).
      2. In the case of FTP, the headers could be used to carry needed FTP credentials.

Following section provides details of the attachment handling erros and responses.
