---
description: >-
  Guidelines to create and definition of eObjects used in the current version of
  the protocol
---

# Domain Data Models

The domain data model consists of the electronic claim (e-claim) objects (a.k.a. **eObjects)** that are designed to capture the required information essential for processing a health claim transaction. The e-claim objects, being machine-readable, facilitate the flow of data exchange between different systems and data processing in health claim transactions without the need for human intervention.

## Guidelines for eObjects

### Bundle Structure

* All e-claim objects will be modelled as cycle specific FHIR bundles of type "collection".
* Every bundle must mandatorily contain at least one cycle-specific resource while also allowing additional resources that may be referenced from the main cycle specific resource.
* For example, the data packet for a coverage eligibility check request will be a bundle of type “HCX CoverageEligibility Request Bundle” and the bundle must have at least one “CoverageEligibilityRequest” FHIR resource embedded in it.

{% tabs %}
{% tab title="HCX CoverageEligibilityRequest Bundle" %}
* type = “collection”
* CoverageEligibilityRequest FHIR resource
* Patient FHIR resource
* Coverage FHIR resource
* Any other resources referenced in the CoverageEligibilityRequest resource
{% endtab %}
{% endtabs %}

### Identifiers:

* For any resources requiring identifiers (e.g. Patient.identifier), naming systems have to be defined and agreed upon within the affinity domain to be specified in the “identifier.system” element to namespace the identifier value. This can allow an entity or resource to be referenced against system-specific identifiers. For example, a patient may be referenced as:

```
{
 "resourceType": "Patient",
 "identifier": [
   {
     "system": "https://ndhm.gov.in/patients",
     "value": "hinapatel@ndhm"
   },
   {
     "system": "https://pmjay.gov.in/beneficiaries",
     "value": "QWRT23456"
   }
 ]
}
```

* For some identifiers, “identifier.type” can be used to provide additional information.
* “identifier.use” can be used to indicate what/where/how a particular identifier might be used for.
* Example:

```
{
 "type": { // type of identifier
   "coding": [
     {
       "system": "http://terminology.hl7.org/CodeSystem/v2-0203",
       "code": "EI",
       "display": "Employee Number"
     }
   ]
 },
 "system": "https://esi.karnataka.org/employees", // naming system
 "value": "BEN-ID-1001"
}
```

### Resources

* For external entities like patients, organisations, practitioners, etc, a reference alone may be enough unless additional information is required to be passed. For example, patient address & other demographics.

### Domain Header

* All eObjects shall be encrypted and sent in the API request body and cannot be accessed by the HCX gateways. However, there is a provision in the API request body for providers and payers to share certain eObjects' related information with the HCX gateway. This information can be sent in the domain\_header part of the request body (as key-value pairs) which can be accessed and stored by HCX gateways for auditing and reporting purposes. Each eObject shall define the domain header values that are to be sent in the API request body.

### Search Parameters

* In addition to the workflow APIs for claim processing workflows, HCX shall also define APIs for searching eObjects. To support the search APIs, all eObjects will define the search request parameters.

## eObjects

This version of the HCX specification defines the domain model specifications required for the following eObjects:

* Coverage Eligibility Request and Coverage Eligibility Response
* Claim Request and Claim Response: These objects will be used for Pre-Determination, Pre-Authorization and Claim use cases.
* Payment Notice and Payment Reconciliation
* Insurance Plan
* Communication Request and Communication
* Task

As mentioned in the design considerations for domain specification, the eObjects leverage HL7/FHIR4 specification and extend it, wherever required.

## Coverage Eligibility Request

As per the design considerations and guidelines listed in the previous sections, the coverage eligibility request payload has to be created as an FHIR document bundle.

