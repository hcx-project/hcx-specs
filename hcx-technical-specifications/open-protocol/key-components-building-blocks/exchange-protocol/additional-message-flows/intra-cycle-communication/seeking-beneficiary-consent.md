---
description: Seeking beneficiary consent whenever deemed necessary
---

# Seeking Beneficiary Consent

Payers can secure beneficiary consent when processing claims initiated by beneficiaries via Beneficiary Service Platforms (BSP) applications.&#x20;

The HCX protocol facilitates obtaining consent through the communication request and communication on\_request API pair. The HCX protocol defines specific consent-seeking [communication reason codes](https://ig.hcxprotocol.io/v0.9/ValueSet-communication-reason-codes.html), streamlining the process for securing beneficiary consent during interactions on the BSP application.

This can be done in two manners:

1. **Using HCX Communication APIs to seek verification token (Recommended)**
   1. A Payer can send a verification token to policyholders using an alternate channel such as SMS or IVR call (similar to how purchase verification OTPs are sent).
   2. The Payers sends a HCX communication request to TSP informing about the need to get the verification token from the policyholder to process the claim.&#x20;
   3. TSP prompts the policyholder and gets the verification token.
   4. TSP submits back the token to the payer using a communication object in response to the communication request API. &#x20;

**Data Attribute mapping:**

[Communication Request](https://ig.hcxprotocol.io/v0.9/StructureDefinition-CommunicationRequest.html):

1. about: reference to the pre-auth, predetermination, claim for which the communication is requested.
2. reasonCode: use the code “Patient Consent Details” in the [Communication Reason codes](https://ig.hcxprotocol.io/v0.9/ValueSet-communication-reason-codes.html) valueset.
3. payload.contentString: optionally, send a description about the request.

[Communication Response](https://ig.hcxprotocol.io/v0.9/StructureDefinition-Communication.html) :

1. about: reference to the pre-auth, predetermination, claim for which the communication is requested
2. reasonCode: use the code “Patient Consent Details” in the [Communication Reason codes](https://ig.hcxprotocol.io/v0.9/ValueSet-communication-reason-codes.html) valueset
3. payload.contentString: OTP/consent token provided by the patient
4. inResponseTo: reference to the request to which this is a response

**Out of band verification (HCX could be used for notification)** -&#x20;

1. On receiving the pre-auth or claim Payer could do an out of band verification with policyholder using an alternate channel such as IVR, Phone call, Email and process the claim on receiving the consent from the policyholder.
2. If the verification fails, the payer responds with a failed claim response.
3. Else, optionally, payer uses HCX notification API to notify the TSP about success of the verification and proceeds with the claim adjudication.

**Typical workflow for the consent handling :**&#x20;

<figure><img src="../../../../../../.gitbook/assets/Typical consent workflow.png" alt=""><figcaption><p>Typical consent handling workflow</p></figcaption></figure>

#### Challenges in typical workflow for consent management :&#x20;

However, as observed in reference app implementation and pointed out by community members during the draft review in comment on [GitHub discussion #113](https://github.com/hcx-project/hcx-specs/discussions/113), the consent verification process may fail or require re-tries due to multiple reasons :

1. OTP not received by the beneficiary due to network problems
2. Invalid token submission, it may be due to human error etc while entering the OTP
3. Consent verification failure due to token expiry
4. Network error while delivering the communication request or response.

To effectively deal with these practical realities, the section below details the proposed approach to handle each of these scenarios.

### Proposed approach :&#x20;

**Scenario 1 : OTP/consent token not received by beneficiary**

A beneficiary may not receive the consent verification token due to token delivery failure e.g. temporary signal issues, network congestion, etc. In such scenarios, we recommend implementing a mechanism to allow the beneficiary to request a resend of the token and perform resend at the payer end. The payers would have the option to specify the number of resend attempts available.

**Proposed workflow :**&#x20;

<div data-full-width="true">

<figure><img src="../../../../../../.gitbook/assets/Usecase 1 - resend token.png" alt=""><figcaption><p>Resend token workflow</p></figcaption></figure>

</div>

**Needed Protocol Enhancements:**

1. Additional communication reason code to indicate resend consent token/OTP (Resend\_token) instead of submitting the token itself.
2. New notification topic for indicating that consent token has been resend to the beneficiary (step 11).

#### Scenario 2 : Incorrect consent token due to human errors

Consent verification may fail due to human errors, such as mistyping or incorrectly inputting the OTP while entering the token. In such scenarios, we suggest implementing a mechanism to allow retries of the token submission. The payers would have the option to specify no. of verification retry attempts.

**Proposed workflow :**&#x20;

<figure><img src="../../../../../../.gitbook/assets/Usecase 2 - Consent failure.png" alt=""><figcaption></figcaption></figure>

**Note :** In case of token expiry, follow Scenario 1 to resend or regenerate the consent token.

**Protocol enhancements:**

* New notification topic to indicate to the beneficiary the need to re-enter the verification token as the last verification failed due to incorrect token.

#### Scenario 3 : Invalid/Expired consent token due to delays in sharing the consent token

If the beneficiary fails to submit the verification token within the specified timeframe stipulated by the payer, the payer may consider the token as invalid or expired. Consequently, the payer will decline the claim request, transmitting a claim denial response to the BSP, marked with the claim denial code "consent\_cycle\_timeout."

In this situation, the BSPs can use the information from the claim and offer a faster way for the beneficiary to resubmit their claim without having to enter all the information again.

**Protocol enhancements:**

* Additional claim denial reason code (consent\_cycle\_timeout) to indicate claim rejection due to delays in consent verification.

#### Scenario 4 : HCX network error while delivering the communication request/response

If a network error occurs during the inline consent verification cycle (communication request and response), the handling is expected to adhere to the guidelines outlined in the HCX protocol error handling section, [as specified here](https://docs.hcxprotocol.io/hcx-technical-specifications/open-protocol/key-components-building-blocks/error-descriptions).
