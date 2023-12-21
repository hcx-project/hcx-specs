---
description: >-
  Enabling use cases for sharing information related to claims with other
  participants
---

# Third party Information sharing

There are multiple use cases in the context of claims where certain information about the claims need to be shared to parties that are not directly involved in the claim processing cycle. Some such examples are:

* Regulators like IIB need to collect information about the processed claims at the completion of a claims cycle. IIB uses this information to help the insurance industry with information and analytical support.
* Sponsors like NHA/SHA/Corporate/Community need to know about completion and details of a claims cycle for all the patients sponsored by them.
* An ISNP needs to know the status and details of a claim on behalf of its patient.

Such information can be made available to the interested parties in either of the following ways in HCX:

1. Parties involved in the cycle can report the information to all the subscribed parties when a claim cycle is completed
2. Parties who need information about a claim cycle can fetch the information from involved parties after the completion of a claim cycle (this is mostly be triggered when the interested party receives the relevant workflow notification)

### Information Reporting

Information reporting can be enabled by leveraging the [notifications](notification-specs-proposal/) capability of the protocol. Since the information to be reported may contain PII information of the patients & other sensitive information, the “PII carrying workflow notification” category of notifications should be used for this purpose.

The steps and process for PII carrying workflow notifications are detailed in the [Notification specifications](notification-specs-proposal/categories.md#workflow-notification).

### Fetching Information

Though a mechanism to report information is available, there still may be some scenarios where the parties may need to fetch the required information on demand (e.g.: if the PII notification is not delivered due to technical problems). In such cases, there should be a way for the participants to fetch the required information by directly querying the involved party (a payor or a provider). As the current known use cases for information fetching are only around claim workflows and such information request can be fulfilled by sending the information in form of an ExplanationOfBenefit (EOB) resource, the protocol includes APIs to fetch claims related information using EOB resource. Details of these APIs are available [here](../api-structure/information-sharing-apis.md).
