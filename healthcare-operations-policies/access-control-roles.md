---
description: Roles and access control policies on Health Claims Exchange
---

# ✨ Access Control (Roles)

Participating organisations in the the Health Claims information exchange ecosystem may possess one or more of the roles mentioned below. These roles are based on the base set of organisation roles defined in hl7 specifications [here](https://www.hl7.org/fhir/valueset-organization-role.html). Namespaced coding is used to further qualify the role in the context of the claims exchange process.

{% hint style="info" %}
This section has undergone significant enhancements to accommodate the scope and the requirements of [OPD and Reimbursement use cases](../use-cases/), and streamlining action categories for clarity. The key changes include:&#x20;

1. **Expansion of Provider Roles:** The Provider role has been expanded to explicitly encompass hospitals, clinics, practitioners, diagnostics, and pharmacies, aligning with the needs of OPD use cases. This expansion serves several vital purposes:&#x20;
   1. **Tailored Onboarding**: Separating provider roles enables the possibility of tailored onboarding processes unique to each role. This approach fosters deeper trust in the participants joining the network.
   2. **Adjudication Flexibility**: The differentiation of roles allows for the application of distinct sets of adjudication rules based on provider and claim types, offering more precise control and compliance.
   3. **Enhanced Visibility and Analytics**: This separation provides a more granular view of network activities, thereby improving analytics and insights into the network's operations.
2. **Introduction of the BSP Role:** A new role, BSP (Beneficiary Service Platform), has been introduced to accommodate digital platforms dedicated to assisting beneficiaries. This addition reflects the evolving landscape of healthcare services and ensures that the protocol remains adaptable to emerging beneficiary support systems.&#x20;
3. **Categorisation of Actions into Access-Groups:** To simplify the understanding of API usage on the HCX network, actions have been grouped into categories.&#x20;
{% endhint %}

1. **provider -** Health Service Provider (An entity that delivers care services) roles as below
   1. **provider.hospital** - Organised hospitals. &#x20;
   2. **provider.clinic** - Independent clinics/ small care setups.
   3. **provider.practitioner** - Individual practitioners. &#x20;
   4. **provider.diagnostics** - Diagnostic testing/laboratory services.
   5. **provider.pharmacy** - Pharmacies and drug stores.
2. **payer -** Insurance service provider, an entity providing reimbursement, payment, or related services.
3. **agency.tpa -** Third party administrator, entity acting on behalf of the payer. In the current version, this role is expected to behave like a payer from the data exchange perspective.
4. **agency.regulator -** IRDAI and IIB like regulatory bodies.
5. **research -** Research groups, etc.
6. **member.isnp -** eCommerce platforms facilitating insurance adoption.
7. **agency.sponsor -** Scheme owners of specific programs, e.g. NHA for. Ayushman Bharat.
8. **HIE/HIO.HCX -** An entity that facilitates electronic clinical data exchange between entities, e.g. other HCXs.
9. **BSP -** Beneficiary Service Platform, digital platforms dedicated to assisting beneficiaries.

Initial recommendations about onboarding policies of the new roles is included in the [Guidelines for Participant Onboarding](participant-onboarding/) section.&#x20;

### Access Groups

To streamline the existing method of delineating access rights for various roles in HCX, we present the following essential access groups:

#### **Claim Initiators**

These roles are responsible for initiating claims on behalf of policyholders, including **providers** and **BSPs**. The table below enumerates the key APIs that are initiated and responded to by these roles.

| APIs initiated             | Apis responded         |
| -------------------------- | ---------------------- |
| /coverageeligibility/check | /communication/request |
| /preauth/submit            | /paymentnotice/request |
| /predetermination/submit   | <p><br></p>            |
| /claim/submit              | <p><br></p>            |
| /hcx/status                | <p><br></p>            |
| /notification              | <p><br></p>            |
| /registry/search           | <p><br></p>            |

#### **Claim Responders**

These roles encompass entities that receive and process claims, such as payers and TPAs. The table below enumerates the key APIs that are initiated and responded to by these roles.

| APIs initiated                 | APIs responded             |
| ------------------------------ | -------------------------- |
| /coverageeligibility/on\_check | /coverageeligibility/check |
| /preauth/on\_submit            | /preauth/submit            |
| /predetermination/on\_submit   | /predetermination/submit   |
| /claim/on\_submit              | /claim/submit              |
| /communication/request         | /hcx/status                |
| /paymentnotice/request         | <p>/eob/fetch<br></p>      |
| /hcx/on\_status                | <p><br></p>                |
| /notification                  | <p><br></p>                |
| /registry/search               | <p><br></p>                |

#### **Claim Observers**

These roles, while not directly engaged in claim processing, monitor claims for various purposes. This category includes regulators, observers, sponsors, and more. The table below enumerates the key APIs that are initiated and responded to by these roles.

| APIs initiated | APIs responded |
| -------------- | -------------- |
| /eob/fetch     | <p><br></p>    |
| /notification  | <p><br></p>    |

