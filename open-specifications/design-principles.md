---
description: Key design principles for Open Specifications
---

# Design Principles

Specifications are fundamental to the success of the envisioned claims data exchange. In order to ensure that they can act as this common foundation, this section proposes design principles for the open specifications in line with basic principles outlined in the [National Digital Health Blueprint](https://main.mohfw.gov.in/sites/default/files/Final%20NDHB%20report\_0.pdf).

#### Open

Specifications must be designed to be open to support technology and promote vendor neutrality. They must be published under the most unrestricted license (_Creative Commons or MIT license_) as applicable to enable wider ecosystem participation and foster innovation through extensibility. Being open also helps leverage wider ecosystem expertise at the time of designing and evolving the specifications.

#### Evolvable and Extendable

They must be designed to be evolvable over a period of time thereby helping adapt to changing needs. By being extendable they provide ecosystems with the capability to leverage these specifications for their context while maintaining interoperability.

#### Interoperability

Given that the key role of HCX specifications is to create and enhance interoperability between diverse ecosystem participants, any feature added to the specification must ensure that it increases interoperability between implementations.

#### Minimalistic and Inclusive

Minimalism is crucial to ensuring that specifications enable and do not restrict innovation or inclusion. In order to be inclusive while maintaining minimalism, before including any new feature/enhancements in the specification, proposers and reviewers should ask the following questions: _1. Do we need it?_ and, _2. Do we need it now?_ If the answer to both these questions is “_**Yes**_” then that feature may be included in the specification.

#### Unification over standardisation

There would be situations when not all the features or requirements of the specifications may be standardised (at least in near term), and may vary with context and ground realities. In such cases, the goal of specification should be to prioritise and harmonize those requirements/features such that there is an integrated set of requirements/features all stakeholders can agree with or at least accept. For example, insurance product-and-services value-set may be defined differently for different contexts (social vs private), then the specification should allow for the ecosystem to use any of these definitions based on context, and allow for the standardisation to happen as a natural consequence of ecosystem adoption rather than a forced adoption.

#### Balance data privacy and security with data empowerment

They must provide for the mechanisms to keep the data secure (e.g. mandating SSL for data in transit, requiring relevant data to be encrypted) and private (e.g. consent-based data access) while still allowing for mechanisms to exchange needed information between trusted parties.

#### Provide for non-repudiability

They must provide mechanisms to view and verify attribute trails - who accessed or updated what and when - through mechanisms like digital signatures and tamper-proof audit trails.

#### Unbundled

They should strive to break down the complexity of the domain into multiple simple pieces thereby resulting in multiple simple specifications which can be bundled in a modular manner to suit the needed context and help solve dynamic challenges.
