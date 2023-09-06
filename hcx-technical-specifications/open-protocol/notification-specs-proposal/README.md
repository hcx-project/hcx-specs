---
description: Specifications to enable participant notifications
---

# Notifications

### Context <a href="#_9wme70gzafwp" id="_9wme70gzafwp"></a>

As a facilitator of the value between various participating entities, while HCX is envisioned to help different participants directly exchange the claims related information in standardised manner, the network would benefit further if the relevant information about such exchanges could also be shared with other interested/relevant participating entities in a safe and secure manner. Example of such information could be onboarding/deboarding of participants, information about participant system maintenance/upgrades, availability of new functionality, or specific information needed by a participant on a particular claims use case - e.g. Regulator (IRDA/IIB) or Sponser (NHA/SHA/Corporate/Community) needing to know about completion of a claims cycle, or an ISNP needing to know status of a claim on behalf of its patient.

Key benefits of such a notification infrastructure would be:

1. Operational efficiency
2. Transparency
3. Trust in ecosystem
4. Better user experience
5. Improved support and risk mitigation

This section of the specification describes such needs and proposed enhancements to facilitate such information exchange in the network.

### Abstract <a href="#_lz5afctazyhj" id="_lz5afctazyhj"></a>

Event driven notification can enable valuable near real time information for the HCX network participants in a privacy preserving and secure manner. This proposal outlays the enhancements in the protocol to detail the approach and proposed APIs and data structures to achieve such notification capabilities. Key capabilities proposed to be included are:

1. Classification of key notification types
2. Notification templates/data structure
3. Notification registry (a set of predefined notifications mapped with access control)
4. Subscribe/Unsubscribe APIs
5. Notify APIs
6. Guidelines for policies related to notification capabilities

As part of the overall HCX specifications, the Notification delivery specifications are designed keeping in mind the [overall HCX design principles](broken-reference).

