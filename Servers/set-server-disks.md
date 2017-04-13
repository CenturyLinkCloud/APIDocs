{{{
  "title": "Set Server Disks",
  "date": "02-11-2015",
  "author": "Bryan Friedman",
  "attachments": []
}}}

Changes (adds or removes) disks on an existing server. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to change the disks on an existing server.

## URL

### Structure

    PATCH https://api.ctl.io/v2/servers/{accountAlias}/{serverId}

### Example

    PATCH https://api.ctl.io/v2/servers/ACCT/WA1ACCTSERV0101

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | string | Short code for a particular account | Yes |
| ServerId | string | ID of the server with the disk configuration to update. Retrieved from query to containing group, or by looking at the URL when viewing a server in the Control Portal. | Yes |


### Content Properties

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| patchOperation | array | A list of properties, values, and the operations to perform with them for the server. | Yes |

### PatchOperation Definition

| Name | Type | Description |
| --- | --- | --- |
| op | string | The operation to perform on a given property of the server. In this case, the value must be "set" for setting the disk configuration. |
| member | string | The property of the server to perform the operation on. In this case, the value must be "disks" for setting the disks. |
| value | array | A list of information for _all disks_ to be on the server including type (raw or partition), size, and path.<br/><br/>_Note: You must specify the complete list of disks to be on the server. If you want to add or resize a disk, specify all existing disks/sizes along with a new entry for the disk to add or the new size of an existing disk. To delete a disk, just specify all the disks that should remain. (You can get existing disk info by using the [Get Server](get-server.md) call to see all the details of the server.)_ |


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
			   "type":"raw"
             },
             {
               "diskId":"0:1",
               "sizeGB":2
			   "type":"raw"
             },
             {
               "diskId":"0:2",
               "sizeGB":16
			   "type":"raw"
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

The response is a link to the [Get Status](../Queue/get-status.md) operation so the asynchronous job can be tracked. Once successfully completed, the server configuration will be changed as specified.

### Entity Definition

|Name|Type|Value|Description|
|---|---|---|---|
|rel|string|status|The link type|
|href|string|/v2/operations/[ALIAS]/status/[ID]|Address of the job in the queue|
|id|string|[ID]|The identifier of the job in queue. Can be passed to [Get Status](../Queue/get-status.md) call to retrieve status of job.|

### Examples

#### JSON

    {
      "rel":"status",
      "href":"/v2/operations/alias/status/wa1-12345",
      "id":"wa1-12345"
    }
