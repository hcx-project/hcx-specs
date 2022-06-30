# Notification Specs Proposal (Internal)

### Notification Specs Proposal <a href="#_4d8ls3vcca8e" id="_4d8ls3vcca8e"></a>

### Context <a href="#_9wme70gzafwp" id="_9wme70gzafwp"></a>

As a facilitator of the value between various participating entities, while HCX is envisioned to help different participants directly exchange the claims related information in standardised manner, the network would benefit further if the relevant information about such exchanges could also be shared with other interested/relevant participating entities in a safe and secure manner. Example of such information could be onboarding/deboarding of participants, information about participant system maintenance/upgrades, availability of new functionality, or specific information needed by a participant on a particular claims use case - e.g. Regulator (IRDA/IIB) or Sponser (NHA/SHA/Corporate/Community) needing to know about completion of a claims cycle, or an ISNP needing to know status of a claim on behalf of its patient.

Key benefits of such a notification infrastructure would be:

1. Operational efficiency
2. Transparency
3. Trust in ecosystem
4. Better user experience
5. Improved support and risk mitigation

This RFC describes such needs and proposed enhancements to facilitate such information exchange in the network.

### Abstract <a href="#_lz5afctazyhj" id="_lz5afctazyhj"></a>

Event driven notification can enable valuable near real time information for the HCX network participants in a privacy preserving and secure manner. This proposal outlays the enhancements in the protocol to detail the approach and proposed APIs and data structures to achieve such notification capabilities. Key capabilities proposed to be included are:

1. Classification of key notification types
2. Notification templates/data structure
3. Notification registry (a set of predefined notifications mapped with access control)
4. Subscribe/Unsubscribe APIs
5. Notify APIs
6. Guidelines for policies related to notification capabilities

