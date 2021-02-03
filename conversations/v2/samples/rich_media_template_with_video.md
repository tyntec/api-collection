# Rich Media Template with video

This is an example request for sending a video together with a rich media template

The template is defined as

*Header:* 

    Video

*Body:* 

````
Hi {{1}}, 
 
we're sorry to hear that you've troubles with our product. 
 
Please find attached a video guide with some useful instructions. 
 
When you're facing additional problems, don't hesitate and come back to us.  
````

*Footer:*

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
      "templateId": "instructions",
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
                "url": "http://techslides.com/demos/sample-videos/small.mp4",
                "type": "video"
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
            }
          ]
        }
      ]
    },
    "contentType": "template"
  }
}
````
