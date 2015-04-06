{{{
  "title": "Update Load Balancer Pool",
  "date": "3-26-2015",
  "author": "Bryan Friedman",
  "attachments": []
}}}

Updates a given shared load balancer pool. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation to update the port, method, or persistence options for a given load balancer pool.

## URL

### Structure

    PUT https://api.ctl.io/v2/sharedLoadBalancers/{accountAlias}/{dataCenter}/{loadBalancerId}/pools/{poolId}

### Example

    PUT https://api.ctl.io/v2/sharedLoadBalancers/ALIAS/WA1/6b66b474fce940b8b581242709b5b2f0/pools/40150dde098640e8b993de0e7417afc4

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | string | Short code for a particular account | Yes |
| DataCenter | string | Short string representing the data center where the load balancer is. Valid codes can be retrieved from the [Get Data Center List](get-data-center.md) API operation. | Yes |
| LoadBalancerId | string | ID of the load balancer | Yes |
| PoolId | string | ID of the pool to update | Yes |

### Content Properties

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| method | string | The balancing method for this load balancer, either `leastConnection` or `roundRobin`. See [Shared Load Balancer Overview](shared-load-balancer-overview.md) for more information about these options. | No |
| persistence | string | The persistence method for this load balancer, either `standard` or `sticky`. See [Shared Load Balancer Overview](shared-load-balancer-overview.md) for more information about these options. | No |

### Examples

#### JSON

    {
    	"method": "roundRobin",
      "persistence": "standard"
    }

## Response

The response will not contain JSON content, but should return the HTTP `204 No Content` response upon updating the load balancer pool.
