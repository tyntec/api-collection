# Sending Stickers with WhatsApp

This is an example request for sending a sticker via WhatsApp

The matching request would look like this

````
{
  "to": "12331132",
  "channels": [
    "whatsapp"
  ],
  "whatsapp": {
    "from": "1233423454",
    "contentType": "media",
    "media": {
      "type": "sticker",
      "url": "https://www.gstatic.com/webp/gallery/1.webp"
    }
  }
}
````

The message would look like this on the device

![Sticker message](/chat-api/v2/samples/sample-image-whatsapp-sticker.jpg)
