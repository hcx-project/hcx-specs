---
description: Recommendations for onboarding onto live network
---

# ✨ Production onboarding (Go live)

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

    <table data-header-hidden><thead><tr><th width="139.66666666666669">Actor</th><th width="122">HCX Role</th><th>Applicable verification details</th></tr></thead><tbody><tr><td>Payers</td><td>Payer</td><td><p>Verification Details:</p><ol><li>Letter from authorized signatory of the company seeking participation</li><li>IRDA registration Number/license number,</li><li>IRDA User ID</li><li>Registered email id,</li><li>System admin details for OTP authentication</li></ol></td></tr><tr><td>State schemes</td><td>agency.sponsor</td><td><p>Verification Details:</p><ol><li>Government licence/approval letter</li><li>Letter from authorized signatory of the company seeking participation</li><li>Registered email id,</li><li>System admin details for OTP authentication</li></ol></td></tr><tr><td>Corporates paying for their employees</td><td>agency.sponsor</td><td><p>Verification Details:</p><ol><li>Letter from authorized signatory of the company seeking participation</li><li>Registered email id,</li><li>System admin details for OTP authentication</li></ol></td></tr><tr><td>TPAs</td><td>agency.tpa</td><td><p>Verification Details:</p><ol><li>Letter from authorized signatory of the company seeking participation</li><li>IRDA registration Number/license number,</li><li>IRDA User ID</li><li>Registered email id</li><li>System admin details for OTP authentication</li></ol></td></tr><tr><td>HIUs (like TSPs, ISNPs) and other user intermediaries</td><td>member.isnp</td><td><p>Verification Details:</p><ol><li>Letter from authorized signatory of the company seeking participation</li><li>Registered email id,</li><li>System admin details for OTP authentication</li><li>IRDA registration Number/license number (if applicable)</li><li>IRDA User ID (if applicable)</li></ol></td></tr><tr><td>ABDM enrolled Providers</td><td>provider (provider.hospital, provider.clinic, provider.practitioner, provider.diagnostics, provider.pharmacy)</td><td><p>Verification Details:</p><ol><li>HFR ID &#x26; Role/type</li><li>Verification status,</li><li>Registered manager’s HFR ID, mobile number &#x26; email ID as per HFR for OTP based authentication and intimation about the HCX onboarding attempt for approval</li><li>An automated lookup API to check the authenticity and availability of the HFR ID in the ABDM registry</li><li>Fetch api with consent from the facility manager to pull facility details from HFR</li><li>ABDM credentials (API based check) via HFR and HPR integration</li><li>For facilities - HFR ID &#x26; OTP auth can work</li><li>For doctors and other health professionals HPR ID with OTP auth or API check can work</li></ol></td></tr><tr><td>Non ABDM enrolled Providers with ROHINI Id</td><td>provider (provider.hospital, provider.clinic, provider.practitioner, provider.diagnostics, provider.pharmacy)</td><td><p>Verification Details:</p><ol><li>Facility details- Name, License , validity, GSTN etc</li><li>ROHINI ID</li><li><strong>Mechanism to verify</strong> the submitted details with ROHINI database (lookup or manual verification by ROHINI admin)</li></ol></td></tr><tr><td>Non ABDM enrolled Providers with no ROHINI id</td><td>provider (provider.hospital, provider.clinic, provider.practitioner, provider.diagnostics, provider.pharmacy)</td><td><p><strong>Facility is empanelled with a Government/public health scheme but is neither registered in HFR nor ROHINI</strong> </p><p></p><p>Verification Details:</p><ol><li>Facility details - Name, License, facility manager details, location address</li><li>Payer ID/Name/name of the scheme that has empanelled the registering provider (This will trigger approval email/notification to the scheme authority/state authority/payer to verify if the requesting facility is empanelled with them or not</li><li>Empanelment proof - Either a copy of physical proofs such as Empanelment ID, attachment of signed contract with the said payer/scheme details, latest transaction with the said payer/scheme, contract validity &#x26; status, or a digitally signed proof from the payer/scheme. </li></ol></td></tr><tr><td>Regulators like IRDA, NHA, IIB or state regulators</td><td>agency.regulator</td><td><strong>Will be worked on a case to case basis based on need.</strong></td></tr><tr><td>Beneficiary facing platforms </td><td>BSP</td><td><p>Considering that BSPs' onboarding primarily revolves around compliance with HCX specifications (with data security and privacy aspects covered by protocol measures as mentioned in the note below), a simple onboarding process is recommended to facilitate and encourage participation from these beneficiary-facing entities. </p><p></p><p>Verification details: </p><ol><li>Name</li><li>Email</li><li>Mobile no.</li><li>GSTN</li><li>Registered Address proof</li><li>Stakeholder serviced (Policyholder for now)</li><li>Compliance certification from the sandbox environment</li></ol></td></tr></tbody></table>

{% hint style="info" %}
**Addressing data privacy and security on BSP platforms** - The HCX protocol necessiate that user/citizen-facing platforms can only assume BSP role with the explicit consent of the beneficiary. The protocol specifies following mechanism and event points for seeking consent:

1. Consent requirement for tracking the claims - Please see “Subscription Mechanism” section under [Workflow notification](../../hcx-technical-specifications/open-protocol/key-components-building-blocks/exchange-protocol/notification-specs-proposal/categories.md#workflow-notification).&#x20;
2. OPD reimbursement proposed workflow section [here](broken-reference). &#x20;
3. IPD reimbursement proposed section workflow [here](broken-reference).
{% endhint %}

#### **Step 3: Gather HCX related details**

In this step, the operator gathers more details of the participant including contact numbers, company registration details, and other details as needed in the HCX registry.

#### **Step 4: Provisioning of production credentials**

Once these requirements are met, the participant id along with the production access secret credentials will be provided. Participants are expected to keep the secret credentials safe and report any compromises at the earliest to the HCX operators.

#### **Step 4: Go-Live**

The application is now expected to be prepared for go-live in respective participant ends. All the participants are advised to plan the change management at their end and conduct necessary training for their staff before going live in production HCX, preferably after piloting with a small set of clients.
