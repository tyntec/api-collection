# Rich Media Template with location

This is an example request for sending a location together with a rich media template

The template is defined as

*Header* : 

    Location

*Body* : 

````
Hi {{1}}, 
 
please be on {{2}} at {{3}} at the specified location for your transfer to the airport. 
````

*Footer* :

    tyntec customer care

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
      "templateId": "pickup_point",
      "language": {
        "policy": "deterministic",
        "code": "en"
      },
      "components": [
        {
          "type": "header",
          "parameters": [
            {
              "type": "location",
              "location": {
                "latitude": 51.5005765,
                "longitude": 7.4954884
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
              "text": "2020/05/01"
            },
            {
              "type": "text",
              "text": "11am"
            }
          ]
        }
      ]
    },
    "contentType": "template"
  }
}
````