{{{
  "title": "Get Csv Restore Points Report",
  "date": "07-02-2018",
  "author": "Jon Tait",
  "attachments": [],
  "sticky": "false"
}}}

Gets a list of restore point details within a specified date range for a Server Policy. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to view the backup history for a server that is configured to use Simple Backup Service.

## URL

### Structure

    GET https://api.backup.ctl.io/clc-backup-api/api/csv/{serverPolicyId}/restorePointsReport

### Example

    GET https://api.backup.ctl.io/clc-backup-api/api/csv/aee021f6-e9d3-4c13-bff1-a9733bef7532/restorePointsReport?inRetentionOnly=false&backupFinishedStartDate=2018-01-01&backupFinishedEndDate=2018-06-26

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| serverPolicyId | string | The server policy id identifies the backup configuration for a specific server | Yes |

### QueryString Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| inRetentionOnly | string | Setting to false will include all restore points found within the date range. Setting to true will omit restore points that have fallen out of retention and can no longer be used to perform restores. | No |
| backupFinishedStartDate | string | Describes the beginning of the date range for inclusion in this report. Format is yyyy-MM-dd | No |
| backupFinishedEndDate | string | Describes the end of date range for inclusion in this report. Cannot be more than one year after the start date. Format is yyyy-MM-dd | No |

## Response

content-type: text/plain, content-disposition: attachment

Note for "Anywhere Servers" in this report: the "Server Id" column will contain the friendly name given to the server, next a colon delimiter, and finally the reference id for the anywhere server record

### Examples

#### CSV

      Server Id,Server Policy Id,Server Policy Status,Storage Region,Account Policy Name,Account Policy Id,Account Policy Status,OS Type,Protected Files,Protected Bytes,Latest Backup Status,Latest Backup Start Time,Latest Backup Finished Time,Latest Files Transferred To Storage,Latest Bytes Transferred To Storage,Latest Files Failed To Transfer To Storage,Latest Bytes Failed To Transfer To Storage,Latest Files Removed From Disk,Latest Bytes Removed From Disk,Latest Unchanged Files Not Transferred,Latest Unchanged Bytes Not Transferred
      UC1BAADWIND1602-clone-2:19452303-9a91-4ba0-907a-c1d0f7ce915d,d6af6782-1d2f-426b-9bdc-377f09433e0a,ACTIVE,US EAST,dcbjr-test-win-sbstest2,3f81cd2f-2134-470f-b403-f96e7b8d0376,ACTIVE,Windows,89,16216064,SUCCESS,20180625 17:02:05,20180625 17:02:09,0,0,0,0,0,0,89,16216064
      UC1BAADWIND1602-clone-2:19452303-9a91-4ba0-907a-c1d0f7ce915d,d6af6782-1d2f-426b-9bdc-377f09433e0a,ACTIVE,US EAST,dcbjr-test-win-sbstest2,3f81cd2f-2134-470f-b403-f96e7b8d0376,ACTIVE,Windows,89,16216064,SUCCESS,20180625 16:02:05,20180625 16:02:10,0,0,0,0,0,0,89,16216064
