{{{
  "title": "Get Data Center List",
  "date": "5-16-2014",
  "author": "Richard Seroter",
  "attachments": []
}}}

Gets the list of data centers that a given account has access to. Calls to this operation must include a token acquired from the authentication endpoint. See the <a href="/api-docs/v2#authentication-login">Login API</a> for information on acquiring this token.

### When to Use It

Use this API operation when you need the list of data center names and codes that you have access to. Using that list of data centers, you can then query for the <a href="/api-docs/v2#datacenters-get-data-center-group">root group</a>, and all the child groups in an entire data center.

### Supported HTTP Verbs

Requests to this endpoint are done via HTTP GET.

## URL

### Structure

    https://api.tier3.com/v2/datacenters/{accountAlias}

### Example

    https://api.tier3.com/v2/datacenters/ALIAS

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

### Links Definition

<table style="border: 1px solid gray; border-collapse: collapse;">
<tbody>
<tr>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;" width="100"><strong>&nbsp;</strong></td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;" width="100"><strong>Name</strong></td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;" width="75"><strong>Type</strong></td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;" width="250"><strong>Value</strong></td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;" width="300"><strong>Description</strong></td>
</tr>
<tr>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;" rowspan="2">Self Link</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">rel</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">string</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">self</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">The link type</td>
</tr>
<tr>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">href</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">string</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">/v2/datacenters/[ALIAS]/[DC]</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">Address of the resource itself</td>
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

            }]

        },

        {

        "id": "DC2",

        "name": "DC2 FRIENDLY NAME",

        "links": [

            {

            "rel": "self",

            "href": "/v2/datacenters/ALIAS/DC2"

            }]

        }

    ]