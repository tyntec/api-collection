# Sending bulk messages

This is an example request for sending bulk messages.

Bulk messages are multiple messages sent, in order, to one user from one sender.

Every channel supported by Chat API is also supported on the bulk messaging

The matching POST request on https://api.tyntec.com/chat-api/v2/bulks would look like this

````
{
  "from": "{{whatsappPhoneNumber}}",
  "to": "{{toPhoneNumber}}",
  "channel": "whatsapp",
  "whatsapp": [
    {
      "contentType": "text",
      "text": "Hi! I'm the first bulk message"
    },
    {
      "contentType": "location",
      "location": {
        "longitude": 0.1,
        "latitude": 0.2
      },
      "name": "with location"
    },
    {
      "media": {
        "type": "image",
        "url": "https://www.pngitem.com/pimgs/m/185-1850014_free-sample-hd-png-download.png",
        "caption": "and media"
      },
      "contentType": "media"
    }
  ]
}
````

The message would look like this on the device

![Sticker message](/conversations/v2/samples/sample-image-whatsapp-bulk_messages.jpg)
