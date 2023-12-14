---
description: Scenario involving multiple HCX switches between sender and the receiver
---

# Relay

In case Sender and receiver are listed/registered on different HCX instances, there may be request/response relays between the HCXs. Steps 2, 5, 8 and 11 in the below diagram may involve such relays. The diagram below provides an example of a provider-payor use case with a relay between two HCXs.

<figure><img src="../../../../../.gitbook/assets/Relay flow.png" alt=""><figcaption></figcaption></figure>

The cross gateway communication will be required in the following scenarios –

1. When a provider is onboarded in a gateway instance but the payer for that health policy scheme is registered in another gateway instance.
2. If a beneficiary enrolled in health policy took treatment in a network hospital in another state and that hospital is onboarded in a different gateway instance than the payer.
3. For top-up cases, the providers and payers are registered in different gateway instances and in such scenarios primary insurance is handled by one payer in one gateway instance but the secondary insurance is handled by another payer registered in a different gateway instance.
