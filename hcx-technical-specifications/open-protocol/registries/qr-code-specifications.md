---
description: QR code specifications and structure guidelines
---

# QR Code Specifications\*

## **Introduction**

In today's fast-paced digital world, the ubiquitous presence of QR codes has made it evident that they are a powerful tool for swiftly and effortlessly capturing information. This proposal outlines the specification and structure of QR code data, aiming to facilitate its generation and use in the context of Health Claims Data Exchange (HCX)

## **Background & Key scenarios**

Healthcare beneficiaries and providers frequently encounter the need to exchange vital information to verify eligibility and facilitate claim processing. It is crucial to define the necessary information to enable and generate HCX protocol requests, offering an efficient and convenient means for exchanging key data. This requirement becomes particularly evident in various scenarios where HCX participants find it beneficial to utilize QR codes as an expedited method for sharing information and streamlining the request process, including:

* Beneficiaries using provider (Hospital) information for claim processing in reimbursement scenarios.
* Providers utilising beneficiary information to assess eligibility and request claims in Cashless scenarios.

To address these scenarios effectively, we must define the specification for two key components:

* Beneficiary Policy Details
* Provider Details

Additionally, we must keep the following considerations in mind for the QR code specifications:

* Determining the minimal required information for capture,
* Providing the means to trust the information contained within the QR code.

## **QR Code Specification**

The QR code specification must encompass all the necessary information to process the desired requests efficiently while adhering to universal standards for widespread understanding and adoption.

