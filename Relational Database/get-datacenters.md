{{{
  "title": "Get Datacenters",
  "date": "04-05-2015",
  "author": "Relational Database Services",
  "attachments": []
}}}

Get a list of datacenters providing RDBS subscriptions. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation to identify datacenters that you may create subscriptions in. You will use the `dataCenter` response attribute in create subscription requests.

## URL

### Example

    GET https://api.rdbs.ctl.io/v1/datacenters

## Response

### Entity Definition

| Name | Type | Description |
| --- | --- | --- |
| dataCenter | string | Short string representing the data center. |
| friendlyName | string | Name of the datacenter. |
| active | boolean | Is the datacenter accepting new subscriptions. |

#### JSON

```json
[
  {
    "dataCenter": "UC1",
    "friendlyName": "UC1 - US West (Santa Clara)",
    "active": true
  },
  {
    "dataCenter": "VA1",
    "friendlyName": "VA1 - US East (Sterling)",
    "active": true
  }
]
```