| **Resource**                            | **Description**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| --------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| HCX Coverage Eligibility Request Bundle | <p><strong>FHIR Profile</strong>: <a href="https://ig.hcxprotocol.io/v0.8/StructureDefinition-CoverageEligibilityRequestBundle.html">link</a></p><p><strong>structure definition</strong>: <a href="../../FHIR%20Definitions/hcx-definitions/StructureDefinition-CoverageEligibilityRequestBundle.json">CoverageEligibilityRequest Bundle</a></p>                                                                                                                                                                                                            |
| CoverageEligibilityRequest              | <p>The bundle must contain a CoverageEligibilityRequest resource.</p><p><strong>FHIR Profile</strong>: <a href="https://ig.hcxprotocol.io/v0.8/StructureDefinition-CoverageEligibilityRequest.html">link</a></p><p><strong>structure definition</strong>: <a href="../../FHIR%20Definitions/hcx-definitions/StructureDefinition-CoverageEligibilityRequest.json">CoverageEligibilityRequest</a></p>                                                                                                                                                          |
| Patient                                 | <p>The document should contain a Patient resource with minimal required information about the patient:</p><ol><li>Patient resources should mandatorily have an NDHM identifier.</li><li>Patient resources can also have a hospital Id (Medical record number).</li><li>Patient resources can also have an insurance id (PMJAY ID).</li><li>Patient resources can also have employee IDs and other business identifiers.</li></ol><p><strong>FHIR Profile</strong>: <a href="https://www.nrces.in/ndhm/fhir/r4/StructureDefinition-Patient.html">link</a></p> |
| Coverage                                | <p>The document should contain one or more Coverage resources with minimal information of the policy about which the information is requested:</p><ul><li>Coverage resources should mandatorily have an identifier for the policy ID issued by the insurer.</li></ul><p><strong>FHIR Profile</strong>: <a href="https://ig.hcxprotocol.io/v0.8/StructureDefinition-Coverage.html">link</a></p><p><strong>structure definition</strong>: <a href="../../FHIR%20Definitions/hcx-definitions/StructureDefinition-Coverage.json">Coverage</a></p>                |

#### Domain Headers:

| **Key** | **Description** |
| ------- | --------------- |
|         |                 |

## Coverage Eligibility Response

| **Resource**                             | **Description**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| ---------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| HCX Coverage Eligibility Response Bundle | <p><strong>FHIR Profile</strong>: <a href="https://ig.hcxprotocol.io/v0.8/StructureDefinition-CoverageEligibilityResponseBundle.html">link</a></p><p><strong>structure definition</strong>: <a href="../../FHIR%20Definitions/hcx-definitions/StructureDefinition-CoverageEligibilityResponseBundle.json">CoverageEligibilityResponse Bundle</a></p>                                                                                                                                                                                                                                            |
| CoverageEligibilityResponse              | <p>The document must contain a CoverageEligibilityResponse resource.</p><p><strong>FHIR Profile</strong>: <a href="https://ig.hcxprotocol.io/v0.8/StructureDefinition-CoverageEligibilityResponse.html">link</a></p><p><strong>structure definition</strong>: <a href="../../FHIR%20Definitions/hcx-definitions/StructureDefinition-CoverageEligibilityResponse.json">CoverageEligibilityResponse</a></p>                                                                                                                                                                                       |
| Coverage                                 | <p>The document should contain one or more Coverage resources with minimal information of the policy about which the information is being returned.</p><p><strong>FHIR Profile details</strong>:</p><ul><li>Coverage resources should mandatorily have an identifier for the policy ID issued by the insurer.</li></ul><p><strong>FHIR Profile</strong>: <a href="https://ig.hcxprotocol.io/v0.8/StructureDefinition-Coverage.html">link</a></p><p><strong>structure definition</strong>: <a href="../../FHIR%20Definitions/hcx-definitions/StructureDefinition-Coverage.json">Coverage</a></p> |

