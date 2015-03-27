{{{
  "title": "Create Load Balancer Pool",
  "date": "3-26-2015",
  "author": "Bryan Friedman",
  "attachments": []
}}}

Creates a new shared load balancer configuration for a given account and data center. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation to create a new shared load balancers in a given account and data center.

## URL

### Structure

    POST https://api.ctl.io/v2/sharedLoadBalancers/{accountAlias}/{dataCenter}/{loadBalancerId}/pools

### Example

    POST https://api.ctl.io/v2/sharedLoadBalancers/ALIAS/WA1/6b66b474fce940b8b581242709b5b2f0/pools

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | string | Short code for a particular account | Yes |
| DataCenter | string | Short string representing the data center where the load balancer is. Valid codes can be retrieved from the [Get Data Center List](get-data-center.md) API operation. | Yes |
| LoadBalancerId | string | ID of the load balancer | Yes |

### Content Properties

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| port | integer | Port to configure on the public-facing side of the load balancer pool. Must be either `80` (HTTP) or `443` (HTTPS). | Yes |
| method | string | The balancing method for this load balancer, either `leastConnection` or `roundRobin`. Default is `roundRobin`. See [Shared Load Balancer Overview](shared-load-balancer-overview.md) for more information about these options. | No |
| persistence | string | The persistence method for this load balancer, either `standard` or `sticky`. Default is `standard`. See [Shared Load Balancer Overview](shared-load-balancer-overview.md) for more information about these options. | No |

### Examples

#### JSON

    {
    	"port": 80,
    	"method": "leastConnection",
      "persistence": "sticky"
    }

## Response

The response will be an entity representing the new load balancer pool that was created.

### Entity Definition

| Name | Type | Description |
| --- | --- | --- |
| id | string | ID of the load balancer pool |
| port | integer | Port configured on the public-facing side of the load balancer pool. |
| method | string | The balancing method for this load balancer, either `leastConnection` or `roundRobin`. See [Shared Load Balancer Overview](shared-load-balancer-overview.md) for more information about these options. |
| persistence | string | The persistence method for this load balancer, either `standard` or `sticky`. See [Shared Load Balancer Overview](shared-load-balancer-overview.md) for more information about these options. |
| nodes | array | Empty array since no nodes will be configured yet for the new pool |
| links | array | Collection of [entity links](../Getting Started/api-v20-links-framework.md) that point to resources related to this load balancer pool |

### Examples

#### JSON

    {
      "id" : "40150dde098640e8b993de0e7417afc4",
      "port" : 80,
      "method" : "leastConnection",
      "persistence" : "sticky",
      "nodes" : [],
      "links" : [
        {
          "rel" : "self",
          "href" : "/v2/sharedLoadBalancers/ALIAS/WA1/6b66b474fce940b8b581242709b5b2f0/pools/40150dde098640e8b993de0e7417afc4",
          "verbs" : [
            "GET",
            "PUT",
            "DELETE"
          ]
        },
        {
          "rel" : "nodes",
          "href" : "/v2/sharedLoadBalancers/ALIAS/WA1/6b66b474fce940b8b581242709b5b2f0/pools/40150dde098640e8b993de0e7417afc4/nodes",
          "verbs" : [
            "GET",
            "PUT"
          ]
        }
      ]
    }
