---
description: Beneficiary authentication valid instruments
---

# Guidelines for Beneficiary Authentication by Providers/Payors

## Aadhaar Digital eKYC API

Authentication of beneficiaries by providers on provider TMS/beneficiary APP.

The Provider TMS system will support Aadhar eKYC open API integration for beneficiary authentication using Aadhar. All the govt schemes and most of the private providers may use Aadhar based KYC process for verification of the beneficiary in their TMS system.

## Optional Aadhaar Authentication (mobile OTP/biometric)

Authentication of beneficiaries by providers on provider TMS/beneficiary APP

The Provider TMS system will use Aadhaar based authentication (Aadhar integrated Mobile OTP based authentication, biometric based authentication) for authentication of a beneficiary to initiate the claim transaction in the provider TMS system. All provider systems that are enrolled with NDHM will have biometric devices for validation and creation of the health ID.

The payer TMS system and HCP will integrate the Aadhar authentication open API for verification of the beneficiary ID during the claim validation stage.

## Verifiable Govt ID based verification (DL/PAN/Voter ID)

Authentication of beneficiaries by providers on provider TMS/beneficiary APP

The providers and payers may choose to integrate different open APIs in their TMS systems to validate the beneficiary ID based on verifiable Government identity database lookup (e.g. PAN, Ration Card, Passport etc.) as well as any other mechanism to verify the beneficiary credentials during enrollment of beneficiary in their systems and validate the beneficiary ID during claim processing

## Token based authentication by Payer

In this case, the payer issues a token (e.g., an OTP) to the customer, which the customer then supplies to the provider for subsequent forwarding back to the payer. This provides a confirmation to the payer that the customer has approved the claim request.

## Direct Authentication by Payer

The payer authenticates the customer by directly interacting with him. For example, the payer sends a message with an OTP and a URL to the beneficiary’s phone. The beneficiary clicks on the URL. The payer displays the beneficiary’s photo and some basic details of the claim (e.g. diagnosis, treatment planned and sum claimed). The beneficiary either rejects the claim or approves it.

#### Next Steps

This section proposes a high-level approach that can be adopted for beneficiary authentication policies for an HCX ecosystem. More deliberation is needed to arrive at model policies that can then be readily extended to be adopted by the ecosystem. Domain working groups will continue to work on developing a detailed approach for beneficiary authentication guidelines for easy adoption. These documents will be released for public consultation in time for an initial pilot of the HCX ecosystem.
