{{{
  "title": "Get Csv Restore Jobs Report",
  "date": "07-02-2018",
  "author": "Jon Tait",
  "attachments": [],
  "sticky": "false"
}}}

Gets an up-to-date list of all restore jobs performed, including a summary for each. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want a list of all the restores performed and summary for each.

## URL

### Structure

    GET https://api.backup.ctl.io/clc-backup-api/api/csv/restoreJobsReport

### Example

    GET https://api.backup.ctl.io/clc-backup-api/api/csv/restoreJobsReport

## Response

content-type: text/plain, content-disposition: attachment

Note for "Anywhere Servers" in this report: the "Server Id" column will contain the friendly name given to the server, next a colon delimiter, and finally the reference id for the anywhere server record

### Examples

#### CSV

      Server Id,Server Policy Id,Restore Point Id,Storage Region,Restore Status,Restore Start Time,Restore Latest Progress Time,Restore Finished Time,Protected Data Bytes Restored,Protected Data Bytes Failed To Restore,Number Of Critical Errors,Files Transferred From Storage,Bytes Transferred From Storage,Files Failed Transfer From Storage,Files Failed Transfer From Storage Due To S3 Throttling,Files Failed Transfer From Storage Due To S3 Unavailable,Files Failed Applying Attributes,Directories Restored,Directories Failed To Restore,Number Of Messages,Messages
      testServerId20180627014200,8903f6d9-40de-47f9-9d2a-9b0dee4f141f,362bef22-e386-4a17-b10c-ae5a4a482a95,CANADA,IN_PROGRESS,2018-06-27T01:42:05.187Z,2018-06-27T01:42:05.641Z,,0,0,0,0,0,0,0,0,0,0,0,0,
      testServerId20180627014130,cc573c6e-aafa-4dc1-956b-4707b7cc8d58,1c11515f-9199-42f0-8602-a83a69657a9e,CANADA,SUCCESS,2018-06-27T01:41:34.978Z,2018-06-27T01:41:35.396Z,2018-06-27T01:41:34.979Z,37188,0,0,345,34688,0,0,0,0,0,0,0,
