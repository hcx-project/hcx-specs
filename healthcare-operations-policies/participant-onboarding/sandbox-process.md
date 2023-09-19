---
description: Phase 1 of the participant onboarding
---

# Sandbox process

The key goal of the sandbox is to help the participants test their software against the HCX protocol, and get certified to ensure interoperability and gain required trust by the other network participants.

All participants including the HCX instance(s) and its participants are expected to go through certifications to ensure adherence/compliance to the specifications. However, as indicated later, the mode of compliance may vary based on the role of the participant. Compliance step would include:

1. Technical Compliance checks - API schema conformance, Security specification (Transport layer, API security, Message security) conformance
2. Domain Compliance checks - Payload schema conformance, Terminology compliance, Publication of extended terminologies
3. Process Compliance checks - Adherence to strategy/ approach/ guidelines/ recommendations on business policies

Sandbox testing environment shall publish a set of test cases (test suite) for each type/role of the participant (payer, provider, etc.). It will require applicants to send a series of messages as defined in the test cases to the Sandbox. The system will analyze the messages received and mark the test as pass or fail as per the requirement of the test case. The sandbox system will provide a list of all messages and their testing status.

The Sandbox environment(s) shall also include documentation and suggestions regarding the software libraries, tools and example implementations for encryption, FHIR resource generation, code generation and other new/complex parts of the HCX protocol. The sandbox portal would ensure that the participants are provided with all the necessary help to get started and complete the API integration.

Based on affiliate HCX policies, the sandbox may necessitate additional security testing and reviews like STQC or CERT-IN. Suggestive pointers on infrastructural requirements for security testing clearance can be found in [this document](https://sandbox.ndhm.gov.in/documents/NDHM\_Secure\_Application\_Development-Reference\_Document.pdf).&#x20;

Key steps for sandbox certification process would be:

#### **Step 1: Sandbox Registration**&#x20;

The participants submit an online application to express their interest to access the chosen HCX sandbox. Sandbox registration/verification process is expected to be simpler than the production process to encourage newer ecosystem actors to try the benefits of the network.

#### **Step 2: Provisioning of sandbox credentials**&#x20;

Once sandbox registration requirements are met, the participant id along with the sandbox access secret credentials will be provided. Participants are expected to keep the secret credentials safe and report any compromises at the earliest to the Sandbox operator.

#### **Step 3: Mock API integration and testing**&#x20;

In this step, the participants integrate their respective claim processing platform applications with the sandbox HCX. This step could be done by software providers on behalf of their customers. This is a one time event/requirement from the solution provider, once they have tested and certified on the sandbox, the same solution can be utilized by multiple payers/providers willing to utilize HCX services.

#### **Step 4: Test result review (tech, Domain, Process compliance)**&#x20;

In this step, the sandbox provider reviews the results of respective test cases and provides necessary feedback to the participant till the compliance is achieved.

#### **Step 5 : Security Certification/Proof submission**&#x20;

Since HCX design principles demand complete security and privacy of the data exchanged safeguarding the personal information of the beneficiaries, it is critical to assess the security & privacy measures a solution provider has implemented. For this, the solution provider either can get a security compliance certificate from an entity like STQC or any other authorized SIs. The solution provider will be required to submit the certificate as a proof to the HCS operator sandbox committee to get a go ahead on access to the production APIs.

#### **Step 6: Sandbox certification**&#x20;

On successful review, the sandbox will issue a successful completion certificate valid for a configured period of time. This certificate can be used by the participant to get onboarded to the production environments of the HCX operators.​

Once a participant successfully completes the sandbox process, they can use the certification to get onboarded to the HCX production environment and production access keys will be shared with the solution provider that can be used to integrate with the production APIs.

{% hint style="info" %}
HCX operator(s) may nominate or list Sandbox operator(s) whose certification will be considered valid for onboarding to their platforms.
{% endhint %}
