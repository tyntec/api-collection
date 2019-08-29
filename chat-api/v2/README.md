# Release notes

## 2.5

This release introduces the first intermediate event type. These event types are meant for informational purposes during the message delivery processes. They will always be followed by a final event (_MessageStatus::failed_, _MessageStatus::delivered_, _MessageStatus::seen_).

In order not to break existing clients, you need to opt-in for the new event(s) before we start pushing them to us.

### Features

#### WhatsApp preview url support

With this release you can toggle if an url in a text messages has a preview rendered. The property to control this behavior is called ``urlPreviewDisplayed`` and is of type ``boolean``. It defaults to ``false``.

#### Failure details on MessageStatus events

The MessageStatus is extended with ``details`` property. This property provides information about ``code`` and ``message`` in case of an errornous situation which lead to a failure.

#### Additional MessageStatus events

Additional MessageStatus events are defined

- MessageStatus::accepted - send out after we have accepted your message
- MessageStatus::channelFailed - send out after a failure occur on the delivery channel. contains the specific information about the error in the property ``details``. This event is an **intermediate** event and will be followed by one of the final events (_MessageStatus::failed_, _MessageStatus::delivered_, _MessageStatus::seen_).
  

### Deprecations

#### content type ``url``

As the content type is not used and in order to make the consumption of the API simpler we will drop the support of content type ``url`` on WhatsApp and SMS in a future release. Starting with this release the url will be translated on WhatsApp messages to content type ``text`` with ``urlPreviewDisplayed`` enabled.

Please use contentType ``text`` on both WhatsApp and SMS.

#### language policy ``fallback``

We got notified by WhatsApp that they will drop the ``fallback`` policy on template messages. As we need to stay up-2-date with the WhatsApp API, we will drop this policy as well in the next month.

Please switch to language policy ``deterministic``.

### Fixes

#### Documentation

##### Fix mistake in WhatsAppGroupInviteLink

Align the described property ``inviteLink`` with the actual property ``link`` produced by the system

##### Fix mistake in MessageStatus

Remove mandatory flag of property ``from`` as one event (``MessageStatus::failed``) does not support it since the beginning.

## 2.4

### General

#### New resources

In order to enable the group management capabilities and be extensible in the future the CHAT API  is extended with a new path pattern

    channels/<channel name>

All channel-specific capabilities will reside under this base path.

#### URL move

The Chat API has been moved to https://api.tyntec.com/chat-api/v2. The old base URL is still accessible, but will not get any further major upgrades.

#### Inbound messages are events

With this release we start to treat the objects send to your API, eg. MoMessage or MessageStatus, as events. In order to support this shift in the model all objects 
pushed actively to your system will contain - from this release on - a property named _event_. This property indicates not only the object type, but as well event details.
For example, if a message was delivered, the event will be: _MessageStatus::delivered_.

This enables your systems to easily filter out unwanted events without the needs to have a deep look into the data transferred.

### Features

#### WhatsApp Group Chat support

Starting with this release the Chat API makes the WhatsApp group chat functionality available.

The current release supports:

 - listing all groups
 - creating a new group
 - getting list of participants and remove them from the group
 - getting information about the group
 - updating the group profile and icon
 - maintaining the invite link
 - group chat itself via the normal messaging API
 - group specific events, such as _user has joined the group_ or _user has left the group_

#### Location support

On inbound and outbound messages locations can be shared.

They are of contentType _location_ and are represented as shown in this example

    "location" : {
      "longitude": 7.4954884,
      "latitude": 51.5005765,
      "name": "tyntec GmbH",
      "address": "tyntec GmbH, Semerteichstraße, Dortmund"
    }

### Deprecations

#### ``deliveryChannel`` property

In order to make the consumption of the API simpler and as a preparation for a future release, we decided to deprecate the property ``deliveryChannel`` on the MessageStatus and HistoryItem object and replace it with the property ``channel``. 

Until the property ``deliveryChannel`` is removed both properties are provided with the same data.

#### ``status`` property on MessageStatus

As a preparation for a future release, we decided to deprecate the property ``status`` on the MessageStatus object and replace it with the property ``event``. 

Until the property ``status`` is removed both properties are provided.

#### ``receivedAt`` property on MoMessage

As a preparation for a future release, we decided to deprecate the property ``receivedAt`` on the MoMessage object and replace it with the property ``timestamp``. 

Until the property ``receivedAt`` is removed both properties are provided.

#### ``DefaultContent`` object

In order to make the consumption of the API simpler (and as it was not being used) we decided to drop the support of the default content in the next major release.

Please migrate to the channel specific objects _WhatsappMessageRequest_, _SMSRequest_ and/or _TyntecEchoRequest_.

### Fixes

Minor fixes that clarify documentation.

### Improvements

#### ``from`` property on History and MessageStatus

In alignment with the Group Chat feature the message History and MessageStatus are enhanced with the property ``from``. This property contains the id of the issuer of the event.

On Group Chats this is usefull to understand if all members of a group have received and/or read the message send. And which member has joined, left, ... the group

#### ``event`` property on MoMessage and MessageStatus 

As a preparation for a future release we introduced the property _event on the MoMessage and MessageStatus object. This property holds the type of event consisting of classification and, if applicable, detail.

For the MoMessage the event is always _MoMessage_.

For the MessageStatus it can be one of:

  - MessageStatus::accepted
  - MessageStatus::delivered
  - MessageStatus::seen
  - MessageStatus::failed
  - MessageStatus::unknown
  - MessageStatus::deleted

#### Documentation

In order to ease the maintenance and improve readability the open API specification file has been slightly rearranged and contains other improvements including the use of more common properties, etc..

## 2.3

### Fixes

#### Missing caption support on MoMedia

The MoMedia object now transfers the caption set by the user.

## 2.2

### Features

#### User Context support

You can now set a user context, which is transferred back to notifications.

#### Notification Callback URL override

You can now override the default notification callback URL per message request.

Our system will then send notifications to this endpoint instead of the default one.

The same rules as for the default notification endpoint applies

#### Video media type support

The video media type can now be send to users.

### Fixes

#### message ID on MO messages

The previous versions stated that the message ID on MO messages is a UUID. As this has changed with Release 2.0,
the documentation has now been updated with the correct information: the message id is just a string.

#### base URL pointing to the correct major version

Here's the previous version that's pointed to a deprecated base url: (https://api.tyntec.com/messaging/v1/chat). The correct version is: (https://api.tyntec.com/messaging/v2/chat)


## 2.1

### Features

#### History object provides details about the status

The history object now provides details why a certain state was reached. For example the error code and reason.

### Fixes

#### Documentation improved

A few improvements to  explanatory texts were made.

## 2.0

### Breaking changes

#### Mo Message ID data type changed from UUID to plain string.

In order to support the delete status without introducing a new model element, we decided to relax the data type definition of the Mo Message ID from UUID to plain string.

### Features

#### Support of video media type

#### Mo Messages provide profile information of the sender

#### Mo Messages provide reply message ID

The Mo Messages transfer the message ID the message replies to. Currently it works only for WhatsApp.

#### Delete status added to notifications

When the client deletes a message that was previously sent, a delete notification is sent.
