# Requesting new templates

These are examples on requesting new WhatsApp templates. 

The name of a template **must** match `^[a-z][a-z_0-9]+$`, so start with lower case letter and consist only of lower case letters, numbers and `_`.

In general a template can consist of the following three components:

#### Header

Could be either a text (up to 60 characters), an image or a document.

In case of a text up to one variable is supported. The variable is indicated by `{{1}}`.

#### Body

Simple text, that can contain newlines, emojis or urls and variables.

Variables are indicated by `{{n}}`, n sequential natural number without repetition.

A variable counts as 1 character for the length.

The body is limited to 1024 characters. **Note** this limit is applied also to the hydrated template, when a footer, header or buttons are used. A hydrated template is a template on which the variable replacements are applied.

The body **must** be present and **not** empty.

#### Footer

Text based footer up to 60 characters.

## Examples

### Body only template request

````
{
  "name": "body_only",
  "category": "ACCOUNT_UPDATE",
  "localizations": [
    {
      "language": "en",
      "components": [
        {
          "type": "BODY",
          "text": "Hello {{1}}!"
        }
      ]
    },
    {
      "language": "fr",
      "components": [
        {
          "type": "BODY",
          "text": "Bonjour {{1}}!"
        }
      ]
    }
  ]
}
````

### Body with footer template request

````
{
  "name": "body_and_footer",
  "category": "ACCOUNT_UPDATE",
  "localizations": [
    {
      "language": "en",
      "components": [
        {
          "type": "BODY",
          "text": "Hello {{1}}!"
        },
        {
          "type": "FOOTER",
          "text": "Your demo team"
        }
      ]
    }
  ]
}
````

### Text-based header template request

````
{
  "name": "body_and_text_header",
  "category": "ACCOUNT_UPDATE",
  "localizations": [
    {
      "language": "en",
      "components": [
        {
          "type": "HEADER",
          "format": "TEXT",
          "text": "Hello {{1}}"
        },
        {
          "type": "BODY",
          "text": "This is an example of a text based header"
        }
      ]
    }
  ]
}
````

### Media-based header template request

````
{
  "name": "body_and_media_header",
  "category": "ACCOUNT_UPDATE",
  "localizations": [
    {
      "language": "en",
      "components": [
        {
          "type": "HEADER",
          "format": "IMAGE"
        },
        {
          "type": "BODY",
          "text": "The format could be as well DOCUMENT"
        }
      ]
    }
  ]
}
````

### Interactive template request with quick reply buttons

You can add up to 3 quick reply buttons.

````
{
  "name": "quick_reply_buttons",
  "category": "ACCOUNT_UPDATE",
  "localizations": [
    {
      "language": "en",
      "components": [
        {
          "type": "BODY",
          "text": "Quick reply buttons are possible as well"
        },
        {
          "type": "BUTTONS",
          "buttons": [
            {
              "type" : "QUICK_REPLY",
              "text" : "Cool!"
            },
            {
              "type" : "QUICK_REPLY",
              "text" : "Nice!"
            }
          ]
        }
      ]
    }
  ]
}
```` 

### Interactive template request with call to action buttons

You can use either one url or one phone number or both types here.

````
{
  "name": "body_and_text_header",
  "category": "ACCOUNT_UPDATE",
  "localizations": [
    {
      "language": "en",
      "components": [
        {
          "type": "BODY",
          "text": "Quick reply buttons are possible as well"
        },
        {
          "type": "BUTTONS",
          "buttons": [
            {
              "type" : "PHONE_NUMBER",
              "text" : "Support",
              "phoneNumber" : "+1231312313"
            },
            {
              "type" : "URL",
              "text" : "Your documents",
              "url" : "https://www.example.com/{{1}}"
            }
          ]
        }
      ]
    }
  ]
}
```` 
 