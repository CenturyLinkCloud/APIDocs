{{{
  "title": "Lorem Ipsum",
  "date": "01-18-2015",
  "author": "Author Name",
  "attachments": [],
  "related_products": [],
  "related_questions": [],
  "preview" : "",
  "contentIsHTML": false
}}}

This is a description and summary of the what this API endpoint provides, and how best to interface with the endpoint. It will also state if an authorization cookie is required.

## URL

<div class="kb-api-urls">
  <div class="kb-api-urls-inner">
    <p>REST: <span class="url"><code>https://api.tier3.com/REST/DomainName/Overview/</code></span>&lt;format&gt;</p>
    <p>SOAP: <span class="url"><code>https://api.tier3.com/SOAP/DomainName/Overview/</code></span></p>
  </div>
</div>

```
REST: https://api.tier3.com/REST/DomainName/Overview/
```


## Request
### Attributes

| Name         | Type   | Description                                                                      | Req. |
|--------------|--------|----------------------------------------------------------------------------------|------|
| AttributeName1 | String | Description of the attributes                                                   | Yes  |
| AttributeName2 | String | Attributes descriptions can sometime be a couple sentence. This is an example of that. | No   |
| AttributeName3 | String | Attributes description.                                      | Yes  |


## Examples

<div class="panel--pre-code panel--pre-code--with-page-numbers">

  <div>
    <a data-toggle="tab" data-target="#2-1-0" class="active">XML</a>
    <a data-toggle="tab" data-target="#2-1-1">JSON</a>
  </div>

  <div class="tab-content">
    <div class="tab-pane active" id="2-1-0">
      <pre>
        <code>
          &lt;LogonResponse Success="true" Message="Login Successful" StatusCode="0" /&gt;
        </code>
      </pre>
    </div>
    <div class="tab-pane" id="2-1-1">
      <pre>
        <code>
{

  "Success":true,

  "Message":"Login Successful",

  "StatusCode":0

}
        </code>
      </pre>
    </div>
</div></div>