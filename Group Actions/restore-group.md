{{{
  "title": "Archive Group",
  "date": "02-27-2015",
  "author": "Bryan Friedman",
  "attachments": []
}}}

Sends the restore operation to an archived group. (See <a href="/knowledge-base/servers/understanding-vm-deployment-options-and-power-states/#archive">Understanding VM Deployment Options and Power States</a> for details on the archive operation.) Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](..Authentication/login.md) for information on acquiring this token.


### When to Use It

Use this API operation when you want to restore an archived group and its groups and servers.

## URL

### Structure

    POST https://api.ctl.io/v2/groups/{accountAlias}/{groupId}/restore

### Example

    POST https://api.ctl.io/v2/groups/ALIAS/wa1-0001/restore

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
      <td>Short code for a particular account.</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>GroupID</td>
      <td>string</td>
      <td>ID of the group to restore. Retrieved from query to parent group, or by looking at the URL on the new UI pages in the Control Portal.</td>
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
      <td>targetGroupId</td>
      <td>string</td>
      <td>The unique identifier of the target group to restore the group to.</td>
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
      <td>isQueued</td>
      <td>boolean</td>
      <td>Boolean indicating whether the operation was successfully added to the queue.</td>
    </tr>
    <tr>
      <td>links</td>
      <td>complex</td>
      <td>Collection of entity links that point to resources related to this group operation.</td>
    </tr>
    <tr>
      <td>errorMessage</td>
      <td>string</td>
      <td>If something goes wrong or the request is not queued, this is the message that contains the details about what happened.</td>
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
      <td>/v2/groups/[ALIAS]/[UUID]?AccountAlias=[ALIAS]&identifier=[UUID]</td>
      <td>Address of the group being restored</td>
    </tr>
  </tbody>
</table>

### Status Link Definition

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
      <td>status</td>
      <td>The link type</td>
    </tr>
    <tr>
      <td>href</td>
      <td>string</td>
      <td>/v2/operations/[ALIAS]/status/[ID]</td>
      <td>Address of the job in the queue</td>
    </tr>
    <tr>
      <td>id</td>
      <td>string</td>
      <td>[ID]</td>
      <td>The identifier of the job in queue. Can be passed to [Get Status](../Queue/get-status.md) call to retrieve status of job.</td>
    </tr>
  </tbody>
</table>

### Examples

#### JSON

    {
      "isQueued":true,
      "links":[
        {
          "rel":"self",
          "href":"/v2/groups/bryf/wa1-0001?AccountAlias=ALIAS&identifier=wa1-0001"
        },
        {
          "rel":"status",
          "href":"/v2/operations/bryf/status/wa1-12345",
          "id":"wa1-12345"
        }
      ]
    }
