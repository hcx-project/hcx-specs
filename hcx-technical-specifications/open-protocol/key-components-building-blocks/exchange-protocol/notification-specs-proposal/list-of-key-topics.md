---
description: >-
  List of key topics identified by working groups as most important to serve the
  ecosystem use cases
---

# List of key topics

## Network Notifications <a href="#_xakf45167wz" id="_xakf45167wz"></a>

### Broadcast  <a href="#_xakf45167wz" id="_xakf45167wz"></a>

List of network notifications essential for efficient HCX operations. These notifications will always be triggered by the HCX.

<table data-header-hidden><thead><tr><th width="162"></th><th width="209"></th><th></th><th></th><th></th></tr></thead><tbody><tr><td><strong>Notification Title</strong></td><td><strong>Description</strong></td><td><strong>Trigger Condition</strong></td><td><strong>Initiating Participant</strong></td><td><strong>Receiving Participants</strong></td></tr><tr><td>Participant Onboarding</td><td>Notification about new participants joining the ecosystem.</td><td>Participant Onboarded</td><td>HCX</td><td>Everyone (By default)</td></tr><tr><td>Participant De-boarding</td><td>Notification about new participants leaving the ecosystem.</td><td>Participant De-boarded</td><td>HCX</td><td>Everyone (By default)</td></tr><tr><td>New Feature Support</td><td>Notification about new feature launch for the participants on the network.</td><td>New feature added</td><td>HCX</td><td>Everyone (By default)</td></tr><tr><td>End of support for old feature</td><td>Notification about removing an old feature for the participants on the network.</td><td>Feature removed</td><td>HCX</td><td>Everyone (By default)</td></tr><tr><td>End of support for old protocol version</td><td>Notification about ending support for an older version of the protocol by the HCX.</td><td>Support ended</td><td>HCX</td><td>Everyone (By default)</td></tr><tr><td>Network maintenance/Downtime</td><td>Notification about planned downtime/maintenance of the gateway switch.</td><td>System down</td><td>HCX</td><td>Everyone (By default)</td></tr><tr><td>Policy change - SLA</td><td>Notification about the policy changes about the SLAs for the participant in the ecosystem.</td><td>SLA change</td><td>HCX</td><td>Everyone (By default)</td></tr><tr><td>Policy change - Security &#x26; Privacy</td><td>Notification about the data security &#x26; privacy standards for the participant in the ecosystem.</td><td>Security updated</td><td>HCX</td><td>Everyone (By default)</td></tr></tbody></table>

### Targeted Network Notifications: <a href="#_p63wqrrbwrll" id="_p63wqrrbwrll"></a>

List of notification to be supported by HCX for timely actions by participant to prevent ecosystem breakdown -

| **Notification Title**    | **Description**                                                                                   | **Trigger Condition** | **Initiating Participant** | **Receiving Participants** |
| ------------------------- | ------------------------------------------------------------------------------------------------- | --------------------- | -------------------------- | -------------------------- |
| Compliance expiry         | Notification about the compliance certificate expiration for the participant in the ecosystem.    | Expiry date           | HCX                        | Relevant participant       |
| Subscription expiry/renew | Notification about the notification subscription expiration for the participant in the ecosystem. | Expiry date           | HCX                        | Relevant participant       |
| Encryption Key expiration | Notification about the encryption key expiration for the participant in the ecosystem.            | Expiry date           | HCX                        | Relevant participant       |

## Participant Notifications <a href="#_167kwqs1n8il" id="_167kwqs1n8il"></a>

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

## Workflow notifications <a href="#_nz2cwuikafm" id="_nz2cwuikafm"></a>

### Non-PII (public information)

Notifications on key use cases that the regulators, educational institutions, etc would like to track -

| **Notification Title**                              | **Description**                                                                     | **Condition detail** | **Initiating Participant** | **Receiving Participants**  |
| --------------------------------------------------- | ----------------------------------------------------------------------------------- | -------------------- | -------------------------- | --------------------------- |
| Status change - Initiation, closure, approved, etc. | Notification about workflow updates on a policy.                                    | Workflow updated     | Payor                      | Subscribed participants     |
| Admission case - For a particular disease           | Notification about patient admission for a particular disease                       | Workflow updated     | Provider                   | Subscribed participants     |
| Claim initiation for a particular disease           | Notification about workflow updates for claim initiation for a particular disease.. | Workflow updated     | Payor                      | Subscribed participants/IIB |



### PII carrying workflow notification: <a href="#_4znhenc5aoq6" id="_4znhenc5aoq6"></a>

Notifications for key business use cases requiring PII to third party participants that are not involved in the data exchange. Please note that these would be enabled through the combination of existing data exchange APIs.

| **Notification Title**                      | **Description**                                                                                       | **Condition detail**       | **Initiating Participant** | **Receiving Participants**  |
| ------------------------------------------- | ----------------------------------------------------------------------------------------------------- | -------------------------- | -------------------------- | --------------------------- |
| Status change of claims of a patient        | Notification about workflow updates on an identified policy.                                          | Workflow initiation/update | Payor                      | Subscribed participants/HIU |
| Change in coverage eligibility of a patient | Notification about change in coverage eligibility on an identified policy.                            | Workflow initiation/update | Payor                      | Subscribed participants/HIU |
| Reimbursements of claim for a patient       | Notification about claim reimbursement..                                                              | Workflow initiation/update | Payor                      | Subscribed participants/HIU |
| Claim verification                          | Notification about claim verification status based on the beneficiary consent authentication by payor | Workflow initiation/update | Payor                      | Subscribed BSPs/HIUs        |
