# eObjects

This version of the HCX specification defines the domain model specifications required for the following eObjects:

* Coverage Eligibility Request and Coverage Eligibility Response
* Claim Request and Claim Response: These objects will be used for both Pre-Authorization and Claim use cases (and for Pre-Determination also in future).
* Payment Notice and Payment Reconciliation

As mentioned in the design considerations for domain specification, the eObjects leverage HL7/FHIR4 specification and extend it, wherever required.

## Coverage Eligibility Request

As per the design considerations and guidelines listed in the previous sections, the coverage eligibility request payload has to be created as an FHIR document bundle. The bundle should have the following resources:

| **Resource**               | **Description**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| -------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Composition                | <p><strong>type</strong>: should be a code representing Coverage Eligibility Request document type.</p><p><strong>section</strong>: The document shall have one section with a single entry having reference to CoverageEligibilityRequest resource.</p><p><strong>structure definition</strong>: <a href="https://github.com/Swasth-Digital-Health-Foundation/standards/blob/main/IG-Publisher/input/hcx-definitions/StructureDefinition-CoverageEligibilityRequestDocument.json">CoverageEligibilityRequest Document</a></p>                                                                                                                                                                                                                                                                                                                                                       |
| CoverageEligibilityRequest | <p>The document must contain a CoverageEligibilityRequest resource.</p><p><strong>FHIR Profile</strong>: <a href="https://swasth-digital-health-foundation.github.io/standards/output/StructureDefinition-CoverageEligibilityRequest.html">link</a></p><p><strong>structure definition</strong>: <a href="https://github.com/Swasth-Digital-Health-Foundation/standards/blob/main/IG-Publisher/input/hcx-definitions/StructureDefinition-CoverageEligibilityRequest.json">CoverageEligibilityRequest</a></p>                                                                                                                                                                                                                                                                                                                                                                         |
| Patient                    | <p>The document should contain a Patient resource with minimal required information about the patient (refer to rows #38-42 in the “<a href="https://docs.google.com/spreadsheets/d/1TlWKl_MJRn15NfTsifSTvwAxOw09ctQzfj72uBNsryA/edit#gid=1625524191">Coverage eligibility check</a>” sheet).</p><p><strong>FHIR Profile details</strong>:</p><ol><li>Patient resources should mandatorily have an NDHM identifier.</li><li>Patient resources can also have a hospital Id (Medical record number).</li><li>Patient resources can also have an insurance id (PMJAY ID).</li><li>Patient resources can also have employee IDs and other business identifiers.</li></ol><p><strong>structure definition</strong>: <a href="https://github.com/Swasth-Digital-Health-Foundation/standards/blob/main/IG-Publisher/input/hcx-definitions/StructureDefinition-Patient.json">Patient</a></p> |
| Coverage                   | <p>The document should contain one or more Coverage resources with minimal information of the policy about which the information is requested (refer to row#30 in the “<a href="https://docs.google.com/spreadsheets/d/1TlWKl_MJRn15NfTsifSTvwAxOw09ctQzfj72uBNsryA/edit#gid=1625524191">Coverage eligibility check</a>” sheet).</p><p><strong>FHIR Profile details</strong>:</p><ul><li>Coverage resources should mandatorily have an identifier for the policy ID issued by the insurer.</li></ul><p><strong>structure definition</strong>: <a href="https://github.com/Swasth-Digital-Health-Foundation/standards/blob/main/IG-Publisher/input/hcx-definitions/StructureDefinition-Coverage.json">Coverage</a></p>                                                                                                                                                                |

#### Domain Headers:

| **Key** | **Description** |
| ------- | --------------- |
|         |                 |
|         |                 |

#### Search Parameters:

| **Key** | **Description** |
| ------- | --------------- |
|         |                 |
|         |                 |

## Coverage Eligibility Response

| **Resource**                | **Description**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| --------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Composition                 | <p><strong>type</strong>: should be a code representing Coverage Eligibility Response document type.</p><p><strong>section</strong>: The document shall have one section with a single entry having reference to CoverageEligibilityResponse resource.</p><p><strong>structure definition</strong>: <a href="https://github.com/Swasth-Digital-Health-Foundation/standards/blob/main/IG-Publisher/input/hcx-definitions/StructureDefinition-CoverageEligibilityResponseDocument.json">CoverageEligibilityResponse Document</a></p>       |
| CoverageEligibilityResponse | <p>The document must contain a CoverageEligibilityResponse resource.</p><p><strong>FHIR Profile</strong>: <a href="https://swasth-digital-health-foundation.github.io/standards/output/StructureDefinition-CoverageEligibilityResponse.html">link</a></p><p><strong>structure definition</strong>: <a href="https://github.com/Swasth-Digital-Health-Foundation/standards/blob/main/IG-Publisher/input/hcx-definitions/StructureDefinition-CoverageEligibilityResponse.json">CoverageEligibilityResponse</a></p>                         |
| Coverage                    | <p>The document should contain one or more Coverage resources with minimal information of the policy about which the information is being returned.</p><p><strong>FHIR Profile details</strong>:</p><ul><li>Coverage resources should mandatorily have an identifier for the policy ID issued by the insurer.</li></ul><p><strong>structure definition</strong>: <a href="https://github.com/Swasth-Digital-Health-Foundation/standards/blob/main/IG-Publisher/input/hcx-definitions/StructureDefinition-Coverage.json">Coverage</a></p> |

#### Domain Headers:

| **Key** | **Description** |
| ------- | --------------- |
|         |                 |
|         |                 |

#### Search Parameters:

| **Key** | **Description** |
| ------- | --------------- |
|         |                 |
|         |                 |

## Claim Request

Claim object is used by providers to submit pre-authorization and claim requests to the payers. The same eObject can be used for both these use cases and the usage can be differentiated by the value of “claim.use” element. The value of this element should be set as “**preauthorization**” for Pre-Authorization requests and as “**claim**” for Claim requests.

| **Resource**        | **Description**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| ------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Composition         | <p><strong>type</strong>: should be a code representing Claim Request document type.</p><p><strong>section</strong>: The document shall have one section with multiple entries having references to Claim and Signature resources.</p><p><strong>structure definition</strong>: <a href="https://github.com/Swasth-Digital-Health-Foundation/standards/blob/main/IG-Publisher/input/hcx-definitions/StructureDefinition-ClaimRequestDocument.json">ClaimRequest Document</a></p>                                                         |
| Claim               | <p>The document must contain a Claim resource.</p><p><strong>FHIR Profile</strong>: <a href="https://swasth-digital-health-foundation.github.io/standards/output/StructureDefinition-Claim.html">link</a></p><p><strong>structure definition</strong>: <a href="https://github.com/Swasth-Digital-Health-Foundation/standards/blob/main/IG-Publisher/input/hcx-definitions/StructureDefinition-Claim.json">Claim</a></p>                                                                                                                 |
| Coverage            | <p>The document should contain one or more Coverage resources with minimal information on the policy about which the information is being returned.</p><p><strong>FHIR Profile details</strong>:</p><ul><li>Coverage resources should mandatorily have an identifier for the policy ID issued by the insurer.</li></ul><p><strong>structure definition</strong>: <a href="https://github.com/Swasth-Digital-Health-Foundation/standards/blob/main/IG-Publisher/input/hcx-definitions/StructureDefinition-Coverage.json">Coverage</a></p> |
| Encounter           | <p>Details of the Encounters during which this Claim was created or to which the creation of this Claim is associated.</p><p><strong>FHIR Profile</strong>: <a href="https://swasth-digital-health-foundation.github.io/standards/output/StructureDefinition-Encounter.html">link</a></p><p><strong>structure definition</strong>: <a href="https://github.com/Swasth-Digital-Health-Foundation/standards/blob/main/IG-Publisher/input/hcx-definitions/StructureDefinition-Encounter.json">Encounter</a></p>                             |
| Condition           | <p>Details of the health conditions relevant to this Claim request.</p><p><strong>FHIR Profile</strong>: <a href="https://swasth-digital-health-foundation.github.io/standards/output/StructureDefinition-Condition.html">link</a></p><p><strong>structure definition</strong>: <a href="https://github.com/Swasth-Digital-Health-Foundation/standards/blob/main/IG-Publisher/input/hcx-definitions/StructureDefinition-Condition.json">Condition</a></p>                                                                                |
| Signature resources | <p>List of signatures by Hospital, Doctor and Patient associated with this Claim request.</p><p><strong>structure definition</strong>: <a href="https://github.com/Swasth-Digital-Health-Foundation/standards/blob/main/IG-Publisher/input/hcx-definitions/StructureDefinition-hcp-signature.json">Signature</a></p>                                                                                                                                                                                                                     |

#### Domain Headers:

| **Key** | **Description**                                                                         |
| ------- | --------------------------------------------------------------------------------------- |
| usage   | “preauthorization” or “claim”, to indicate the use case this eObject is being used for. |
|         |                                                                                         |

#### Search Parameters:

| **Key** | **Description** |
| ------- | --------------- |
|         |                 |
|         |                 |

## Claim Response

ClaimResponse object is used by payers to send the response for pre-authorization and claim requests to the providers. The same eObject can be used for both these use cases and the usage can be differentiated by the value of “ClaimResponse.use” element. The value of this element should be set as “**preauthorization**” for Pre-Authorization responses and as “**claim**” for Claim responses.

| **Resource**  | **Description**                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Composition   | <p><strong>type</strong>: should be a code representing Claim Response document type.</p><p><strong>section</strong>: The document shall have one section with a single entry having reference to ClaimResponse resource.</p><p><strong>structure definition</strong>: <a href="https://github.com/Swasth-Digital-Health-Foundation/standards/blob/main/IG-Publisher/input/hcx-definitions/StructureDefinition-ClaimResponseDocument.json">ClaimResponse Document</a></p> |
| ClaimResponse | <p>The document must contain a ClaimResponse resource.</p><p><strong>FHIR Profile</strong>: <a href="https://swasth-digital-health-foundation.github.io/standards/output/StructureDefinition-ClaimResponse.html">link</a></p><p><strong>structure definition</strong>: <a href="https://github.com/Swasth-Digital-Health-Foundation/standards/blob/main/IG-Publisher/input/hcx-definitions/StructureDefinition-ClaimResponse.json">ClaimResponse</a></p>                  |

#### Domain Headers:

| **Key** | **Description**                                                                         |
| ------- | --------------------------------------------------------------------------------------- |
| usage   | “preauthorization” or “claim”, to indicate the use case this eObject is being used for. |
|         |                                                                                         |

#### Search Parameters:

| **Key** | **Description** |
| ------- | --------------- |
|         |                 |
|         |                 |

## Payment Notice

| **Resource**          | **Description**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| --------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Composition           | <p><strong>type</strong>: should be a code representing Payment Notice document type.</p><p><strong>section</strong>: The document shall have one section with a single entry having reference to PaymentNotice resource.</p>                                                                                                                                                                                                                                                                                                                                |
| PaymentNotice         | <p>The document must contain a PaymentNotice resource.</p><p><strong>FHIR Profile</strong>: <a href="https://swasth-digital-health-foundation.github.io/standards/output/StructureDefinition-PaymentNotice.html">link</a></p><p><strong>structure definition</strong>: <a href="https://github.com/Swasth-Digital-Health-Foundation/standards/blob/main/IG-Publisher/input/hcx-definitions/StructureDefinition-PaymentNotice.json">PaymentNotice</a></p>                                                                                                     |
| PaymentReconciliation | <p>The document should contain a PaymentReconciliation resource with information about the payment related to this payment notice.</p><p><strong>FHIR Profile</strong>: <a href="https://swasth-digital-health-foundation.github.io/standards/output/StructureDefinition-PaymentReconciliation.html">link</a></p><p><strong>structure definition</strong>: <a href="https://github.com/Swasth-Digital-Health-Foundation/standards/blob/main/IG-Publisher/input/hcx-definitions/StructureDefinition-PaymentReconciliation.json">PaymentReconciliation</a></p> |

#### Domain Headers:

| **Key** | **Description** |
| ------- | --------------- |
|         |                 |
|         |                 |

#### Search Parameters:

| **Key** | **Description** |
| ------- | --------------- |
|         |                 |
|         |                 |
