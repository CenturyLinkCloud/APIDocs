{{{
  "title": "Get LBaaS Instance",
  "date": "9-10-2018",
  "author": "Matt Peterson",
  "attachments": []
}}}

Allows the user to retrieve a single LBaaS instance. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token

### When to Use It

Use this API operation when you need to retrieve the details of a single LBaaS instance. 

## URL

### Structure

    GET https://api.loadbalancer.ctl.io/{accountAlias}/{dataCenter}/loadbalancers/{loadBalancerId}

### Example

    GET https://api.loadbalancer.ctl.io/DV01/NY1/loadbalancers/329a98e6-977a-4c25-a7c8-174209fe1d31

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| accountAlias | string | Short code for a particular account | Yes |
| dataCenter | string | Short string representing the data center in which the load balancer was created | Yes |
| loadBalancerId | string | The id of the load balancer. | Yes |

## Response

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
    "name": "ExampleGroup",
    "description": "Sample load balancer",
    "publicIPAddress": "64.211.224.123",
    "pools": [
        {
            "id": "efdfc028-a694-481d-b406-cb68e5bf2f04",
            "port": 443,
            "loadBalancingMethod": "roundrobin",
            "persistence": "none",
            "idleTimeout": 180000,
            "loadBalancingMode": "tcp",
            "nodes": [
                {
                    "ipAddress": "10.140.218.125",
                    "privatePort": 443,
                    "status": "enabled",
                    "healthCheck": null,
                    "serverWeight": null
                },
                {
                    "ipAddress": "10.140.218.126",
                    "privatePort": 443,
                    "status": "enabled",
                    "healthCheck": null,
                    "serverWeight": null
                }
            ],
            "forceHttps": true,
            "healthCheck": null,
            "sslOffloading": null
        }
    ],
    "status": "active",
    "accountAlias": "DV01",
    "dataCenter": "NY1",
    "creationTime": 1471902898537,
    "deletionTime": null
}
```
