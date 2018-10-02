{{{
  "title": "Get LBaaS Request",
  "date": "9-10-2018",
  "author": "Matt Peterson",
  "attachments": []
}}}

Allows the user to retrieve a request from the LBaaS service.

### When to Use It

Use this API operation when you need to check the status of a request to the LBaaS service. 

## URL

### Structure

    GET https://api.loadbalancer.ctl.io/{accountAlias}/{dataCenter}/loadbalancers/requests/{id}

### Example

    GET https://api.loadbalancer.ctl.io/DV01/NY1/loadbalancers/requests/d685c028-5852-4b6f-8511-a407147db0e4

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| accountAlias | string | Short code for a particular account | Yes |
| dataCenter | string | Short string representing the data center the request was created in | Yes |
| id | string | The id of the request the user is interested in. | Yes |

## Response

### Entity Definition

| Name | Type | Description |
| --- | --- | --- |
| id | string | ID of the request |
| status | string | Current status of the request. Possible values are 'ACTIVE', 'COMPLETE', and 'FAILED' |
| description | string | Describes the type of the request |
| requestDate | string | Date-time stamp of the request |
| completionDate | string | Date-time stamp of when request completed. |
| links | array | Collection of entity links that point to resources related to this LBaaS Group |

### Examples

#### JSON
```json
{  
    "id": "d685c028-5852-4b6f-8511-a407147db0e4",  
    "status": "COMPLETE",  
    "description": "Create Load Balancer a4ad7c71-1575-400e-8eb2-cef74ed557ad",  
    "requestDate": 1450383770701,  
    "completionDate": 1450383813624,  
    "links": [  
        {  
            "rel": "loadbalancer",  
            "href": "",  
            "resourceId": "a4ad7c71-1575-400e-8eb2-cef74ed557ad"  
        }  
    ]  
}
```
