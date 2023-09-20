# Domain Specific Languages (DSLs)

There are two key DSLs being considered for the Health Claims Exchange - Policy Markup Language (PML) and Bill Markup Language (BML). These are currently work in progress and are expected to be released in the later version of HCX specifications after substantial proof of concept development with various members of domain working groups.

## Policy Markup Language (PML)

As indicated in the previous version of the protocol, policy markup language was being envisioned by the working groups to provide a digital encoding mechanism to payers such that the policies can be encoded in machine readable format, thereby helping with the accurate communication of plan details to various ecosystem actors that could help with use cases like:

1. Intuitive UIs for provider/TPAs to help patients navigate policy information
2. Allow providers to validate their submissions and help reduce multiple roundtrip for a valid claim submission
3. Potential automation of coverage eligibility checks
4. Automation of claim submission and adjudication processes, etc.

In earlier discussions, PML was being thought of as a single DSL to express Insurance Plans (products) and Policies/rules around these plans. However, further analysis with various groups suggested that needs from PML can be unbundled into the following keys asks:

1. Plan/Product details - Publically shareable generic details of plan e.g. procedures covered, limits etc. that are not specific to a subscriber.
2. Constraints (including pre-submission validations) - Key constraints on various plan elements. These may include:
   1. Document checklist against procedure/package
   2. Informational/compliance messages against procedure/package
   3. Procedure specific questionnaires
   4. Requirements for Proof of identification and Proof of Presence
   5. Inclusion/exclusion constraints.
3. Routing information - Information of where to send claims related to the plan and details of various processing stages/entities if a plan supports multi party processing

This version of the protocol has focused on digitally encoding the Insurance Plan (usually called Product) by the payers. In order to keep it consistent with rest of the domain specifications, protocol proposes to use a combination of FHIR resources and FHIR DSLs to express plans (#1 above) and most prevalent constraints (a large part of #2 above).

The policies that are derived from the products specific to the individual or a group, would be planned in the future versions. Insurance Plan information is expected to be available publicly as it is not specific to any subscriber or group.

The [FHIR InsurancePlan profile with some extensions](https://ig.hcxprotocol.io/v0.9/StructureDefinition-HCXInsurancePlan.html) are used to encode the above and covers the following key aspects:

1. The basic plan details required for admistrative purposes - Most of the basic details like name, IRDA UIN as identifier, validity, etc.. are covered in InsurancePlan profile.
2. The benefits that are covered under the plan - The InsurancePlan.plan.specificCost is used to describe the individual benefits. A benefit could be expressed against a procedure, a package (in the context of Indian Health Insurance industry), a diagnosis, a physical good or a service. For each benefit, the cost and the count upto which the benefit would be reimbursed could be specified.
3. The documents required to submit at preauthorization and/or claim stage - An [extension](https://ig.hcxprotocol.io/v0.9/StructureDefinition-HCXDiagnosticDocumentsExtension.html) has been provided to describe the documents that are required as part of the preauthorization or claim submission.
4. The proof of presence and identity requirements prior to the preauthorization and/or claim stage - The extensions for the inclusion of proof of identity [here](https://ig.hcxprotocol.io/v0.9/StructureDefinition-HCXProofOfIdentificationExtension.html) and proof of presence [here](https://ig.hcxprotocol.io/v0.9/StructureDefinition-HCXProofOfPresenceExtension.html) are provided. In this version, the list of the documents could be described. The rules on top of these would included in a later version of the protocol.
5. The questionnaires required to be answered and submitted along with a preauthorization and/or a claim request - [Questionnaire Extension](https://ig.hcxprotocol.io/v0.9/StructureDefinition-HCXQuestionnairesExtension.html)
6. The informational and compliance messages that the provider should be aware of, prior to the preauthorization or claim request - [InformationalMessages Extension](https://ig.hcxprotocol.io/v0.9/StructureDefinition-HCXInformationalMessagesExtension.html)
7. The inclusion and exclusion constraints against a particular benefit or a group of benefits (Not covered in this version)
8. The routing information to determine the right recipient for a claim (Not covered in this version)

An [example](../FHIR%20Definitions/examples/insurancePlan1.json) InsurancePlan object is provided for reference. The digital encoding of policies and adjudication rules would be discussed in the later versions of the protocol.

## Bill markup Language

After analysis needs from the Bill Markup Language and further deliberation from phase 1 work, [Claims profile/eObject](domain-data-models/#claim-request) adopted from HL7 FHIR financial module is considered good enough to hold the needed bill related information, thereby eliminating the need for a separate markup language.
