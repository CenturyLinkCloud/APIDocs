{{{
  "title": "Get Data Center",
  "date": "5-16-2014",
  "author": "Richard Seroter",
  "attachments": []
}}}

Gets the details of a specific data center the account has access to. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to discover the name of the root hardware group for a data center. Once you have that group alias, you can issue a secondary query to retrieve the entire group hierarchy for a given data center.

## URL

### Structure

    GET https://api.ctl.io/v2/datacenters/{accountAlias}/{dataCenter}?groupLinks=true|false

### Example

    GET https://api.ctl.io/v2/datacenters/ALIAS/UC1?groupLinks=true

## Request

### URI and Querystring Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | string | Short code for a particular account | Yes |
| DataCenter | string | Short string representing the data center you are querying. Valid codes can be retrieved from the [Get Data Center List](get-data-center.md) API operation. | Yes |
| GroupLinks | boolean | Determine whether link collections are returned for each group | No |

## Response

### Entity Definition

| Name | Type | Description |
| --- | --- | --- |
| id | string | Short value representing the data center code |
| name | string | Full, friendly name of the data center |
| links | array | Collection of [entity links](../Getting Started/api-v20-links-framework.md) that point to resources related to this data center |

### Examples

#### JSON

    {
      "id": "DC1",
      "name": "DC FRIENDLY NAME",
      "links": [
        {
          "rel": "self",
          "href": "/v2/datacenters/ALIAS/DC1"
        },
        {
          "rel":"group",
          "href":"/v2/groups/ALIAS/54faef9c2bfd41d6b30f787567f9b0d4",
          "id":"54faef9c2bfd41d6b30f787567f9b0d4",
          "name":"DC1 Hardware"
        }
      ]
    }
