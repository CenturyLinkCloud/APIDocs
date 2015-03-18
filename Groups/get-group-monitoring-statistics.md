{{{
  "title": "Get Group Monitoring Statistics",
  "date": "10-13-2014",
  "author": "Richard Seroter",
  "attachments": []
}}}

Gets the resource consumption details for whatever window specified in the request. Data can be retrieve for a variety of time windows and intervals. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to track the resource usage of servers within a group hierarchy. It can be used to populate a local data mart or chart the results on a dashboard.

## URL

### Structure

    GET https://api.ctl.io/v2/groups/{accountAlias}/{groupId}/statistics?start={datetime}&sampleInterval=dd:hh:mm:ss

### Example

    GET https://api.ctl.io/v2/groups/ALIAS/2a5c0b9662cf4fc8bf6180f139facdc0/statistics?start=2014-04-05&sampleInterval=01:00:00

## Request

### URI and Querystring Parameters

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
      <td>GroupID</td>
      <td>string</td>
      <td>ID of the group being queried. Retrieved from query to parent group, or by looking at the URL on the new UI pages in the Control Portal.</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>start</td>
      <td>datetime</td>
      <td>DateTime (UTC) of the query window. Note that statistics are only held for 14 days. Start date (and optional end date) must be within the past 14 days. Value is not required if choosing the "Latest" query type.</td>
      <td>No</td>
    </tr>
    <tr>
      <td>end</td>
      <td>datetime</td>
      <td>DateTime (UTC) of the query window. End date (and start date) must be within the past 14 days. Not a required value if results should be up to the current time.</td>
      <td>No</td>
    </tr>
    <tr>
      <td>sampleInterval</td>
      <td>timespan</td>
      <td>Result interval. For the default "hourly" type, the minimum value is 1 hour (01:00:00) and maximum is the full window size of 14 days. Note that interval must fit within start/end window, or you will get an exception that states: "The 'end'
        parameter must represent a time that occurs at least one 'sampleInterval' before 'start." If "realtime" type specified, interval can be as small as 5 minutes (05:00).</td>
      <td>No</td>
    </tr>
    <tr>
      <td>type</td>
      <td>string</td>
      <td>Default is "Hourly" which returns hourly data (possibly in a different interval if a sampleInterval is specified) for the past 14 days (or whatever window is specified). Value "Realtime" means that data from the last 4 hours is available in smaller
        increments. To use "Realtime" type, start parameter must be within the last 4 hours. Final valid type is "Latest" which returns a single data point that reflects the last monitoring data collected. No start, end, or sampleInterval values are needed
        for this type.</td>
      <td>No</td>
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
      <td>name</td>
      <td>string</td>
      <td>User-defined name of the group</td>
    </tr>
    <tr>
      <td>stats</td>
      <td>array</td>
      <td>Collection of stats for the server for the interval chosen</td>
    </tr>
  </tbody>
</table>

### Stats Definition

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
      <td>timestamp</td>
      <td>datetime</td>
      <td>Timestamp of the monitoring results</td>
    </tr>
    <tr>
      <td>cpu</td>
      <td>float</td>
      <td>CPU allocation during the interval</td>
    </tr>
    <tr>
      <td>cpuPercent</td>
      <td>float</td>
      <td>CPU consumption (out of 100%) during the interval</td>
    </tr>
    <tr>
      <td>memoryMB</td>
      <td>float</td>
      <td>Memory allocation during the interval</td>
    </tr>
    <tr>
      <td>memoryPercent</td>
      <td>float</td>
      <td>Memory consumption (out of 100%) during the interval</td>
    </tr>
    <tr>
      <td>networkReceivedKbps</td>
      <td>float</td>
      <td>Public network consumption in during the interval</td>
    </tr>
    <tr>
      <td>networkTransmittedKbps</td>
      <td>float</td>
      <td>Public network consumption out during the interval</td>
    </tr>
    <tr>
      <td>diskUsageTotalCapacityMB</td>
      <td>float</td>
      <td>Total disk allocation during the interval</td>
    </tr>
    <tr>
      <td>diskUsage</td>
      <td>array</td>
      <td>List of physical disks attached to the virtual machine</td>
    </tr>
    <tr>
      <td>guestDiskUsage</td>
      <td>array</td>
      <td>List of partitions used inside the guest OS</td>
    </tr>
  </tbody>
</table>

### Disk Usage Definition

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
      <td>id</td>
      <td>string</td>
      <td>Disk identifier</td>
    </tr>
    <tr>
      <td>capacityMB</td>
      <td>integer</td>
      <td>Capacity (in MB) allocated for this disk</td>
    </tr>
  </tbody>
</table>

### Guest Usage Definition

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
      <td>path</td>
      <td>string</td>
      <td>Path of this partition</td>
    </tr>
    <tr>
      <td>capacityMB</td>
      <td>integer</td>
      <td>Total capacity available to this partition</td>
    </tr>
    <tr>
      <td>consumedMB</td>
      <td>integer</td>
      <td>Amount of capacity in use by this partition</td>
    </tr>
  </tbody>
</table>

### Examples

#### JSON

    (/v2/groups/ALIAS/GROUP/statistics?start=2014-04-09T20:00:00&sampleInterval=01:00:00)

    [
      {
        "name": "wa1acctser7101",
        "stats": [
          {
            "timestamp": "2014-04-09T20:00:00Z",
            "cpu": 2.0,
            "cpuPercent": 5.0,
            "memoryMB": 3072.0,
            "memoryPercent": 0.0,
            "networkReceivedKBps": 0.0,
            "networkTransmittedKBps": 0.0,
            "diskUsageTotalCapacityMB": 40960.0,
            "diskUsage": [
              {
                "id": "0:0",
                "capacityMB": 40960
              }
            ],
            "guestDiskUsage": []
          },
          {
            "timestamp": "2014-04-09T21:00:00Z",
            "cpu": 2.0,
            "cpuPercent": 2.0,
            "memoryMB": 3072.0,
            "memoryPercent": 0.0,
            "networkReceivedKBps": 0.0,
            "networkTransmittedKBps": 0.0,
            "diskUsageTotalCapacityMB": 40960.0,
            "diskUsage": [
              {
                "id": "0:0",
                "capacityMB": 40960
              }
            ],
            "guestDiskUsage": []
          }
        ]
      },
      {
        "name": "wa1acctser7202",
        "stats": [
          {
            "timestamp": "2014-04-09T20:00:00Z",
            "cpu": 1.0,
            "cpuPercent": 1.14,
            "memoryMB": 2048.0,
            "memoryPercent": 9.24,
            "networkReceivedKBps": 0.0,
            "networkTransmittedKBps": 0.0,
            "diskUsageTotalCapacityMB": 40960.0,
            "diskUsage": [
              {
                "id": "0:0",
                "capacityMB": 40960
              }
            ],
            "guestDiskUsage": [
              {
                "path": "C:\\",
                "capacityMB": 40607,
                "consumedMB": 16619
              }
            ]
          },
          {
            "timestamp": "2014-04-09T21:00:00Z",
            "cpu": 1.0,
            "cpuPercent": 1.02,
            "memoryMB": 2048.0,
            "memoryPercent": 2.32,
            "networkReceivedKBps": 0.0,
            "networkTransmittedKBps": 0.0,
            "diskUsageTotalCapacityMB": 40960.0,
            "diskUsage": [
              {
                "id": "0:0",
                "capacityMB": 40960
              }
            ],
            "guestDiskUsage": [
              {
                "path": "C:\\",
                "capacityMB": 40607,
                "consumedMB": 16619
              }
            ]
          }
        ]
      }
    ]
