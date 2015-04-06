{{{
  "title": "Create Shared Load Balancer",
  "date": "3-26-2015",
  "author": "Bryan Friedman",
  "attachments": []
}}}

Creates a new shared load balancer configuration for a given account and data center. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation to create a new shared load balancer in a given account and data center.

## URL

### Structure

    POST https://api.ctl.io/v2/sharedLoadBalancers/{accountAlias}/{dataCenter}

### Example

    POST https://api.ctl.io/v2/sharedLoadBalancers/ALIAS/WA1

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | string | Short code for a particular account | Yes |
| DataCenter | string | Short string representing the data center where the load balancer is. Valid codes can be retrieved from the [Get Data Center List](../Data Centers/get-data-center.md) API operation. | Yes |

### Content Properties

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| name | string | Friendly name for new the load balancer | Yes |
| description | string | Description for new the load balancer | Yes |
| status | string | Status to create the load balancer with: `enabled` or `disabled` | No |

### Examples

#### JSON

    {
    	"name":"New Load Balancer",
    	"description":"A brand new load balancer"
    }


## Response

The response will be an entity representing the new load balancer that was created.

### Entity Definition

| Name | Type | Description |
| --- | --- | --- |
| id | string | ID of the load balancer |
| name | string | Friendly name of the load balancer |
| description | string | Description for the load balancer |
| ipAddress | string | The external (public) IP address of the load balancer |
| status | string | Status of the load balancer: `enabled`, `disabled` or `deleted` |
| pools | array | Empty array since no pools will be configured yet for the new shared load balancer |
| links | array | Collection of [entity links](../Getting Started/api-v20-links-framework.md) that point to resources related to this load balancer |

### Examples

#### JSON

    {
      "id" : "6b66b474fce940b8b581242709b5b2f0",
      "name" : "New Load Balancer",
      "description" : "A brand new load balancer",
      "ipAddress" : "98.76.54.32",
      "status" : "enabled",
      "pools" : [],
      "links" : [
        {
          "rel" : "self",
          "href" : "/v2/sharedLoadBalancers/ALIAS/WA1/6b66b474fce940b8b581242709b5b2f0",
          "verbs" : [
            "GET",
            "PUT",
            "DELETE"
          ]
        },
        {
          "rel" : "pools",
          "href" : "/v2/sharedLoadBalancers/ALIAS/WA1/6b66b474fce940b8b581242709b5b2f0/pools",
          "verbs" : [
            "GET",
            "POST"
          ]
        }
      ],
    }
