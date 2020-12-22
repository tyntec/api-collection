# Conversations V3

## BETA - Phase 1

### Breaking changes

- multi channel support dropped
- `from` moved to the top level object
- `media` container object replaced by simple media type structures
- templates define now specific sections, such as `header`, `body`, `buttons` in contrast to a simple list
- channel specific structures replaced by `content`
- bulk messages are now configured on the `messages` object instead of the channel specific one

### Features

- Harmonized data models between all channels
- WeChat support

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