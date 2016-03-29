{{{
  "title": "Get Details of Patches Applied to a Server During a Single Execution",
  "date": "3-14-2016",
  "author": "Benjamin Swoboda",
  "attachments": [],
  "contentIsHTML": false
}}}

This services returns details on all attempted patches for a single execution against a server.

Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation to get a list of the patches applied for a given execution to a server using the [Patching-as-a-Service feature](../Patching/apply-patches-to-servers.md).

The response will contain information from the vendor about the patch and the status of the attempt.

## URL

### Structure

  GET https://patching.useast.appfog.ctl.io/rest/servers/{alias}/server/{serverID}/patch/{execution_id}

### Example

  GET https://patching.useast.appfog.ctl.io/rest/servers/OSD/server/VA1OSDPATCH33/patch/VA1-132457

## Request

### URI

| Name | Type | Description |
 --- | --- | ---
| accountAlias | string | Short code for a particular account |
| serverID | string | ID of the server |
| execution_id | string | Correlation ID for all the patches included with a single update execution, obtained from the Patch Summary response or emails regarding a patch request. The execution ID format will be aa#-###### |

## Response

| Name | Type | Description |
| --- | --- | --- |
| execution_id | string | The execution ID associated with a particular patch
| status | string | Either `pending` or `completed` |
| start_time | dateTime | When this value is superior to patches, indicates the start time of the entire execution (which contains all initiations). When this value is inferior to patches, indicates the start time of the patch. |
| end_time |  dateTime | When this value is superior to patches, indicates the end time of the entire execution (which contains all initiations). When this value is inferior to patches, indicates the end time of the patch. |
| duration | string | The minutes and seconds between the start and end time |
| begin_message | string | "Update Process BEGIN" |
| end_message | string | "Updating Complete" |
| patches | Number | Quantity of patches installed |
| patch_begin_message | string | Identifies the Software or OS updated and the reference number (if Windows, KB#######) for that particular update |
| patch_end_message | string | Result code established by Microsoft, defining the possible results of an install. These same codes will be used for other Operating Systems as well. https://msdn.microsoft.com/en-us/library/windows/desktop/aa387095(v=vs.85).aspx |
| status | string | Status of an individual patch, either pending, completed, or failed |
