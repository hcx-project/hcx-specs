---
description: Details of APIs that support in the exchange of claims within HCX.
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

Following [OpenAPI 3.0 specification](https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.9/API%20Definitions/openapi\_hcx.yaml) details these APIs in detail. These API specs can be opened in swagger editor via this [link](https://editor.swagger.io/?url=https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.9/API%20Definitions/openapi\_hcx.yaml).
