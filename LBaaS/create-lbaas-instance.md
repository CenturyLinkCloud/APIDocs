{{{
  "title": "Create LBaaS",
  "date": "9-10-2018",
  "author": "Matt Peterson",
  "attachments": []
}}}

Creates an LBaaS instance for a given account in a given data center. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you need to create a new load balancer and get a VIP assigned in a given data center and for a given account.

## URL

### Structure

    POST https://api.loadbalancer.ctl.io/{accountAlias}/{dataCenter}/loadbalancers

### Example

    POST https://api.loadbalancer.ctl.io/DV01/NY1/loadbalancers

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| accountAlias | string | Short code for a particular account | Yes |
| dataCenter | string | Short string representing the target data center for the new load balancer. Valid codes can be retrieved from the [Get Data Center List](../Data Centers/get-data-center.md) API operation. | Yes |

### Content Properties

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| name | string | The intended name of the new instance | Yes |
| description | string | A short description of the load balancer | No |

### Examples

#### JSON
```json
{  
    "name": "ExampleGroup",
    "description": "Example Group for demo purposes"
} 
```

## Response

The response will be an entity representing the request to create the new load balancer. Request status can be tracked from the [Get LBaaS Request](get-lbaas-request.md).

### Entity Definition

| Name | Type | Description |
| --- | --- | --- |
| id | string | ID of the LBaaS create request |
| status | string | Initially the response will show a status for the request of "ACTIVE".  A status of "COMPLETE" will show in the Response of a function when the Group has been created with the new configuration. |
| description | string | Describes the activity running within the LBaaS Group create process |
| requestDate | string | Date-time stamp of the request |
| completionDate | string | Date-time stamp of LBaaS Group creation.  Null value returned until process has completed |
| links | array | Collection of entity links that point to resources related to this LBaaS Group |

### Examples

#### JSON
```json
{  
    "id": "d685c028-5852-4b6f-8511-a407147db0e4",
    "status": "ACTIVE",  
    "description": "Create Load Balancer a4ad7c71-1575-400e-8eb2-cef74ed557ad",  
    "requestDate": 1450383770701,  
    "completionDate": null,  
    "links": [  
        {  
            "rel": "loadbalancer",  
            "href": "",  
            "resourceId": "a4ad7c71-1575-400e-8eb2-cef74ed557ad"  
        }  
    ]  
}
```
