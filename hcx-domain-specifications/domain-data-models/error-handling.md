---
description: Handling domain/business processing related errors
---

# Error Handling

While the protocol related errors are expected to be handled as per [Error Response section in the Technical Specifications](../../hcx-technical-specifications/open-protocol/key-components-building-blocks/error-descriptions.md), this section provides detail on responding when there are errors during business processing of the request.&#x20;

An error in business processing will be responded using corresponding on\_\* callback containing corresponding response FHIR profile with following additional constraints:

1. **x-hcx-status** needs to be set to "response.error"
2. Error code in **x-hcx-error**_**details** header needs to be set to "_ERR\_DOMAIN\_PROCESS" as mentioned in [Recipient error scenarios table](../../hcx-technical-specifications/open-protocol/key-components-building-blocks/error-descriptions.md#recipient-error-scenarios) in the Error Response section in the Technical Specifications. &#x20;
