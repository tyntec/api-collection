# Release notes

## 2.2

### Features

#### User Context support

You can now set a user context, which is transfered back on notifications.

#### Notification Callback URL override

You can now override the default notification callback url per message request.

Our system will send notifications than to this endpoint instead of the default one.

The same rules as for the default notification endpoint applies

### Fixes

#### message id on MO messages

The previous versions stated that the message id on MO messages is a UUID. As this has changed with release 2.0,
the documentation states now the correctly that the message id is just astring.


## 2.1



## 2.0
