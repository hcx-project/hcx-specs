---
description: Code sets or domain metadata standards
---

# Terminologies

To achieve semantic interoperability, it is recommended that HCX data standards incorporate well established and suitable terminology and coding systems.

In various HL7 standards (including FHIR), these are expressed as Concepts and codes and forms essential vocabulary, ontological binding for resources used to describe document types/categories, element codes and clinical coding like procedure codes, diagnosis codes etc. The data standards defined using FHIR resources and types usually will require agreement on references and usages, through agreed Code Systems and codes, typically manifested through ValueSets.

## Guidelines

* For Clinical resources (e.g. Condition, Procedure, Observations) - please refer to the guidance issued by NRCeS.
  * In India, SNOMED-CT is free for use by all as Clinical Terminology, while ICD codes are used for classifications.
  * Labs typically use LOINC codes
* For other code/concepts in the FHIR based data standards, we would recommend guidelines as per [FHIR Terminology binding strength definitions (Section 4.1.5)](https://www.hl7.org/fhir/terminologies.html).
  * If any attributes are marked as “required” - then, use of the codes defined in the value sets
  * If it is marked as “preferred” or “extensible” - then, users are encouraged to draw from the specified codes for interoperability purposes, unless deemed appropriate within the affinity domain.
  * If marked as “example” - then the domain must agree and define a value set for usage.
  * ValueSet may be created derived from existing sets, either composed/included from the base or expanded.
* For insurance claim domain specific element attributes (e.g. Claim.type) - the domain may define and establish value sets, as suitable in India’s context.

For the broader NDHM interoperability and conformance, HCX would align with domain specific guidelines published by NRCeS.

The code systems/valuesets proposed by the HCX working groups are published as part of the [HCX FHIR Implementation Guide](https://ig.hcxprotocol.io/v0.9/valuesets.html). The IG and the code systems/valuesets are versioned and published independently of the HCX protocol.

HCX switch provider or neutral protocol supporting organisations may host domain specific FHIR Terminology Services which the ecosystem can leverage to retrieve information and use, and validate resources as defined by the IG.
