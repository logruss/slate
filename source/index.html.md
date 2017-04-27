---
title: Chat API Reference

language_tabs:
  - json
  - shell

toc_footers:
  - <a href='#'>First Online Solutions</a>

includes:
  - templates
  - event_types
  - button_types
  - errors

search: true
---

# Introduction

## Environments

- `LIVE` - api.fantasticservices.com
- `STAGE` - middlepoint-stg.1dxr.com
- `DEV` - middlepoint-dev.1dxr.com

In this document `{{BASE_URL}}` is used as a placeholder for current environment.

## Namespaces

Namespace is added after version.

- GLOBAL FOR SYSTEM - **/system**

Example:

http://`{{BASE_URL}}`/v2/**system**

In this document namespace is included in examples.

## Applications identifying tokens

To access API all request must include identifying token header field.

> X-Application: `{{APPLICATION_TOKEN}}`

<aside class="notice">You must replace {{APPLICATION_TOKEN}} with your personal APP token.</aside>

# Communication Protocol

## Requests
All requests to the API have `path` component. 
It’s used to access resources and actions. 

<aside class="notice">All requests must be of type application/json</aside>
 
 Accepted request `methods` are:

- `POST`

Example requests URL: http://`{{BASE_URL}}`/v2/[system](#namespaces)/chat

## Response

> Response structure

```json
{
  "data": [],
  "success": [
    {
      "code": 1020,
      "message": "Message received",
      "debug_message": "message text missing.",
      "debug_id": 213124
    }
  ],
  "meta": {
    "db_version": 25,
    "latest_build": 27
  }
}
```

All responses are with HTTP status 200 and contain `data` and `meta` parameters. 
Optionally there can be success, error and warning parameters.

Parameter                   | Type    | Description
---------                   | ------- | -----------
data                        | array   | Array of data objects returned in the result of the request
success, warning, error     | array   | Messages with information for the request. More than one type of message can be returned in a response. success and error can’t come in the same response. warning can be combined with success or error.
meta                        | object  | Parameter containing information for the system.

## Events
There are `event_type` to identify the chat requests:

- `start_chat` - indicates that a new chat session is starting 

# Chat
## Start chat

> Example events request structure from chat server:

```json
{
  "events": [
    {
      "chat_id": "hash",
      "event_type": "start_chat",
      "data": {
        "name": "John Smith",
        "email": "john.smith@example.com",
        "phone": "+4400000000000"
      }
    }
  ],
  "meta": {
      "operator_available": true
    }
}
```

```shell
curl -X POST \
  {{BASE_URL}}/v2/system/chat \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/json' \
  -H 'postman-token: 05f4290c-7075-3edc-190a-71b96c1c266e' \
  -d '{
  "events": [
    {
      "chat_id": "hash",
      "event_type": "start_chat",
      "data": {
        "name": "John Smith",
        "email": "john.smith@example.com",
        "phone": "+4400000000000"
      }
    }
  ]
}'
```

> Structure that will be send to the chat server:

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

<b>Request parameters</b>

