{{{
  "title": "API Introduction",
  "date": "01-18-2015",
  "author": "Author Name",
  "attachments": [],
  "related_products": [],
  "related_questions": [],
  "preview" : "",
  "contentIsHTML": false
}}}

Below you will find a current list of the available methods on our CenturyLink Cloud API. If you need help or support, please head over to our Knowledge Base or Getting Started pages.

The calling conventions for the REST API is to send a POST request to the URL of the given method (e.g.  https://api.tier3.com/rest/VirtualServer/CreateServer/FORMAT   where FORMAT is either XML or JSON). In addition, the content type of the HTTP request must be set as well to either "text/xml" for XML requests, or "application/json; charset=utf-8" for JSON requests. The combination of the format node and the Content Type will determine how the request is interpreted as well as control what format the responses are returned.

The SOAP based API supports the same features as the REST API, and while the request and response messages are essentially identical to those of the REST API, you will want to pull down the WSDL for each API to verify the details. URL's to each API's SOAP WSDL can be found on the individual API pages.

All requests will receive a response (in either JSON or XML format) with at least the following three attributes:


### Attributes

| Name         | Type   | Description                                                                      | Req. |
|--------------|--------|----------------------------------------------------------------------------------|------|
| ParentAlias  | String | Account alias of the parent account                                              | Yes  |
| AccountAlias | String | New, four character account alias. If left empty, one is automatically generated | No   |
| Location     | String | Account alias of the parent account                                              | Yes  |


Many API calls will also return additional information which will be described in detail.

h1 hello
h1
  hello


<pre class="code-panel">
```
{
  t: t,
  t: t,
}
```
</pre>




<span class="code-panel">
  ### Examples
  #### JSON
  ```
  {
    t: t,
    t: t,
  }
  ```
  #### XML
  ```
  <sdsds>s</sdsds>
  ```
</span>




