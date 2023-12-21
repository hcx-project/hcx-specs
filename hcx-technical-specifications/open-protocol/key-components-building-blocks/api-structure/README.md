---
description: Specifications of API for Claims Exchange in the HCX Ecosystem
---

# API Specifications\*

This section provides details about the following API categories designated for implementation and utilization by participants within the HCX ecosystem for claims exchange:

* Registry APIs: Manage and access participants & users data in the HCX ecosystem.
* Primary Flow APIs: Facilitate the core processes and workflows crucial for claims exchange.
* Supporting APIs: Provide auxiliary functionalities and support for operations within HCX.
* Notification APIs: Enable communication and alerts related to claims & other activities within HCX.
* Third Party Information Sharing APIs: Enable exchange of claim related information among participants in the HCX ecosystem.

## API Structure

Based on the protocol definition and the message structure, all APIs in the HCX ecosystem follow the following pattern:

\<transport\_protocol>://\<server\_address>/\<protocol\_version/>\<resource\_name>/\<action|on\_action>, where

* **transport\_protocol** - for currently published versions, it will always be **https**
* **server\_address** is the address of the server on which the API is called (an HCX for payor/provider or a payor/provider/HCX for an HCX)
* **protocol\_version** - API version for the current protocol to help support protocol transitions
* **resource\_name** is the name of the registry entity, domain resource or other objects that the API is serving. E.g. for claims, it may be “coverage eligibility”, “claims”, etc; for registries, it may be "participant" or "user".
* **action** is the action sought within the context of the resource. E.g. for claims, it may be "check" (for checking coverage eligibility), "submit" (for submitting a pre-auth or a claim request), etc; for registry entities, it may be "create", "read", "search", etc; for notifications, it may be "subscribe", "unsubscribe", "notify", etc.
* **on\_action** is applicable for asynchronous APIs, where the response to the API is sent asynchronously by the receiving system for responding to the original message. All the primary flow and supporting APIs have the asynchronous behaviour and will have an "on\_action" API for every "action" API. E.g. "coverageeligibility/on\_check" as response to "coverageeligibility/check", "claim/on\_submit" as response to "claim/submit", etc.&#x20;

Following subsections elaborates on the various API endpoints within each category, their request and response formats, along with additional details.
