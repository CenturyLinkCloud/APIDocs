{{{
  "title": "Get Pool",
  "date": "9-13-2018",
  "author": "Matt Peterson",
  "attachments": []
}}}

Gets the configuration of a pool on an LBaaS instance for a given account in a given data center. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you need to retrieve the configuration of an existing pool on a load balancer. 

## URL

### Structure

    GET https://api.loadbalancer.ctl.io/{accountAlias}/{dataCenter}/loadbalancers/{loadBalancerId}/pools/{poolId}

### Example

    GET https://api.loadbalancer.ctl.io/DV01/NY1/loadbalancers/329a98e6-977a-4c25-a7c8-174209fe1d31/pools/a4ad7c71-1575-400e-8eb2-cef74ed557ad

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| accountAlias | string | Short code for the particular account which owns the load balancer | Yes |
| dataCenter | string | Short string representing the data center in which the load balancer resides | Yes |
| loadBalancerId | string | Id of the load balancer | Yes |
| poolId | string | Id of the pool you want to view | Yes |

## Response

### Entity Definition

| Name | Type | Description |
| --- | --- | --- |
| id | string | The id of the pool |
| port | integer | The port on which incoming traffic will send requests. Valid port ranges are between `23` and `65534` |
| loadBalancingMethod | string | Method for load balancing - valid values are `leastconn`, `roundrobin`, `source`, or `uri`. If null will default to `roundrobin` |
| persistence | string | Persistence method for client connections to backend nodes - `none` or `source_ip`. If null will default to `none` |
| idleTimeout | integer | Timeout value for idle client connections to backend nodes in milliseconds - defaults to 180000 |
| loadBalancingMode | string | Indicates the type of load balancing – `tcp` or `http` (layer4-TCP or layer7-HTTP(s)) |
| nodes | array | Collection of entity values that describe the customer backend nodes being load balanced |
| forceHttps | boolean | Will redirect incoming traffic on port 80 to port 443. |
| healthCheck | object | Configures a health check that is applied to all nodes in the pool, provided they do not already have a healthCheck configured |

### Node Definition 

| Name | Type | Description |
| --- | --- | --- |
| ipAddress | string | IP of the server that will be load balanced |
| privatePort | integer | Port on which the server that will be load balanced is listening |
| status | string | `enabled` or `disabled`. Nodes set to disabled will not have any traffic directed to them. Defaults to `enabled` | 
| healthCheck | object | Configures a health check on this specific node. Will override any healthCheck configured on the pool |
| serverWeight | integer | Adjust the server's weight relative to other servers. All servers will receive a load proportional to their weight relative to the sum of all weights. Range is `1` to `256`. Default is `1` |

### HealthCheck Definition 

| Name | Type | Description |
| --- | --- | --- |
| unhealthyThreshold | integer | Number of times server healthcheck can fail befre being removed from rotation. Valid range between `2` and `10` |
| healthyThreshold | integer | Number of times unhealthy servers must pass healthcheck before being readded to rotation. Valid range is between `2` and `10` |
| intervalSeconds | integer | Seconds to wait between healthchecks. Valid range is between `5` and `300` |
| targetPort | integer | Port of the healthcheck on the server |
| mode | string | Mode over which to send healthcheck. Options are `TCP`, `SSL`, `HTTP`. Defaults to `TCP` |
| httpHealthCheckMethod | string | HttpMethod to use when querying healthcheck. Only valid when mode is set to `HTTP` |
| httpHealthCheckUrl | string | Url location of healthcheck. Only valid when mode is set to `HTTP` |

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
