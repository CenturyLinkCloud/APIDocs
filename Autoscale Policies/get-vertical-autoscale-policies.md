{{{
  "title": "Get Vertical Autoscale Policies",
  "date": "5-23-2015",
  "author": "Bryan Friedman",
  "attachments": [],
  "sticky":"true"
}}}

Gets a list of vertical autoscale policies for a given account. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to get a list of vertical autoscale policies for a given account, and to see what servers are associated with these policies. You can also use the IDs provided in this list to add a server to that autoscale policy using [Set Vertical Autoscale Policy On Server](../Autoscale Policies/set-vertical-autoscale-policy-on-server.md) API method.

## URL

### Structure

    GET https://api.ctl.io/v2/autoscalePolicies/{accountAlias}

### Example

    GET https://api.ctl.io/v2/autoscalePolicies/ALIAS

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| accountAlias | string | Short code for a particular account | Yes |

## Response

The response will be an array containing one entity for each autoscale policy in the given account.

### Entity Definition

| Name | Type | Description |
| --- | --- | --- |
| id | string | ID of the vertical autoscale policy |
| name | string | Name of the vertical autoscale policy |
| resourceType | string | The resource type to autoscale; only `cpu` is supported at this time |
| thresholdPeriodMinutes | integer | Duration the resource must be at min/max in order to autoscale (5, 10, 15, or 30 minutes)  |
| scaleUpIncrement | integer | Number of CPU to increase on a scale up event (1, 2, or 4) |
| range | complex | The range defining the minimum and maximum number of CPU to allow (between 1-16) |
| scaleUpThreshold | integer | Will scale up when resource it at this setting for at least the threshold period (between 1-100) |
| scaleDownThreshold | integer | Will scale down when resource it at this setting for at least the threshold period (between 1-100) |
| scaleDownWindow | complex | A server reboot is required for all resource scale downs; this is the scale down window during which the resource will be set to the policy's minimum value. |
| links | array | Collection of [entity links](../Getting Started/api-v20-links-framework.md) that point to resources related to this policy |

### Range Definition

| Name | Type | Description |
| --- | --- | --- |
| min | integer | Maximum number of CPU |
| max | integer | Minimum number of CPU |

### ScaleDownWindow Definition

| Name | Type | Description |
| --- | --- | --- |
| start | string | Start time of window in UTC |
| end | string | End time of window in UTC |

### Examples

#### JSON
```json
      {
        "id": "3b6f26003c224596bc7e748a0adc97d5",
        "name": "Production Database Scale Policy",
        "resourceType": "cpu",
        "thresholdPeriodMinutes": 5,
        "scaleUpIncrement": 1,
        "range": {
          "max": 6,
          "min": 2
        },
        "scaleUpThreshold": 85,
        "scaleDownThreshold": 15,
        "scaleDownWindow": {
          "start": "02:00",
          "end": "04:00"
        },
        "links": [
          {
            "rel": "self",
            "href": "/v2/autoscalePolicies/ALIAS/3b6f26003c224596bc7e748a0adc97d5"
          }
        ]
      },
      {
        "id": "23a68b22e35b4983abd1051fae10ee7b",
        "name": "Another CPU Autoscale Policy",
        "resourceType": "cpu",
        "thresholdPeriodMinutes": 5,
        "scaleUpIncrement": 1,
        "range": {
          "max": 4,
          "min": 1
        },
        "scaleUpThreshold": 85,
        "scaleDownThreshold": 15,
        "scaleDownWindow": {
          "start": "00:00",
          "end": "23:00"
        },
        "links": [
          {
            "rel": "self",
            "href": "/v2/autoscalePolicies/ALIAS/23a68b22e35b4983abd1051fae10ee7b"
          }
        ]
      }
```
