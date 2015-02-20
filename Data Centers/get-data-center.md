{{{
  "title": "Get Data Center Group",
  "date": "5-16-2014",
  "author": "Richard Seroter",
  "attachments": []
}}}

Gets the details of a specific data center the account has access to. Calls to this operation must include a token acquired from the authentication endpoint. See the <a href="/api-docs/v2#authentication-login">Login API</a> for information on acquiring this token.

### When to Use It

Use this API operation when you want to discover the name of the root hardware group for a data center. Once you have that group alias, you can issue a secondary query to retrieve the entire group hierarchy for a given data center.

## URL

### Structure

    GET https://api.tier3.com/v2/datacenters/{accountAlias}/{dataCenter}?groupLinks=true|false

### Example

    GET https://api.tier3.com/v2/datacenters/ALIAS/UC1?groupLinks=true

## Request

### URI and Querystring Parameters

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
      <td>DataCenter</td>
      <td>string</td>
      <td>Short string representing the data center you are querying. Valid codes can be retrieved from the&nbsp;<strong>List Data Centers</strong> API operation.</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>GroupLinks</td>
      <td>boolean</td>
      <td>Determine whether link collections are returned for each group</td>
      <td>No</td>
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

### Group Link Definition

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
      <td>group</td>
      <td>The link type</td>
    </tr>
    <tr>
      <td>href</td>
      <td>string</td>
      <td>/v2/datacenters/[ALIAS]/[DC]</td>
      <td>Address of the root hardware group</td>
      </tr>
    <tr>
      <td>id</td>
      <td>string</td>
      <td>[GROUPID]</td>
      <td>Identifier of the root hardware group</td>
    </tr>
    <tr>
      <td>name</td>
      <td>string</td>
      <td>[GROUP NAME]</td>
      <td>Friendly name of the group</td>
    </tr>
  </tbody>
</table>

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
          "rel": "group",
          "href": "/v2/groups/ALIAS/GROUP123",
          "id": "GROUP123"
        }
      ]
    }
