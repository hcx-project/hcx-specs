# Implementation Considerations

This section identifies the key workflow and data attribute considerations for implementing the cashless claims for both IPD and OPD usecases.&#x20;

**Workflow considerations :**&#x20;

The existing V0.8 version caters to all the workflow requirements for the reimagined claims workflows.&#x20;

**Data attributes considerations :**&#x20;

| Scenario   | Remarks                                                                                                                                                                                                                                                                                                                                                   |
| ---------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| IPD vs OPD | Use the element “type” in the Claim object to identify whether the claim is an OPD or an IPD claim. The claim-type value set (binded to the “type” element) has a code “professional” which is meant to be used typically for outpatient claims from Physician, Psychological, Chiropractor, Physiotherapy, Speech Pathology, rehabilitative, consulting. |
|            |                                                                                                                                                                                                                                                                                                                                                           |



**Future Considerations :**&#x20;

* Analysing/enhancing the protocol for non-insurance benefits - Corporate wellness, health CSR, community/cooperatives benefits
* Analyse and expand for other OPD categories: Exploring other categories within the OPD use case, understanding their unique challenges, and enhancing the workflow to address specific nuances.&#x20;
* Understanding Master policy holder (MPH) as stakeholder :  Cater and engage with MPH as stakeholders to understand their specific use cases and analyse/prescribe/enhance the HCX  workflow and specifications to serve their needs.
