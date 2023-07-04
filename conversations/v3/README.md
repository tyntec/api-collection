# Release notes

## 3.12

### Changes

#### Added whatsapp reaction message type

With this message type, businesses can send and receive emoji reactions to formely sent messages.

Please note that due to Whatsapp API restrictions, this feature is currently only available for phone numbers connected
via Whatsapps Cloud API. On-Premise installations don't have access to this feature at the moment.

Also note that to be able to receive inbound reactions from endusers, the callback version needs to be set >= 2.13

## 3.11

### Changes

#### Added support for new whatsapp authentication templates


## 3.10

### Changes

#### Aligned Whatsapp Template Categories to new Meta category based billing

The new options for Whatsapp template categories are: MARKETING, UTILITY, AUTHENTICATION

#### Added new property "allowCategoryChange" in Template Submission

Whatsapp can now reject template submissions because of wrong categorization. To avoid this and let whatsapp
change the category instead, the "allowCategoryChange" property can be set to true.  
If obmitted, the default value is false.

#### Examples are now mandatory for all placeholders in whatsapp template submissions

Previously only media placeholders needed example files when submitting templates, now this is also 
mandatory for text 

## 3.9

### Changes

#### MMS Channel was added

## 3.8

### Changes

#### Support for new Whatsapp template categories

Whatsapp reworked their template categories to only three choices: MARKETING, PROMOTION and OTP.

The old categories are deprecated and will be removed in one of the next releases.

## 3.7

### Features

#### WhatsApp supports Product and Product Lists

WhatsApp supports now sending products from a Facebook catalog.

It can be either a single product or multiple products through the product list.

The message type is `interactive` with the subtype `product` or `productList`.

You need to link your Facebook Catalog to your WhatsApp Business Account.

The customer can place an order through their app. Then a new MoMessage event `MoMessage::Order` is triggered.

## 3.6

### Features

#### Viber support for files

Viber supports now sending files up to 200 MB.

At least the properties `url` and the `filename` must be specified.
The optional property `type` is determined from the `url` value if not set.

It's advised to set that value always to avoid false resolutions or failed messages.

#### Viber dropped service id types

As of 4th of October 2021 Viber dropped the support of different service id types (one way, two way, session) and
replaced them by rate types for transaction, promotion and session messages.

The rate types determine the charging applied by Viber per message.

In order to avoid breaking existing clients, the message purpose field is made an alias for the new property
`rateType` and supports also the type _session_ to indicate session based messages.

## 3.5

### Features

#### Media credentials

With this release we support on the account level basic and oauth2 client secret flow for protecting 
media downloads **from** your server when sending messages with media files.

#### WhatsApp - Preview URL on text messages

With this release we support now the missing toggle to preview urls on pure text messages.

The property is called `renderUrlPreview`

### Fixes

Small fixes on the WhatsApp documentation


## 3.4

### Features

#### Channel support now names

With this release the listing of channels can carry now a custom name aside to the channel id.

This name is at the moment not configurable,

## 3.3

### Bugfixes

#### Template status on pending deletes corrected

The prior documented status `DELETE_PENDING` has been replaced by the returned `DELETION_PENDING`.

### Features

#### WhatsApp - Restriction of media caption

The maximal length of  media caption is now 4096 chars.


## 3.2

### Features

#### WhatsApp - New outbound message types

This release enables the 2 new message types `list` and `buttons` on the Conversations API.

`buttons` allows you to specify up to 3 quick reply buttons alongside with an optional header (text or media), a body and an optional footer.

`list` allows you to define up to 10 list option the user can choose from alongside with an optional text header, a body and an optional footer.

#### WhatsApp - New MoMessage::Postback data

With the new outbound message types the `MoMessage::Postback` data model has been adapted to transfer back also the

 - title (list & buttons)
 - description (list only)

information in the `whatsapp` property.

## 3.1

### Features

#### WhatsApp - Examples on template submissions

Template submissions allow now to specify examples for the review by WhatsApp.

It's advised to do this at least for the media templates, as WhatsApp has changed the policies due abuse of
media headers to distribute spam / inappropriate content.  

The examples must be provided up on template submission, later modifications are not supported.

This first release requires the examples to be hosted publicly, a later release will allow a pre-upload of the 
same and reuse of examples via a media id.

#### WhatsApp - New languages added to template localizations

WhatsApp allows now to submit templates in 

- Hausa (ha)
- Malayalam (ml) 
- Zulu (zu)

### Fixes

#### Missing / wrong constraints on Webhook Header

The webhook header key missed the length constraint. It's now correctly documented with 8-125 characters.

The webhook header value had a too short max length documented. It's now updated to 1024 characters max length.

## 3.0

### Breaking changes

- multi channel support dropped
- `from` moved to the top level object
- `media` container object replaced by simple media type structures
- templates define now specific sections, such as `header`, `body`, `buttons` in contrast to a simple list
- channel specific structures replaced by `content`
- bulk messages are now configured on the `messages` object instead of the channel specific one
- The concept of `applications` is replaced by a general `configurations` concept

### Features

#### Harmonized data models between all channels

With this release we put a major effort in reworking and harmonizing the data models between all channels.

Switching between channels for the "standard types" text, and most media messages types, can now be done by 
exchanging the `channel`, `from` and `to`.

We started introducing the concept of components on all places where complex objects are needed. 

#### WeChat (Beta)

