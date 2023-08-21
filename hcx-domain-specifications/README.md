---
description: >-
  Domain data specifications and business policies to implement health claims
  data exchange
---

# Domain Specifications

This section focuses on **domain** **specifications** needed to realize the health claims data exchange. As detailed in the [key specification](../open-specifications/key-specifications.md) section, the most significant aspect of domain specification would be agreement on formats for data exchange (data models and any domain specific languages to assist standardisation) and terminologies (taxonomies) being used in those data models.

In order to achieve this, in line with the key design principles detailed in [Health Claims Data Exchange - Open Specifications](../open-specifications/design-principles.md), the following key design guidelines are proposed for domain specifications:

## Key Design Considerations

1. Data specifications should be broken down to simpler fundamental units as far as possible.
2. In order to leverage existing knowledge and resources and provide wider interoperability, data specifications should extend/ reuse/ adopt international/ national models wherever available/applicable. In order to follow this in claims context, data specification should leverage resources as follows:
   * Leverage HL7/FHIR R4 specifications wherever possible
   * Leverage NRCES FHIR specifications where base FHIR specs need contextualization to the Indian context
   * Create minimal extensions needed in case both base FHIR and NRCES specs are not enough to support the use case
   * FHIR Document profiles appropriate for the protocol should be created composed of base FHIR resources
3. Data specifications should be created with the principle of minimalism and inclusivity. In order to achieve this:
   * Specs should permissive cardinalities as much as possible. E.g. they should require minimal mandatory fields to enable maximal inclusion. As a thumb rule, wherever unsure of the cardinality of an attribute, the most permissible one should be used.
   * Specs should use permissive terminologies/code binding strength as much as possible. E.g. in the [FHIR terminology construct](https://www.hl7.org/fhir/terminologies.html) (Section 4.1.5), if there’s a conflict in choosing between “extensible” and “preferred” strengths for a coding system, “preferred” should be chosen.
4. Data specifications should be extensible i.e. they should allow a way to capture extra information that was not initially included during the model design. To achieve this:
   * It may provide a simple map of key-value pairs. Future versions of the data model may choose to create mandatory/optional names attributes in the data models after researching the wider applicability of such fields.
   * Data specifications should allow for namespacing in field names to indicate the source/reason/category of the extended fields.
5. It is recommended that all timestamps be captured in ISO-8601 format e.g. 2020-08-15T17:02:53.495+05:30. APIs may define display format property to indicate the human-readable format most suitable for display.

Based on these principles and design considerations, subsections below define the following key elements of the proposed domain specifications:

1. Domain Data Models
2. Terminologies (Code sets and Metadata standards)
3. Domain Specific Languages (DSLs)

Details of Open Protocol and TechOps policies are covered in the [previous section](../hcx-technical-specifications/), and the details of Business Policy Specifications are covered in the subsequent section.
