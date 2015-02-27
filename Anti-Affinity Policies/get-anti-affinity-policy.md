{{{
  "title": "Get Anti-Affinity Policy",
  "date": "11-20-2014",
  "author": "Bryan Friedman",
  "attachments": []
}}}

Gets a given anti-affinity policy by ID. Calls to this operation must include a token acquired from the authentication endpoint. See the <a href="/api-docs/v2#authentication-login">Login API</a> for information on acquiring this token.

### When to Use It

Use this API operation when you want to get the details of a specific anti-affinity policy within a given account.

## URL

### Structure

    GET https://api.tier3.com/v2/antiAffinityPolicies/{accountAlias}/{policyId}

### Example

    GET https://api.tier3.com/v2/antiAffinityPolicies/ALIAS/80a7bf90b199454b859399bff54f4173

## Request

### URI Parameters

<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
      <th>Description</th>
      <th>Req.</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>AccountAlias</td>
      <td>string</td>
      <td>Short code for a particular account</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>PolicyId</td>
      <td>string</td>
      <td>ID of the anti-affinity policy being queried.</td>
      <td>Yes</td>
    </tr>
  </tbody>
</table>

## Response

### Entity Definition

<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>id</td>
      <td>string</td>
      <td>ID of the anti-affinity policy.</td>
    </tr>
    <tr>
      <td>name</td>
      <td>string</td>
      <td>Name of the anti-affinity policy.</td>
    </tr>
    <tr>
      <td>location</td>
      <td>string</td>
      <td>Data center location of the anti-affinity policy.</td>
    </tr>
    <tr>
      <td>links</td>
      <td>complex</td>
      <td>Collection of entity links that point to resources related to this policy.</td>
    </tr>
  </tbody>
</table>

### Self Link Definition

<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
      <th>Value</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>rel</td>
      <td>string</td>
      <td>self</td>
      <td>The link type</td>
    </tr>
    <tr>
      <td>href</td>
      <td>string</td>
      <td>/v2/antiAffinityPolicies/[ALIAS]/[POLICYID]</td>
      <td>Address of the resource itself</td>
    </tr>
    <tr>
      <td>verbs</td>
      <td>array</td>
      <td>GET | DELETE | PUT</td>
      <td>Valid HTTP verbs that can act on this resource</td>
    </tr>
  </tbody>
</table>

### Server Link Definition

<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
      <th>Value</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>rel</td>
      <td>string</td>
      <td>server</td>
      <td>The link type</td>
    </tr>
    <tr>
      <td>href</td>
      <td>string</td>
      <td>/v2/servers/[ALIAS]/[SERVERID]</td>
      <td>Address of a server that is part of this policy</td>
    </tr>
    <tr>
      <td>id</td>
      <td>string</td>
      <td>[SERVERID]</td>
      <td>ID of a server that is part of this policy</td>
    </tr>
    <tr>
      <td>name</td>
      <td>string</td>
      <td>[SERVER NAME]</td>
      <td>Name of a server that is part of this policy </td>
    </tr>
  </tbody>
</table>

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
