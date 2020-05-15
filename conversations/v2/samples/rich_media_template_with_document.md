# Rich Media Template with document

This is an example request for sending a document together with a rich media template

The template is defined as

*Header* : 

    Document

*Body* : 

````
Hi {{1}}!

Please show the attached voucher when you arrive at the hotel {{2}}.

Your tyntec travel team
````

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
      "templateId": "checkin_voucher",
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
                "url": "https://www.tyntec.com/sites/default/files/uploads/1608_tyntec_CorporateBackground.pdf",
                "type": "document",
                "filename": "tyntec background.pdf"
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
              "text": "tyntec 5 stars"
            }
          ]
        }
      ]
    },
    "contentType": "template"
  }
}
````

The message would look like this on the device

![](sample-document-template.png)
