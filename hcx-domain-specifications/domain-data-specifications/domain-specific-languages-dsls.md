# Domain Specific Languages (DSLs)

There are two key DSLs being considered for the Health Claims Exchange - Policy Markup Language (PML) and Bill Markup Language (BML). These are currently work in progress and are expected to be released in the later version of HCX specifications after substantial proof of concept development with various members of domain working groups.

## Policy Markup Language (PML)

The purpose of policy markup language is to provide a digital encoding mechanism to payers such that the policies can be encoded in machine readable format, thereby helping with the automation of claim submission and adjudication processes.

This version of the protocol is focused on digitally encoding the Insurance Plan (usually called Product) by the payers. The policies that are derived from the products specific to the individual or a group, would be planned in the future versions. We recommend the Insurance Plan information to be avialable publicly as it is not specific to any subscriber or group.

Though PML has long been thought of as a single DSL to express Insurance Plans (products) and Policies, we are going to use a combination of FHIR resources and FHIR DSLs to express plans and policies.

To ease claim submission, the following aspects are encoded. The [FHIR InsurancePlan profile with some extensions](https://gist.github.com/gopi-vitraya/7c1a3a8526a64487fe04a91b17927b24#file-hcx-insuranceplan-json) are used to encode the above.

1. The basic plan details required for admistrative purposes
  *  Most of the basic details like name, IRDA UIN as identifier, validity, etc.. are covered in InsurancePlan profile.
2. The benefits that are covered under the plan
  * The `InsurancePlan.plan.specificCost` is used to describe the individual benefits. A benefit could be expressed against a procedure, a package (in the context of Indian Health Insurance industry), a diagnosis, a physical good or a service. For each benefit, the cost and the count upto which the benefit would be reimbursed could be specified.
3. The documents required to submit at preauthorization and/or claim stage
  * An [extension](https://gist.github.com/gopi-vitraya/7c1a3a8526a64487fe04a91b17927b24#file-hcx-investigations-extension-json) has been provided to describe the documents that are requrired as part of the preauthorization or claim submission.
4. The proof of presence and identity requirements prior to the preauthorization and/or claim stage
  * The extensions for the inclusion of proof of identity [here](https://gist.github.com/gopi-vitraya/7c1a3a8526a64487fe04a91b17927b24#file-hcx-poid-extension-json) and proof of presence [here](https://gist.github.com/gopi-vitraya/7c1a3a8526a64487fe04a91b17927b24#file-hcx-popr-extension-json) are provided. In this version, the list of the documents could be described. The rules on top of these would included in a later version of the protocol.
5. The questionnaires required to be answered and submitted along with a preauthorization and/or a claim request
  * [Questionnaire Extension](https://gist.github.com/gopi-vitraya/7c1a3a8526a64487fe04a91b17927b24#file-hcx-questionnaires-extension-json)
6. The informational and compliance messages that the provider should be aware of, prior to the preauthorization or claim request
  * [InformationalMessages Extension](https://gist.github.com/gopi-vitraya/7c1a3a8526a64487fe04a91b17927b24#file-hcx-questionnaires-extension-json)
7. The inclusion and exclusion constraints against a particular benefit or a group of benefits (Not covered in this version)
8. The routing information to determine the right recipient for a claim (Not covered in this version)

An [example](https://gist.github.com/gopi-vitraya/c55fafdd6f932e4fdbf00b79bda9f71a) InsurancePlan object is provided for reference.

The digital encoding of policies and adjudication rules would be discussed in the later versions of the protocol.

## Bill Markup Language (BML)

The purpose of bill markup language is to provide a DSL to payers such that the supporting bills can be parsed as machine readable structured data, thereby helping with the automation of adjudication processes.

## Questions for Consultation

#### Question 1

The section above refers to adopting appropriate DSLs for policy and bills. Kindly suggest your views on the useability of such domain-specific language and provide prior examples.&#x20;

#### Question 2&#x20;

Are there any existing solutions that have been used/experimented with? Please provide examples.&#x20;

{% hint style="info" %}
Instructions to send responses to the consultation questions are available [here](../../how-to-submit-responses.md).
{% endhint %}
