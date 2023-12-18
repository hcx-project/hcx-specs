---
description: Technology backbone for the Health Claims Data Exchange
---

# Open Protocol

As described in Key Specifications, Open protocol defines the technology backbone for the Health Claims Data Exchange. In order to fulfil architectural principles listed [here](https://hcxprotocol.io/governance/), the protocol needs to consider the following key design elements:

## Key Design Considerations

* The protocol must be designed to support the asynchronous exchange of information to support the scale and asynchronous nature of processes in the industry
* The protocol must support the federated deployment of multiple HCX instances.
* In order to ensure the security and privacy of sensitive data
  * The protocol must allow for separation of transport (and any other common information) from sensitive information in the respective flows
  * The protocol must provide for encryption, signing, and auditing of relevant information
* The protocol should allow creating unique identifiers for each message exchange
* The protocol should allow related multiple messages that are part of a single business flow
* The protocol should allow using existing registries for key entities - beneficiary, provider, and payor with a facility to extend them for the specific use case
* The protocol should be designed to allow for the inclusion of the new types of use cases
* The protocol should be designed to allow extending a use case as per the need of the use case/program (for example, a particular government scheme or innovative health financing solution may need different information about the beneficiary, provider, or intervention)

Based on these principles and design considerations, subsections below define the following key elements of the proposed Open Protocol:

1. Registries - Definition of key registries needed for the functioning of the exchange.
2. Health Claims data Exchange (HCX) Protocol - Details of the exchange flows including terminologies used, key constructs, message structures, unbundled APIs and error handling.
3. Data Privacy and Security - Details of key security features of the protocol.
4. Audit and Reporting

Following sub-section provides details on the HCX registries and different participant registries.
