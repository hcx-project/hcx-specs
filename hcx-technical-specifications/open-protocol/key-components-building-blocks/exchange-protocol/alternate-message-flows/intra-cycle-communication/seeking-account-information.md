---
description: Seeking payment account information to help process the payment
---

# Seeking Account Information

This can be enabled via the Communication cycle between the payor and the TSP.&#x20;

Ref. :  [Seeking support information sequence diagram for detailed workflow.](seeking-supporting-information.md)

Communication Request

1. about: reference to the pre-auth, predetermination, claim for which the communication is requested
2. reasonCode: use the code “Payment Account Information” in the [Communication Reason codes](https://ig.hcxprotocol.io/v0.9/ValueSet-communication-reason-codes.html) valueset
3. payload.contentString: optionally, send a description about the request

Communication Response

1. about: reference to the pre-auth, predetermination, claim for which the communication is requested
2. reasonCode: use the code “Payment Account Information” in the [Communication Reason codes](https://ig.hcxprotocol.io/v0.9/ValueSet-communication-reason-codes.html) valueset
3. payload.contentReference: Send the payment account information in this element.
