{{{
  "title": "Update Load Balancer Nodes",
  "date": "3-26-2015",
  "author": "Bryan Friedman",
  "attachments": []
}}}

Updates the nodes behind a given shared load balancer pool. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation to update the list of nodes in a given load balancer pool.

## URL

### Structure

    PUT https://api.ctl.io/v2/sharedLoadBalancers/{accountAlias}/{dataCenter}/{loadBalancerId}/pools/{poolId}/nodes

### Example

    PUT https://api.ctl.io/v2/sharedLoadBalancers/ALIAS/WA1/6b66b474fce940b8b581242709b5b2f0/pools/40150dde098640e8b993de0e7417afc4/nodes

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | string | Short code for a particular account | Yes |
| DataCenter | string | Short string representing the data center where the load balancer is. Valid codes can be retrieved from the [Get Data Center List](get-data-center.md) API operation. | Yes |
| LoadBalancerId | string | ID of the load balancer | Yes |
| PoolId | string | ID of the pool to update | Yes |

### Content Properties

The body of the request is an array of node entities.

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| name | string | Name of the node (generally the IP address) | Yes |
| status | string | Status of the node: `enabled`, `disabled` or `deleted`. | No |
| ipAddress | string | The internal (private) IP address of the node server | Yes |
| privatePort | integer | The internal (private) port of the node server. Must be a value between 1 and 65535. | Yes |

### Examples

#### JSON

    [
      {
        "ipAddress" : "10.11.12.18",
        "privatePort" : 8080,
        "name" : "10.11.12.18"
      },
      {
        "ipAddress" : "10.11.12.19",
        "privatePort" : 8080,
        "name" : "10.11.12.19"
      }
    ]

## Response

The response will not contain JSON content, but should return the HTTP `204 No Content` response upon updating the list of load balancer nodes.
