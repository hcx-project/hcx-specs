---
description: Handling domain/business processing related errors
---

# Handling Processing Errors

While the protocol related errors are expected to be handled as per [Error Response section in the Technical Specifications](../../hcx-technical-specifications/open-protocol/key-components-building-blocks/error-descriptions.md), this section provides detail on responding when there are errors during business processing of the request.

An error in business processing will be responded using corresponding on\_\* callback containing corresponding response FHIR profile with following additional constraints:

1. **x-hcx-status** needs to be set to "response.error"
2. Error code in **x-hcx-errordetails** header needs to be set to "ERR\_DOMAIN\_PROCESSING" as mentioned in [Recipient error scenarios table](../../hcx-technical-specifications/open-protocol/key-components-building-blocks/error-descriptions.md#recipient-error-scenarios) in the Error Response section in the Technical Specifications.
3. Within the corresponding response FHIR profile {response\_resource}
   1. Error status need to be indicated in {response\_resource}.**outcome** attribute
   2. Details of error need to be carried in the corresponding {resopnse\_resource}.**error** attribute.
