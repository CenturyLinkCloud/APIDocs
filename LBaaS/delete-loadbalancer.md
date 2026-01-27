{{{
  "title": "Delete Load Balancer",
  "date": "9-13-2018",
  "author": "Matt Peterson",
  "attachments": []
}}}

Deletes an LBaaS instance for a given account in a given data center. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you need to delete an existing load balancer. 

## URL

### Structure

    DELETE https://api.loadbalancer.ctl.io/{accountAlias}/{dataCenter}/loadbalancers/{loadBalancerId}

### Example

    DELETE https://api.loadbalancer.ctl.io/DV01/NY1/loadbalancers/329a98e6-977a-4c25-a7c8-174209fe1d31

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| accountAlias | string | Short code for the particular account which owns the load balancer | Yes |
| dataCenter | string | Short string representing the data center in which the load balancer resides | Yes |
| loadBalancerId | string | Id of the load balancer you want to delete | Yes |

## Response

The response will be an entity representing the request to delete the load balancer. Request status can be tracked from the [Get LBaaS Request](get-lbaas-request.md).

### Entity Definition

| Name | Type | Description |
| --- | --- | --- |
| id | string | ID of the load balancer delete request |
| status | string | Initially the response will show a status for the request of "ACTIVE".  A status of "COMPLETE" will show in the Response of a function when the load balancer has been deleted. |
| description | string | Describes the activity running within the Load Balancer delete process |
| requestDate | string | Date-time stamp of the request |
| completionDate | string | Date-time stamp of load balancer delete.  Null value returned until process has completed |
| links | array | Collection of entity links that point to resources related to this LBaaS Group |

### Examples

#### JSON
```json
{  
    "id": "d685c028-5852-4b6f-8511-a407147db0e4",
    "status": "ACTIVE",  
    "description": "Delete Load Balancer 329a98e6-977a-4c25-a7c8-174209fe1d31",  
    "requestDate": 1450383770701,  
    "completionDate": null,  
    "links": [  
        {  
            "rel": "loadbalancer",  
            "href": "",  
            "resourceId": "329a98e6-977a-4c25-a7c8-174209fe1d31"  
        }
    ]  
}
```
