{{{
  "title": "Update LBaaS",
  "date": "9-10-2018",
  "author": "Matt Peterson",
  "attachments": []
}}}

Updates an LBaaS instance for a given account in a given data center. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you need to update the name and description of a given load balancer.

## URL

### Structure

    PUT https://api.loadbalancer.ctl.io/{accountAlias}/{dataCenter}/loadbalancers/{loadBalancerId}

### Example

     PUT https://api.loadbalancer.ctl.io/DV01/NY1/loadbalancers/329a98e6-977a-4c25-a7c8-174209fe1d31

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| accountAlias | string | Short code for a particular account | Yes |
| dataCenter | string | Short string representing the data center in which the load balancer was created | Yes |
| loadBalancerId | string | The id of the load balancer. | Yes |

### Content Properties

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| name | string | The intended name of the new instance | Yes |
| description | string | A short description of the load balancer | No |

### Examples

#### JSON
```json
{  
    "name": "ExampleGroup-updated",
    "description": "Example Group for demo purposes"
} 
```

## Response

The response will be the updated load balancer

### Entity Definition

| Name | Type | Description |
| --- | --- | --- |
| id | string | ID of the request |
| name | string | Name of this load balancer instance |
| description | string | A short description of this load balancer |
| publicIPAddress | string | The external (public) IP address of the load balancer  |
| pools | array | Collection of pools configured for this load balancer |
| status | string | Status of the load balancer: `active`, `deleted`, `creating`, or `failed` |
| accountAlias | string | The account which owns the load balancer |
| dataCenter | string | The data center in which the load balancer resides |
| creationTime | string | Date-time stamp of the load balancer creation |
| deletionTime | string | Date-time stamp of the load balancer deletion. Will be null if load balancer not in `deleted` status |

### Examples

#### JSON
```json
{
    "id": "329a98e6-977a-4c25-a7c8-174209fe1d31",
    "name": "ExampleGroup-updated",
    "description": "Example group for demo purposes",
    "publicIPAddress": "64.211.224.123",
    "pools": [],
    "status": "active",
    "accountAlias": "DV01",
    "dataCenter": "NY1",
    "creationTime": 1471902898537,
    "deletionTime": null
}
```
