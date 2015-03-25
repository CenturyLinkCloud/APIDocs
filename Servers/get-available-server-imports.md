{{{
  "title": "Get Available Server Imports",
  "date": "03-24-2015",
  "author": "Bryan Friedman",
  "attachments": []
}}}

Gets the list of available servers that can be imported. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to get the list of available OVFs that can be imported with the [Import Server](import-server.md) API. These OVFs are ones that have been uploaded to your FTP server as described in [Using Self-Service VM Import](http://www.centurylinkcloud.com/knowledge-base/servers/using-self-service-vm-import/).

## URL

### Structure

    GET https://api.ctl.io/v2/vmImport/{accountAlias}/available

### Example

    GET https://api.ctl.io/v2/vmImport/ALIAS/available

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | string | Short code for a particular account | Yes |

## Response

The response is an array of available servers for import. The list of available servers is dependent upon what OVFs have been uploaded to your FTP server as described in [Using Self-Service VM Import](http://www.centurylinkcloud.com/knowledge-base/servers/using-self-service-vm-import/).

### Entity Definition

| Name | Type | Description |
| --- | --- | --- |
| id | string | ID of the OVF. |
| name | string | Name of the OVF. |
| storageSizeGB | integer | Number of GB of storage the server is configured with. |
| cpuCount | integer | Number of processors the server is configured with. |
| memorySizeMB | integer | Number of MB of memory the server is configured with. |

### Examples

#### JSON

    [
      {
        "id":"ALIAS/CUSTOM-OVF-IMPORT",
        "name":"CUSTOM-OVF-IMPORT-RHEL-6-64",
        "storageSizeGB":16,
        "cpuCount":1,
        "memorySizeMB":1024
      },
      {
        "id":"ALIAS/CUSTOM-OVF-IMPORT-2",
        "name":"CUSTOM-OVF-IMPORT-2",
        "storageSizeGB":60,
        "cpuCount":2,
        "memorySizeMB":4096
      }
    ]
