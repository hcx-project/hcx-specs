---
description: Exchanging supporting information using attachments
---

# Handling Attachments

In HCX context, sender's may need to include supporting information like required  documents, checklists, answers to questionnaires, scans, Proof of Identity, Proof of presence, images, X-Rays, Prescriptions, etc.&#x20;

As described in [section 13.0.10 of FHIR financial module](http://build.fhir.org/financial-module.html#attachments), supporting information may be provided, as a reference or the actual material to support claims cycle (predetermination, pre-auth, claim submission) in a variety of manners:&#x20;

1. Included: in the {resource}.supportingInfo section; or&#x20;
2. Unsolicited: in a Communication which refers to the Claim or Explanation of Benefit; or&#x20;
3. Solicited: in a Communication in response to a CommunicationRequest from the insurer requesting more information; or&#x20;
4. Input: in the input parameters of a FHIR operation or Task.input element if a Task resource is used.

This version of protocol supports the “**Included**” and “**Solicited**” mechanisms to share such supporting information as detailed below:&#x20;

### “Included” in the “{resource}.supportingInfo”&#x20;

Supporting documents can be included in the {resource}.supportingInfo section as below: &#x20;

1. As a reference to an external system url, e.g. PHR systems, using supportingInfo.value\[x].valueAttachment.url (along with other needed details in the attachment profile). Please note that the receiving party (e.g. payor) may need to perform the needed access processes on the resource against the URL as needed, e.g. the consent process as per ABDM HIE-CM in case the url points to a PHR system URL.&#x20;
2. As inline data blob inside the {resource} using supportingInfo.value\[x].valueAttachment.data (along with other needed details in the attachment profile).

### “Solicited” using “Communication.payload”&#x20;

Using communication APIs provided as part of this version, supporting documents can be included in the communication.payload section in response to the CommunicationRequest as below:&#x20;

1. As a reference to an external system url, e.g. PHR systems, using payload.content\[x].contentAttachment.url (along with other needed details in the attachment profile). Please note that the receiving party (e.g. payor) may need to perform the needed access processes on the resource against the URL as needed, e.g. the consent process as per ABDM HIE-CM in case the url points to a PHR system URL.&#x20;
2. As inline data blob inside the {resource} using payload.content\[x].contentAttachment.data (along with other needed details in the attachment profile).
