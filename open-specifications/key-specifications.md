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

#### Domain Data Specifications

Specifications about format and definition of domain data. A lot of these may be adopted from existing domain standards like FHIR, SNOMED, ICD-10-PCS. In the context of claims data exchange few key focus areas will be:

1. **Domain data model** - Schema definition of domain entities like Claims, Providers, Payors, Policies, etc. Please note that based on available DSLs some of these data models may be flexible, e.g. policy schema if Policy Markup Language (PML) is available.
2. **Metadata specifications -** Metadata is data about data, data associated with an object, a document, or a dataset for purposes of description, administration, technical functionality, and preservation. For the context of claims, this would mainly involve coding systems and suggested values for key claim attributes like disease codes, procedure codes, diagnostic codes, billing codes (e.g. room rent, ICU charges), etc.
3. **Domain-Specific Language(s)** - Usually known as DSL, these may be developed When the attributes of the entity are variable from use case to use case but need to adhere to some common constraints/characteristics like types of data element it can contain, the relationship between two data elements, number of occurrences of data elements, etc. Examples of such entities within a claims data exchange would be policies, bills, contracts. In such cases, defining a markup language (DSL) rather than the entity itself allows needed flexibility to the ecosystem to innovate on such entities. These can be thought of like HTML, where multiple flavours of web pages can be defined using the markup elements.

#### Business Policy Specifications

A thriving data exchange will also require clear rules of engagement to ensure trust from all actors. These specifications will involve guidelines around:

1. Access control (Data sharing) policies - which actor plays what role and gets to see which parts of the data. These policies will then affect the visibility and access to domain-specific attributes that will typically travel in the body of the data structures defined by the data exchange.
2. Business SLAs
3. Charges/Fees - these would be policies around charges various data exchange entities will be allowed to levy on others depending on the role they play
4. Dispute resolution policies
5. Onboarding
6. Defaulting/deboarding policies
7. Service rating policies - that would be the parameters and mechanisms to rate each type of actor on the data exchange.