As part of the overall HCX specifications, the Notification delivery specifications are designed keeping in mind the [overall HCX design principles](https://docs.swasth.app/hcx-specifications/open-specifications/design-principles).

### Terminology? <a href="#_gsartcn8934s" id="_gsartcn8934s"></a>

**HCX Network**: In the context of HCX, HCX network refers to instances of an HCX and its participating systems governed by a common network policy.

**HCX Switch**: Instance of the HCX gateway, implemented as per the HCX protocol, that facilitates the information exchange between its participants.

**Network participants**: Any platform that has implemented the HCX protocol and becomes the part of a network as above.

**Schema**: A JSON data structure that defines an entity as per OpenAPI 3.0 schema specifications.

**FHIR Profile**: A JSON data structure that defines a domain model eligible to be carried as part of JWE payload in the HCX protocol APIs.

**Notification**: A logical unit of information sent to relevant network participants. Notifications can be triggered by an event, activity or time trigger on the network.

**Template**: Message structure with placeholder for context dependent data variable that helps in standardising the message parsing on the network.

**Notify**: Act of sending a notification.

**Registry**: A tamper proof, audited collection of entries with their provenance.

### Categorisation of notifications <a href="#_j3k234ghi2oh" id="_j3k234ghi2oh"></a>

Categorisation of notifications is important from the point of view of data security/privacy and reducing information load on the receivers. It is proposed to classify the HCX Notifications based on the **subject of the notification** as follows:

![](../.gitbook/assets/0)

**Network notifications**

**Broadcast network notifications**

These notifications are expected to carry information about the activities in the network and would be of interest to multiple (if not all) participants in the network. Key use cases for these types of notifications would be:

1. Onboarding of new participants
2. Deboarding of an existing participants
3. Change in network capabilities
   1. Support for new features (either through protocol upgrade or extended features)
   2. End of life for an existing capability
4. Change in network policies like terms of services, SLAs, grievance policies, etc.
5. Switch/Network maintenance and downtime related notifications

![](<../.gitbook/assets/1 (1)>)

Such notifications will be triggered by the HCX switch operator and will be broadcasted to all participating entities on the network. In the initial version of the protocol, it is proposed that participants will be auto-subscribed to these notifications at the time of onboarding and are not given a facility to block or unsubscribe from such notifications.

**Targeted network notifications**

In addition, there's a special category of network notifications that would be targeted at the specified participants in the network. K ey use for such notifications would be:

1. Compliance expiry (re-compliance needed)
2. Encryption key expiration
3. SLA threshold breach, etc.

![](../.gitbook/assets/2)

Thes notifications will be triggered by the HCX switch operator and will be directed to the concerned entities on the network. In the initial version of the protocol, it is proposed that participants will be auto-subscribed to these notifications at the time of onboarding and will not be given a facility to block or unsubscribe from such notifications.

**Participant Notifications**

**Broadcast Participant notifications:**

These notifications are expected to carry participant system related public information that may be helpful for other participants in efficient operations and processing of the claims related information. They would be of interest to multiple (if not all) participants in the network. Key use cases for these types of notifications would be:

1. System maintenance and downtime updates
2. Change in system capabilities :
   1. Support for new version of protocol
   2. Support for prescribed terminologies
   3. End of life for an existing capability (usually as part of protocol upgrades)
   4. New insurance plans/products, end of support for existing products/plans
3. Policy Compliance changes - terms of services, SLAs, grievance policy etc.

![](<../.gitbook/assets/3 (1)>)

Such notifications will be triggered by the network participants and would be expected to be broadcasted to all entities on the network. HCX operators may choose to by default subscribe all onboarding entities to such notifications and provide the facility to unsubscribe from such notifications.

It is recommended that subscribe/unsubscribe facility is made available for the combination of sender and specific topic to allow for granular subscription and avoiding spams.

**Workflow Notification:**

**Public Information carrying Workflow Notifications**

These notifications are expected to carry use case/workflow related information to a third party participant who is not directly participating in the data exchange process. These are expected to be targeted to a set of identified recipients who have expressed explicit interest in observing such workflow events and are assigned the needed role on the network.

Important: Please note that these categories of notification are not designed to carry information about an identified beneficiary, rather general status of any workflow/cycles to interested participants.

Key use cases for these kind of notifications would be:

1. Updates about initiation, closure or change in status of claims cycle: Regulators like IIB needing the information about processed claims at the completion of a claim cycle or; a state or private sponsor needing to know the initiation and closure of claims, etc.
2. Updates about claims for a particular disease type: Surveillance notification to indicate workflow related to a particular clinical type.

![](<../.gitbook/assets/4 (1)>)

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

![](<../.gitbook/assets/5 (1)>)

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

### Proposed APIs <a href="#_as5nkkfw3036" id="_as5nkkfw3036"></a>

Following key APIs are envisioned to achieve the above mentioned objectives (NOTE: OpenAPI specifications for these APIs are work in progress and will be presented for review in next few days):

#### List supported notifications <a href="#_3sax78uu6y0b" id="_3sax78uu6y0b"></a>

Get the list of notification types supported by the network along with their classification and access control parameters. Key attributes of notification type master data are:

| **Attribute/Property** | **DataType**  | **Description**                                                                                                                                                                                                                                                                          |
| ---------------------- | ------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| title                  | String        | The title of the notification                                                                                                                                                                                                                                                            |
| description            | String        | The details about the notification                                                                                                                                                                                                                                                       |
| sender                 | List\<String> | List of roles who can send this notification.                                                                                                                                                                                                                                            |
| recipient              | List\<String> | List of roles who can subscribe to this notification.                                                                                                                                                                                                                                    |
| topic\_code            | String        | Unique code for the notification topic                                                                                                                                                                                                                                                   |
| category               | String        | Category of the notification as detailed above - network (broadcast & target), participant, use\_case                                                                                                                                                                                    |
| priority               | int           | Default priority assigned to the topic. 0 means highest, positive integer would carry the respective relative priority. Negative would be that the topic is disabled. Relative order of category for different message categories is recommended to be use\_case > participant > network |

**Proposed APIs**

/notifications/list

As evident sanctity of the master list of notification is important for effective notification service on the network, hence it is recommended that master list of the notification is given the same treatment as an operator would give to its code for the switch.

#### Subscription to notifications <a href="#_cza39c77xpok" id="_cza39c77xpok"></a>

APIs to subscribe or unsubscribe to a notification type based on its subscribability. For Use case type notifications, this API is also expected to be implemented by the participating systems supporting such notifications. Key attributes of the subscription model are:

| **Column**         | **DataType** | **Description**                                                                                                                                                                           |
| ------------------ | ------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| subscription\_id   | UUID         | Unique identifier for the subscription.                                                                                                                                                   |
| participant\_code  | String       | Identifier of the subscriber.                                                                                                                                                             |
| topic\_code        | String       | Identifier of the notification topic.                                                                                                                                                     |
| status             | Integer      | Status of the notification. Values: 1 - active, 0 - inactive, -1 - pending for approval.                                                                                                  |
| subscription\_data | Object       | Encrypted details subject of subscription for the use\_case category                                                                                                                      |
| subscribed\_on     | timestamp    |                                                                                                                                                                                           |
| expires\_on        | timestamp    | Timestamp when the notification expires. Can use a reasonably long period to indicate forever valid notifications, however it is recommended that subscriptions are periodically renewed. |

**Proposed APIs**

Input would be the topic\_code and payloads containing use case related details wherever applicable. The final response would be returned asynchronously.

/notifications/subscribe and /notifications/on\_subscribe - to subscribe

/notifications/unsubscribe and

NOTE: The schema details and detailed workflow of the subscription API are work in progress and will be included in next few days.

#### Trigger notifications <a href="#_jk5n4j2dcr89" id="_jk5n4j2dcr89"></a>

APIs to trigger the actual notification that would be used by the participants (including HCX switch) to notify the intended participants. This API would be used in two modes:

1. by HCX switch on participants to deliver the final notification (of all categories)
2. By participants on HCX to trigger delivery notifications of participants and use case categories on the intended recipients.

Proposed attributes of notification header and payload:

| **Column**     | **DataType**          | **Description**                                                                                                                                                                                                                                                                                                                    |
| -------------- | --------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| notificationId | String (UUID)         | Unique id assigned by the initiator to the notification                                                                                                                                                                                                                                                                            |
| sender         | String                | Participant code of the notification initiator                                                                                                                                                                                                                                                                                     |
| category       | String                | Category of the notification as defined by the specs - **network**, **participant** or **use\_case**                                                                                                                                                                                                                               |
| topic          | String                | Topic of notification as defined in the master list of notifications                                                                                                                                                                                                                                                               |
| recipientCodes | String\[]             | Participant code of the recipient(s) of the notification. Could be one or more based on the need.                                                                                                                                                                                                                                  |
| recipientRoles | String\[]             | <p>Participant role of the recipient(s) of the notification. Could be one or more based on the need.</p><p><em>recipientCodes and/or recipientRoles can be used to send a notification (network or participant category) to a subset of participants defined in the notification master data for the corresponding topic.</em></p> |
| subscriptions  | String\[]             | Conditional mandatory: list of subscription\_ids (at least one) is mandatory for use\_case category notifications.                                                                                                                                                                                                                 |
| Locale         | String                | Placeholder if localisation needs to be supported in future                                                                                                                                                                                                                                                                        |
| reference      | String                | <p>Optional reference to the context for which the notification is meant. E.g. could be correlation_id or workflow_id for a use_case notification.</p><p>Maybe another notification that was sent earlier.</p>                                                                                                                     |
| initiationTime | Timestamp             | Protocol suggested format timestamp of when the notification was initiated by the sender                                                                                                                                                                                                                                           |
| expiry         | Timestamp             | Expiry of the notification - should be later than initiationTime and currentTime.                                                                                                                                                                                                                                                  |
| message        | String                | Detailed message - usually picked from the template associated with the topic.                                                                                                                                                                                                                                                     |
| messageData    | Key: Value dictionary | Key value pairs containing data for the replaceable attributes in the message template                                                                                                                                                                                                                                             |



**Proposed APIs**

/notifications/notify: return a synchronous acknowledgement of notification being received. Please note that no callback pair is defined for notify API.

Header (same as protocol header) with some additional constraints + notification payload

#### Updating the notification subscriptions: <a href="#_1d926rz3zlxf" id="_1d926rz3zlxf"></a>

APIs to track and expire the notification subscription that will be used by the notification initiating participants to stop sending notifications to the subscribed participants after the expiry trigger condition is satisfied.

There can be two type of subscription expiry conditions:

1. Event based triggers
2. Time based triggers

This API will be used by the initiating participants to revoke the subscription access of the receiving participants.

**Subscription update alerts:**

Any change in the subscription from the sending participant would be notified to all the affected receiving participants using the proposed targeted network notification capability. This is proposed to ensure that receiving participants are not inadvertently affected by change in subscription and may trigger renewal workflows for cases when subscriptions are revoked by sending participants.

**API Attributes:**

[Mahesh Kumar Gangula](mailto:mahesh@sanketika.in)[Abhishek Jain](mailto:abhishek@swasthapp.org) Please add the technical details of the API.

/notifications/subscriptions/update

#### Design Constraints : <a href="#_3c37zmyw8f6w" id="_3c37zmyw8f6w"></a>

In order to make notifications secure, lightweight and easily deliverable and actionable, following constraints are proposed:

* Reuse existing protocol features wherever possible
* Limit the Maximum size of notification payload
* Templatized messages based on notification topic to encourage semantic interoperability

### &#x20;<a href="#_7qvgd9nrcvv1" id="_7qvgd9nrcvv1"></a>

### Proposed list of initial Notification Topics: <a href="#_tvoq9y61od8b" id="_tvoq9y61od8b"></a>

Here are the proposed notification topics that every HCX instance should support

by default.

#### Broadcast Network Notifications: <a href="#_xakf45167wz" id="_xakf45167wz"></a>

List of network notifications essential for efficient HCX operations. These notifications will always be triggered by the HCX.

| **Notification Title**                  | **Description**                                                                                | **Trigger Condition**  | **Initiating Participant** | **Receiving Participants** |
| --------------------------------------- | ---------------------------------------------------------------------------------------------- | ---------------------- | -------------------------- | -------------------------- |
| Participant Onboarding                  | Notification about new participants joining the ecosystem.                                     | Participant Onboarded  | HCX                        | Everyone (By default)      |
| Participant De-boarding                 | Notification about new participants leaving the ecosystem.                                     | Participant De-boarded | HCX                        | Everyone (By default)      |
| New Feature Support                     | Notification about new feature launch for the participants on the network.                     | New feature added      | HCX                        | Everyone (By default)      |
| End of support for old feature          | Notification about removing an old feature for the participants on the network.                | Feature removed        | HCX                        | Everyone (By default)      |
| End of support for old protocol version | Notification about ending support for an older version of the protocol by the HCX.             | Support ended          | HCX                        | Everyone (By default)      |
| Network maintenance/Downtime            | Notification about planned downtime/maintenance of the gateway switch.                         | System down            | HCX                        | Everyone (By default)      |
| Policy change - SLA                     | Notification about the policy changes about the SLAs for the participant in the ecosystem.     | SLA change             | HCX                        | Everyone (By default)      |
| Policy change - Security & Privacy      | Notification about the data security & privacy standards for the participant in the ecosystem. | Security updated       | HCX                        | Everyone (By default)      |

#### Targeted Network Notifications: <a href="#_p63wqrrbwrll" id="_p63wqrrbwrll"></a>

List of notification to be supported by HCX for timely actions by participant to prevent ecosystem breakdown -

| **Notification Title**    | **Description**                                                                                   | **Trigger Condition** | **Initiating Participant** | **Receiving Participants** |
| ------------------------- | ------------------------------------------------------------------------------------------------- | --------------------- | -------------------------- | -------------------------- |
| Compliance expiry         | Notification about the compliance certificate expiration for the participant in the ecosystem.    | Expiry date           | HCX                        | Relevant participant       |
| Subscription expiry/renew | Notification about the notification subscription expiration for the participant in the ecosystem. | Expiry date           | HCX                        | Relevant participant       |
| Encryption Key expiration | Notification about the encryption key expiration for the participant in the ecosystem.            | Expiry date           | HCX                        | Relevant participant       |

#### Broadcast Participant Notifications: <a href="#_167kwqs1n8il" id="_167kwqs1n8il"></a>

List of notification about actions/events of any participant that the ecosystem should be informed about -

| **Notification Title**                                                   | **Description**                                                                                              | **Condition detail**          | **Initiating Participant** | **Receiving Participants** |
| ------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------ | ----------------------------- | -------------------------- | -------------------------- |
| System maintenance/Downtime                                              | Notification about participant system downtime/maintenance                                                   | System down                   | Any participant            | Subscribed participants    |
| Support for new version of protocol                                      | Notification about the participant system supporting the new version of the HCX protocol.                    | Protocol version supported    | Any participant            | Subscribed participants    |
| Support for prescribed terminologies                                     | Notification about a participant system supporting a particular format of terminologies of the HCX protocol. | Terminology version supported | Any participant            | Subscribed participants    |
| End of life for an existing capability                                   | Notification about participant system ending/discontinuing a particular feature of the HCX protocol.         | Feature remove/discontinued   | Any participant            | Subscribed participants    |
| New insurance plans/products, end of support for existing products/plans | Notification about a participant system adding a new product or a particular feature of the HCX protocol.    | Feature supported/launched    | Payor                      | Subscribed participants    |
| Policy Compliance changes - terms of services                            | Notification about the participant system changing terms of the services.                                    | Policy Updated                | Any participant            | Subscribed participants    |
| Policy Compliance changes - SLAs                                         | Notification about participant system SLA of the services.                                                   | Service SLA Updated           | Any participant            | Subscribed participants    |

#### &#x20;<a href="#_8qkfuggr5nve" id="_8qkfuggr5nve"></a>

#### Workflow notifications (Non-PII): <a href="#_nz2cwuikafm" id="_nz2cwuikafm"></a>

Notifications on key use cases that the regulators, educational institutions, etc would like to track -

| **Notification Title**                              | **Description**                                                                     | **Condition detail** | **Initiating Participant** | **Receiving Participants**  |
| --------------------------------------------------- | ----------------------------------------------------------------------------------- | -------------------- | -------------------------- | --------------------------- |
| Status change - Initiation, closure, approved, etc. | Notification about workflow updates on a policy.                                    | Workflow updated     | Payor                      | Subscribed participants     |
| Admission case - For a particular disease           | Notification about patient admission for a particular disease                       | Workflow updated     | Provider                   | Subscribed participants     |
| Claim initiation for a particular disease           | Notification about workflow updates for claim initiation for a particular disease.. | Workflow updated     | Payor                      | Subscribed participants/IIB |

#### &#x20;<a href="#_jq0viou62fi" id="_jq0viou62fi"></a>

#### PII carrying workflow notification: <a href="#_4znhenc5aoq6" id="_4znhenc5aoq6"></a>

Notifications for key business use cases requiring PII to third party participants that are not involved in the data exchange. Please note that these would be enabled through the combination of existing data exchange APIs.

| **Notification Title**                      | **Description**                                                            | **Condition detail**       | **Initiating Participant** | **Receiving Participants**  |
| ------------------------------------------- | -------------------------------------------------------------------------- | -------------------------- | -------------------------- | --------------------------- |
| Status change of claims of a patient        | Notification about workflow updates on an identified policy.               | Workflow initiation/update | Payor                      | Subscribed participants/HIU |
| Change in coverage eligibility of a patient | Notification about change in coverage eligibility on an identified policy. | Workflow initiation/update | Payor                      | Subscribed participants/HIU |
| Reimbursements of claim for a patient       | Notification about claim reimbursement..                                   | Workflow initiation/update | Payor                      | Subscribed participants/HIU |

### Future Enhancement considerations <a href="#_69zbwvo21imj" id="_69zbwvo21imj"></a>

* Notification Delivery status API
* Notification - Failure and retry policies
* Consumers wanting to unsubscribe notification from a HIU/ISNP - Consumers may want to stop notifications from the HIUs (Like policy bazaar, etc.) or switch the HIU to get updates on their policies.

### Appendix 1 <a href="#_opga3he38qh5" id="_opga3he38qh5"></a>

Difference between Notification and Communication API:

| **Communication API**                                              | **Notification API**                                                                |
| ------------------------------------------------------------------ | ----------------------------------------------------------------------------------- |
| Its solicited on need basis                                        | Subscribed                                                                          |
| Information pull - Initiated by parties that needs the information | Information push - Initiated by party that sends info (based on prior subscription) |