Parameter                  | Type    | Description
---------                  | ------- | -----------
[event_type](#event-types) | string  | Type of the event (**required**)
chat_id                    | string  | Id of the initialized chat (**required**)
name                       | string  | Client name if available (**optional**)
email                      | string  | Client email if available (**optional**)
phone                      | string  | Client phone if available (**optional**)

<b>Response parameters</b>

Parameter                        | Type    | Description
---------                        | ------- | -----------
[event_type](#event-types)       | string  | Type of the event 
[template_type](#template-types) | string  | Type of the template to use
state                            | string  | It can be either auto or manual
title                            | string  | Display in bold bellow the image_url
subtitle                         | string  | Display bellow the title
image_url                        | string  | Display on top if available
[buttons](#button-types)         | array   | Array of button objects

**Response visualization**

[![N|GetStartedVisual](http://files.dxr.cloud/bOW1wle4gbUEmlBQuWyIV8J9CT2PtNXJFF7PycI74TepOKGbJi9n5Ils2WuS)](http://files.dxr.cloud/bOW1wle4gbUEmlBQuWyIV8J9CT2PtNXJFF7PycI74TepOKGbJi9n5Ils2WuS)

## Postback request 

> Events request structure from chat server:

```json
{
  "events": [
    {
      "chat_id": "hash",
      "event_type": "postback",
      "data": {
        "payload": "{\"class\":\"CategoriesListPostback\"}"
      }
    }
  ],
  "meta": {
    "operator_available": true
  }
}
```

```shell
curl -X POST \
  {{BASE_URL}}/v2/system/chat \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/json' \
  -H 'postman-token: d87ac2ec-9ff4-d28b-e08f-f1cf1b7abfe8' \
  -d '{
  "events": [
    {
      "chat_id": "1231231231",
      "event_type": "postback",
      "data": {
        "payload": "{\"class\":\"CategoriesListPostback\"}"
      }
    }
  ]
}'
```

> Structure that will be send to the chat server:

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
          "title": "Cleaning",
          "subtitle": "Get a quote from Fantastic Services for home & office cleaning in London & UK!",
          "item_url": "",
          "image_url": "http://dev.fantasticxrm.com/data/uploads/uploaded_images/u7hwb8atld.png",
          "buttons": [
            {
              "type": "postback",
              "title": "Book now",
              "payload": "{\"class\":\"ServicesListPostback\", \"categoryId\":70}"
            }
          ]
        },
        {
          "title": "Handyman & Tradesman",
          "subtitle": "Handyman short description",
          "item_url": "",
          "image_url": "http://dev.fantasticxrm.com/data/uploads/uploaded_images/yj3yeecnyk.png",
          "buttons": [
            {
              "type": "postback",
              "title": "Book now",
              "payload": "{\"class\":\"ServicesListPostback\", \"categoryId\":72}"
            }
          ]
        }
      ]
    }
  ],
  "success": [
    {
      "code": 1020,
      "message": "Postback successfull."
    }
  ],
  "meta": {
    "db_version": 25,
    "latest_build": 27
  }
}
```
<aside class="warning">Any template that has payload need to send Postback request back to the server</aside>

When the [event_type](#event-types) is **postback** in most cases a button needs to be clicked.
When that button is clicks the content of **data.payload** needs to be **POST back** to the server.
 

## Regular message

> Events request structure from chat server:

```json
{
  "events": [
    {
      "chat_id": "hash",
      "event_type": "message",
      "data": {
        "text": "Hello"
      }
    }
  ],
  "meta": {
    "operator_available": true
  }
}
```

```shell
curl -X POST \
  {{BASE_URL}}/v2/system/chat \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/json' \
  -H 'postman-token: 05345cc4-2927-ac96-11f9-4caa6cc562d5' \
  -d '{
  "events": [
    {
      "chat_id": "ha123123sh",
      "event_type": "message",
      "data": {
        "text": "Hello"
      }
    }
  ]
}'
```

> Response:

```json
{
  "data": [],
  "success": [
    {
      "code": 1020,
      "state": "auto",
      "message": "Message received",
      "debug_message": "message text missing.",
      "debug_id": 213124
    }
  ]
}
```

> Structure that will be send to the chat server with separate request

```json
{
  "data": [
    {
      "chat_id": "hash",
      "state": "auto",
      "event_type": "message",
      "elements": [
        {
          "text": "Hello"
        }
      ]
    }
  ]
}
```

When the [event_type](#event-types) is **message** a regular text message is displayed to the client.


## Buttons

> Events request structure from chat server:

```json
{
  "events": [
    {
      "chat_id": "hash",
      "event_type": "postback",
      "data": {
        "payload": "{\"class\":\"BottonExamplePostback\"}"
      }
    }
  ],
  "meta": {
    "operator_available": true
  }
}
```

> Structure that will be send to the chat server:

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

Look at [templates](#templates) on how buttons are displayed.