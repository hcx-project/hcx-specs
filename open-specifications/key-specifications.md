---
description: List of key types of specifications needed for Health Claims Data Exchange
---

# Key Specifications

#### Open protocol for claims data exchange - Health Claims Transfer Protocol

Like HTTP or SMTP, open protocol for claims exchange will define the following key aspects:

1. Authentication (Payor, Provider, Regulator, Observer, ...)
2. Request/response message syntax - header and header attributes, optional body, mandatory vs optional, transport constraint on the messages, etc.
3. Supported methods (APIs)
4. Communication mode (synchronous or asynchronous nature of APIs)
5. Response codes
6. Data security and privacy considerations: Security, authenticity, and non-repudiability aspects of message exchange
   1. Encryption of certain parts of message for transport security (beyond SSL on Health Claims data exchange)
   2. Message signing protocol for verifiability and non-repudiation
7. Sequence of interactions

#### Tech Ops Policy Specifications

These will include the following policies for participation in the health claims data exchange:

1. Onboarding policies - How does any entity get on board on the data exchange? Adherence to protocol, the process for a compliance review, frequency of compliance review, etc
2. Deboarding policies: What makes an entity to be blocked or ejected from the data exchange. Things like adherence to technical SLAs, non-compliance with expected protocol versions, message security or privacy violations, etc.
3. Access control policies - Role-based, need for consent to access APIs, data attributes, etc.
4. Exchange operation policies
   1. Key rotation requirements
   2. Segregation of duties and responsibilities within various teams of exchange operators
   3. Operational reports and dashboards
   4. Audit checklist and frequency

#### Domain Specifications

Specifications about format and definition of domain specific elements. A lot of these may be adopted from existing domain standards like FHIR, SNOMED, ICD-10-PCS. In the context of claims data exchange few key focus areas will be:

1. **Domain data model** - Schema definition of domain entities like Coverage Eligibility, Claims, Providers, Payers, Policies, etc. [FHIR specifications](https://hl7.org/fhir/overview.html) from HL7 have been adopted by the HCX community to define domain entities.
2. **Metadata specifications** - Metadata is data that describes data, data associated with an object, a document, or a dataset for the purposes of description, administration, technical functionality, and preservation. In the context of claims, this would mainly involve coding systems and value sets for key claim attributes, such as disease codes, procedure codes, diagnostic codes, billing codes (product or service e.g. room rent, ICU charges), etc.
3. **Domain-Specific Language(s)** - These may be developed when the attributes of the entity are different from use case to use case, but they need to follow some common rules/characteristics, like the types of data elements it can have. It essentially helps define the needed Data Models in a particular domain. The HCX community has investigated and found that combination and extension of the FHIR resources suffices for the currently envisioned use cases, and therefore has not felt a need to define any DSL as of now. The DSL option is included here as a possible option if a need ever arises for future use cases.&#x20;

#### Business Policy Specifications

A thriving data exchange will also require clear rules of engagement to ensure trust from all actors. These specifications will involve guidelines around:

1. Data sharing policies (implemented through Access control) - which actor plays what role and gets to see which parts of the data. These policies will then affect the visibility and access to domain-specific attributes that will typically travel in the body of the data structures defined by the data exchange.
2. Business SLAs
3. Charges/Fees - these would be policies around charges various data exchange entities will be allowed to levy on others depending on the role they play
4. Dispute resolution policies
5. Onboarding
6. Defaulting/deboarding policies
7. Service rating policies - that would be the parameters and mechanisms to rate each type of actor on the data exchange.
