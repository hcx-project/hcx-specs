---
description: Details of the APIs that facilitate the claims exchange flow
---

# Primary Flow APIs

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
