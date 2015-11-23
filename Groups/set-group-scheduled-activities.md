{{{
  "title": "Set Group Scheduled Activities",
  "date": "11-24-2015",
  "author": "Jared Ruckle",
  "attachments": []
}}}

Sets scheduled activities for a group. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to set scheduled activities for a group.

## URL

### Structure

    PUT https://api.ctl.io/v2/groups/{accountAlias}/{groupId}/ScheduledActivities/

### Example

    PUT https://api.ctl.io/v2/groups/ALIAS/2a5c0b9662cf4fc8bf6180f139facdc0/ScheduledActivities

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| accountAlias | string | Short code for a particular account | Yes |
| GroupID | string | ID of the group being queried. Retrieved from query to parent group, or by looking at the URL of the Group in the Control Portal UI. | Yes |
| status | string | State of scheduled activity: on or off | Yes |
| type | string| Type of activity: archive, createsnapshot, delete, deletesnapshot, pause, poweron, reboot, shutdown | Yes |
| beginDateUTC | datetime | Time when scheduled activity should start | Yes |
| repeat | string | How often to repeat: never, daily, weekly, monthly, customWeekly | Yes |
| customWeeklyDays | array | An array of strings for the days of the week: sun, mon, tue, wed, thu, fri, sat | No |
| expire | string | When the scheduled activities are set to expire: never, afterDate, afterCount | Yes |
| expireCount | int | Number of times scheduled activity should run before expiring | No |
| expireDateUTC | datetime | When the scheduled activity should expire | No |
| timeZoneOffset | string | To display in local time | Yes |

### Examples

#### JSON
```
{
  "status": "on",
  "type": "reboot",
  "beginDateUTC": "2015-11-23T19:41:00.000Z",
  "timeZoneOffset": "-08:00",
  "repeat": "weekly",
  "expire": "never"
}

{
  "status": "on",
  "type": "reboot",
  "beginDateUTC": "2015-11-23T19:40:00.000Z",
  "timeZoneOffset": "-08:00",
  "repeat": "customWeekly",
  "expire": "never",
  "customWeeklyDays": [
    "mon",
    "wed",
    "fri"
  ]
}

{
  "status": "on",
  "type": "reboot",
  "beginDateUTC": "2015-11-23T21:27:00.000Z",
  "timeZoneOffset": "-08:00",
  "repeat": "daily",
  "expire": "afterCount",
  "expireCount": "10"
}
```

## Response

| Name | Type | Description |
| --- | --- | --- |
| id | string | ID of the group |
| locationId | string | Data center location identifier |
| changeInfo | complex | Change history |
| links | array | Collection of [entity links](../Getting Started/api-v20-links-framework.md) that point to resources related to this data center |
| status | string | State of scheduled activity: on or off |
| type | string| Type of activity: archive, createsnapshot, delete, deletesnapshot, pause, poweron, reboot, shutdown |
| beginDateUTC | datetime | Time when scheduled activity should start |
| repeat | string | How often to repeat: never, daily, weekly, monthly, customWeekly |
| customWeeklyDays | array | An array of strings for the days of the week: sun, mon, tue, wed, thu, fri, sat |
| expire | string | When the scheduled activities are set to expire: never, afterDate, afterCount |
| expireCount | int | Number of times scheduled activity should run before expiring |
| expireDateUTC | datetime | When the scheduled activity should expire |
| timeZoneOffset | string | To display in local time |
| isExpired | bool | True: scheduled activity has expired. False: scheduled activity is active |
| lastOccurrenceDateUtc | datetime | Last time scheduled activity was run |
| occurrenceCount | int | How many times scheduled activity has been run |
| nextOccurrenceDateUtc | datetime | When the next scheduled activty will be run |

```
{
  "id": "2a5c0b9662cf4fc8bf6180f139facdc0",
  "locationId": "WA1",
  "changeInfo": {
    "createdBy": "user@user.com",
    "createdDate": "2015-11-23T21:17:16Z",
    "modifiedBy": "user@user.com",
    "modifiedDate": "2015-11-23T21:17:16Z"
  },
  "links": [
    {
      "rel": "group",
      "href": "/v2/groups/ALIAS/2a5c0b9662cf4fc8bf6180f139facdc0",
      "id": "2a5c0b9662cf4fc8bf6180f139facdc0",
      "name": "Default Group Name"
    },
    {
      "rel": "self",
      "href": "/v2/groups/ALIAS/5b824632e319e411929e00505682315a/scheduledActivities/2a5c0b9662cf4fc8bf6180f139facdc0",
      "verbs": [
        "GET",
        "PUT",
        "DELETE"
      ]
    }
  ],
  "status": "on",
  "type": "pause",
  "beginDateUTC": "2015-11-23T19:41:00Z",
  "repeat": "daily",
  "customWeeklyDays": [],
  "expire": "never",
  "timeZoneOffset": "-08:00:00",
  "isExpired": false,
  "occurrenceCount": 0,
  "nextOccurrenceDateUTC": "2015-11-24T19:41:00Z"
}
```