With this release an early beta access to our WeChat integration is available. Please reach out to us for details.

#### Telegram (Beta)

With this release an early beta access to our Telegram integration is available. Please reach out to us for details.

#### Upload outbound media files (Beta)

With this release we start providing the option to upload media files prior to the message sending and use them later
when messages are sent.

Please reach out to us for details.

#### _Configurations_ replacing _Applications_

With this release we introduce a generic Configurations concept. 

The Configurations concept starts with the management of callbacks and provides you insights into the scopes 
available to your API account and Channels.

##### Callbacks
We start with providing access to  callback configurations on the API account level (formerly known as Default application), and the channel sender 
id specific level.

This enables you to have a default for all of your channels and define specific overrides on a per channel base.

The settings are resolved later to an effective callback configuration, which enables you to only override a part of the 
global callback configuration, when needed.

The formerly used **PATCH** `/applications/default` is translated to change the API account level callback configuration.

In addition, we start providing you control over the HTTP header sent which each request and configure 
a message signature to detect tampering during the transport. 

#### Scope based access control

With this release we make use of scope based access control to overcome the known limitations of the formerly used concept
of messaging and managing accounts.

In case of WhatsApp: 

This enables us to grant the managing (or owning account), and the messaging account rights on the template management
for modification. As well to control if a profile can be configured by the messaging account.


### Migration 

In order to use the new API the following changes need to be applied

(!) the WhatsApp channel is used as an example

(!) this is not exhaustive for all media types

#### channels -> channel

*V2*

    {
      "channels" : ["whatsapp"] 
    }
*V3*

    {
      "channel" : "whatsapp"
    }

#### {channelType}.from -> from

*V2*

    {
      "whatsapp" : {
        "from": "1324213432"
      }
    }

*V3*

    {
      "from": "1324213432"
    }

#### {channelType} -> content

*V2*

    {
      "whatsapp" : {
        "contentType": "text"
      }
    }

*V3*

    {
      "content" : {
        "contentType": "text"
      }
    }

#### media -> specific media

*V2*

    {
      "whatsapp" : {
        "contentType": "media",
        "media" : {
          "type": image",
          "url" : "https://www.my.cool.image.png"
        }
      }
    }

*V3*

    {
      "content" : {
        "contentType": "image",
        "image" : {
          "url" : "https://www.my.cool.image.png"
        }
      }
    }

#### template components -> specific components

*V2*

    "template": {
    "templateId": "event_review",
    "language": {
      "policy": "deterministic",
      "code": "en"
    },
    "components": [
      {
        "type": "header",
        "parameters": [
          {
            "type": "media",
            "media": {
              "url": "https://images.freeimages.com/images/small-previews/fec/sunset-rays-1391805.jpg",
              "type": "image"
            }
          }
        ]
      },
      {
        "type": "body",
        "parameters": [
          {
            "type": "text",
            "text": "Peter"
          },
          {
            "type": "text",
            "text": "API Beta"
          },
          {
            "type": "text",
            "text": "December 2020"
          }
        ]
      },
      {
        "type": "button",
        "subType": "quick_reply",
        "index": 0,
        "parameters": [
          {
            "type": "payload",
            "payload": "test payload"
          }
        ]
      }
    ]
    }

*V3*

    "template": {
    "templateId": "event_review",
    "templateLanguage": "en",
    "components" : {
      "header" : [
        {
          "type": "image",
          "image": {
            "url" : "https://images.freeimages.com/images/small-previews/fec/sunset-rays-1391805.jpg"
          }
        }
      ],
      "body" : [
        {
          "type": "text",
          "text": "Peter"
        },
        {
          "type": "text",
          "text": "API Beta"
        },
        {
          "type": "text",
          "text": "December 2020"
        }
      ],
      "button" : [
        {
          "type" : "quick_reply",
          "index": 0,
          "payload": "test payload"
        }
      ]
    }
    }

#### Bulk messages

*v2*

    {
    "channel": "whatsapp",
    "from": "4923147790813",
    "to": "491728953754",
    "whatsapp": [
        {
          "contentType": "media",
          "media": {
            "type": "media",
            "url" : "https://www.tyntec.com/sites/default/files/uploads/1608_tyntec_CorporateBackground.pdf",
 	        "caption" : "tyntec corporate background",
            "filename" : "background.pdf"
          }
        },
        {
          "contentType": "media",
          "media": {
            "type": "image",
            "url" : "https://images.freeimages.com/images/small-previews/fec/sunset-rays-1391805.jpg",
 	        "caption" : "nice!"
          }
        }
      ]
    }

*V3*

    {
    "channel": "whatsapp",
    "from": "4923147790813",
    "to": "491728953754",
    "messages": [
      {
        "contentType": "document",
        "document": {
            "url" : "https://www.tyntec.com/sites/default/files/uploads/1608_tyntec_CorporateBackground.pdf",
 	        "caption" : "tyntec corporate background",
            "filename" : "background.pdf"
        }
      },
      {
        "contentType": "image",
        "image": {
            "url" : "https://images.freeimages.com/images/small-previews/fec/sunset-rays-1391805.jpg",
 	        "caption" : "nice!"
        }
      }
      ]
    }
    
#### context.userContext -> context

*V2*

    {
      "context" : {
        "userContext": "my context"
      }
    }

*V3*

    {
      "context": "my context"
    }
