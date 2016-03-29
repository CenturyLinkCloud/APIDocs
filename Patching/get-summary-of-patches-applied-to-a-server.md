{{{
  "title": "Get a Summary of All Patches Deployed to a Server",
  "date": "3-14-2016",
  "author": "Benjamin Swoboda",
  "attachments": [],
  "contentIsHTML": false
}}}

This service shows a history of all the patches deployed to a given server.

Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation to get a list of the patches applied to a server using the [Patching-as-a-Service feature](../Patching/apply-patches-to-servers.md).

The response will contain a high-level overview of all the patches installed for each execution and when they were applied.

## URL

### Structure

  GET  https://patching.useast.appfog.ctl.io/rest/servers/{accountAlias}/server/{serverID}/patch

### Example

  GET  https://patching.useast.appfog.ctl.io/rest/servers/ALIAS/server/WA1ALIASSERV0101/patch

### Request

#### URI

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| accountAlias | string | Short code for a particular account | Yes |
| serverId | string | ID of the server | Yes |

### Response

| Name | Type | Description |
| --- | --- | --- |
| execution_id | string | The execution ID associated with a particular patch |
| status | string | Either `pending` or `completed` |
| start_time | date/Time | Either the start time of the entire execution (which contains all initiations) or a particular initiation |
| end_time |  date/Time | Either the end time of the entire execution (which contains all initiations) or a particular initiation |
| init_messages | complex | Shows the quantity of initiations |
| init_begin_message | string | "Invoking SUS API" or "Invoking yum check-update" |
|init_end_mesasge | string | identifies how many updates were installed and the URLS (for Windows) or names of the patches/updates |
