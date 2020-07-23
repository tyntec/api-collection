# Rich Media Template with text

This is an example request for sending a text together with a rich media template

The template is defined as

*Header* : 

    Text
    
    Account {{1}} has been upgraded

*Body* : 

````
Hi {{1}}, 
 
we're happy to inform you that your account {{2}} has been upgraded to {{3}}.
````

*Footer* :

    Your tyntec support team

The matching request would look like this

````
{
  "to": "{{toPhoneNumber}}",
  "channels": [
    "whatsapp"
  ],
  "whatsapp": {
    "from": "{{whatsappPhoneNumber}}",
    "template": {
      "templateId": "account_upgrade",
      "language": {
        "policy": "deterministic",
        "code": "en"
      },
      "components": [
        {
          "type": "header",
          "parameters": [
            {
              "type": "text",
              "text" : "Demo
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
              "text": "Demo"
            },
            {
              "type": "text",
              "text": "Tier-2"
            }
          ]
        }
      ]
    },
    "contentType": "template"
  }
}
````