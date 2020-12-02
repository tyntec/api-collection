# Rich Media Template with quick reply buttons

This is an example request for sending a rich media template with quick reply buttons.

The template is defined as

*Body:* 

````
Hi {{1}}, 
 
thank you for visiting {{2}}. 
 
We would like to know how much you enjoyed it. 
````

*Footer:*

    Your tyntec event team 
    
*Buttons:*

 - It was great     
 - It was OK         
 - It was bad 

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
      "templateId": "event_rating",
      "language": {
        "policy": "deterministic",
        "code": "en"
      },
      "components": [        
        {
          "type": "body",
          "parameters": [
            {
              "type": "text",
              "text": "Peter"
            },
            {
              "type": "text",
              "text": "WhatsApp Demo"
            },
          ]
        },
        {"type" : "button",
           "subType" : "quick_reply",
           "index": 0,
           "parameters" : [{"type":"payload", "payload": "event-id-1233"}]        
        },
        {"type" : "button",
           "subType" : "quick_reply",
           "index": 1,
           "parameters" : [{"type":"payload", "payload": "event-id-1233"}]        
        },
        {"type" : "button",
           "subType" : "quick_reply",
           "index": 2,
           "parameters" : [{"type":"payload", "payload": "event-id-1233"}]        
        }
      ]
    },
    "contentType": "template"
  }
}
````
