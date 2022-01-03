---
description: Introduction to Health Claims Data Exchange
---

# Introduction to HCX

The Health Claims data Exchange can be envisioned as analogous to the internet in general and email exchange networks more specifically, where data packets travel to and fro between an origin and the destination. In this context, Health Claims Data Exchanges can be thought of as routing switches or email gateways that facilitate communication with the desired level of consistency, security, privacy, and durability. However, unlike the internet or email, this protocol is defined for a specialized use case of exchanging claims-related information between relevant actors - payors, providers, beneficiaries, regulators, observers.

The figure below shows a simple depiction of a health claims network facilitated by an HCX instance:

![](<.gitbook/assets/HCX Diagram-2.png>)

### Vision, Mission, and Objectives

1. Expand Insurance Penetration
   1. Significantly lower cost of claims processing implies new use cases – such as OPD and Pharmacy
   2. New kinds of payors in the market that can lead to an increase in insured base
   3. Reduce receivable cycles and increase acceptance of cashless claims (even in smaller hospitals)
2. Facilitate insurance innovation
   1. Highly personalized policies
   2. Short duration, low premium policies
   3. Auto adjudication, better fraud, and abuse prevention
3. Simplify and bring efficiency to claims processing
   1. Standardized claims process, less operational overheads
   2. Increase trust among payers and providers through a transparent, rule-based mechanism
4. Better patient experience

### Key Use cases/Workflows

In its initial version, HCN is focused on facilitating message exchange for the cashless claims process and envisions to facilitate the following information flows:

1. Get provider/payor details
2. Eligibility check
3. Pre auth request flow
4. Claims request flow
5. Payment notification
6. Payment acknowledgement&#x20;
7. Search/fetch claims data for status checks, regulatory compliance, etc.

### Key constituents

The claims network will consist of the following key building blocks:

1. **Specifications** - this layer defines the blueprint for different aspects of the claims network. These include communication protocols, data packet specifications, Taxonomies, privacy and security specifications, network policies (onboarding and deboarding rules), business rules, operational specifications, etc. Please note that the document intentionally calls these artifacts as specifications to indicate that they become standards only after a “de jure” or “de facto” adoption by the ecosystem.
2. **Reference Health Claims Exchange (aka switch) software** - A reference gateway implementation build as per the standards defined above. The main goal here will be to provide fundamental software building blocks of the network to enable faster adoption by the ecosystem.
3. **Compliance sandbox** - Implemented using the above reference software, the key goal of the sandbox will be to help the ecosystem test its specific components against the network standards defined above and get certified to become part of the network.
4. **Health Claim Platform runtime(s)** - Operating instances of the health claims platform that enable real-world claims interactions on the network. Like with the internet and email example, there can be multiple such running instances that are expected to be interoperable by adhering to the standards defined as in #1 above.
5. **Participating platforms** - These are digital systems of the network participants (Payors, Providers, Regulators, Observers, etc) that sit on the edges of the claims network and initiate/receive the communication happening through the network. These would be analogous to client/servers in the internet analogy and various email service providers in the email analogy.

The following sections describe the key aspects of the proposed open specifications including design principles, a list of key specifications, proposed governance and details of technology and domain specifications work completed so far.&#x20;

## Questions for Consultation

#### Question 1

HCX specifications could enable the existence of multiple HCX instances and relays between them (please see example flow [here](hcx-technical-specifications/appendix-a-hcx-relay-example.md)). What challenges do you foresee in both scenarios - single HCX for all stakeholders v/s multiple connected HCXs? What would be your criteria to choose one scenario over the other?&#x20;

{% hint style="info" %}
Instructions to send responses to the consultation questions are available [here](how-to-submit-responses.md).
{% endhint %}
