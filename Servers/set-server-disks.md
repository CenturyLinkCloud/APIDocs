{{{
  "title": "Set Server CPU/Memory",
  "date": "02-11-2015",
  "author": "Bryan Friedman",
  "attachments": []
}}}

Changes (adds or removes) disks on an existing server. Calls to this operation must include a token acquired from the authentication endpoint. See the <a href="/api-docs/v2#authentication-login">Login API</a> for information on acquiring this token.

### When to Use It

Use this API operation when you want to change the disks on an existing server.

## URL

### Structure

    PATCH https://api.ctl.io/v2/servers/{accountAlias}/{serverId}

### Example

    PATCH https://api.ctl.io/v2/servers/ACCT/WA1ACCTSERV0101

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
      <td>ServerId</td>
      <td>string</td>
      <td>ID of the server with the disk configuration to update. Retrieved from query to containing group, or by looking at the URL when viewing a server in the Control Portal.</td>
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
      <td>patchOperation</td>
      <td>array</td>
      <td>A list of properties, values, and the operations to perform with them for the server.</td>
      <td>Yes</td>
    </tr>
  </tbody>
</table>

### PatchOperation Definition

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
      <td>op</td>
      <td>string</td>
      <td>The operation to perform on a given property of the server. In this case, the value must be "set" for setting the disk configuration.
</td>
    </tr>
    <tr>
      <td>member</td>
      <td>string</td>
      <td>The property of the server to perform the operation on. In this case, the value must be "disks" for setting the disks.</td>
    </tr>
    <tr>
      <td>value</td>
      <td>array</td>
      <td>A list of information for _all disks_ to be on the server including type (raw or partition), size, and path.<br/><br/>_Note: You must specify the complete list of disks to be on the server. If you want to add or resize a disk, specify all existing disks/sizes along with a new entry for the disk to add or the new size of an existing disk. To delete a disk, just specify all the disks that should remain. (You can get existing disk info by using the <a href="/api-docs/v2#servers-get-server">Get Server</a> call to see all the details of the server.)_</td>
    </tr>
  </tbody>
</table>


### Examples

#### JSON

    [
       {
          "op":"set",
          "member":"disks",
          "value":[
             {
               "diskId":"0:0",
               "sizeGB":1
             },
             {
               "diskId":"0:1",
               "sizeGB":2
             },
             {
               "diskId":"0:2",
               "sizeGB":16
             },
             {
               "path":"/extra",
               "sizeGB":"20",
               "type":"partitioned"
             }
          ]  
       }
    ]

## Response

The response is a link to the <a href="/api-docs/v2#queue-get-status">Get Status</a> operation so the asynchronous job can be tracked. Once successfully completed, the server configuration will be changed as specified.

### Entity Definition

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
      <td>Address of the server creation job in the queue</td>
    </tr>
    <tr>
      <td>id</td>
      <td>string</td>
      <td>[ID]</td>
      <td>The identifier of the job in queue. Can be passed to <a href="/api-docs/v2#queue-get-status">Get Status</a> call to retrieve status of job.</td>
    </tr>
  </tbody>
</table>

### Examples

#### JSON

    {
      "rel":"status",
      "href":"/v2/operations/alias/status/wa1-12345",
      "id":"wa1-12345"
    }
