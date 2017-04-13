# Templates

> Start chat template:

```json
{
  "data": [
    {
      "chat_id": "hash",
      "state": "auto",
      "event_type": "template",
      "template_type": "generic",
      "elements": [
        {
          "title": "Fantastic Services",
          "subtitle": "The One-Stop Shop for All Home Services",
          "image_url": "https://files.dxr.cloud/ShmtDmH6fi6HbIcxsAOUkj9L2Jc41cropp8WdVLWtOfgj0iNvZkfESwzgsOl",
          "buttons": [
            {
              "type": "postback",
              "title": "Book now",
              "payload": "{\"class\":\"CategoriesListPostback\"}"
            },
            {
              "type": "postback",
              "title": "Help",
              "payload": "HelpPostback"
            },
            {
              "type": "web_url",
              "title": "View website",
              "url": "https://www.fantasticservices.com/"
            }
          ]
        }
      ]
    }
  ],
  "success": [
    {
      "code": 1020,
      "message": "Chat session started"
    }
  ],
  "meta": {
    "db_version": 25,
    "latest_build": 27
  }
}
```

> Generic template:
 
 ```json
{
  "data": [
    {
      "template_type": "generic",
      "state": "auto",
      "elements": [
        {
          "title": "Fantastic Services",
          "subtitle": "The One-Stop Shop for All Home Services",
          "item_url": "",
          "image_url": "https://files.dxr.cloud/ShmtDmH6fi6HbIcxsAOUkj9L2Jc41cropp8WdVLWtOfgj0iNvZkfESwzgsOl",
          "buttons": [
            {
              "type": "postback",
              "title": "Book now",
              "payload": "{\"class\":\"CategoriesListPostback\"}"
            },
            {
              "type": "postback",
              "title": "Help",
              "payload": "HelpPostback"
            },
            {
              "type": "web_url",
              "title": "View website",
              "url": "https://www.fantasticservices.com/"
            }
          ]
        }
      ]
    }
  ]
}
 ```
 
 > Button template:
 
 ```json
{
  "data": [
    {     
      "chat_id": "hash",
      "state": "auto",
      "event_type": "template",
      "template_type": "button",
      "elements": [
        {
          "title": "Bedroom(s) Flat",
          "buttons": [
            {
              "type": "postback",
              "title": 1,
              "payload": "{\"class\":\"ChoiceViewQuestionPostback\",\"choiceViewId\":33,\"objectId\":85,\"selectedValue\":1}"
            },
            {
              "type": "postback",
              "title": 2,
              "payload": "{\"class\":\"ChoiceViewQuestionPostback\",\"choiceViewId\":33,\"objectId\":85,\"selectedValue\":2}"
            }
          ]
        }
      ]
    }
  ]
}
 ```
 
 **Start chat visualization**
     [![N|GetStartedVisual](http://files.dxr.cloud/bOW1wle4gbUEmlBQuWyIV8J9CT2PtNXJFF7PycI74TepOKGbJi9n5Ils2WuS)](http://files.dxr.cloud/bOW1wle4gbUEmlBQuWyIV8J9CT2PtNXJFF7PycI74TepOKGbJi9n5Ils2WuS)
 **Generic visualization** 
     [![N|CategoriesListVisualization](http://files.dxr.cloud/lkiAQMSO4fi1CaQHNrrzucSvuGdD7ZDvXFEE09qFyiOoGkOHUkpJeeERZMWy)](http://files.dxr.cloud/lkiAQMSO4fi1CaQHNrrzucSvuGdD7ZDvXFEE09qFyiOoGkOHUkpJeeERZMWy)
 **Button visualization**
     [![N|ButtonVisualization](http://files.dxr.cloud/vtm0Rh3cifR7fPjAl6v238atPGj12AjOn95jD67op52gaPL7gejhWvHNKNxn)](http://files.dxr.cloud/vtm0Rh3cifR7fPjAl6v238atPGj12AjOn95jD67op52gaPL7gejhWvHNKNxn)
