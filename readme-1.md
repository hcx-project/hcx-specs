---
description: Background of the Health Claims Data Exchange effort
---

# Context

## Need for a new approach

### Overview of the Current Process

The current health claims filing and processing experience is fairly manual in nature.

Patients usually reach the health service provider and provide the provider with either the policy details or a card issued by the Payers. The provider fills out the pre-auth/claim form by hand, scans all the required documents that need to be part of the claim, and sends these to the appropriate Payer (Insurance, TPA, …) typically over email. Several Payers also provide providers with their own electronic portal where their claims can be submitted as an alternative to email.

On receipt of the pre-auth/claim form, the Payer verifies and digitizes the form in the software they use internally for claims processing. The team then adjudicates the claims. A large portion of adjudication in India is currently manual while many developed markets auto-adjudicate over 90% of their claims.

A response to the pre-auth/claim is sent back to the provider over email. Payments are done electronically and notifications for payment advice are sent via email. Similar to the cashless procedures outlined here, reimbursement and other processes in health claims require considerable levels of manual intervention.

Furthermore, most payer including all insurers have to report claim details in a specified format to the Insurance Information Bureau of India (IIB). This is done on a monthly basis by the payers.

_(_[_Reference: NHA IRDAI Joint Working Group Report_](https://pmjay.gov.in/sites/default/files/2019-09/Sub%20Group%20on%20Common%20IT%20Infrastructure%20Report\_11-09-19.pdf)_)_

### Challenges of the Current Process

* The current claims exchange process is not standardized across the ecosystem
* Most data flow is PDF/manual
* High variability of process between payers/insurer/TPA/provider

This results in:

* Multiple follow-ups, lack of visibility
* Long receivable cycles
* High cost of processing
* Poor scalability
* Poor patient experience

Inspired by the [recommendations of the Joint Working Group of NHA and IRDAI (2019)](https://pmjay.gov.in/sites/default/files/2019-09/Sub%20Group%20on%20Common%20IT%20Infrastructure%20Report\_11-09-19.pdf), these specifications have been developed over the last two years by 100+ volunteers from across the healthcare ecosystem (including Insurers, Hospitals, TPAs, Insurance Technology players and Think tanks), as a part of a transparent, collaborative and open effort anchored by Swasth.

The goal is to create an open, widely agreed Health Claims data Exchange Specifications as a public good that can be adopted. Specifications in this context refer to the blueprint of each aspect of the envisioned claims network and are fundamental to the working of the network. They have been carefully designed to be open to support technology and vendor neutrality, evolvable over a period of time thereby helping adapt to changing needs, enable and not restrict innovation or inclusion. The specifications are comprehensively evaluated for various health claims scenarios, including cashless and reimbursement procedures for both Inpatient (IPD) and Outpatient (OPD) treatments. This evaluation is conducted by volunteers from various sectors within the health claims industry. And there are plans to evaluate and incorporate additional use cases in the future.

{% hint style="info" %}
While the [recommendations of the Joint Working Group of NHA and IRDAI (2019)](https://pmjay.gov.in/sites/default/files/2019-09/Sub%20Group%20on%20Common%20IT%20Infrastructure%20Report\_11-09-19.pdf) refers to the concept as HCP (Health Claims Platform), working groups decided to choose the new name HCX (Health Claims Data Exchange) after the feedback from the ecosystem that an HCP would involve many more things than data exchange facilitation.
{% endhint %}

The next section provides high level details of the HCX vision, mission, & structure of the protocol.
