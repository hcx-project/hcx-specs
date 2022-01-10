# Terminologies (Code sets or Metadata standards)

To achieve semantic interoperability, it is recommended that HCX data standards incorporate well established and suitable terminology and coding systems.

In various HL7 standards (including FHIR), these are expressed as Concepts and codes and forms essential vocabulary, ontological binding for resources used to describe document types/categories, element codes and clinical coding like procedure codes, diagnosis codes etc. The data standards defined using FHIR resources and types usually will require agreement on references and usages, through agreed Code Systems and codes, typically manifested through ValueSets.

## Guidelines

* For Clinical resources (e.g. Condition, Procedure, Observations) - please refer to the guidance issued by NRCeS.
  * In India, SNOMED-CT is free for use by all as Clinical Terminology, while ICD codes are used for classifications.
  * Labs typically use LOINC codes
* For other code/concepts in the FHIR based data standards, we would recommend guidelines
  * If any attributes are marked as “required” - then, use of the codes defined in the value sets
  * If it is marked as “preferred” or “extensible” - then, users are encouraged to draw from the specified codes for interoperability purposes, unless deemed appropriate within the affinity domain.
  * If marked as “example” - then the domain must agree and define a value set for usage.
  * ValueSet may be created derived from existing sets, either composed/included from the base or expanded.
* For insurance claim domain specific element attributes (e.g. Claim.type) - the domain may define and establish value sets, as suitable in India’s context.

For the broader NDHM interoperability and conformance, HCX would align/inherit domain specific guidelines.

The table below lists the code systems/value sets proposed by current domain working groups. Based on the above guidelines, we are proposing them to be “preferred” or “example” binding strengths as per [FHIR Terminology binding strength definitions (Section 4.1.5)](https://www.hl7.org/fhir/terminologies.html).

| **Terminology name**                                                       | **FHIR Value Set link**                                                                                                | **Proposed Binding Strength** |
| -------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------- | ----------------------------- |
| <p>Insurance Company Owners</p><p>(coverageeligibilityrequest.insurer)</p> | [link](https://swasth-digital-health-foundation.github.io/standards/output/ValueSet-insurance-company-owners.html)     | Preferred                     |
| <p>Procedure Type</p><p>(claim.procedure.type)</p>                         | [link](https://swasth-digital-health-foundation.github.io/standards/output/ValueSet-procedure-type-description.html)   | Example                       |
| <p>Procedure Code</p><p>(claim.procedure.procedureCode)</p>                | [link](https://icd.who.int/browse10/2010/en)                                                                           | Example                       |
| Denial Codes (claimresponse.item.adjudication.reason)                      | [link](https://swasth-digital-health-foundation.github.io/standards/output/ValueSet-claim-denial-codes.html)           | Preferred                     |
| <p>Procedure Modifiers</p><p>(claim.item.modifier)</p>                     | TODO                                                                                                                   | Example                       |
| <p>Service Categories</p><p>(claim.item.category)</p>                      | [link](https://swasth-digital-health-foundation.github.io/standards/output/ValueSet-claim-service-categories.html)     | Example                       |
| <p>Service Codes</p><p>(claim.item.productOrService)</p>                   | TODO                                                                                                                   | Preferred                     |
| <p>Medical Speciality Type</p><p>(practitionerRole.speciality)</p>         | [link](https://swasth-digital-health-foundation.github.io/standards/output/ValueSet-medical-specialty-provider.html)   | Preferred                     |
| <p>Health Service Provider role</p><p>(claim.careTeam.role)</p>            | [link](https://swasth-digital-health-foundation.github.io/standards/output/ValueSet-health-service-provider-role.html) | Example                       |

HCX or a neutral protocol supporting organisation will host domain specific FHIR Terminology Services which the ecosystem can leverage to retrieve information and use, and validate resources as defined by the IG.



## Questions for Consultation

#### Question 1

During multiple discussions with the ecosystem, it has been suggested that while the specifications suggest recommended terminologies, they are not yet mandated (hence the low binding strength's against each terminology). Kindly provide your view on mandatory standardisation of terminologies and approaches to enable your suggestions.&#x20;

#### Question 2

In your view, what clinical terminologies and codes (e.g SNOMED-CT, ICD-10, LOINC) be considered? In addition, are you aware of any well established and accepted codes/value sets available that can be applicable to the Indian scenario? Kindly provide details.&#x20;

{% hint style="info" %}
Instructions to send responses to the consultation questions are available [here](../../how-to-submit-responses.md).
{% endhint %}
