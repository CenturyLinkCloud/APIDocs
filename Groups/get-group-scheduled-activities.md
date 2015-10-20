{{{
  "title": "Group Scheduled Activities",
  "date": "02-27-2015",
  "author": "Bryan Friedman",
  "attachments": []
}}}

Get group scheduled activities. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to get group scheduled activities.

## URL

### Structure

    GET https://api.ctl.io/v2/groups/{accountAlias}/{groupId}/ScheduledActivities/

### Example

    GET https://api.ctl.io/v2/groups/ALIAS/2a5c0b9662cf4fc8bf6180f139facdc0/ScheduledActivities

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | string | Short code for a particular account | Yes |
| GroupID | string | ID of the group being queried. Retrieved from query to parent group, or by looking at the URL on the new UI pages in the Control Portal | Yes |

## Response

| Name | Type | Description |
| --- | --- | --- |
| id | string | ID of the group |
| locationId | string | Data center location identifier |
| changeInfo | complex | Change history |
| links | array | Collection of [entity links](../Getting Started/api-v20-links-framework.md) that point to resources related to this data center |
| status | string | State of scheduled activity: on or off |
| type | string| Type of activity: archive, createsnapshot, delete, deletesnapshot, pause, poweron, reboot, shutdown |
| beginDateUtc | datetime | Time when scheduled activity should start |
| repeat | string | How often to repeat: never, daily, weekly, monthly, customWeekly |
| customWeeklyDays | array | An array of strings for the days of the week: sun, mon, tue, wed, thu, fri, sat |
| expire | string | When the scheduled activities are set to expire: never, afterDate, afterCount |
| expireCount | int | Number of times scheduled activity should run before expiring |
| expireDateUtc | datetime | When the scheduled activity should expire |
| timeZoneOffset | string | To display in local time |
| isExpired | bool | True: scheduled activity has expired. False: scheduled activity is active |
| lastOccurrenceDateUtc | datetime | Last time scheduled activity was run |
| occurrenceCount | int | How many times scheduled activity has been run |
| nextOccurrenceDateUtc | datetime | When the next scheduled activty will be run |

### Examples

#### JSON
```
[
  {
    "id": "95715f96f8a145d68ace797fe542c9ae",
    "locationId": "WA1",
    "changeInfo": {
      "createdBy": "john.doe",
      "createdDate": "2015-03-16T18:12:02Z",
      "modifiedBy": "john.doe",
      "modifiedDate": "2015-10-20T22:20:25Z"
    },
    "links": [
      {
        "rel": "group",
        "href": "/v2/groups/ALIAS/fc06fd421e2ee41190460050568600e8",
        "id": "fc06fd421e2ee41190460050568600e8",
        "name": "Default Group"
      },
      {
        "rel": "self",
        "href": "/v2/groups/ALIAS/fc06fd421e2ee41190460050568600e8/scheduledActivities/95715f96f8a145d68ace797fe542c9ae",
        "verbs": [
          "GET",
          "PUT",
          "DELETE"
        ]
      }
    ],
    "status": "on",
    "type": "shutdown",
    "beginDateUTC": "2015-03-16T18:11:00Z",
    "repeat": "customWeekly",
    "customWeeklyDays": [
      "tue",
      "thu"
    ],
    "expire": "never",
    "timeZoneOffset": "-07:00:00",
    "isExpired": false,
    "occurrenceCount": 0,
    "nextOccurrenceDateUTC": "2015-10-22T18:11:00Z"
  }
]
```
