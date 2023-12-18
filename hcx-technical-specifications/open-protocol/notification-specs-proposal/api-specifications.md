---
description: APIs to enable notifications
---

# API specifications

## Key Design Considerations <a href="#_3c37zmyw8f6w" id="_3c37zmyw8f6w"></a>

In order to make notifications secure, lightweight and easily deliverable and actionable, following constraints are proposed:

* Reuse existing protocol features wherever possible
* Limit the Maximum size of notification payload
* Templatized messages based on notification topic to encourage semantic interoperability

Following key APIs are envisioned to enable notifications in HCX. Full API specifications in OpenAPI 3.0 format are available [here](https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.9/API%20Definitions/openapi\_hcx\_notifications.yaml).

## List supported notifications <a href="#_3sax78uu6y0b" id="_3sax78uu6y0b"></a>

Get the list of notification types supported by the network along with their classification and access control parameters. Key attributes of notification type master data are:

| **Attribute/Property** | **DataType**  | **Description**                                                                                                                                                                                                                                                                          |
| ---------------------- | ------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| title                  | String        | The title of the notification                                                                                                                                                                                                                                                            |
| description            | String        | The details about the notification                                                                                                                                                                                                                                                       |
| sender                 | List\<String> | List of roles who can send this notification.                                                                                                                                                                                                                                            |
| recipient              | List\<String> | List of roles who can subscribe to this notification.                                                                                                                                                                                                                                    |
| topic\_code            | String        | Unique code for the notification topic                                                                                                                                                                                                                                                   |
| category               | String        | Category of the notification as detailed above - network (broadcast & target), participant, use\_case                                                                                                                                                                                    |
| priority               | int           | Default priority assigned to the topic. 0 means highest, positive integer would carry the respective relative priority. Negative would be that the topic is disabled. Relative order of category for different message categories is recommended to be use\_case > participant > network |

### **API details**

/notification/list

As evident sanctity of the master list of notification is important for effective notification service on the network, hence it is recommended that master list of the notification is given the same treatment as an operator would give to its code for the switch.

{% swagger src="https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.9/API%20Definitions/openapi_hcx_notifications.yaml" path="/notification/list" method="post" %}
[https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.9/API%20Definitions/openapi_hcx_notifications.yaml](https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.9/API%20Definitions/openapi_hcx_notifications.yaml)
{% endswagger %}

## Subscription to notifications <a href="#_cza39c77xpok" id="_cza39c77xpok"></a>

APIs to subscribe or unsubscribe to a notification type based on its subscribability. For Use case type notifications, this API is also expected to be implemented by the participating systems supporting such notifications. Key attributes of the subscription model are:

| **Column**         | **DataType** | **Description**                                                                                                                                                                           |
| ------------------ | ------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| subscription\_id   | UUID         | Unique identifier for the subscription.                                                                                                                                                   |
| participant\_code  | String       | Identifier of the subscriber.                                                                                                                                                             |
| topic\_code        | String       | Identifier of the notification topic.                                                                                                                                                     |
| status             | Integer      | Status of the notification. Values: 1 - active, 0 - inactive, -1 - pending for approval.                                                                                                  |
| subscription\_data | Object       | Encrypted details subject of subscription for the use\_case category                                                                                                                      |
| subscribed\_on     | timestamp    |                                                                                                                                                                                           |
| expires\_on        | timestamp    | Timestamp when the notification expires. Can use a reasonably long period to indicate forever valid notifications, however it is recommended that subscriptions are periodically renewed. |

### **API details**

Input would be the topic\_code and payloads containing use case related details wherever applicable. The final response would be returned asynchronously.

/notification/subscribe&#x20;

{% swagger src="https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.9/API%20Definitions/openapi_hcx_notifications.yaml" path="/notification/subscribe" method="post" %}
[https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.9/API%20Definitions/openapi_hcx_notifications.yaml](https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.9/API%20Definitions/openapi_hcx_notifications.yaml)
{% endswagger %}

/notification/unsubscribe

{% swagger src="https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.9/API%20Definitions/openapi_hcx_notifications.yaml" path="/notification/unsubscribe" method="post" %}
[https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.9/API%20Definitions/openapi_hcx_notifications.yaml](https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.9/API%20Definitions/openapi_hcx_notifications.yaml)
{% endswagger %}

/notification/subscription/list

