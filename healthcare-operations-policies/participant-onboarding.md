# Guidelines for Participant Onboarding

While the actual onboarding/deboarding process for an HCX ecosystem would be drafted by its operator and agreed upon by its participants, this section outlines key design guidelines and an overall approach to arrive at such a policy.

A list of different kinds of participants who would need onboarding into an HCX registry is provided in the [Access Control](access-control-roles.md) section above. Onboarding onto the HCX is envisioned as a two step process:

1. Sandbox - for compliance testing and certification
2. Go Live on live instances

Sections below provide high level guidelines for each of these steps.

#### Sandbox Process

The key goal of the sandbox is to help the ecosystem test its specific components against the communication standards, and get certified to become a part of the system. Once a participant successfully completes the sandbox process, they can use the certification to get onboarded to the HCX production environment with the necessary access.

HCX operator(s) may nominate or list Sandbox operator(s) whose certification will be considered valid for onboarding to their platforms.

The following are the steps to integrate, test and launch with the help of sandbox.

Step 1: Registration

The participants submit an online application to express their interest to access the HCX sandbox. The requests from different participants are verified to see if the participant is eligible to participate in the sandbox environment by doing basic checks against the details provided in the application form. Details of the model application form for various roles will be developed in the upcoming phase of the specifications.

There may be requests that would not satisfy the conditions required for the sandbox access such as multiple requests from the same participant, participants not registered with any registry, TSPs without a valid website, spam applications, etc., which would prove to be redundant and may have to be filtered. This process would be semi-manual.

On successful verification, the approved participants are added to the HCX sandbox and provisioned with the necessary credentials to access the sandbox environment.

Step 2: API integration and testing

In this step, the participants integrate their respective claim processing applications with the sandbox HCX. This is to aid the developments as well as ensure that their applications are compliant with the HCX standards and build all the missing pieces on their side to use the set of HCX APIs necessary for their planned workflows.

Sandbox website would also include documentation and suggestions regarding the software libraries, tools and example implementations for encryption, FHIR resource generation, code generation and other new/complex parts of the HCX protocol. The sandbox portal would ensure that the participants are provided with all the necessary help to get started and complete the API integration.

Step 3: Sandbox certification

All participants are expected to fulfil a set of functional and security tests/flows applicable to them.

Based on affiliate HCX policies, the sandbox may necessitate additional security testing and reviews like STQC or CERT-IN. Suggestive pointers on infrastructural requirements for security testing clearance can be found in this [document](https://sandbox.ndhm.gov.in/documents/NDHM\_Secure\_Application\_Development-Reference\_Document.pdf).

Once the system is ready and tested against the applicable test cases, the participant will be required to submit their test results including the application's usage of and interaction with HCX APIs to the Sandbox Operator for review and approval.

On successful review, the sandbox will issue a successful completion certificate valid for a configured period of time. This certificate can be used by the participant to get onboarded to the production environments of the HCX operators.

#### Go Live process

After obtaining the affiliated sandbox certification, the participant would have to apply for onboarding into the HCX production environment. This process will consist of the following key steps:

Step 1: Registration on HCX

In this step, interested participants will be required to go through the onboarding process with the HCX. HCX operators are expected to provide a choice of registration flows with the following high level guidelines:

1. If the participants are registered in the NDHM Health Facility registry, then they should be allowed to use HFR authentication as a means to register in the HCX registry, if they choose to do so.
2. If the participants are not registered in the NDHM Health facility registry then the participant should be allowed to use alternate means of verification like
   1. Option to complete the NDHM HFR process and use the resultant credentials.
   2. Authentication/Certificates/documents from IRDA or equivalent such agency identified and clearly stated in HCX’s onboarding policy.
3. Summary details of the HCX application duly filled. This application form will be more detailed, requiring more details of the participant including contact numbers, company registration details, and other details as needed in the HCX registry.

Step 2: Review of Sandbox certification

A final round of approval for application go-live will be sought from the internal team at HCX. Applicants will be required to share Functional and security testing certificates issued by the affiliate sandbox environment.

Step 3: Provisioning of production credentials

Once these requirements are met, the participant id along with the production access secret credentials will be provided. Participants are expected to keep the secret credentials safe and report any compromises at the earliest to the HCX operators.

Step 4: Go-Live

The application is now expected to be prepared for go-live in respective participant ends. All the participants are advised to plan the change management at their end and conduct necessary training for their staff before going live in production HCX, preferably after piloting with a small set of clients.

#### Deboarding scenarios

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

#### Next Steps

This section proposes a high-level approach that can be adopted for onboarding/deboarding policies for an HCX ecosystem. More deliberation is needed to arrive at model policies that can then be readily extended to be adopted by the ecosystem. Domain working groups will continue to work on developing a detailed approach for onboarding/deboarding policy formulation as well as a model policy for easy adoption. These documents will be released for public consultation in time for an initial pilot of the HCX ecosystem.
