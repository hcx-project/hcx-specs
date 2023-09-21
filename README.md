---
description: Current status and enhancements from previous version
---

# ✨ Summary

Inspired by the recommendations of the Joint Working Group of NHA and IRDAI (2019), Health Claims Data Exchange (HCX) is an ambitious open source project that aims to define interoperable protocol specifications to enable a multi-party exchange of health claims information.

The HCX switches can be thought of as routing switches or email gateways that facilitate communication with the desired level of consistency, security, privacy, and durability. However, unlike the internet or email, this protocol is defined for a specialized use case of exchanging health claims (or benefits) related information between relevant actors - payors, providers, beneficiaries, regulators, observers, etc.

### Version Information

Version - 0.9-draft | Release date - September, 2023 | Published documentation [link](https://docs.hcxprotocol.io/v/v0.9/) | Github [link](https://github.com/hcx-project/hcx-specs/tree/v0.9) | Protocol [website](https://hcxprotocol.io)

{% hint style="info" %}
**Important Note:** The version of the HCX Protocol documentation currently published is a draft and is subject to revisions and updates as we engage in the public consultation process. The sections that have significant changes since previous version (v0.8) are marked with a ✨ icon[^1].&#x20;

Please be aware that this version is comprehensive and self-contained, making it [**suitable for use independently**](#user-content-fn-2)[^2]. Furthermore, there are **no identified backward compatibility breaking changes** from the previous version.

We value your feedback and encourage you to participate in shaping the final version of the protocol. Your insights and contributions are essential to ensure the protocol's effectiveness and alignment with ecosystem needs.&#x20;

**To provide feedback or suggestions:** Please use information provided in "[Contributing to the protocol](how-to-submit-responses.md)" reach out or contribute to the protocol.&#x20;
{% endhint %}

#### Summary[^3] of changes (Changelog):

* Relocated the design principles and proposed governance approach from the specification documentation to the HCX protocol [website](https://hcxprotocol.io/governance/).
* Introduced additional methods for managing attachments using Document Management Systems (DMS) in [handling attachment](hcx-domain-specifications/domain-data-models/handling-attachments.md) section.
* Updates to the [user registry schema](hcx-technical-specifications/open-protocol/registries.md#user-registry) definitions for multi-tenancy, allowing for distinct user roles within a tenant.
* Introduced "[Use Cases](use-cases/)" section to list various use cases (Cashless/Reimbursement and IPD/OPD), their mapping with the HCX protocol and important implementation considerations.
* In the process of mapping Cashless and Reimbursement use cases, both for Inpatient (IPD) and Outpatient (OPD) treatments, the following protocol enhancements have been incorporated:
  * [Access control](healthcare-operations-policies/access-control-roles.md):
    * Additional participant roles are added to enable appropriate access control levels.
    * Defined [Access Groups](healthcare-operations-policies/access-control-roles.md#access-groups) to simplify access mapping to roles.
  * [Guidelines for Participant onboarding](healthcare-operations-policies/participant-onboarding/):  &#x20;
    * Restructured the section into multiple subpages for enhancing the readability&#x20;
    * [Production Onboarding](healthcare-operations-policies/participant-onboarding/production-onboarding-go-live.md):&#x20;
      * Include recommendations on BSP verification
      * Enhanced recommendations for "Non ABDM enrolled Providers with no ROHINI id" to  encompass verification through both public and private payers.
  * [Recommended Communication request/response flow](use-cases/reimbursement/implementation-considerations.md) for seeking patients consent verification token when submitting reimbursement claims through a TSP/ISNP platform.
  * Following valueset have been enhanced in the [Implementation Guide](hcx-domain-specifications/implementation-guide.md)
    * Communication Reason Codes - Enhanced to facilitate the sharing of patient consent and account information in reimbursement claims.
    * [Claim Supporting Info Codes](https://ig.hcxprotocol.io/v0.9/ValueSet-claim-supporting-info-codes.html) - Added new codes for bills/receipts associated with a claim, covering items such as medicines, lab tests, medical services, and more.
    * [Claim Denial Codes](https://ig.hcxprotocol.io/v0.9/ValueSet-claim-denial-codes.html) - Introduced codes to address claim denials resulting from policyholder consent declines or missing consent in reimbursement claims.

{% hint style="warning" %}
**Open Items**:&#x20;

Addressing open comments/feedback by the domain working group in [GitHub discussion #113](https://github.com/hcx-project/hcx-specs/discussions/113).
{% endhint %}

### Previous Versions

The following table provides a summary of the existing specification versions and links to the respective documentation.

| Version details                                                                                                                                                                                                                                                                                                                             | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Version - 0.8 \| Release date - April, 2023 \| Published documentation [link](https://docs.hcxprotocol.io/v/v0.8-draft/) \| Github [link](https://github.com/hcx-project/hcx-specs/tree/v0.8)                                                                                                                                               | <p></p><p></p><p>The 0.8 version of HCX specifications has been developed based on inputs and feedback from the HCX community and in accordance with the planned roadmap. This version includes several key enhancements:</p><ul><li>Notifications capability which allows for the sharing of important updates regarding the network, participants, and workflows with various entities.</li><li>Information Fetch API has been introduced to facilitate the sharing of information with authorized third parties.</li><li>API security enhancements have been made, which will allow for the generation of password-based API tokens.</li><li>Based on the business policy working group's recommendations, following enhancements have been made in the business policy specifications: improvements in onboarding and grievance redressal, as well as the inclusion of guidelines on SLAs, participant satisfaction, and operating charges.</li><li>Access control roles have been redefined to support the specification improvements and new use cases.</li></ul>      |
| Version - 0.7.1 \| Release date - February, 2023 \| Published documentation [link](https://docs.hcxprotocol.io/v/v0.7.1/) \| Github [link](https://github.com/hcx-project/hcx-specs/tree/v0.7.1)                                                                                                                                            | <p>After consulting with NRCes, the FHIR community, and the HCX community, this version of specification incorporates a significant simplification by changing the bundle type from "document" to "collection." This new structure effectively reduces the overhead associated with the "document" bundle type and supports cycle-specific constraints on the bundles, making the integration process much more straightforward for integrators.</p><p></p><p>Some of the significant advantages of using the "collection" bundle type include simplifying programming for bundle parsing and verification, eliminating extraneous details such as the signature, and reducing the payload size.</p><p></p><p>In summary, this new bundle type significantly streamlines the integration process and reduces unnecessary complexities, ultimately improving the overall experience for all parties involved.</p>                                                                                                                                                             |
| Version - 0.7 (Draft) \| Release date - January, 2022 \| Published documentation [link](https://docs.hcxprotocol.io/v/v0.7-draft/) \| Github [link](https://github.com/Swasth-Digital-Health-Foundation/hcx-specs/tree/v0.7)                                                                                                                | <p>Based on feedback from various ecosystem players on the baseline version and rigorous feasibility analysis with the NHA team on the adoption of the specifications in public scheme use cases, this version includes the following key enhancements over the baseline version:</p><ul><li>Multi-party processing support through REDIRECT and FORWARD constructs</li><li>Initial support for digital encoding of policies using InsurancePlan FHIR profile</li><li>New APIs to support pre-determination cycle</li><li>Introduction of communication APIs to support additional information exchange during various claim cycles - pre-determination, pre-auth, or claims.</li><li>Introduction of status API to support fetching of the status of a submitted request</li><li>Search API definition deferred to future version to allow further deliberation</li><li>Simplification of Protocol Headers - identifiers and status</li><li>Standardisation of protocol errors</li><li>Restructuring, examples, and language modifications to enhance readability</li></ul> |
| Version - 0.6 (Baseline) \| Release date - September 08, 2021 \| Published documentation [link](https://docs.swasth.app/hcx-specifications/) \| Github [link](https://github.com/Swasth-Digital-Health-Foundation/hcx-specs) \| Consultation questions [link](https://docs.hcxprotocol.io/v/v0.6/how-to-submit-responses#list-of-questions) | Base version of specifications. It was built by 60+ volunteers from across the healthcare ecosystem (including Insurers, Hospitals, TPAs, Insurance Technology players and Think tanks) as a part of a transparent, collaborative and open effort during July 2020-September 2021 and launched for public consultation on September 08, 2021. You can find the launch details and list of volunteers [here](https://hcx.swasth.app).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |

[^1]: 

[^2]: 

[^3]: 
