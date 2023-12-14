---
description: >-
  Forwarding the message to one or more participants to seek inputs in
  processing
---

# Forward

After the original message is received and acknowledged by the receiver, the receiver may forward the request to multiple parties for processing and get their responses before finally responding to the original requestor (sender).

A forward flow would have the following steps:

1. Current Recipient \[R] reads the message from sender \[S] and identifies that it requires help from other parties for processing.
2. Recipient \[R] creates the message to be forwarded to the next Recipient \[R1].
3. \[R] sends across the message to \[R1] by marking appropriate recipient details to HCX. The message needs to carry the same correlation\_id as included by the sender \[S] in step 1.
4. HCX checks the validity of correlation\_id (that it is initiated by a sender and is open for processing) and forwards the message to the \[R1].
5. \[R1] responds to \[R]
6. \[R] may repeat steps 2-4 for multiple next recipients (\[R2], \[R3], …) in parallel or sequentially and receive responses.
7. \[R] processes responses from all forwarded requests and respond with the final response to \[S]

<figure><img src="../../../../../.gitbook/assets/Forward flow.png" alt=""><figcaption></figcaption></figure>

