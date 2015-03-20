{{{
  "title": "Get Anti-Affinity Policies",
  "date": "11-20-2014",
  "author": "Bryan Friedman",
  "attachments": []
}}}

Gets a list of anti-affinity policies within a given account. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to get a list of anti-affinity policies within a given account and what servers are part of these policies. You can also use the IDs provided in this list to add a server to that anti-affinity policy using the API.

## URL

### Structure

    GET https://api.ctl.io/v2/antiAffinityPolicies/{accountAlias}

### Example

    GET https://api.ctl.io/v2/antiAffinityPolicies/ALIAS

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | string | Short code for a particular account | Yes |

## Response

The response will be an array containing one entity for each anti-affinity policy in the given account.

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
      "items":[
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
        },
        {
          "id":"ca8b07035cf844f3b4f953074c2630eb",
          "name":"My Other Anti-Affinity Policy",
          "location":"WA1",
          "links":[
            {
              "rel":"self",
              "href":"/v2/antiAffinityPolicies/alias/ca8b07035cf844f3b4f953074c2630eb",
              "verbs":[
                "GET",
                "DELETE",
                "PUT"
              ]
            }
          ]
        }
      ],
      "links":[
        {
          "rel":"self",
          "href":"/v2/antiAffinityPolicies/alias",
          "verbs":[
            "GET",
            "POST"
          ]
        }
      ]
    }