The Coverage Eligibility Response should include the Insurance Plan URL as part of the domain header as described below . The URL should point to an Insurance Plan object as defined [here](./#insurance-plan).

#### Domain Headers:

| **Key**                    | **Description**                                                                                                                   |
| -------------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| x-hcx-insurance\_plan\_url | Url to the InsurancePlan object with the details on benefits, required documents and other important information to submit claims |

## Claim Request

Claim object is used by providers to submit pre-determination, pre-authorization and claim requests to the payers. The same eObject can be used for all these use cases and the usage can be differentiated by the value of “claim.use” element. The value of this element should be set as "**predetermination**" for Pre-Determination requests, “**preauthorization**” for Pre-Authorization requests and as “**claim**” for Claim requests.

| **Resource**             | **Description**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| ------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| HCX Claim Request Bundle | <p><strong>FHIR Profile</strong>: <a href="https://ig.hcxprotocol.io/v0.8/StructureDefinition-ClaimRequestBundle.html">link</a></p><p><strong>structure definition</strong>: <a href="../../FHIR%20Definitions/hcx-definitions/StructureDefinition-ClaimRequestBundle.json">ClaimRequest Bundle</a></p>                                                                                                                                                                                                                                                                            |
| Claim                    | <p>The document must contain a Claim resource.</p><p><strong>FHIR Profile</strong>: <a href="https://ig.hcxprotocol.io/v0.8/StructureDefinition-Claim.html">link</a></p><p><strong>structure definition</strong>: <a href="../../FHIR%20Definitions/hcx-definitions/StructureDefinition-Claim.json">Claim</a></p>                                                                                                                                                                                                                                                                  |
| Coverage                 | <p>The document may contain one or more Coverage resources with minimal information on the policy for which the claim is being raised.</p><p><strong>FHIR Profile details</strong>:</p><ul><li>Coverage resources should mandatorily have an identifier for the policy ID issued by the insurer.</li></ul><p><strong>FHIR Profile</strong>: <a href="https://ig.hcxprotocol.io/v0.8/StructureDefinition-Coverage.html">link</a></p><p><strong>structure definition</strong>: <a href="../../FHIR%20Definitions/hcx-definitions/StructureDefinition-Coverage.json">Coverage</a></p> |
| Encounter                | <p>Details of the Encounters during which this Claim was created or to which the creation of this Claim is associated.</p><p><strong>FHIR Profile</strong>: <a href="https://www.nrces.in/ndhm/fhir/r4/StructureDefinition-Encounter.html">link</a></p>                                                                                                                                                                                                                                                                                                                            |
| Condition                | <p>Details of the health conditions relevant to this Claim request.</p><p><strong>FHIR Profile</strong>: <a href="https://www.nrces.in/ndhm/fhir/r4/StructureDefinition-Condition.html">link</a></p>                                                                                                                                                                                                                                                                                                                                                                               |

#### Domain Headers:

| **Key** | **Description** |
| ------- | --------------- |
|         |                 |

## Claim Response

ClaimResponse object is used by payers to send the response for pre-determination, pre-authorization and claim requests to the providers. The same eObject can be used for all these use cases and the usage can be differentiated by the value of “ClaimResponse.use” element. The value of this element should be set as "**predetermination**" for Pre-Determination requests, “**preauthorization**” for Pre-Authorization responses and as “**claim**” for Claim responses.

| **Resource**              | **Description**                                                                                                                                                                                                                                                                                                                                   |
| ------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| HCX Claim Response Bundle | <p><strong>FHIR Profile</strong>: <a href="https://ig.hcxprotocol.io/v0.8/StructureDefinition-ClaimResponseBundle.html">link</a></p><p><strong>structure definition</strong>: <a href="../../FHIR%20Definitions/hcx-definitions/StructureDefinition-ClaimResponseBundle.json">ClaimResponse Bundle</a></p>                                        |
| ClaimResponse             | <p>The document must contain a ClaimResponse resource.</p><p><strong>FHIR Profile</strong>: <a href="https://ig.hcxprotocol.io/v0.8/StructureDefinition-ClaimResponse.html">link</a></p><p><strong>structure definition</strong>: <a href="../../FHIR%20Definitions/hcx-definitions/StructureDefinition-ClaimResponse.json">ClaimResponse</a></p> |

#### Domain Headers:

| **Key** | **Description** |
| ------- | --------------- |
|         |                 |

## Payment Notice

| **Resource**          | **Description**                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| --------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| PaymentNotice         | <p>The document must contain a PaymentNotice resource.</p><p><strong>FHIR Profile</strong>: <a href="https://ig.hcxprotocol.io/v0.8/StructureDefinition-PaymentNotice.html">link</a></p><p><strong>structure definition</strong>: <a href="../../FHIR%20Definitions/hcx-definitions/StructureDefinition-PaymentNotice.json">PaymentNotice</a></p>                                                                                                     |
| PaymentReconciliation | <p>The document should contain a PaymentReconciliation resource with information about the payment related to this payment notice.</p><p><strong>FHIR Profile</strong>: <a href="https://ig.hcxprotocol.io/v0.8/StructureDefinition-PaymentReconciliation.html">link</a></p><p><strong>structure definition</strong>: <a href="../../FHIR%20Definitions/hcx-definitions/StructureDefinition-PaymentReconciliation.json">PaymentReconciliation</a></p> |

#### Domain Headers:

| **Key** | **Description** |
| ------- | --------------- |
|         |                 |

## Insurance Plan

The Insurance Plan object helps in determining the benefits of the plan (not the policy specific to the subscriber which is present in the Coverage object), but more generic information about the plan/product. It also contains the documents required, questionnaires to answer and any important information necessary for a successful preauthorization/claim submission, with an objective to reduce the claim submission errors. It may also help in rendering the claim creation UI on the provider side by allowing to filter/view only the necessary options in stages. More details about it can be found in the Policy Markup Language [section](../domain-specific-languages-dsls.md).

This object covers the following aspects of an insurance plan:

| Resource                 | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| ------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| InsurancePlan            | <p>InsurancePlan basic plan details required for administrative purposes:</p><ul><li>Most of the basic details like name, IRDA UIN as identifier, validity, etc.. are covered in InsurancePlan profile.</li><li>InsurancePlan.plan.specificCost is used to describe the individual benefits that are covered under the plan. A benefit could be expressed against a procedure, a package (in the context of Indian Health Insurance industry), a diagnosis, a physical good or a service. For each benefit, the cost and the count upto which the benefit would be reimbursed could be specified.</li></ul><p><strong>FHIR Profile:</strong> <a href="https://ig.hcxprotocol.io/v0.8/StructureDefinition-HCXInsurancePlan.html">link</a></p><p><strong>structure definition</strong>: <a href="../../FHIR%20Definitions/hcx-definitions/StructureDefinition-HCXInsurancePlan.json">Insurance Plan</a></p> |
| HCXDiagnosticDocuments   | <p>The documents required to submit at predetermination, preauthorization and/or claim stage.</p><p><strong>FHIR Profile:</strong> <a href="https://ig.hcxprotocol.io/v0.8/StructureDefinition-HCXDiagnosticDocumentsExtension.html">link</a><br><strong>structure definition</strong>: <a href="../../FHIR%20Definitions/hcx-definitions/StructureDefinition-HCXDiagnosticDocumentsExtension.json">Diagnostic Documents Extension</a></p>                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| ProofOfIdentityDocuments | <p>The proof of identity requirements prior to the predeteermination, preauthorization and/or claim stage.</p><p><strong>FHIR Profile:</strong> <a href="https://ig.hcxprotocol.io/v0.8/StructureDefinition-HCXProofOfIdentificationExtension.html">link</a><br><strong>structure definition</strong>: <a href="../../FHIR%20Definitions/hcx-definitions/StructureDefinition-HCXProofOfIdentificationExtension.json">Proof Of Identification Extension</a></p>                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| ProofOfPresenceDocuments | <p>The proof of presence requirements prior to the predeteermination, preauthorization and/or claim stage.</p><p><strong>FHIR Profile:</strong> <a href="https://ig.hcxprotocol.io/v0.8/StructureDefinition-HCXProofOfPresenceExtension.html">link</a><br><strong>structure definition</strong>: <a href="../../FHIR%20Definitions/hcx-definitions/StructureDefinition-HCXProofOfPresenceExtension.json">Proof Of Presence Extension</a></p>                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| Questionnaires           | <p>The questionnaires required to be answered and submitted along with a predeteermination, preauthorization and/or a claim request.</p><p><strong>FHIR Profile:</strong> <a href="https://ig.hcxprotocol.io/v0.8/StructureDefinition-HCXQuestionnairesExtension.html">link</a><br><strong>structure definition</strong>: <a href="../../FHIR%20Definitions/hcx-definitions/StructureDefinition-HCXQuestionnairesExtension.json">Questionnaires Extension</a></p>                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| InformationalMessages    | <p>The informational and compliance messages that the provider should be aware of, prior to the predetermination, preauthorization or claim request.</p><p><strong>FHIR Profile:</strong> <a href="https://ig.hcxprotocol.io/v0.8/StructureDefinition-HCXInformationalMessagesExtension.html">link</a><br><strong>structure definition</strong>: <a href="../../FHIR%20Definitions/hcx-definitions/StructureDefinition-HCXInformationalMessagesExtension.json">Informational Messages Extension</a></p>                                                                                                                                                                                                                                                                                                                                                                                                   |

## Communication Request

The FHIR resource CommunicationRequest is used by payors to send a communication request to providers requesting additional information about a predetermination, preauthorization or a claim request. In future, this object may be used for other communication purposes also.

| Resource             | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| -------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| CommunicationRequest | <p>This resource is a record of a request for a communication to be performed. It shall contain the following details:</p><ul><li><strong>about</strong> - reference to the predetermination, preauthorization or claim request for which the communication request is created</li><li><strong>payload</strong> - text, attachments or resources to be communicated to the recipient of the communication request</li></ul><p><strong>FHIR Profile</strong>: <a href="https://ig.hcxprotocol.io/v0.8/StructureDefinition-CommunicationRequest.html">link</a></p><p><strong>structure definition</strong>: <a href="../../FHIR%20Definitions/hcx-definitions/StructureDefinition-CommunicationRequest.json">link</a></p> |

## Communication

The FHIR resource "HCX Communication Bundle" is used by providers to respond to the communication requests sent to them. Communication is a conveyance of information from one entity, a sender, to another entity, a receiver.

| Resource                 | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| ------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| HCX Communication Bundle | <p><strong>type</strong>: should be a code representing Communication document type.</p><p><strong>section</strong>: The document shall have one section with a single entry having reference to Communication resource.<br><strong>FHIR Profile</strong>: <a href="https://ig.hcxprotocol.io/v0.8/StructureDefinition-CommunicationBundle.html">link</a><br><strong>structure definition</strong>: <a href="../../FHIR%20Definitions/hcx-definitions/StructureDefinition-CommunicationBundle.json">Communication Bundle</a></p>                                                                                                                                                                                                                     |
| Communication            | <p>The bundle must contain a Communication resource which is a record of a communication even if it is planned or has failed. It shall contain the following details:</p><ul><li><strong>about</strong> - reference to the predetermination, preauthorization or claim request for which the communication is being sent</li><li><strong>payload</strong> - text, attachments or resources to be communicated to the recipient of the communication</li></ul><p><strong>FHIR Profile</strong>: <a href="https://ig.hcxprotocol.io/v0.8/StructureDefinition-Communication.html">link</a></p><p><strong>structure definition</strong>: <a href="../../FHIR%20Definitions/hcx-definitions/StructureDefinition-Communication.json">Communication</a></p> |

## Task

The Task object is used for capturing activities that can be performed and for tracking the completion of the activity. In this version of the specification, the Task object is intended to be used for providers to do a status check of requests submitted by them and for the payors to respond with the status details. FHIR also recommends the usage of Task FHIR resource for status requests & responses ([link](https://hl7.org/fhir/R4/financial-module.html#order)).

| Resource | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| -------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Task     | <p>Task object is used as the payload in status request and response APIs. The object shall have the following details:</p><ul><li><strong>code</strong> - specifies the nature of the task, i.e. status check</li><li><strong>focus</strong> - specifies the context identifiers (e.g case-id for a registered pre-auth, claim id of the provider TMS)</li><li><strong>input</strong> - additional information about the context that may be needed in the execution of the task. e.g.: type of entity - preauthorization or claim, etc</li><li><strong>output</strong> - carries the result of a status request. The result is the status code reflecting the status of the corresponding request (CoverageEligibilityCheck, PreAuthorization, Claim, etc..). The valueSets for the status codes must be the same as specified in the corresponding response FHIR profiles</li></ul><p><strong>FHIR Profile</strong>: <a href="https://ig.hcxprotocol.io/v0.8/StructureDefinition-Task.html">link</a></p><p><strong>structure definition</strong>: <a href="../../FHIR%20Definitions/hcx-definitions/StructureDefinition-Task.json">Task</a></p> |
