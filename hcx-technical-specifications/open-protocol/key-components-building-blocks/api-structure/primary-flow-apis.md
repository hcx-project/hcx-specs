---
description: Details of the APIs that facilitate the claims exchange flow
---

# Primary Flow APIs

## API Structure

Based on the protocol definition and the message structure, each use case API in the HCX ecosystem is expected to follow the following pattern for the onward and return journey of the use case message:

\<transport\_protocol>://\<server\_address>/\<protocol\_version/>\<resource\_name>/\<action|on\_action>, where

* **transport\_protocol** - for HCX V1 purpose it will always be **https**
* **server\_address** is the address of the server on which the API is called (an HCX for payor/provider or a payor/provider/HCX for an HCX)
* **protocol\_version** - API version for the current protocol to help support protocol transitions
* **resource\_name** is the name of the domain resource that the API is serving. E.g. for cashless claims, it may be “claims”, “coverage eligibility”, etc. based on the use case.
* **action** is the action sought within the context of that resource
* **on\_action** represents the callback from the receiving system for responding to the original message

Keeping this pattern in mind, following APIs are expected to be supported.

### **CoverageEligibility**

* **Eligibility check**
* /coverageeligibility/check (provider->HCX, HCX->payor)

{% swagger src="https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.9/API%20Definitions/openapi_hcx.yaml" path="/coverageeligibility/check" method="post" %}
[https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.9/API%20Definitions/openapi_hcx.yaml](https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.9/API%20Definitions/openapi_hcx.yaml)
{% endswagger %}

* /coverageeligibility/on\_check (payor->HCX, HCX->provider)

{% swagger src="https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.9/API%20Definitions/openapi_hcx.yaml" path="/coverageeligibility/on_check" method="post" %}
[https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.9/API%20Definitions/openapi_hcx.yaml](https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.9/API%20Definitions/openapi_hcx.yaml)
{% endswagger %}

### **Claims**

* **PreDetermination submission**
* /predetermination/submit (provider->HCX, HCX->payor)

{% swagger src="https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.9/API%20Definitions/openapi_hcx.yaml" path="/predetermination/submit" method="post" %}
[https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.9/API%20Definitions/openapi_hcx.yaml](https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.9/API%20Definitions/openapi_hcx.yaml)
{% endswagger %}

* /predetermintation/on\_submit (payor->HCX, HCX->provider)

{% swagger src="https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.9/API%20Definitions/openapi_hcx.yaml" path="/predetermination/on_submit" method="post" %}
[https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.9/API%20Definitions/openapi_hcx.yaml](https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.9/API%20Definitions/openapi_hcx.yaml)
{% endswagger %}

* **PreAuth submission**
* /preauth/submit (provider->HCX, HCX->payor)

{% swagger src="https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.9/API%20Definitions/openapi_hcx.yaml" path="/preauth/submit" method="post" %}
[https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.9/API%20Definitions/openapi_hcx.yaml](https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.9/API%20Definitions/openapi_hcx.yaml)
{% endswagger %}

* /preauth/on\_submit (payor->HCX, HCX->provider)

{% swagger src="https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.9/API%20Definitions/openapi_hcx.yaml" path="/preauth/on_submit" method="post" %}
[https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.9/API%20Definitions/openapi_hcx.yaml](https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.9/API%20Definitions/openapi_hcx.yaml)
{% endswagger %}

* **Claim submission**
* /claim/submit (provider->HCX, HCX->payor)

{% swagger src="https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.9/API%20Definitions/openapi_hcx.yaml" path="/claim/submit" method="post" %}
[https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.9/API%20Definitions/openapi_hcx.yaml](https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.9/API%20Definitions/openapi_hcx.yaml)
{% endswagger %}

* /claim/on\_submit (payor->HCX, HCX->provider)

{% swagger src="https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.9/API%20Definitions/openapi_hcx.yaml" path="/claim/on_submit" method="post" %}
[https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.9/API%20Definitions/openapi_hcx.yaml](https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.9/API%20Definitions/openapi_hcx.yaml)
{% endswagger %}

### **Payments**

* **Payment notice and acknowledgement**
* /paymentnotice/request (payor>HCX, HCX->provider-)

{% swagger src="https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.9/API%20Definitions/openapi_hcx.yaml" path="/paymentnotice/request" method="post" %}
[https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.9/API%20Definitions/openapi_hcx.yaml](https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.9/API%20Definitions/openapi_hcx.yaml)
{% endswagger %}

* /paymentnotice/on\_request (provider->HCX, HCX->payor)

{% swagger src="https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.9/API%20Definitions/openapi_hcx.yaml" path="/paymentnotice/on_request" method="post" %}
[https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.9/API%20Definitions/openapi_hcx.yaml](https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.9/API%20Definitions/openapi_hcx.yaml)
{% endswagger %}

Following [OpenAPI 3.0 specification](https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.9/API%20Definitions/openapi\_hcx.yaml) details these APIs in detail. These API specs can be opened in swagger editor via this [link](https://editor.swagger.io/?url=https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.9/API%20Definitions/openapi\_hcx.yaml).