To accomplish this, we propose using the [W3C Verifiable Credential](https://www.w3.org/TR/vc-data-model/) framework to define the QR code's structure. This approach ensures the authenticity of the data contained within the QR code. The standard structure of the data to generate the QR code is as follows:

<pre><code>{
    "@context": [
        "https://www.w3.org/2018/credentials/v1",
        "https://www.w3.org/2018/credentials/examples/v1"
    ],
    "id": "http://hcxprotocol.io/credentials/3732",
    "type": [
                "VerifiableCredential"
    ],
    "issuer": "https://hcxprotocol.io/participant/565049",
    "issuanceDate": "2023-10-01T00:00:00Z",
    "expirationDate": "2020-01-01T19:23:24Z",
    "preferredHCXPath": "http://&#x3C;valid_HCX_URL>/v0.9/",
    "credentialSubject": {
        "id": "did:example:ebfeb1f712ebc6f1c276e12ec21",
        // Details about the Beneficiary, Provider, or any other participant
<strong>    },
</strong>    "proof": {
        "type": "Ed25519Signature2020",
        "created": "2023-10-01T00:00:02Z",
        "verificationMethod": "https://hcxprotocol.io/issuers/565049#key-1",
        "proofPurpose": "assertionMethod",
        "proofValue": "z3FXQjecWufY46yg5abdVZsXqLhxhueuSoZgNSARiKBk9czhSePTFehP8c3PGfb6a22gkfUKods5D2UAUL5n2Brbx"
    }
}
</code></pre>

{% hint style="info" %}
**Note :** For now the the QR code specifications are detailed  for the  providers and beneficiary policies . While policy registry is not yet a part of the HCX specifications;  it was recommended by the workstream that a policy QR code standard should be prescribed.
{% endhint %}

In the context of this specification, we employ the JSON-LD + JWT format for Verifiable Credentials. This format encompasses the following key elements:



<table><thead><tr><th width="193">Attribute/ Term</th><th>Description</th></tr></thead><tbody><tr><td><strong>Issuer</strong></td><td>This specification defines a property for expressing the issuer of a verifiable credential.</td></tr><tr><td><strong>Issuance Date</strong></td><td>The specification includes a property that signifies the date and time at which a credential becomes valid, known as the "issuance date."</td></tr><tr><td><strong>Expiration Date</strong></td><td>The expirationDate is expected to be within an expected range for the verifier. For example, a verifier can check that the expiration date of a verifiable credential is not in the past.</td></tr><tr><td><strong>Proofs (Signatures)</strong></td><td>At least one proof mechanism, and the details necessary to evaluate that proof, MUST be expressed for a credential to be a verifiable credential that is, to be verifiable.</td></tr><tr><td><strong>Credential Subject</strong></td><td>The essential information related to the credential resides within the "credential subject."</td></tr><tr><td><strong>id</strong></td><td>The unique identifier of the credential subject.</td></tr><tr><td><strong>preferredHCXPath</strong></td><td>The base path of the chosen HCX instance to send the API requests. The system uses this base path to make the coverage, claim requests.</td></tr><tr><td><strong>credentialSubject</strong></td><td>The essential information related to the credential resides within the "credential subject." Example the details about the beneficiary and part of this block to confirm the identity.</td></tr></tbody></table>



The verifiable credential, complete with proof data in Base64String format, will serve as the foundation for generating the QR code.\
Within this protocol, we outline the proposal for defining the credential subject for both beneficiaries and providers. Moreover, we establish the procedural framework for issuing QR codes in the format of Verifiable Credentials.

The subsequent step involves proposing the delineation of beneficiary and provider-specific information within the standard structure. By proposing these measures, we aim to streamline the use of QR codes in the Health Claims Data Exchange, providing a secure, efficient, and universally accessible means of exchanging essential healthcare information.

### Beneficiary Policy

The QR code representing the beneficiary is designed to encapsulate the following essential details within the credential subject. These details are critical for participants in the HCX gateway to seamlessly capture and process coverage eligibility and claim requests:

```
{
    "beneficiary": {
        "identifier": [{ // Required
            "value": "",
            "system": "",
            "assigner": "",
            "period": {
            "start": "",
            "end": ""
    }
    }],
        "name": "", // Required
        "insurer": "", // Required
        "mobile": "",
        "location": ""
    }
}
```

\
The identifier is an array of objects. We inherited the Identifier specification from FHIR here to allow multiple values from different systems representing the same object.\
Issuance mechanism\


Given that beneficiaries rely on the insurance-related information contained within these credentials, the issuance of QR codes in verifiable credentials format is proposed to be the responsibility of the payer. This issuance process should strictly adhere to the specifications outlined herein, ensuring a standardised and secure approach to information exchange.

### Participant

The provider's QR code is intended to encompass the following vital details, accompanied by necessary proofs, to enable beneficiaries to capture information and initiate claim requests effectively:

```
{
    "participant": {
        "identifier": [{ // Required
            "value": "",
            "system": "",
            "assigner": "",
            "period": {
                "start": "",
                "end": ""
            }
        }],
        "name": "", // Required
        "type": "", // Required - payor, provider.hospital, etc,.
        "location": ""
    }
}
```

\
\
Similar to the identifier for beneficiary, the participant also follows the same format to allow multiple values from different systems to represent the same.\
Issuance mechanism

\
These QR codes, presented in the verifiable credentials format, are proposed to be self generated by the provider using the signing certificate shared with the HCX network as part of the onboarding process. This flexibility ensures a seamless and secure means of data exchange between providers and beneficiaries.

## **QR Code image specifications**

1. **Colour Palette:** Utilize a high-contrast colour scheme, preferably black and white, for better readability. The background colour should be light, while the QR code itself should be a dark colour to ensure optimal contrast.
2. **QR Code Size:** Maintain an appropriate QR code size to enhance scanning accuracy. The minimum recommended size is 2 × 2 inches (5 × 5 cm) to ensure clarity.
3. **Quiet Zone:** Surround the QR code with a quiet zone (blank space) at least equal to four modules (the small squares that form the QR code) on all sides. This helps prevent interference with the scanning process.
4. **Error Correction Level:** Opt for a suitable error correction level based on the environment where the QR code will be scanned. Higher error correction is recommended for situations where the code might be partially obscured or damaged.
5. **Logo Placement:** If incorporating a logo within the QR code, ensure it doesn't compromise the scanning capability. Place the logo in a designated area that doesn't overlap with essential data.
6. **Encoding Format:** Use the QR code encoding format specified in the W3C Verifiable Credential standard, employing JSON-LD + JWT.
7. **Clear Text:** If applicable, provide clear instructions or text near the QR code to guide users on its purpose and usage.
8. **Testing:** Always test the QR code in various scanning environments and devices to ensure widespread compatibility and functionality.

By adhering to these visual guidelines, we aim to create QR codes that are not only aesthetically pleasing but also optimised for efficient and accurate information exchange within the HCX ecosystem.