{% swagger src="https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.9/API%20Definitions/openapi_hcx_notifications.yaml" path="/notification/subscription/list" method="post" %}
[https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.9/API%20Definitions/openapi_hcx_notifications.yaml](https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.9/API%20Definitions/openapi_hcx_notifications.yaml)
{% endswagger %}

## Trigger notifications <a href="#_jk5n4j2dcr89" id="_jk5n4j2dcr89"></a>

APIs to trigger the actual notification that would be used by the participants (including HCX switch) to notify the intended participants. This API would be used in two modes:

1. by HCX switch on participants to deliver the final notification (of all categories)
2. By participants on HCX to trigger delivery notifications of participants and use case categories on the intended recipients.

Proposed attributes of notification header and payload:

| **Column**     | **DataType**          | **Description**                                                                                                                                                                                                                                                                                                                    |
| -------------- | --------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| notificationId | String (UUID)         | Unique id assigned by the initiator to the notification                                                                                                                                                                                                                                                                            |
| sender         | String                | Participant code of the notification initiator                                                                                                                                                                                                                                                                                     |
| category       | String                | Category of the notification as defined by the specs - **network**, **participant** or **use\_case**                                                                                                                                                                                                                               |
| topic          | String                | Topic of notification as defined in the master list of notifications                                                                                                                                                                                                                                                               |
| recipientCodes | String\[]             | Participant code of the recipient(s) of the notification. Could be one or more based on the need.                                                                                                                                                                                                                                  |
| recipientRoles | String\[]             | <p>Participant role of the recipient(s) of the notification. Could be one or more based on the need.</p><p><em>recipientCodes and/or recipientRoles can be used to send a notification (network or participant category) to a subset of participants defined in the notification master data for the corresponding topic.</em></p> |
| subscriptions  | String\[]             | Conditional mandatory: list of subscription\_ids (at least one) is mandatory for use\_case category notifications.                                                                                                                                                                                                                 |
| Locale         | String                | Placeholder if localisation needs to be supported in future                                                                                                                                                                                                                                                                        |
| reference      | String                | <p>Optional reference to the context for which the notification is meant. E.g. could be correlation_id or workflow_id for a use_case notification.</p><p>Maybe another notification that was sent earlier.</p>                                                                                                                     |
| initiationTime | Timestamp             | Protocol suggested format timestamp of when the notification was initiated by the sender                                                                                                                                                                                                                                           |
| expiry         | Timestamp             | Expiry of the notification - should be later than initiationTime and currentTime.                                                                                                                                                                                                                                                  |
| message        | String                | Detailed message - usually picked from the template associated with the topic.                                                                                                                                                                                                                                                     |
| messageData    | Key: Value dictionary | Key value pairs containing data for the replaceable attributes in the message template                                                                                                                                                                                                                                             |

### **API details**

/notification/notify: return a synchronous acknowledgement of notification being received. Please note that no callback pair is defined for notify API.

{% swagger src="https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.9/API%20Definitions/openapi_hcx_notifications.yaml" path="/notification/notify" method="post" %}
[https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.9/API%20Definitions/openapi_hcx_notifications.yaml](https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.9/API%20Definitions/openapi_hcx_notifications.yaml)
{% endswagger %}

## Updating the notification subscriptions <a href="#_1d926rz3zlxf" id="_1d926rz3zlxf"></a>

APIs to track and expire the notification subscription that will be used by the notification initiating participants to stop sending notifications to the subscribed participants after the expiry trigger condition is satisfied.

There can be two type of subscription expiry conditions:

1. Event based triggers
2. Time based triggers

This API will be used by the initiating participants to revoke the subscription access of the receiving participants.

### **Subscription update alerts**

Any change in the subscription from the sending participant would be notified to all the affected receiving participants using the proposed targeted network notification capability. This is proposed to ensure that receiving participants are not inadvertently affected by change in subscription and may trigger renewal workflows for cases when subscriptions are revoked by sending participants.

### **API Details**

/notification/subscription/update

{% swagger src="https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.9/API%20Definitions/openapi_hcx_notifications.yaml" path="/notification/subscription/update" method="post" %}
[https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.9/API%20Definitions/openapi_hcx_notifications.yaml](https://raw.githubusercontent.com/hcx-project/hcx-specs/v0.9/API%20Definitions/openapi_hcx_notifications.yaml)
{% endswagger %}

Following section lists the key notification for each notification category, sender & recipient details, and triggers.
