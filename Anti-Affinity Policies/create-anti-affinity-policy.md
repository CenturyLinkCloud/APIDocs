{{{
  "title": "Create Anti-Affinity Policy",
  "date": "11-20-2014",
  "author": "Bryan Friedman",
  "attachments": []
}}}

Creates an anti-affinity policy in a given account. Calls to this operation must include a token acquired from the authentication endpoint. See the <a href="/api-docs/v2#authentication-login">Login API</a> for information on acquiring this token.

### When to Use It

Use this API operation when you want to create a new anti-affinity policy within a given account.

## URL

### Structure

    POST https://api.ctl.io/v2/antiAffinityPolicies/{accountAlias}

### Example

    POST https://api.ctl.io/v2/antiAffinityPolicies/ALIAS

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

### Content Properties

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
      <td>name</td>
      <td>string</td>
      <td>Name of the anti-affinity policy.</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>location</td>
      <td>string</td>
      <td>Data center location of the anti-affinity policy.</td>
      <td>Yes</td>
    </tr>
  </tbody>
</table>

### Examples

#### JSON

    {
      "name":"New Anti-Affinity Policy",
      "location":"VA1"
    }

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
  <tbody>
    <tr>
      <td width="100"><strong>Name</strong></td>
      <td width="75"><strong>Type</strong></td>
      <td width="250"><strong>Value</strong></td>
      <td width="300"><strong>Description</strong></td>
    </tr>
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
  </tbody>
</table>

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
