# Button Types

> `postback` button type structure

```json
{
  "type": "postback",
  "title": "Book now",
  "payload": "{\"class\":\"CategoriesListPostback\"}"
}
```
> `web_url` button type structure

```json
{
  "type": "web_url",
  "title": "View website",
  "url": "https://www.fantasticservices.com/"
}
```
Depending on the button type it can perform different function. 

Type             | Meaning
----------       | -------
`postback`       | Button that should return the content of the <code>payload</code> element
`web_url`        | Button that links to a web page
 
 - `postback` 
   - payload - only available with postback button type. When the button is click the client must return the entire contend fot the payload.
 - `web_url` 
   - used to open a web page
