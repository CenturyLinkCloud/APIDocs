{{{
  "title": "Update Shared Load Balancer",
  "date": "3-26-2015",
  "author": "Bryan Friedman",
  "attachments": []
}}}

Updates a given shared load balancer. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation to update the name, description, or status of a given shared load balancer.

## URL

### Structure

    PUT https://api.ctl.io/v2/sharedLoadBalancers/{accountAlias}/{dataCenter}/{loadBalancerId}

### Example

    PUT https://api.ctl.io/v2/sharedLoadBalancers/ALIAS/WA1/6b66b474fce940b8b581242709b5b2f0

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | string | Short code for a particular account | Yes |
| DataCenter | string | Short string representing the data center where the load balancer is. Valid codes can be retrieved from the [Get Data Center List](get-data-center.md) API operation. | Yes |
| LoadBalancerId | string | ID of the load balancer to update | Yes |

### Content Properties

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| name | string | Friendly name for new the load balancer | Yes |
| description | string | Description for new the load balancer | Yes |
| status | string | Status to create the load balancer with: `enabled` or `disabled` | No |

### Examples

#### JSON

    {
    	"name":"Updated Load Balancer",
    	"description":"An updated load balancer"
    }


## Response

The response will not contain JSON content, but should return the HTTP `204 No Content` response upon updating the load balancer.
