# Rich Media Template with document

This is an example request for sending an image a long with a rich media template

The template is defined as

*Header* : 

    Image

*Body* : 

````
Hi {{1}},

we were notified by the shipment partner, that your parcel got damaged (see attached image).

Contact us for a free of charge replacement of your order.
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
                "url": "https://www.publicdomainpictures.net/pictures/70000/velka/parcel-1384599612Lor.jpg",
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
            }
          ]
        }
      ]
    },
    "contentType": "template"
  }
}
````
