{{{
  "title": "Get Load Balancer Nodes",
  "date": "3-26-2015",
  "author": "Bryan Friedman",
  "attachments": []
}}}

Gets the list of nodes configured behind a given shared load balancer pool. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation to get a list of nodes configured behind a given shared load balancer pool.

## URL

### Structure

GET https://api.ctl.io/v2/sharedLoadBalancers/{accountAlias}/{dataCenter}/{loadBalancerId}/pools/{poolId}/nodes

### Example

GET https://api.ctl.io/v2/sharedLoadBalancers/ALIAS/WA1/ae3bbac5d9694c70ad7de062476ccb70/pools/2fa937bd20dd47c9b856376e9499c0c1/nodes

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | string | Short code for a particular account | Yes |
| DataCenter | string | Short string representing the data center where the load balancer is. Valid codes can be retrieved from the [Get Data Center List](get-data-center.md) API operation. | Yes |
| LoadBalancerId | string | ID of the load balancer | Yes |
| PoolId | string | ID of the pool containing the nodes | Yes |

## Response

### Entity Definition

The response will be an array containing one entity for each node configured.

| Name | Type | Description |
| --- | --- | --- |
| status | string | Status of the node: `enabled`, `disabled` or `deleted`. |
| ipAddress | string | The internal (private) IP address of the node server |
| privatePort | integer | The internal (private) port of the node server |
| links | array | Collection of [entity links](../Getting Started/api-v20-links-framework.md) that point to resources related to this node |

### Examples

#### JSON

    [
      {
        "status" : "enabled",
        "ipAddress" : "10.11.12.13",
        "privatePort" : 80
      },
      {
        "status" : "enabled",
        "ipAddress" : "10.11.12.14",
        "privatePort" : 80
      }
    ]
