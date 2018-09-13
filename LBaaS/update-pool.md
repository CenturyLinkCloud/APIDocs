{{{
  "title": "Update Pool",
  "date": "9-13-2018",
  "author": "Matt Peterson",
  "attachments": []
}}}

Updates an existing pool on an LBaaS instance for a given account in a given data center. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you need to modify the configuration of an existing pool on a load balancer. 

## URL

### Structure

    PUT https://api.loadbalancer.ctl.io/{accountAlias}/{dataCenter}/loadbalancers/{loadBalancerId}/pools/{poolId}

### Example

    PUT https://api.loadbalancer.ctl.io/DV01/NY1/loadbalancers/329a98e6-977a-4c25-a7c8-174209fe1d31/pools/a4ad7c71-1575-400e-8eb2-cef74ed557ad

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| accountAlias | string | Short code for the particular account which owns the load balancer | Yes |
| dataCenter | string | Short string representing the data center in which the load balancer resides | Yes |
| loadBalancerId | string | Id of the load balancer | Yes |
| poolId | string | Id of the pool you want to update | Yes |

### Content Properties

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| id | string | The id of the pool | Yes |
| port | integer | The port on which incoming traffic will send requests. Valid port ranges are between `23` and `65534` | Yes |
| loadBalancingMethod | string | Method for load balancing - valid values are `leastconn`, `roundrobin`, `source`, or `uri`. If null will default to `roundrobin` | No |
| persistence | string | Persistence method for client connections to backend nodes - `none` or `source_ip`. If null will default to `none` | No |
| idleTimeout | integer | Timeout value for idle client connections to backend nodes in milliseconds - defaults to 180000 | No |
| loadBalancingMode | string | Indicates the type of load balancing – `tcp` or `http` (layer4-TCP or layer7-HTTP(s)) | Yes |
| nodes | array | Collection of entity values that describe the customer backend nodes being load balanced | No |
| forceHttps | boolean | Will redirect incoming traffic on port 80 to port 443. loadBalancingMode must be set to `tcp` and port must be set to `443` | No |
| healthCheck | object | Configures a health check that is applied to all nodes in the pool, provided they do not already have a healthCheck configured | No |

### Node Properties

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| ipAddress | string | IP of the server that will be load balanced | Yes |
| privatePort | integer | Port on which the server that will be load balanced is listening | Yes |
| status | string | `enabled` or `disabled`. Nodes set to disabled will not have any traffic directed to them. Defaults to `enabled`  | No |
| healthCheck | object | Configures a health check on this specific node. Will override any healthCheck configured on the pool | No |
| serverWeight | integer | Adjust the server's weight relative to other servers. All servers will receive a load proportional to their weight relative to the sum of all weights. Range is `1` to `256`. Default is `1` | No |

### HealthCheck Properties

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| unhealthyThreshold | integer | Number of times server healthcheck can fail befre being removed from rotation. Valid range between `2` and `10` | Yes |
| healthyThreshold | integer | Number of times unhealthy servers must pass healthcheck before being readded to rotation. Valid range is between `2` and `10` | Yes |
| intervalSeconds | integer | Seconds to wait between healthchecks. Valid range is between `5` and `300` | Yes |
| targetPort | integer | Port of the healthcheck on the server | Yes |
| mode | string | Mode over which to send healthcheck. Options are `TCP`, `SSL`, `HTTP`. Defaults to `TCP` | No |
| httpHealthCheckMethod | string | HttpMethod to use when querying healthcheck. Only valid when mode is set to `HTTP` | No |
| httpHealthCheckUrl | string | Url location of healthcheck. Only valid when mode is set to `HTTP` | No |

### Examples

#### JSON
```json
{
    "id": "a4ad7c71-1575-400e-8eb2-cef74ed557ad",
    "port": 443,
    "loadBalancingMethod": "roundrobin",
    "persistence": "none",
    "idleTimeout": 180000,
    "loadBalancingMode": "tcp",
    "nodes": [
        {
            "ipAddress": "10.140.218.25",
            "privatePort": 8443,
            "status": "enabled",
            "healthCheck": null,
            "serverWeight": null
        },
        {
            "ipAddress": "10.140.218.26",
            "privatePort": 8443,
            "status": "enabled",
            "healthCheck": null,
            "serverWeight": null
        }
    ],
    "forceHttps": true,
    "healthCheck": {
        "unhealthyThreshold": 5,
        "healthyThreshold": 2,
        "intervalSeconds": 60,
        "targetPort": 122,
        "mode": "TCP",
        "httpHealthCheckMethod": null,
        "httpHealthCheckUrl": null
    } 
}
```

## Response

The response will be an entity representing the request to update the pool. Request status can be tracked from the [Get LBaaS Request](get-lbaas-request.md).

### Entity Definition

| Name | Type | Description |
| --- | --- | --- |
| id | string | ID of the Pool update request |
| status | string | Initially the response will show a status for the request of "ACTIVE".  A status of "COMPLETE" will show in the Response of a function when the load balancer has been updated with the new configuration. |
| description | string | Describes the activity running within the Pool update process |
| requestDate | string | Date-time stamp of the request |
| completionDate | string | Date-time stamp of pool update.  Null value returned until process has completed |
| links | array | Collection of entity links that point to resources related to this LBaaS Group |

### Examples

#### JSON
```json
{  
    "id": "d685c028-5852-4b6f-8511-a407147db0e4",
    "status": "ACTIVE",  
    "description": "Update Pool to Load Balancer 329a98e6-977a-4c25-a7c8-174209fe1d31",  
    "requestDate": 1450383770701,  
    "completionDate": null,  
    "links": [  
        {  
            "rel": "loadbalancer",  
            "href": "",  
            "resourceId": "329a98e6-977a-4c25-a7c8-174209fe1d31"  
        },
        {
            "red": "pool",
            "href": "",
            "resourceId": "a4ad7c71-1575-400e-8eb2-cef74ed557ad"
        } 
    ]  
}
```
