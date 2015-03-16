{{{
  "title": "Get Group Billing Details",
  "date": "10-13-2014",
  "author": "Richard Seroter",
  "attachments": []
}}}

Gets the current and estimated charges for each server in a designated group hierarchy. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](..Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to find out the charges associated with a specific group.

## URL

### Structure

    GET https://api.ctl.io/v2/groups/{accountAlias}/{groupId}/billing

### Example

    GET https://api.ctl.io/v2/groups/ALIAS/wa1-5030/billing

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
      <td>GroupID</td>
      <td>string</td>
      <td>ID of the group being queried. Retrieved from query to parent group, or by looking at the URL on the new UI pages in the Control Portal</td>
      <td>Yes</td>
    </tr>
  </tbody>
</table>

## Response

### Group Entity Definition

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
      <td>date</td>
      <td>datetime</td>
      <td>Date that this billing information applies to</td>
    </tr>
    <tr>
      <td>Groups</td>
      <td>array</td>
      <td>List of groups (with the first being the queried group) in the requested hierarchy.
        <br />Group ID listed before each group entity description</td>
    </tr>
  </tbody>
</table>

### Groups Definition

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
      <td>name</td>
      <td>string</td>
      <td>User-defined name of the group</td>
    </tr>
    <tr>
      <td>servers</td>
      <td>array</td>
      <td>Collection of servers in this group, each with billing information.
        <br />Server ID listed before each entity description</td>
    </tr>
  </tbody>
</table>

### Servers Definition

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
      <td>templateCost</td>
      <td>float</td>
      <td>Cost of templates stored in the group</td>
    </tr>
    <tr>
      <td>archiveCost</td>
      <td>float</td>
      <td>Cost of archived servers in this group</td>
    </tr>
    <tr>
      <td>monthlyEstimate</td>
      <td>float</td>
      <td>Projected charges for the servers given current usage</td>
    </tr>
    <tr>
      <td>monthToDate</td>
      <td>float</td>
      <td>Charges up until the requested time</td>
    </tr>
    <tr>
      <td>currentHour</td>
      <td>float</td>
      <td>Charges for the most recent hour</td>
    </tr>
  </tbody>
</table>

### Examples

#### JSON

    {
      "date": "2014-04-07T21:33:51.9743015Z",
      "groups": {
        "wa1-0003": {
          "name": "Web Applications",
          "servers": {
            "wa1acctserv7101": {
              "templateCost": 0.0,
              "archiveCost": 0.0,
              "monthlyEstimate": 77.76,
              "monthToDate": 17.93,
              "currentHour": 0.108
            },
            "wa1acctserv7202": {
              "templateCost": 0.0,
              "archiveCost": 0.0,
              "monthlyEstimate": 156.96,
              "monthToDate": 36.19,
              "currentHour": 0.218
            }
          }
        },
        "wa1-0004": {
          "name": "Training Environment",
          "servers": {}
        }
      }
    }
