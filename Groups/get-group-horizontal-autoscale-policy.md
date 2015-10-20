{{{
  "title": "Group Horizontal Autoscale Policy",
  "date": "02-27-2015",
  "author": "Bryan Friedman",
  "attachments": []
}}}

Get group horizontal autoscale policy. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to get group horizontal autoscale policy.

## URL

### Structure

    GET https://api.ctl.io/v2/groups/{accountAlias}/{groupId}/horizontalAutoscalePolicy/

### Example

    GET https://api.ctl.io/v2/groups/ALIAS/2a5c0b9662cf4fc8bf6180f139facdc0/horizontalAutoscalePolicy

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | string | Short code for a particular account | Yes |
| GroupID | string | ID of the group being queried. Retrieved from query to parent group, or by looking at the URL on the new UI pages in the Control Portal | Yes |

## Response

| Name | Type | Description |
| --- | --- | --- |
| groupId | string | ID of the group |
| policyId | string | The unique identifier of the autoscale policy. |
| locationId | string | Data center location identifier |
| name | string | Name of the Policy |
| availableServers | int | The number of servers available for scaling |
| targetSize | int | Number of servers to scale to |
| scaleDirection | string | Direction to Scale (In or Out ) |
| scaleResourceReason | string | Reason for scaling, either: CPU, Memory, MinimumResourceCount, or None |
| loadBalancer | complex | |
| links | array | Collection of [entity links](../Getting Started/api-v20-links-framework.md) that point to resources related to this data center |

### Load Balancer Definition
| Name | Type | Description |
| --- | --- | --- |
| id | string | ID of the load balancer |
| name | string | Friendly name of the load balancer |
| publicPort | int | Port configured on the public-facing side of the load balancer pool. |
| privatePort| int | The internal (private) port of the node server |
| publicIP | string | The external (public) IP address of the load balancer |
| links | array | Collection of [entity links](../Getting Started/api-v20-links-framework.md) that point to resources related to this data center |

### Examples

#### JSON
```
{
  "groupId": "fc06fd421e2ee41190460050568600e8",
  "policyId": "6cf7f7d139ee4d4f98a09bd0400b1a56",
  "locationId": "WA1",
  "availableServers": 2,
  "targetSize": 1,
  "scaleDirection": "Up",
  "scaleResourceReason": "MinimumResourceCount",
  "loadBalancer": {
    "id": "bf82320cc96d42048fc7d5e41b0cdada",
    "name": "hotfix111314",
    "publicPort": 443,
    "privatePort": 300,
    "publicIP": "1.1.1.1",
    "links": [
      {
        "rel": "self",
        "href": "/v2/sharedLoadBalancers/ALIAS/WA1/bf82320cc96d42048fc7d5e41b0cdada"
      }
    ]
  },
  "timestamp": "2015-10-20T21:20:02Z",
  "links": [
    {
      "rel": "self",
      "href": "/v2/groups/WHIM/fc06fd421e2ee41190460050568600e8/horizontalAutoscalePolicy"
    },
    {
      "rel": "group",
      "href": "/v2/groups/ALIAS/fc06fd421e2ee41190460050568600e8"
    },
    {
      "rel": "horizontalAutoscalePolicy",
      "href": "/v2/horizontalAutoscalePolicies/ALIAS/6cf7f7d139ee4d4f98a09bd0400b1a56"
    }
  ]
}
```
