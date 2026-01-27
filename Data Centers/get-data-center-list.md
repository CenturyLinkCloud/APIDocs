{{{
  "title": "Get Data Center List",
  "date": "5-16-2014",
  "author": "Richard Seroter",
  "attachments": []
}}}

Gets the list of data centers that a given account has access to. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you need the list of data center names and codes that you have access to. Using that list of data centers, you can then query for the [root group](get-data-center.md), and all the child groups in an entire data center.

## URL

### Structure

    GET https://api.ctl.io/v2/datacenters/{accountAlias}

### Example

    GET https://api.ctl.io/v2/datacenters/ALIAS

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | string | Short code for a particular account | Yes |

## Response

### Entity Definition

| Name | Type | Description |
| --- | --- | --- |
| id | string | Short value representing the data center code |
| name | string | Full, friendly name of the data center |
| links | array | Collection of [entity links](../Getting Started/api-v20-links-framework.md) that point to resources related to this data center |

### Examples

#### JSON

    [
      {
        "id": "DC1",
        "name": "DC FRIENDLY NAME",
        "links": [
          {
            "rel": "self",
            "href": "/v2/datacenters/ALIAS/DC1"
          }
        ]
      },
      {
        "id": "DC2",
        "name": "DC2 FRIENDLY NAME",
        "links": [
          {
            "rel": "self",
            "href": "/v2/datacenters/ALIAS/DC2"
          }
        ]
      }
    ]
