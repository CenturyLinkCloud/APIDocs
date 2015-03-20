{{{
  "title": "Get Anti-Affinity Policy",
  "date": "11-20-2014",
  "author": "Bryan Friedman",
  "attachments": []
}}}

Gets a given anti-affinity policy by ID. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to get the details of a specific anti-affinity policy within a given account.

## URL

### Structure

    GET https://api.ctl.io/v2/antiAffinityPolicies/{accountAlias}/{policyId}

### Example

    GET https://api.ctl.io/v2/antiAffinityPolicies/ALIAS/80a7bf90b199454b859399bff54f4173

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | string | Short code for a particular account | Yes |
| PolicyId | string | ID of the anti-affinity policy being queried. | Yes |

## Response

### Entity Definition

| Name | Type | Description |
| --- | --- | --- |
| id | string | ID of the anti-affinity policy. |
| name | string | Name of the anti-affinity policy. |
| location | string | Data center location of the anti-affinity policy. |
| links | array | Collection of [entity links](../Getting Started/api-v20-links-framework.md) that point to resources related to this policy. |

### Examples

#### JSON

    {
      "id":"80a7bf90b199454b859399bff54f4173",
      "name":"My Anti-Affinity Policy",
      "location":"VA1",
      "links":[
        {
          "rel":"self",
          "href":"/v2/antiAffinityPolicies/alias/80a7bf90b199454b859399bff54f4173",
          "verbs":[
            "GET",
            "DELETE",
            "PUT"
          ]
        },
        {
          "rel":"server",
          "href":"/v2/servers/alias/va1aliashypsc01",
          "id":"va1aliashypsc01",
          "name":"VA1ALIASHYPSC01"
        }
      ]
    }
