---
description: Redirection of the message to another participant
---

# Redirect

After the original message is received and acknowledged by the initial receiver, the receiver may choose to completely hand over the processing of the request to another entity (new receiver). The receiver can achieve this by informing the sender to send (i.e. redirect) the request to the new receiver.

Redirect flow would have the following steps:

1. Current Recipient \[R] reads the message from Sender \[S] and identifies that the request needs to be redirected to another entity \[R1] for processing.
2. \[R] response to the original request with a redirection response (using the status parameter in the header) \[S]. Redirection response includes the next recipient’s \[R1] details (participant id on the hcx platform).
3. \[S] sends a new request to \[R1] by re-encrypting the request using the \[R1] key and marking the appropriate participant id to HCX.
4. HCX forwards the new request to \[R1]. Further processing of the request is handled by the recipient \[R1].

<figure><img src="../../../../../.gitbook/assets/Redirect flow.png" alt=""><figcaption></figcaption></figure>

