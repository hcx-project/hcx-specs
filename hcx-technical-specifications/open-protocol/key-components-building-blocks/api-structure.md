---
description: Details of the protocol APIs that facilitate the exchange
---

# API Structure

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

Please note that search APIs are expected to support search parameters as detailed in the [domain data specifications](../../../hcx-domain-specifications/). For FHIR based entities this is expected to be clearly published in the corresponding implementation guides. Visibility and availability of the attributes in the search result payloads are also expected to be defined in domain data specifications.

### **CoverageEligibility**

* **Eligibility check**
* /coverageeligibility/check (provider->HCX, HCX->payor)

{% swagger src="https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.8/API%20Definitions/openapi_hcx.yaml" path="/coverageeligibility/check" method="post" %}
[https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.8/API%20Definitions/openapi_hcx.yaml](https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.8/API%20Definitions/openapi_hcx.yaml)
{% endswagger %}

* /coverageeligibility/on\_check (payor->HCX, HCX->provider)

{% swagger src="https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.8/API%20Definitions/openapi_hcx.yaml" path="/coverageeligibility/on_check" method="post" %}
[https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.8/API%20Definitions/openapi_hcx.yaml](https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.8/API%20Definitions/openapi_hcx.yaml)
{% endswagger %}

### **Claims**

* **PreDetermination submission**
* /predetermination/submit (provider->HCX, HCX->payor)

{% swagger src="https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.8/API%20Definitions/openapi_hcx.yaml" path="/predetermination/submit" method="post" %}
[https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.8/API%20Definitions/openapi_hcx.yaml](https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.8/API%20Definitions/openapi_hcx.yaml)
{% endswagger %}

* /predetermintation/on\_submit (payor->HCX, HCX->provider)

{% swagger src="https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.8/API%20Definitions/openapi_hcx.yaml" path="/predetermination/on_submit" method="post" %}
[https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.8/API%20Definitions/openapi_hcx.yaml](https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.8/API%20Definitions/openapi_hcx.yaml)
{% endswagger %}

* **PreAuth submission**
* /preauth/submit (provider->HCX, HCX->payor)

{% swagger src="https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.8/API%20Definitions/openapi_hcx.yaml" path="/preauth/submit" method="post" %}
[https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.8/API%20Definitions/openapi_hcx.yaml](https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.8/API%20Definitions/openapi_hcx.yaml)
{% endswagger %}

* /preauth/on\_submit (payor->HCX, HCX->provider)

{% swagger src="https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.8/API%20Definitions/openapi_hcx.yaml" path="/preauth/on_submit" method="post" %}
[https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.8/API%20Definitions/openapi_hcx.yaml](https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.8/API%20Definitions/openapi_hcx.yaml)
{% endswagger %}

* **Claim submission**
* /claim/submit (provider->HCX, HCX->payor)

{% swagger src="https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.8/API%20Definitions/openapi_hcx.yaml" path="/claim/submit" method="post" %}
[https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.8/API%20Definitions/openapi_hcx.yaml](https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.8/API%20Definitions/openapi_hcx.yaml)
{% endswagger %}

* /claim/on\_submit (payor->HCX, HCX->provider)

{% swagger src="https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.8/API%20Definitions/openapi_hcx.yaml" path="/claim/on_submit" method="post" %}
[https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.8/API%20Definitions/openapi_hcx.yaml](https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.8/API%20Definitions/openapi_hcx.yaml)
{% endswagger %}

### **Communications**

Communications API will be used for communications between the payors and providers within the claims cycle.

* /communication/request

{% swagger src="https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.8/API%20Definitions/openapi_hcx.yaml" path="/communication/request" method="post" %}
[https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.8/API%20Definitions/openapi_hcx.yaml](https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.8/API%20Definitions/openapi_hcx.yaml)
{% endswagger %}

* /communication/on\_request

{% swagger src="https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.8/API%20Definitions/openapi_hcx.yaml" path="/communication/on_request" method="post" %}
[https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.8/API%20Definitions/openapi_hcx.yaml](https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.8/API%20Definitions/openapi_hcx.yaml)
{% endswagger %}

### **Payments**

* **Payment notice and acknowledgement**
* /paymentnotice/request (payor>HCX, HCX->provider-)

{% swagger src="https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.8/API%20Definitions/openapi_hcx.yaml" path="/paymentnotice/request" method="post" %}
[https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.8/API%20Definitions/openapi_hcx.yaml](https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.8/API%20Definitions/openapi_hcx.yaml)
{% endswagger %}

* /paymentnotice/on\_request (provider->HCX, HCX->payor)

{% swagger src="https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.8/API%20Definitions/openapi_hcx.yaml" path="/paymentnotice/on_request" method="post" %}
[https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.8/API%20Definitions/openapi_hcx.yaml](https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.8/API%20Definitions/openapi_hcx.yaml)
{% endswagger %}

### **Operational APIs**

* **Entity Status API**: Status API can be used by providers to know the status of a request made by them. For example, a provider can query the status of a pre-auth request using the status API. HCX gateway shall return the protocol status synchronously and the recipient returns the status in the on\_status callback API asynchronously.
* /hcx/status

{% swagger src="https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.8/API%20Definitions/openapi_hcx.yaml" path="/hcx/status" method="post" %}
[https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.8/API%20Definitions/openapi_hcx.yaml](https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.8/API%20Definitions/openapi_hcx.yaml)
{% endswagger %}

* /hcx/on\_status

{% swagger src="https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.8/API%20Definitions/openapi_hcx.yaml" path="/hcx/on_status" method="post" %}
[https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.8/API%20Definitions/openapi_hcx.yaml](https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.8/API%20Definitions/openapi_hcx.yaml)
{% endswagger %}

Following [OpenAPI 3.0 specification](https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.8/API%20Definitions/openapi\_hcx.yaml) details these APIs in detail.: Search API is for regulators/observers to fetch the details of claims for reconciliation and maybe for grievance redressal (in future). For example, NHA can request for all claims processed by all payors in the last one week. The response to the search request will be via the callback API (/hcx/on\_search) containing a list of encrypted FHIR objects matching the search criteria.
