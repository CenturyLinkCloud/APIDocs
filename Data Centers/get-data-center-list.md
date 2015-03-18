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
      <td>Short value representing the data center code</td>
    </tr>
    <tr>
      <td>Name</td>
      <td>string</td>
      <td>Full, friendly name of the data center</td>
    </tr>
    <tr>
      <td>Links</td>
      <td>array</td>
      <td>Collection of entity links that point to resources related to this data center</td>
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
      <td>/v2/datacenters/[ALIAS]/[DC]</td>
      <td>Address of the resource itself</td>
    </tr>
  </tbody>
</table>

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
