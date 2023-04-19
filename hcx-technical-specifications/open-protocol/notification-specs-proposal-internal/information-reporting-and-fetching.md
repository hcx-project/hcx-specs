---
description: Enabling use cases for sharing information related to claims
---

# Information Reporting & Fetching

There are multiple use cases in the context of claims where certain information about the claims need to be shared to parties that are not directly involved in the claim processing cycle. Some such examples are:

* Regulators like IIB need to collect information about the processed claims at the completion of a claims cycle. IIB uses this information to help the insurance industry with information and analytical support.
* Sponsors like NHA/SHA/Corporate/Community need to know about completion and details of a claims cycle for all the patients sponsored by them.
* An ISNP needs to know the status and details of a claim on behalf of its patient.

Such information can be made available to the interested parties in either of the following ways in HCX:

1. Parties involved in the cycle can report the information to all the subscribed parties when a claim cycle is completed
2. Parties who need information about a claim cycle can fetch the information from involved parties after the completion of a claim cycle (this is mostly be triggered when the interested party receives the relevant workflow notification)

### Information Reporting

Information reporting can be enabled by leveraging the [notifications](../../../import/notification-specs-proposal-internal.md) capability of the protocol. Since the information to be reported may contain PII information of the patients & other sensitive information, the “PII carrying workflow notification” category of notifications should be used for this purpose.

The steps and process for PII carrying workflow notifications are detailed in the [Notification specifications](../notifications/categories.md#workflow-notification).

### Fetching Information

Though a mechanism to report information is available, there still may be some scenarios where the parties may need to fetch the required information on demand (e.g.: if the PII notification is not delivered due to technical problems). In such cases, there should be a way for the participants to fetch the required information by directly querying the involved party (a payor or a provider). As the current known use cases for information fetching are only around claim workflows and such information request can be fulfilled by sending the information in form of an ExplanationOfBenefit (EOB) resource, the API paths are qualified to clearly scope the usage of API only for this purpose (i.e. reporting of claims information using EOB resource).&#x20;

Following two APIs will be enabled for claim information fetching using EOB resource:

* _**eob/fetch**_: Used by third parties (like IIB, sponsor or an ISNP) to request for information about a specific claim (or pre-auth or a pre-determination). The third party shall call the fetch API on the HCX switch and HCX internally routes the fetch request to the relevant participant. The payload for this API should contain the correlation\_id of the cycle for which the information is being requested for.
* _**eob/on\_fetch**_: This is the callback API via which the requested information is sent back to the third party via the HCX switch.

**Request Payload**\
Similar to [Status API](../key-components-building-blocks/api-structure.md#operational-apis) where a [Task](../../../hcx-domain-specifications/domain-data-models/#task) FHIR resource is used as the payload to request for status of a specific API call, the Fetch API shall also use Task resource to request for information about a specific claim workflow. The Task resource shall contain details about the claim workflow for which the information is being requested and optionally the purpose of the fetch request.

Sample Task resource as Fetch API request payload:

```
{
  "resourceType": "Task",
  "id": "fm-example4",
  "status": "requested",
  "intent": "order",
  "priority": "stat",
  "code": {
    "coding": [
      {
        "system": "http://terminology.hl7.org/CodeSystem/Insurance",
        "code": "EOB-15C"
      }
    ]
  },
  "authoredOn": "2018-10-04T08:25:05+10:00",
  "lastModified": "2018-10-04T08:25:05+10:00",
  "requester": {
    "display": "IIB"
  },
  "input": [
    {
      "type": {
        "coding": [
          {
            "system": "http://terminology.hl7.org/CodeSystem/financialtaskinputtype",
            "code": "correlation-id"
          }
        ]
      },
      "valueId": "correlation-id-xyz"
    }
  ]
}
```

**Response Payload**\
The payload of response to a fetch request should contain all information related to a claim cycle. As per HL7, the ExplanationOfBenefit (EOB) resource combines key information from a Claim, a ClaimResponse, optional account information and can be used as a resource for data exchange for use cases like reporting. Hence, the ExplanationOfBenefit resource shall be used as the response payload for a claim workflow fetch request.

#### API Definitions

{% swagger src="https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.8/API%20Definitions/openapi_hcx_fetch.yaml" path="/eob/fetch" method="post" %}
[https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.8/API%20Definitions/openapi_hcx_fetch.yaml](https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.8/API%20Definitions/openapi_hcx_fetch.yaml)
{% endswagger %}

{% swagger src="https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.8/API%20Definitions/openapi_hcx_fetch.yaml" path="/eob/on_fetch" method="post" %}
[https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.8/API%20Definitions/openapi_hcx_fetch.yaml](https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.8/API%20Definitions/openapi_hcx_fetch.yaml)
{% endswagger %}

