# Domain Data Models

The domain data model consists of the electronic claim (e-claim) objects (a.k.a. **eObjects)** that are designed to capture the required information essential for processing a health claim transaction. The e-claim objects, being machine -eadable, facilitate the flow of data exchange between different systems and data processing in health claim transactions without the need for human intervention.

## Guidelines for eObjects

### Bundle Structure

* All e-claim objects will be modelled as FHIR bundles of type "document", with "bundle.composition.type" specifying the type of bundle.
* The first resource in the bundle shall be a “Composition” resource followed by a series of other resources referenced from the “Composition” resource. The elements “type”, “category” and “section” in the “Composition” shall be used to define the purpose and set the context of the document.
* For example, the data packet for a coverage eligibility check request will be a bundle with “bundle.composition.type” as “Coverage Eligibility Check” and the bundle will have a “CoverageEligibilityRequest” FHIR resource embedded in it.

{% tabs %}
{% tab title="CoverageEligibilityRequest Document" %}
* type = “document”
* composition
  * type = “_Coverage Eligibility Check Bundle_”
  * section : cardinality (1..1)
    * code = “_Coverage Eligibility Request_”
    * entry : cardinality (1..1)
      * reference : “CoverageEligibilityRequest”
* CoverageEligibilityRequest FHIR resource
* Patient FHIR resource
* Coverage FHIR resource
* Any other resources referenced in the CoverageEligibilityRequest resource
{% endtab %}
{% endtabs %}

### Identifiers:

* For any resources requiring identifiers (e.g. Patient.identifier), naming systems have to be defined and agreed upon within the affinity domain to be specified in the “identifier.system” element to namespace the identifier value. This can allow an entity or resource to be referenced against system-specific identifiers. For example, a patient may be referenced as:

```
{
 "resourceType": "Patient",
 "identifier": [
   {
     "system": "https://ndhm.gov.in/patients",
     "value": "hinapatel@ndhm"
   },
   {
     "system": "https://pmjay.gov.in/beneficiaries",
     "value": "QWRT23456"
   }
 ]
}
```

* For some identifiers, “identifier.type” can be used to provide additional information.
* “identifier.use” can be used to indicate what/where/how a particular identifier might be used for.
* Example:

```
{
 "type": { // type of identifier
   "coding": [
     {
       "system": "http://terminology.hl7.org/CodeSystem/v2-0203",
       "code": "EI",
       "display": "Employee Number"
     }
   ]
 },
 "system": "https://esi.karnataka.org/employees", // naming system
 "value": "BEN-ID-1001"
}
```

### Resources

* For external entities like patients, organisations, practitioners, etc, a reference alone is enough unless additional information is required to be passed. For example, patient address & other demographics.

### Domain Header

* All eObjects shall be encrypted and sent in the API request body and cannot be accessed by the HCX gateways. However, there is a provision in the API request body for providers and payers to share certain eObjects' related information with the HCX gateway. This information can be sent in the domain\_header part of the request body (as key-value pairs) which can be accessed and stored by HCX gateways for auditing and reporting purposes. Each eObject shall define the domain header values that are to be sent in the API request body.

### Search Parameters

* In addition to the workflow APIs for claim processing workflows, HCX also defines APIs for searching eObjects. To support the search APIs, all eObjects will define the search request parameters.

## Questions for Consultation

#### Question 1

Payors/Providers can share certain information about eObjects with the HCX gateways as part of [domain headers](./#domain-header) in the request body. At present, domain working groups have kept these headers empty. Please suggest the data in each eObject that can be shared with the HCX gateways.

#### Question 2

HCX defines search APIs to search eObjects. The search parameters for each eObject are not currently defined. Please suggest the search parameters for each eObject. Also, should there be additional search APIs that do not require FHIR encoding of the response payload? Kindly elaborate on the nature of these APIs.&#x20;

#### Question 3

Proposed domain data models and terminologies require adopting FHIR as domain object standards. How does one facilitate and enable the participants to adopt FHIR and change their systems and processes?

{% hint style="info" %}
Instructions to send responses to the consultation questions are available [here](../../../how-to-submit-responses.md).
{% endhint %}

