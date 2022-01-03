# Domain Data Specifications

The most significant aspect of domain specification would be agreement on formats for data exchange and terminologies (taxonomies) being used in those data models. These would mainly include:

1. **Domain data model** - Schema definition of domain entities like Claims, Providers, Payors, Policies, etc. Please note that based on available DSLs some of these data models may be flexible, e.g. policy schema if Policy Markup Language (PML) is available.
2. **Metadata specifications -** Metadata is data about data, data associated with an object, a document, or a dataset for purposes of description, administration, technical functionality, and preservation. For the context of claims, this would mainly involve coding systems and suggested values for key claim attributes like disease codes, procedure codes, diagnostic codes, billing-related codes (e.g. room rent, ICU charges, etc.), etc.
3. **Domain Specific Language(s)** - Usually known as DSL, these may be developed When the attributes of the entity are variable from use case to use case but need to adhere to some common constraints/characteristics like types of data element it can contain, the relationship between two data elements, number of occurrences of data elements, etc. Examples of such entities within a claims data exchange would be policies, bills, contracts. In such cases, defining a markup language (DSL) rather than the entity itself allows needed flexibility to the ecosystem to innovate on such entities. These can be thought of like HTML, where multiple flavours of web pages can be defined using the markup elements.

In order to achieve this, in line with the key design principles detailed in [Health Claims Data Exchange - Open Specifications](../../open-specifications/design-principles.md), following key design guidelines are proposed:

#### Key Design Considerations

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

Based on the priorities listed above and design considerations, key domain specifications included in Phase 1 are detailed in the following sub-sections.&#x20;
