---
description: Process of onboarding network participants
---

# Guidelines for Participant Onboarding

While the actual onboarding/deboarding process for an HCX ecosystem would be drafted by its operator and agreed upon by its participants, this section outlines key design guidelines and an overall approach to arrive at such a policy.

### Key design considerations  <a href="#key-design-considerations" id="key-design-considerations"></a>

Building further from the key design considerations laid out for business policies in the HCX open specifications, the onboarding approach should:

1. Aim to enable rather than control the participation of the interested ecosystem actors.
2. Require minimal and necessary information, enough to prove the identity of the participant and enable working of the network. The process requirements should be non-discriminatory and at the same time requrie enough detail to keep out any frivolous organizations.
3. Needs to be simple and cost effective enough to encourage participation of entities working with low income segments.

A list of different kinds of participants who would need onboarding into an HCX registry is provided in the [Access Control](https://docs.swasth.app/enhancements-policy-guidelines-group-phase-1/9EKhP0MBRjkQ0mAd1A3W/healthcare-operations-policies/access-control-roles) section above. Onboarding onto the HCX is envisioned as a two step process:

1. Sandbox - for compliance testing and certification
2. Go Live on live instances

Diagrams below depicts the key steps in onboarding process across these two phases:Proposed onbaording process flowSections below provide high level description for each of these steps:

<figure><img src="https://lh6.googleusercontent.com/xa8Y0i1jVYqAgiYbWVjO6WhzY0wB-h9-8g1_JV3QN27FfK7ogVSLgeelqU3AKQJ2TC_3biTUqQz98gKP0HlV6CuWPimhFhQ09WClIIytNvuDxqrYXXr_1U3CXkChFNyvefYnuBr5ie08-Mn_8wZXpHG6-32f5cWoHUH7CaeoGBTrtUMjZmmVTETAWw" alt=""><figcaption><p>Proposed onbaording process flow</p></figcaption></figure>

Sections below provide high level description for each of these steps:

### Phase 1 - Sandbox Process <a href="#phase-1-sandbox-process" id="phase-1-sandbox-process"></a>

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

### **Phase 2 - Production onboarding and go live** <a href="#phase-2-production-onboarding-and-go-live" id="phase-2-production-onboarding-and-go-live"></a>

After obtaining the affiliated sandbox certification, the participant would have to apply for onboarding into the HCX production environment. This process will consist of the following key steps:

#### **Step 1: Validate sandbox certificate**&#x20;

In this step, HCX operator validates the sandbox certificate for applicability (whether it allows for certification from the sandbox provider) and validity.

#### **Step 2: Registration on HCX**

In this step, interested participants will be required to go through the onboarding verification process with the HCX. HCX operators are expected to provide a choice of registration flows with the following high level guidelines:

1. If the participants are registered in the NDHM Health Facility registry, then they should be allowed to use HFR authentication as a means to register in the HCX registry, if they choose to do so.
2.  If the participants are not registered in the NDHM Health facility registry then the participant should be allowed to use alternate means of verification like

    1. Option to complete the NDHM HFR process and use the resultant credentials.
    2. Authentication/Certificates/documents from IRDA or equivalent such agency identified and clearly stated in HCX’s onboarding policy. Proposed list of documents/requirements needed for such an on-boarding based on type of participant are as follows:

    ​

    <table data-header-hidden><thead><tr><th width="205.66666666666669">Actor</th><th width="178">HCX Role</th><th>Applicable verification details</th></tr></thead><tbody><tr><td>Payers</td><td>Payer</td><td><p>Verification Details:</p><ol><li>Letter from authorized signatory of the company seeking participation</li><li>IRDA registration Number/license number,</li><li>IRDA User ID</li><li>Registered email id,</li><li>System admin details for OTP authentication</li></ol></td></tr><tr><td>State schemes</td><td>agency.sponsor</td><td><p>Verification Details:</p><ol><li>Government licence/approval letter</li><li>Letter from authorized signatory of the company seeking participation</li><li>Registered email id,</li><li>System admin details for OTP authentication</li></ol></td></tr><tr><td>Corporates paying for their employees</td><td>agency.sponsor</td><td><p>Verification Details:</p><ol><li>Letter from authorized signatory of the company seeking participation</li><li>Registered email id,</li><li>System admin details for OTP authentication</li></ol></td></tr><tr><td>TPAs</td><td>agency.tpa</td><td><p>Verification Details:</p><ol><li>Letter from authorized signatory of the company seeking participation</li><li>IRDA registration Number/license number,</li><li>IRDA User ID</li><li>Registered email id</li><li>System admin details for OTP authentication</li></ol></td></tr><tr><td>HIUs (like TSPs, ISNPs) and other user intermediaries</td><td>member.isnp</td><td><p>Verification Details:</p><ol><li>Letter from authorized signatory of the company seeking participation</li><li>Registered email id,</li><li>System admin details for OTP authentication</li><li>IRDA registration Number/license number (if applicable)</li><li>IRDA User ID (if applicable)</li></ol></td></tr><tr><td>ABDM enrolled Providers</td><td>provider</td><td><p>Verification Details:</p><ol><li>HFR ID &#x26; Role/type</li><li>Verification status,</li><li>Registered manager’s HFR ID, mobile number &#x26; email ID as per HFR for OTP based authentication and intimation about the HCX onboarding attempt for approval</li><li>An automated lookup API to check the authenticity and availability of the HFR ID in the ABDM registry</li><li>Fetch api with consent from the facility manager to pull facility details from HFR</li><li>ABDM credentials (API based check) via HFR and HPR integration</li><li>For facilities - HFR ID &#x26; OTP auth can work</li><li>For doctors and other health professionals HPR ID with OTP auth or API check can work</li></ol></td></tr><tr><td>Non ABDM enrolled Providers with ROHINI Id</td><td>provider</td><td><p>Verification Details:</p><ol><li>1.Facility details- Name, License , validity, GSTN etc</li><li>2.ROHINI ID</li><li>3.<strong>Mechanism to verify</strong> the submitted details with ROHINI database (lookup or manual verification by ROHINI admin)</li></ol></td></tr><tr><td>Non ABDM enrolled Providers with no ROHINI id</td><td>provider</td><td><p><strong>Facility is empanelled with a Government/public health scheme but is neither registered in HFR nor ROHINI</strong>Note-This is a special use case wherein only the public/state health scheme can verify that the requesting facility is empanalled with them and approve the onboarding​Verification Details:</p><ol><li>1.Facility details - Name, License, facility manager details, location address</li><li>2.Payer ID/Name/name of the scheme that has empanelled the registering provider (This will trigger approval email/notification to the scheme authority/state authority to verify if the requesting facility is empanelled with them or not</li><li>3.Empanelment details- Empanelment ID, attachment of signed contract with the said payer/scheme details, latest transaction with the said payer/scheme, contract validity &#x26; status</li></ol></td></tr><tr><td>Regulators like IRDA, NHA, IIB or state regulators</td><td>agency.regulator</td><td><strong>Will be worked on a case to case basis based on need.</strong></td></tr></tbody></table>



#### **Step 3: Gather HCX related details**

In this step, the operator gathers more details of the participant including contact numbers, company registration details, and other details as needed in the HCX registry.

#### **Step 4: Provisioning of production credentials**

Once these requirements are met, the participant id along with the production access secret credentials will be provided. Participants are expected to keep the secret credentials safe and report any compromises at the earliest to the HCX operators.

#### **Step 4: Go-Live**

The application is now expected to be prepared for go-live in respective participant ends. All the participants are advised to plan the change management at their end and conduct necessary training for their staff before going live in production HCX, preferably after piloting with a small set of clients.

### Envisioned Deboarding scenarios <a href="#envisioned-deboarding-scenarios" id="envisioned-deboarding-scenarios"></a>

This section lists some of the deboarding scenarios that may be considered as part of the final deboarding policies by the HCX operators:

1. Involuntary deboarding of a participant initiated by Regulator/Legal Authority. Few examples:
   1. Suspension/Deactivation of a provider by a regulator for fraudulent activity.
   2. Suspension/Deactivation of a TPA or a Payer by IRDA
2. Involuntary deboarding of a participant (mostly TSPs) initiated by HCX. Few cases:
   1. Serious violation of HCX policies (e.g. grave SLA violation repeatedly)
   2. Hacking attempts made by participants for unauthorized access, after an investigation by HCX
   3. Bad or irresponsible behaviour from participants if it significantly impacts the stability and performance of the HCX (like frequent bursts of requests beyond authorised rate limits).
3. Voluntary deboarding of participants. Few examples:
   1. A provider or payer shifting to another HCX
   2. A provider or payer shuts down their business
   3. A provider or payer merges with another entity listed on the exchange

Please note that while the above list suggests a few of the scenarios for potential deboarding of a participant, this process should be treated with utmost care and an elaborate warning mechanism should be kept in place whenever the deboarding is not voluntary.

In addition, to provide a fair chance of appeal, the grievance redressal process on HCX is expected to provide grievance mechanisms to handle appeal against deboarding of a participant.

#### Next Steps <a href="#next-steps" id="next-steps"></a>

Building on the earlier work on these guidelines, this section now provides recommended approach for HCX onbaording. In future there may be further work on:

1. Inclusion of new type of members in HCX network and their respective verification processes.
2. Evolution of verification process for curently defined participants
3. Recommendations on ways to automate and simplify the onbaording process\
