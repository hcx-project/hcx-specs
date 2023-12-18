---
description: Categories of notifications in HCX
---

# Categories

### Categories of notifications <a href="#_j3k234ghi2oh" id="_j3k234ghi2oh"></a>

Categorisation of notifications is important from the point of view of data security/privacy and reducing information load on the receivers. It is proposed to classify the HCX Notifications based on the **subject of the notification** as follows:

![](<../../../.gitbook/assets/0 (1)>)

#### **Network notifications**

**Broadcast network notifications**

These notifications are expected to carry information about the activities in the network and would be of interest to multiple (if not all) participants in the network. Key use cases for these types of notifications would be:

1. Onboarding of new participants
2. Deboarding of an existing participants
3. Change in network capabilities
   1. Support for new features (either through protocol upgrade or extended features)
   2. End of life for an existing capability
4. Change in network policies like terms of services, SLAs, grievance policies, etc.
5. Switch/Network maintenance and downtime related notifications

![](<../../../.gitbook/assets/1 (1)>)

Such notifications will be triggered by the HCX switch operator and will be broadcasted to all participating entities on the network. In the initial version of the protocol, it is proposed that participants will be auto-subscribed to these notifications at the time of onboarding and are not given a facility to block or unsubscribe from such notifications.

**Targeted network notifications**

In addition, there's a special category of network notifications that would be targeted at the specified participants in the network. K ey use for such notifications would be:

1. Compliance expiry (re-compliance needed)
2. Encryption key expiration
3. SLA threshold breach, etc.

![](<../../../.gitbook/assets/2 (1)>)

Thes notifications will be triggered by the HCX switch operator and will be directed to the concerned entities on the network. In the initial version of the protocol, it is proposed that participants will be auto-subscribed to these notifications at the time of onboarding and will not be given a facility to block or unsubscribe from such notifications.

#### **Participant Notifications**

**Broadcast Participant notifications:**

These notifications are expected to carry participant system related public information that may be helpful for other participants in efficient operations and processing of the claims related information. They would be of interest to multiple (if not all) participants in the network. Key use cases for these types of notifications would be:

1. System maintenance and downtime updates
2. Change in system capabilities :
   1. Support for new version of protocol
   2. Support for prescribed terminologies
   3. End of life for an existing capability (usually as part of protocol upgrades)
   4. New insurance plans/products, end of support for existing products/plans
3. Policy Compliance changes - terms of services, SLAs, grievance policy etc.

![](<../../../.gitbook/assets/3 (1)>)

Such notifications will be triggered by the network participants and would be expected to be broadcasted to all entities on the network. HCX operators may choose to by default subscribe all onboarding entities to such notifications and provide the facility to unsubscribe from such notifications.

It is recommended that subscribe/unsubscribe facility is made available for the combination of sender and specific topic to allow for granular subscription and avoiding spams.

#### **Workflow Notification:**

**Public Information carrying Workflow Notifications**

These notifications are expected to carry use case/workflow related information to a third party participant who is not directly participating in the data exchange process. These are expected to be targeted to a set of identified recipients who have expressed explicit interest in observing such workflow events and are assigned the needed role on the network.

Important: Please note that these categories of notification are not designed to carry information about an identified beneficiary, rather general status of any workflow/cycles to interested participants.

Key use cases for these kind of notifications would be:

1. Updates about initiation, closure or change in status of claims cycle: Regulators like IIB needing the information about processed claims at the completion of a claim cycle or; a state or private sponsor needing to know the initiation and closure of claims, etc.
2. Updates about claims for a particular disease type: Surveillance notification to indicate workflow related to a particular clinical type.

![](<../../../.gitbook/assets/4 (1)>)

Such notifications would be expected to be explicitly subscribed to, and may or may not be granted access based on the network’s policy. Subscription to such notifications will depend on the role of the participating entity and approval/acceptance from the intended sender participant but do not require explicit consent from the patient as they will not be carrying any PII of the patients.

Notification Trigger and Delivery Mechanism:

These type of notification can be triggered in two ways:

1. **Mechanism 1:** Notification triggered by the initiating participant using the trigger APIs and delivered by the HCX to the subscribed receiving participant.
2. **Mechanism 2:** If the trigger information is available to the HCX switch as part of the protocol header, the sending participant may choose to delegate the triggering to the HCX on its behalf.

**PII carrying workflow notification:**

These notifications are a special use case of workflow notifications, and are expected to carry PII information about an identified beneficiary to a third party participant who is not directly participating in the data exchange process, e.g. HIUs (ISNP, Regulator, etc). These are expected to be targeted and to be delivered only to the intended subscribers.

Key use cases for these kind of notifications would be:

1. Notifications about claims, reimbursements,etc. of a patient to an HIU
2. Notifications about change in coverage eligibility, etc.

Subscription to such notifications will depend on the role of the participating entity and will require explicit consent from the patient. Given the nature of data expected to be carried, it is proposed that such scenarios are instead treated as usual data exchange scenarios on the exchange and hence leverage the same protocol APIs. Keeping this constraint in mind, protocol proposes following flow for such notifications:

![](<../../../.gitbook/assets/5 (1)>)

**Subscription Mechanism :**

Subscription to such notifications will mainly involve checking the policy/coverage details on behalf of the patient with their explicit consent. Therefore, protocol proposes that:

1. To raise subscription requests to user/beneficiary notification, participants will use the Check Coverage Eligibility APIs which are anyway intended to find the status of coverage on behalf of the patient. .
2. Before responding with the Coverage Eligibility Response, payors are expected to collect consent from patients either through HIE-CM, or any other existing mechanism. Such consent is expected to be stored by the payer for the duration required by the law to help resolve any future contentions.
3. Payers are expected to save the details of the subscribed participant against their user/subscriber/patient to enable them to trigger the notifications when an event related to the patient takes place. This is similar to how a payer would currently store a registered mobile number against their users to send them SMS notifications.

**Delivery Mechanism :**

Post subscription, the key challenge would be to inform the subscriber of the notification, e.g. HIU, about initiation of the event for a patient under its subscription. Given that an HIU may subscribe to such information on behalf of many patients it may represent, this would require sharing PII information about the patient, e.g. its policy number, current case id apart from the correlation\_id/workflow\_id that can be used to track the particular case/episode. Therefore, following mechanism is proposed to ensure safe delivery of such notifications:

1. At the time of initiation of such an event (let’s say a pre-authorisation is submitted by a provider for the subscribed patient), the payer uses Communication Request API to send the communication to the subscribed HIU/third party.
   1. It is expected to carry details about the patient's policy, any earlier patient related id shared by the subscriber at the time of subscription, current case details/id as part of the encrypted payload, and HCX correlation/workflow id as part of the payload protected header.
   2. In later versions, Payer may also use the CommunicationRequest profile to send any additional information to the user/patient, as well as ask any additional details related to the case (like it would do with a provider for seeking any additional information).
2. Post initiation of an episode/case, payer may
   1. choose to delegate the status/header related notifications to the HCX (as mentioned Public Information category of workflow notifications), or
   2. Trigger the public workflow notifications by itself, or
   3. Keep leveraging CommunicationRequest API to send further encrypted notifications on the episode/case.

Examples section below lists a set of example notifications by phase 1 working groups along with their classification as above.

Following section provides the API specifications and structure to facilitate notifications through HCX.
