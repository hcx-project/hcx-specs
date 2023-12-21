---
description: >-
  Details of APIs that provide support for operations within HCX. These APIs are
  useful in enabling the additional message flows in HCX.
---

# Supporting APIs

### **Communication APIs**

Communications API will be used for communications between multiple participants in the HCX ecosystem.

* /communication/request

{% swagger src="https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.9/API%20Definitions/openapi_hcx.yaml" path="/communication/request" method="post" %}
[https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.9/API%20Definitions/openapi_hcx.yaml](https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.9/API%20Definitions/openapi_hcx.yaml)
{% endswagger %}

* /communication/on\_request

{% swagger src="https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.9/API%20Definitions/openapi_hcx.yaml" path="/communication/on_request" method="post" %}
[https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.9/API%20Definitions/openapi_hcx.yaml](https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.9/API%20Definitions/openapi_hcx.yaml)
{% endswagger %}

### **Status APIs**

Status API can be used by providers to know the status of a request made by them. For example, a provider can query the status of a pre-auth request using the status API. HCX gateway shall return the protocol status synchronously and the recipient returns the status in the on\_status callback API asynchronously.

* /hcx/status

{% swagger src="https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.9/API%20Definitions/openapi_hcx.yaml" path="/hcx/status" method="post" %}
[https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.9/API%20Definitions/openapi_hcx.yaml](https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.9/API%20Definitions/openapi_hcx.yaml)
{% endswagger %}

* /hcx/on\_status

{% swagger src="https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.9/API%20Definitions/openapi_hcx.yaml" path="/hcx/on_status" method="post" %}
[https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.9/API%20Definitions/openapi_hcx.yaml](https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.9/API%20Definitions/openapi_hcx.yaml)
{% endswagger %}

### **Third Party Information Sharing APIs**

Following APIs are included in the protocol for claim information fetching using EOB resource:

* _**eob/fetch**_: Used by third parties (like IIB, sponsor or an ISNP) to request for information about a specific claim (or pre-auth or a pre-determination). The third party shall call the fetch API on the HCX switch and HCX internally routes the fetch request to the relevant participant. The payload for this API should contain the correlation\_id of the cycle for which the information is being requested for.
* _**eob/on\_fetch**_: This is the callback API via which the requested information is sent back to the third party via the HCX switch.

**Request Payload**\
Similar to [Status API](./#operational-apis) where a [Task](../../../../hcx-domain-specifications/domain-data-models/#task) FHIR resource is used as the payload to request for status of a specific API call, the Fetch API shall also use Task resource to request for information about a specific claim workflow. The Task resource shall contain details about the claim workflow for which the information is being requested and optionally the purpose of the fetch request.

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

{% swagger src="https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.9/API%20Definitions/openapi_hcx_fetch.yaml" path="/eob/fetch" method="post" %}
[https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.9/API%20Definitions/openapi_hcx_fetch.yaml](https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.9/API%20Definitions/openapi_hcx_fetch.yaml)
{% endswagger %}

{% swagger src="https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.9/API%20Definitions/openapi_hcx_fetch.yaml" path="/eob/on_fetch" method="post" %}
[https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.9/API%20Definitions/openapi_hcx_fetch.yaml](https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.9/API%20Definitions/openapi_hcx_fetch.yaml)
{% endswagger %}

Third Party Information Sharing API specifications in OpenAPI 3.0 format are available [here](https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.9/API%20Definitions/openapi\_hcx\_fetch.yaml).
