{{{
  "title": "CreateAccount",
  "date": "01-18-2015",
  "author": "Author Name",
  "attachments": [],
  "related_products": [],
  "related_questions": [],
  "preview" : "",
  "contentIsHTML": false
}}}

Create a brand new (sub) account in the CenturyLink Cloud system. Calls to this operation must include an authorization cookie acquired from the Logon operation.

## URL

<div class="kb-api-urls">
  <div class="kb-api-urls-inner">
    <p>REST: <span class="url">https://api.tier3.com/REST/Account/CreateAccount/</span><format> (format =  XML | JSON)</p>
    <p>SOAP: http://...</p>
  </div>
</div>


## Request
### Attributes

| Name         | Type   | Description                                                                      | Req. |
|--------------|--------|----------------------------------------------------------------------------------|------|
| ParentAlias  | String | Account alias of the parent account                                              | Yes  |
| AccountAlias | String | New, four character account alias. If left empty, one is automatically generated | No   |
| Location     | String | Account alias of the parent account                                              | Yes  |

## Examples

