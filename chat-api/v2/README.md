# Release notes

## 2.2

### Features

#### User Context support

You can now set a user context, which is transfered back on notifications.

#### Notification Callback URL override

You can now override the default notification callback url per message request.

Our system will send notifications than to this endpoint instead of the default one.

The same rules as for the default notification endpoint applies

#### Video media type support

The video media type can now be send to users.

### Fixes

#### message id on MO messages

The previous versions stated that the message id on MO messages is a UUID. As this has changed with release 2.0,
the documentation states now the correctly that the message id is just astring.

#### base url pointing to the correct major version

The previous versions pointed to a deprecated base url (https://api.tyntec.com/messaging/v1/chat). This version provides now the correct url (https://api.tyntec.com/messaging/v2/chat)


## 2.1

### Features

#### History object provides details about the status

The history object provides now details why a certain state was reached. For example the error code and reason

### Fixes

#### Documentation improved

Some explainatory texts are improved.

## 2.0

### Breaking changes

#### Mo Message Id data type changed from UUID to plain string.

In order to support the delete status without introducing a new model element, we decided to relax the data type definition of the Mo Message Id from UUID to plain string.

### Features

#### Support of video media type

#### Mo Messages provide profile information of the sender

#### Mo Messages provide reply message id

The Mo Messages transfer as well the message id the message replies to. Works only in case of WhatsApp right now.

#### Delete status added to notifications

When the client deletes a message previously send the delete notification is send.
