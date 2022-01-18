---
description: Overview of audit requirements
---

# Audit and Reporting

HCX instances are expected to log each API call received along with the non encrypted details (domain headers, sig/enc algorithm details, sender & recipient details) and status of signature verification.&#x20;

#### Key Requirements:

* HCX instances should provide reports against the audit logs for different actors - payors, providers, beneficiaries, regulators, observers. Each HCX instance shall publish the list of reports supported by that instance and also define the level/details of information in each report.&#x20;
* The audit information stored should be made available through an API, so that the participating systems can query the audit log related to them.
* Each HCX instance shall define an archival policy for retention & deletion of audit logs. The policy shall also define the process for accessing the logs after archival, if the HCX instance has support for it.
* It is recommended for HCX instances to have a configuration to control the amount of information that gets stored in the audit logs.

## Questions for Consultation

#### Question 1

Apart from the list mentioned here, what other audit and reporting requirements would you expect HCX to fulfil?&#x20;

{% hint style="info" %}
Instructions to send responses to the consultation questions are available [here](../../../how-to-submit-responses.md).
{% endhint %}
