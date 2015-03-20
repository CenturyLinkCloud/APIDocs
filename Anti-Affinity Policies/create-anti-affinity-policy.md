{{{
  "title": "Create Anti-Affinity Policy",
  "date": "11-20-2014",
  "author": "Bryan Friedman",
  "attachments": []
}}}

Creates an anti-affinity policy in a given account. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to create a new anti-affinity policy within a given account.

## URL

### Structure

    POST https://api.ctl.io/v2/antiAffinityPolicies/{accountAlias}

### Example

    POST https://api.ctl.io/v2/antiAffinityPolicies/ALIAS

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | string | Short code for a particular account | Yes |

### Content Properties

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| name | string | Name of the anti-affinity policy. | Yes |
| location | string | Data center location of the anti-affinity policy. | Yes |

### Examples

#### JSON

    {
      "name":"New Anti-Affinity Policy",
      "location":"VA1"
    }

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

      "id":"80a7bf90b459454b859399aef54f4173",
      "name":"New Anti-Affinity Policy",
      "location":"VA1",
      "links":[
        {
          "rel":"self",
          "href":"/v2/antiAffinityPolicies/alias/80a7bf90b459454b859399aef54f4173"
        }
      ]
    }
