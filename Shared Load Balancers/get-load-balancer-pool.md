{{{
  "title": "Get Load Balancer Pool",
  "date": "3-26-2015",
  "author": "Bryan Friedman",
  "attachments": []
}}}

Gets a specified pool configured for the given shared load balancer. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation to get the details for a given shared load balancer pool.

## URL

### Structure

    GET https://api.ctl.io/v2/sharedLoadBalancers/{accountAlias}/{dataCenter}/{loadBalancerId}/pools/{poolId}

### Example

    GET https://api.ctl.io/v2/sharedLoadBalancers/ALIAS/WA1/ae3bbac5d9694c70ad7de062476ccb70/pools/2fa937bd20dd47c9b856376e9499c0c1

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | string | Short code for a particular account | Yes |
| DataCenter | string | Short string representing the data center where the load balancer is. Valid codes can be retrieved from the [Get Data Center List](get-data-center.md) API operation. | Yes |
| LoadBalancerId | string | ID of the load balancer | Yes |
| PoolId | string | ID of the pool | Yes |

## Response

### Entity Definition

| Name | Type | Description |
| --- | --- | --- |
| id | string | ID of the load balancer pool |
| port | integer | Port configured on the public-facing side of the load balancer pool. |
| method | string | The balancing method for this load balancer, either `leastConnection` or `roundRobin`. See [Shared Load Balancer Overview](shared-load-balancer-overview.md) for more information about these options. |
| persistence | string | The persistence method for this load balancer, either `standard` or `sticky`. See [Shared Load Balancer Overview](shared-load-balancer-overview.md) for more information about these options. |
| nodes | array | Collection of nodes configured behind this shared load balancer |
| links | array | Collection of [entity links](../Getting Started/api-v20-links-framework.md) that point to resources related to this load balancer pool |

### Nodes Definition

| Name | Type | Description |
| --- | --- | --- |
| name | string | Name of the node (generally the IP address) |
| status | string | Status of the node: `enabled`, `disabled` or `deleted`. |
| ipAddress | string | The internal (private) IP address of the node server |
| privatePort | integer | The internal (private) port of the node server |
| links | array | Collection of [entity links](../Getting Started/api-v20-links-framework.md) that point to resources related to this node |

### Examples

#### JSON

    {
      "id" : "2fa937bd20dd47c9b856376e9499c0c1",
      "port" : 80,
      "method" : "roundRobin",
      "persistence" : "standard",
      "nodes" : [
        {
          "status" : "enabled",
          "ipAddress" : "10.11.12.13",
          "privatePort" : 80,
          "name" : "10.11.12.13"
        },
        {
          "status" : "enabled",
          "ipAddress" : "10.11.12.14",
          "privatePort" : 80,
          "name" : "10.11.12.14"
        }
      ],
      "links" : [
        {
          "rel" : "self",
          "href" : "/v2/sharedLoadBalancers/ALIAS/WA1/ae3bbac5d9694c70ad7de062476ccb70/pools/2fa937bd20dd47c9b856376e9499c0c1",
          "verbs" : [
            "GET",
            "PUT",
            "DELETE"
          ]
        },
        {
          "rel" : "nodes",
          "href" : "/v2/sharedLoadBalancers/ALIAS/WA1/ae3bbac5d9694c70ad7de062476ccb70/pools/2fa937bd20dd47c9b856376e9499c0c1/nodes",
          "verbs" : [
            "GET",
            "PUT"
          ]
        }
      ]
    }
