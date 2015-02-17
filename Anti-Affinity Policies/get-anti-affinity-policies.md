{{{
  "title": "Get Anti-Affinity Policies",
  "date": "11-20-2014",
  "author": "Bryan Friedman",
  "attachments": []
}}}

Gets a list of anti-affinity policies within a given account. Calls to this operation must include a token acquired from the authentication endpoint. See the <a href="/api-docs/v2#authentication-login">Login API</a> for information on acquiring this token.

### When to Use It

Use this API operation when you want to get a list of anti-affinity policies within a given account and what servers are part of these policies. You can also use the IDs provided in this list to add a server to that anti-affinity policy using the API.

### Supported HTTP Verbs

Requests to this endpoint are done via HTTP GET.

## URL

### Structure

    https://api.tier3.com/v2/antiAffinityPolicies/{accountAlias}

### Example

    https://api.tier3.com/v2/antiAffinityPolicies/ALIAS

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
  </tbody>
</table>

## Response

The response will be an array containing one entity for each anti-affinity policy in the given account.

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

### Links Definition

<table style="border: 1px solid gray; border-image: none; border-collapse: collapse;">
<tbody>
<tr>
<td style="padding: 5px; border: 1px solid gray; border-image: none;" width="100"><strong>&nbsp;</strong></td>
<td style="padding: 5px; border: 1px solid gray; border-image: none;" width="100"><strong>Name</strong></td>
<td style="padding: 5px; border: 1px solid gray; border-image: none;" width="75"><strong>Type</strong></td>
<td style="padding: 5px; border: 1px solid gray; border-image: none;" width="250"><strong>Value</strong></td>
<td style="padding: 5px; border: 1px solid gray; border-image: none;" width="300"><strong>Description</strong></td>
</tr>
<tr>
<td style="padding: 5px; border: 1px solid gray; border-image: none;" rowspan="2">Self Link</td>
<td style="padding: 5px; border: 1px solid gray; border-image: none;">rel</td>
<td style="padding: 5px; border: 1px solid gray; border-image: none;">string</td>
<td style="padding: 5px; border: 1px solid gray; border-image: none;">self</td>
<td style="padding: 5px; border: 1px solid gray; border-image: none;">The link type</td>
</tr>
<tr>
<td style="padding: 5px; border: 1px solid gray; border-image: none;">href</td>
<td style="padding: 5px; border: 1px solid gray; border-image: none;">string</td>
<td style="padding: 5px; border: 1px solid gray; border-image: none;">/v2/antiAffinityPolicies/[ALIAS]/[POLICYID]</td>
<td style="padding: 5px; border: 1px solid gray; border-image: none;">Address of the resource itself</td>
</tr>
</tbody>
</table>


<table style="border: 1px solid gray; border-image: none; border-collapse: collapse;">
<tbody>
<tr>
<td style="padding: 5px; border: 1px solid gray; border-image: none;" width="100"><strong>&nbsp;</strong></td>
<td style="padding: 5px; border: 1px solid gray; border-image: none;" width="100"><strong>Name</strong></td>
<td style="padding: 5px; border: 1px solid gray; border-image: none;" width="75"><strong>Type</strong></td>
<td style="padding: 5px; border: 1px solid gray; border-image: none;" width="250"><strong>Value</strong></td>
<td style="padding: 5px; border: 1px solid gray; border-image: none;" width="300"><strong>Description</strong></td>
</tr>
<tr>
<td style="padding: 5px; border: 1px solid gray; border-image: none;" rowspan="4">Server Link</td>
<td style="padding: 5px; border: 1px solid gray; border-image: none;">rel</td>
<td style="padding: 5px; border: 1px solid gray; border-image: none;">string</td>
<td style="padding: 5px; border: 1px solid gray; border-image: none;">server</td>
<td style="padding: 5px; border: 1px solid gray; border-image: none;">The link type</td>
</tr>
<tr>
<td style="padding: 5px; border: 1px solid gray; border-image: none;">href</td>
<td style="padding: 5px; border: 1px solid gray; border-image: none;">string</td>
<td style="padding: 5px; border: 1px solid gray; border-image: none;">/v2/servers/[ALIAS]/[SERVERID]</td>
<td style="padding: 5px; border: 1px solid gray; border-image: none;">Address of a server that is part of this policy</td>
</tr>
<tr>
<td style="padding: 5px; border: 1px solid gray; border-image: none;">id</td>
<td style="padding: 5px; border: 1px solid gray; border-image: none;">string</td>
<td style="padding: 5px; border: 1px solid gray; border-image: none;">[SERVERID]</td>
<td style="padding: 5px; border: 1px solid gray; border-image: none;"><span>ID of a server that is part of this policy</span></td>
</tr>
<tr>
<td style="padding: 5px; border: 1px solid gray; border-image: none;">name</td>
<td style="padding: 5px; border: 1px solid gray; border-image: none;">string</td>
<td style="padding: 5px; border: 1px solid gray; border-image: none;">[SERVER NAME]</td>
<td style="padding: 5px; border: 1px solid gray; border-image: none;"><span>Name of a server that&nbsp;is part of this policy&nbsp;</span></td>
</tr>
</tbody>
</table>

### Examples

#### JSON

    [
      {
        "id":"80a7bf90b199454b859399bff54f4173",
        "name":"My Anti-Affinity Policy",
        "location":"VA1",
        "links":[
          {
            "rel":"self",
            "href":"/v2/antiAffinityPolicies/alias/80a7bf90b199454b859399bff54f4173"
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
            "href":"/v2/antiAffinityPolicies/alias/ca8b07035cf844f3b4f953074c2630eb"
          }
        ]
      }
    ]