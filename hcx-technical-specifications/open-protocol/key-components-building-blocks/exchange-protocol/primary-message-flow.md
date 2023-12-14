# Primary Message Flow

HCX protocol is designed for the exchanges to work in an asynchronous manner (like SMTP), therefore each use case will be completed in a cycle of messages as detailed below:

<figure><img src="../../../../.gitbook/assets/Primary User Flow.png" alt=""><figcaption></figcaption></figure>

**Sender to HCX (Leg 1)**

* **The sender** (originator of the communication) sends the initial message to its preferred HCX instance.
* HCX validates the status of the sender and the next intended recipient (maybe another HCX instance) on its registries.
* HCX then performs required signature verifications etc before responding with an acknowledgement to the sender.
* It then forwards it to either the end recipient (if registered with the same instance) or the next HCX in the chain.

Steps 1 and 7 in the above diagram are examples of this leg.

**HCX to Receiver (Leg 2)**

* Final HCX in the relay chain (could be the original HCX itself) checks the status of the recipient on its registries,
* performs needed verifications and forwards the message to the recipient.
* The recipient acknowledges the receipt of the message.

Steps 3 and 9 in the above diagram are examples of this leg.

**Receiver to HCX (Leg 3)**

* **The recipient** (receiver of the original request message) sends the response message to its preferred HCX instance.
* HCX validates the status of the recipient and original sender (maybe another HCX instance) on its registries.
* HCX then performs required signature verifications etc before responding with an acknowledgement to the recipient.
* It then forwards it to either the initial sender (if registered with the same instance) or the next HCX in the chain.

Steps 4 and 10 in the above diagram are examples of this leg.

**HCX to Sender (Leg 4)**

* Final HCX in the relay chain (could be the original HCX itself) checks the status of the original sender on its registries,
* Performs needed verifications and forwards the response message to the sender.
* The sender acknowledges the receipt of the response message.

Steps 6 and 12 in the above diagram are examples of this leg.

As indicated in the [**overall message flow diagram**](primary-message-flow.md#overall-message-flow-diagram), the exchange platform will be the routing engine that will be responsible for receiving the data from either participant (provider, payor, another HCX instance, ...), performing necessary validations, and forwarding it to the intended recipients.

Following subsections will provide details about the alternate flows facilitated by HCX.
