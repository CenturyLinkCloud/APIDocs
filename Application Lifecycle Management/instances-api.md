{{{
"title": "Instances API",
"date": "09-01-2016",
"author": "",
"attachments": [],
"contentIsHTML": false
}}}

**Manage and perform actions on instances.**

**Create or List Instances**

| Resource | Description |
|----------|-------------|
| [GET /services/instances](#get-servicesinstances)) | Gets the list of instances. |
| [POST /services/instances](#post-servicesinstances) | Creates a new instance, imports an unregistered instance or instances based on schema. |

GET /services/instances/{instance_id}/service
**Perform Instance Operations**

| Resource | Description |
|----------|-------------|
| [GET /services/instances/{instance_id}](#get-servicesinstancesinstance_id)| Fetches an existing instance.|
| [PUT /services/instances/{instance_id}](#put-servicesinstancesinstance_id) | Updates an existing instance. |
| [DELETE /services/instances/{instance_id}](#delete-servicesinstancesinstance_id) | Terminates, force-terminates, or deletes an existing instance.|
| [GET /services/instances/{instance_id}/service](#get-servicesinstancesinstance_idservice) | Gets the instance service. |
| [GET /services/instances/{instance_id}/activity](#get-servicesinstancesinstance_idactivity) | Gets all activity logs from the executed operations of an instance. |
| [GET /services/instances/{instance_id}/machine_logs](#get-servicesinstancesinstance_idmachine_logs) | Gets the logs of all machines of a deployed instance. |
| [GET /services/instances/{instance_id}/bindings](#get-servicesinstancesinstance_idbindings) | Gets the binding of a instance. |
| [GET /services/instances/{instance_id}/operations](#get-servicesinstancesinstance_idoperations) | Gets all operations of an instance. |
| [PUT /services/instances/{instance_id}/deploy](#put-servicesinstancesinstance_iddeploy) | Re-deploy an existing instance. |
| [PUT /services/instances/{instance_id}/poweron](#put-servicesinstancesinstance_idpoweron) | Power-on an existing instance. |
| [PUT /services/instances/{instance_id}/shutdown](#put-servicesinstancesinstance_idshutdown) | 	Shutdown an existing instance. |
| [PUT /services/instances/{instance_id}/   ](#put-servicesinstancesinstance_idreinstall) | Re-install an existing instance. |
| [PUT /services/instances/{instance_id}/reconfigure](#put-servicesinstancesinstance_idreconfigure) | Re-configure an existing instance. |
| [PUT /services/instances/{instance_id}/import](#put-servicesinstancesinstance_idimport) | Retry to import an unregistered instance. |
| [PUT /services/instances/{instance_id}/cancel_import](#put-servicesinstancesinstance_idcancel_import) | Cancel a failed import of an unregistered instance. |


### GET /services/instances
Gets instances that are accessible in the personal workspace of the authenticated user.
### URL

#### Structure
```
[GET] /services/instances
```

#### Example
```
[GET] https://cam.ctl.io/services/instances
```

### Request

#### Headers
```
Content-Type: application/json
Authorization: Bearer your_json_web_token
ElasticBox-Release: 4.0
```
#### URI Parameters
* None

### Response
#### Normal Response Codes

- **200** OK

#### Common Error Response Codes

- **400** Bad Request
- **401** Unauthorized

#### Response Parameters

| Parameter | Type |Description |
|-----------|------|------------|
| box | string | Box unique identifier used to create the instance. |
| lease | array | Schedules an instance with three parameters: <li>released. Is a true or false boolean value. False means that the operation scheduled on the instance is not executed yet.</li><li>operation. Specifies an instance to stop with **shutdown** or **terminate**. When not scheduled, the instance is set to **alwayson**.</li><li>expire. Specifies in UTC format YYYY-MM-DD HH:MM:SS.SSSSSS, the time and date for stopping an instance. It’s required only when an instance is set to terminate or shut down.</li> |
| created | string | Creation date. |
| updated |  string | Date of the last update. |
| automatic_updates | string | One of the: major, minor, patch, off. Default off. |
| members | array | List of members whom you shared the instance. |
| owner | string | Instance owner. |
| operation | string | Last operation, there are seven types of operations: deploy , shutdown , poweron , reinstall , reconfigure , terminate and terminate_service |
| name | string | Instance name. |
| service | object | Instance service. |
| service.type | string | Required. Can be one of these types: Linux Compute, Windows Compute and CloudFormation Service. |
| service.id | string | Service unique identifier. |
| service.machines | array | List of service machines |
| machine | object | Machine contained in the service machines list. |
| machine.state | string | Machine state, there are three possible states: processing , done and unavailable. |
| machine.name | string | Machine name. |
| machine.workflow | array | List of workflow actions, where each workflow action object contains three parameters: box, event, and script. |
| workflow.box | string | Workflow action box. |
| workflow.event | string | Workflow action event. |
| workflow.script | string | Workflow action script uri. |
| tags | array | Instance tags. |
| variables | array | 	List of instance variables, each variable object contains the parameters: type , name and value. |
| boxes | array | List of boxes where each box object contains a service parameter. The service parameter can have one of these values: Linux Compute, Windows Compute and CloudFormation Service. |
| uri |  string | Instance uri. |
| state | string | Instance state, there are three possible states: processing , done and unavailable |
| bindings | array | List of instance bindings. |
| binding | object | Binding contained in the bindings list, each binding object contains the parameters: instance and name. |
| id | array | Instance unique identifier |
| icon | string | Instance icon uri. |
| schema | string | Instance schema uri. |


#### Response Body
```
[{
   "box": "691df09c-7588-4310-9e9a-a7993f3670b0",
   "updated": "2015-10-27 16:17:42.237233",
   "automatic_updates": "off",
   "name": "TestVSphere",
   "service": {
       "type": "Linux Compute",
       "id": "eb-ay43t",
       "machines": [
           {
               "state": "done",
               "name": "eb-ay43t-1",
               "workflow": []
           }
       ]
   },
   "tags": [],
   "policy_box": {
       "profile": {
           "resource_pool": "pullrequest",
           "datacenter": "ElasticBox - Development",
           "network": "Cluster Network",
           "disks": [
               {
                   "datastore": "Development Storage",
                   "name": "Hard disk 1",
                   "template": true,
                   "size": 97
               }
           ],
           "customization_spec": "None",
           "network_mor": "network-15",
           "instances": 1,
           "template": "debian-7-8-x86-64",
           "datastore": "Development Storage",
           "flavor": "Tiny",
           "schema": "http://elasticbox.net/schemas/vsphere/compute/profile"
       },
       "provider_id": "cac26e4c-16f8-46ad-83ae-52a2b1ba4fca",
       "automatic_updates": "off",
       "name": "TestVSphere",
       "created": "2015-10-09 08:25:02.378295",
       "deleted": null,
       "variables": [],
       "updated": "2015-10-09 08:25:02.378295",
       "lifespan": {
           "operation": "none"
       },
       "visibility": "workspace",
       "members": [],
       "organization": "elasticbox",
       "owner": "operations",
       "claims": [
           "linux"
       ],
       "id": "691df09c-7588-4310-9e9a-a7993f3670b0",
       "schema": "http://elasticbox.net/schemas/boxes/policy"
   },
   "created": "2015-10-09 08:25:36.025086",
   "uri": "/services/instances/i-6bdwwm",
   "id": "i-6bdwwm",
   "state": "done",
   "boxes": [
       {
           "profile": {
               "resource_pool": "pullrequest",
               "datacenter": "ElasticBox - Development",
               "network": "Cluster Network",
               "disks": [
                   {
                       "datastore": "Development Storage",
                       "name": "Hard disk 1",
                       "template": true,
                       "size": 97
                   }
               ],
               "customization_spec": "None",
               "network_mor": "network-15",
               "instances": 1,
               "template": "debian-7-8-x86-64",
               "datastore": "Development Storage",
               "flavor": "Tiny",
               "schema": "http://elasticbox.net/schemas/vsphere/compute/profile"
           },
           "provider_id": "cac26e4c-16f8-46ad-83ae-52a2b1ba4fca",
           "automatic_updates": "off",
           "name": "TestVSphere",
           "created": "2015-10-09 08:25:02.378295",
           "deleted": null,
           "variables": [],
           "updated": "2015-10-09 08:25:02.378295",
           "lifespan": {
               "operation": "none"
           },
           "visibility": "workspace",
           "members": [],
           "organization": "elasticbox",
           "owner": "operations",
           "claims": [
               "linux"
           ],
           "id": "691df09c-7588-4310-9e9a-a7993f3670b0",
           "schema": "http://elasticbox.net/schemas/boxes/policy"
       }
   ],
   "members": [],
   "owner": "operations",
   "icon": null,
   "operation": {
       "event": "terminate_service",
       "workspace": "operations",
       "created": "2015-10-27 16:17:36.268988"
   },
   "variables": [],
   "schema": "http://elasticbox.net/schemas/instance"
},
{
   "box": "15b5bc28-5ac5-4897-bd72-d4f2101da47a",
   "updated": "2015-10-09 10:00:07.434386",
   "automatic_updates": "off",
   "name": "Test2",
   "service": {
       "type": "Linux Compute",
       "id": "eb-l8gqr",
       "machines": []
   },
   "tags": [],
   "policy_box": {
       "profile": {
           "resource_pool": "pullrequest",
           "datacenter": "ElasticBox - Development",
           "network": "Cluster Network",
           "disks": [],
           "customization_spec": "None",
           "compute_resource": null,
           "instances": 1,
           "network_mor": "network-15",
           "template": "ebx-no-disks",
           "folder": "Templates",
           "flavor": "Tiny",
           "datastore": "Development Storage",
           "schema": "http://elasticbox.net/schemas/vsphere/compute/profile"
       },
       "provider_id": "cac26e4c-16f8-46ad-83ae-52a2b1ba4fca",
       "automatic_updates": "off",
       "name": "Test2",
       "created": "2015-10-09 08:30:52.736712",
       "deleted": null,
       "variables": [],
       "updated": "2015-10-09 08:31:10.338900",
       "lifespan": {
           "operation": "none"
       },
       "visibility": "workspace",
       "members": [],
       "claims": [
           "linux"
       ],
       "owner": "operations",
       "organization": "elasticbox",
       "id": "15b5bc28-5ac5-4897-bd72-d4f2101da47a",
       "schema": "http://elasticbox.net/schemas/boxes/policy"
   },
   "created": "2015-10-09 08:31:16.536012",
   "uri": "/services/instances/i-jt8p5d",
   "id": "i-jt8p5d",
   "state": "done",
   "boxes": [
       {
           "profile": {
               "resource_pool": "pullrequest",
               "datacenter": "ElasticBox - Development",
               "network": "Cluster Network",
               "disks": [],
               "customization_spec": "None",
               "compute_resource": null,
               "instances": 1,
               "network_mor": "network-15",
               "template": "ebx-no-disks",
               "folder": "Templates",
               "flavor": "Tiny",
               "datastore": "Development Storage",
               "schema": "http://elasticbox.net/schemas/vsphere/compute/profile"
           },
           "provider_id": "cac26e4c-16f8-46ad-83ae-52a2b1ba4fca",
           "automatic_updates": "off",
           "name": "Test2",
           "created": "2015-10-09 08:30:52.736712",
           "deleted": null,
           "variables": [],
           "updated": "2015-10-09 08:31:10.338900",
           "lifespan": {
               "operation": "none"
           },
           "visibility": "workspace",
           "members": [],
           "claims": [
               "linux"
           ],
           "owner": "operations",
           "organization": "elasticbox",
           "id": "15b5bc28-5ac5-4897-bd72-d4f2101da47a",
           "schema": "http://elasticbox.net/schemas/boxes/policy"
       }
   ],
   "members": [],
   "owner": "operations",
   "icon": null,
   "operation": {
       "event": "terminate_service",
       "workspace": "operations",
       "created": "2015-10-09 09:59:37.618930"
   },
   "variables": [],
   "schema": "http://elasticbox.net/schemas/instance"
}]
```

### POST /services/instances
Creates a new instance and gets the created instance.

### URL

#### Structure
```
[POST] /services/instances
```

#### Example
```
[POST] https://cam.ctl.io/services/instances
```
The next example its the request schedules the new instance.
```
{
    "schema": "http://elasticbox.net/schemas/deploy-instance-request",
    "owner": "operations",
    "name": "TestServe",
    "box": {
        "id": "4f996250-a420-4e44-8e97-4af86328148f",
        "variables": [
            {
                "name": "variable_name",
                "type": "Text",
                "value": "overridden variable value at deployment time",
                "required": true,
                "visibility": "public"
            }
        ]
    },
    "instance_tags": [],
    "automatic_updates": "off",
    "policy_box": {
        "id": "11c8882e-3888-4bdd-bd2d-b92766a423c7",
        "variables": []
    }
}
```


### Request

#### Headers
```
Content-Type: application/json
Authorization: Bearer your_json_web_token
ElasticBox-Release: 4.0
```
#### URI Parameters
| Parameter | Type |Description |
|-----------|------|------------|
| schema | string | Required. Instance schema URI. |
| owner | string | ID of the workspace where the instance is posted. |
| box | Object | Box object with its id and a list of overridden variable objects at deployment time |
| policy_box | Object | Box object with its id and a list of overridden variable objects at deployment time |
| automatic_updates | string | One of the: major, minor, patch, off. Default off. |
| lease | array | Schedules an instance with two parameters:<li>expire. Specifies in UTC format YYYY-MM-DD HH:MM:SS.SSSSSS, the time and date for stopping an instance. It’s required only when an instance is set to terminate or shut down.</li><li>operation. Specifies an instance to stop with **shutdown** or **terminate**. When not scheduled, the instance is set to **alwayson**.</li> |
| name | string | Instance name. |
| instance_tags | array | List of tags defined at deployment time. |

### Response
#### Normal Response Codes
- **202** OK

#### Common Error Response Codes
- **400** Invalid Data


#### Response Body

```
{
    "automatic_updates": "off",
    "variables": [
        {
            "required": true,
            "type": "Text",
            "name": "variable_name",
            "value": "overridden variable value at deployment time",
            "visibility": "public"
        }
    ],
    "automatic_reconfiguration": true,
    "owner": "operations",
    "pricing_history": [
        {
            "pricing_info": {
                "estimated_monthly": 3168000,
                "provider_type": "Amazon Web Services",
                "hourly_price": 4400,
                "factor": 100000
            },
            "from": "2018-12-26 15:18:26.524612"
        }
    ],
    "bindings": [],
    "operation": {
        "event": "deploy",
        "workspace": "operations",
        "created": "2018-12-26 15:18:26.524612"
    },
    "service": {
        "type": "Linux Compute",
        "id": "eb-l2gmi",
        "machines": []
    },
    "id": "i-b1qtkz",
    "is_deploy_only": true,
    "state": "processing",
    "schema": "http://elasticbox.net/schemas/instance",
    "updated": "2018-12-26 15:18:26.532799",
    "tags": [],
    "deleted": null,
    "boxes": [
        {
            "updated": "2018-12-26 15:17:00.128048",
            "automatic_updates": "off",
            "requirements": [],
            "name": "php-server",
            "created": "2018-12-11 14:29:56.791167",
            "deleted": null,
            "variables": [
                {
                    "required": false,
                    "type": "Text",
                    "name": "variable_name",
                    "value": "value",
                    "visibility": "public"
                }
            ],
            "visibility": "workspace",
            "id": "4f996250-a420-4e44-8e97-4af86328148f",
            "members": [],
            "owner": "operations",
            "organization": "centurylink",
            "events": {
                "pre_install": {
                    "url": "/services/blobs/download/5c0fcb8cc9a9d120195a3f7a/pre_install",
                    "length": 39,
                    "destination_path": "scripts",
                    "content_type": "text/x-shellscript"
                },
                "configure": {
                    "url": "/services/blobs/download/5c0fca3dc9a9d120195a3f71/configure",
                    "length": 23,
                    "destination_path": "scripts",
                    "content_type": "text/x-shellscript"
                }
            },
            "draft_from": "f0023f62-8e43-41d6-a248-691f092d6287",
            "schema": "http://elasticbox.net/schemas/boxes/script"
        }
    ],
    "members": [],
    "box": "4f996250-a420-4e44-8e97-4af86328148f",
    "name": "TestServe",
    "created": "2018-12-26 15:18:26.532799",
    "policy_box": {
        "profile": {
            "subnet": "us-east-1a",
            "security_groups": [
                "Automatic"
            ],
            "pricing_info": {
                "estimated_monthly": 3168000,
                "provider_type": "Amazon Web Services",
                "hourly_price": 4400,
                "factor": 100000
            },
            "image": "Linux Compute",
            "instances": 1,
            "keypair": "None",
            "cloud": "EC2",
            "volumes": [],
            "flavor": "m1.small",
            "schema": "http://elasticbox.net/schemas/aws/ec2/profile",
            "managed_os": false,
            "location": "us-east-1"
        },
        "provider_id": "0669730b-6f01-421b-8a5e-597bca20c1bf",
        "automatic_updates": "off",
        "name": "default-small-us-east-1",
        "created": "2018-12-11 13:53:56.512649",
        "deleted": null,
        "variables": [],
        "updated": "2018-12-11 13:53:56.512649",
        "visibility": "workspace",
        "readme": {
            "url": "services/resources/default_box_overview.md",
            "upload_date": "2018-12-11 13:53:56.512131",
            "length": 1307,
            "content_type": "text/x-markdown"
        },
        "members": [],
        "claims": [
            "small",
            "linux"
        ],
        "owner": "operations",
        "organization": "centurylink",
        "id": "11c8882e-3888-4bdd-bd2d-b92766a423c7",
        "schema": "http://elasticbox.net/schemas/boxes/policy"
    },
    "uri": "/services/instances/i-b1qtkz"
}
```

### POST /services/instances
Register an unregistered instance: notice that it's the same endpoint to create a new instance.

### URL

#### Structure

```
[POST] /services/instances
```

#### Example
```
[POST] https://cam.ctl.io/services/instances
```

```
{
   "schema": "http://elasticbox.net/schemas/register-instance-request",
   "owner": "operations",
   "name": "LDAP Box",
   "unregistered_id": "7a99f95c-30e6-4986-9059-f6999d1jhgf9",
   "description": "Ldap server registered",
   "linux_username": "root",
   "private_key": "-----BEGIN RSA PRIVATE KEY-----
..................................................
-----END RSA PRIVATE KEY-----",
   "instance_tags": [],
   "automatic_updates": "off",
   "lease": {
       "expire": "2017-11-11 23:00:00.000000",
       "operation": "shutdown"
   }
}
```

For use bulk import, the request must have bulk import request schema, and a list of
unregistered instances:

```
Body:
{
  "schema": "http://elasticbox.net/schemas/bulk-import-request",
  "owner": "operations",
  "unregistered_instances": [
    {
      "schema": "http://elasticbox.net/schemas/register-instance-request",
      "name": "msql-a",
      "unregistered_id": "5eed8408-3ece-45d9-8e78-3f3472bea165",
      "instance_tags": [
        "zoneA"
      ]
    },
    {
      "schema": "http://elasticbox.net/schemas/register-instance-request",
      "name": "msql-b",
      "unregistered_id": "6b9b9ecc-f22d-4101-991c-c55f8de80439",
      "instance_tags": [
        "zoneB"
      ]
    }
  ],
  "instance_tags": [
    "registered"
  ]
}
```


### Request

#### Headers
```
Content-Type: application/json
Authorization: Bearer your_json_web_token
ElasticBox-Release: 4.0
```
#### URI Parameters

| Parameter | Type |Description |
|-----------|------|------------|
| schema | string | Required. Register Instance Request schema URI. |
| owner | string | ID of the workspace where the instance is imported. |
| name | string | Instance name to register. |
| description | string | Instance description to register. |
| unregistered_id | string | Instance unique identifier |
| linux_username | string | Linux user to install agent |
| private_key | string | Linux key to install agent  |
| windows_username | string | Windows username to install agent |
| windows_password | string | Windows password to install agent |
| instance_tags | array | List of tags defined at deployment time. |
| automatic_updates | string | One of the: major, minor, patch, off. Default off. |
| lease | array | Schedules an instance with two parameters:<li>expire. Specifies in UTC format YYYY-MM-DD HH:MM:SS.SSSSSS, the time and date for stopping an instance. It’s required only when an instance is set to terminate or shut down.</li><li>operation. Specifies an instance to stop with **shutdown** or **terminate**. When not scheduled, the instance is set to **alwayson**.</li> |

### Response
#### Normal Response Codes
- **202** OK

#### Common Error Response Codes
- **400** Invalid Data

#### Response Parameters

| Parameter | Type |Description |
|-----------|------|------------|
| lease | array | If scheduled, this object displays these parameters for the instance:<li>released. Is a true or false boolean value. False means that the operation scheduled on the instance is not executed yet.</li><li>expire. Specifies in UTC format YYYY-MM-DD HH:MM:SS.SSSSSS, the time and date for stopping an instance. It applies only when an instance is set to terminate or shut down.</li><li>operation. Specifies the stop operation scheduled as either **shutdown** or **terminate**. When not scheduled, the instance is set to **alwayson**.</li> |
| bindings | array | List of instance bindings. |
| binding | object | Binding contained in the bindings list, each binding object contains the parameters: instance and name. |
| updated | string | Date of the last update. |
|name | string | Instance name. |
| service | Object | Instance service. |
| service.type | string | Required. Can be one of these types: Linux Compute, Windows Compute and CloudFormation Service. |
| service.id | string | Service type. |
| service.machines | array | List of service machines. |
| machine | object | Machine contained in the service machines list. |
| machine.state | string | Machine state, there are three possible states: processing , done and unavailable. |
| machine.name | string | Machine name. |
| machine.workflow | array | 	List of workflow actions, where each workflow action object contains three parameters: box, event, and script. |
| workflow.box | string | Workflow action box. |
| workflow.event | string |	Workflow action event.|
| workflow.script | string | Workflow action script uri. |
| tags | array | Instance tags. |
| variables | array | 	List of instance variables, each variable object contains the parameters: type , name and value. |
| created | string | Creation date. |
| boxes | array | List of boxes |
| box.visibility | string | Indicates at what level the box is visible. By default, boxes are visible to the workspace they’re created in. Can have one of these values:<li>public: Visible to Cloud Application Manager users across all organizations.</li><li>organization: Visible to all users in the organization where the box was created.</li><li>workspace: By default, the box is visible only to members of the workspace where it was created.</li> |
| box.organization | string | Organization to which the box belongs. |
| box.updated | string | Date of the last update. |
| box.description | string | Box description. |
| box.service | string | Required. Can be one of these types: Linux Compute, Windows Compute and CloudFormation Service. |
| box.tags | array | Box tags. |
| box.variables | array | 	List of box variables, each variable object contains the parameters: type , name and value. |
| box.created | string | Creation date. |
| box.uri | string | Box uri. |
| box.id | array | Box unique identifier. |
| box.schema | string | Box schema uri. |
| box.members | array | List of Box members. |
| box.owner | string | Box owner. |
| box.bindings | array | List of Box bindings. |
| box.binding | object | Binding contained in the bindings list, each binding have a box and a name. |
| box.icon | string | Box icon uri. |
| box.events | array | 	List of Box events, there may be nine event lists: configure, dispose, install, post_configure, post_dispose, post_install, post_start, post_stop, start, and stop. |
| box.event | object | Event contained in one of the event lists, each event object contains the parameters: url , upload_date , length and destination_path. |
| box.name | string | Box name. |
| uri | string | instance uri. |
| state | string | Instance state, there are three possible states: processing , done and unavailable |
| members | array | Instance members. |
| owner | string | Instance owner. |
| operation | string | Last operation, there are seven types of operations: deploy , shutdown , poweron , reinstall , reconfigure , terminate and terminate_service |
| icon | string | Instance icon uri. |
| id | array | Instance unique identifier. |
| schema | string | Instance schema uri. |
| policy_box | object | specific deployment policy for a provider |
| policy_box.provider_id | string | provider id |
| policy_box.automatic_updates | string | One of them: mayor, minor, patch, off |
| policy_box.name | string | Policy box name |
| policy_box.variables | array | List of deployment box policy variables |
| policy_box.claims | array | List of deployment box policy claims |
| policy_box.id | string | Deployment box policy id |
| policy_box.schema | string | Deployment box policy schema |
| policy_box.members | array | 	List of members sharing the deployment policy box |
| policy_box.owner | string | Deployment box policy owner |
| policy_box.readme | object | Readme file for the Deployment policy box |


#### Response Body

```
{
 "box": "7a99f75c-30e6-4986-9059-f6889d1ff5f9",
 "policy_box": {
   "profile": {
     "image": "test",
     "instances": 1,
     "keypair": "test_keypair",
     "location": "Simulated Location",
     "flavor": "test.micro",
     "schema": "http://elasticbox.net/schemas/test/compute/profile"
   },
   "provider_id": "0476718d-2b00-45ce-8a1c-30b10a16cfc7",
   "automatic_updates": "off",
   "name": "Linux Compute",
   "created": "2015-10-21 08:35:50.165822",
   "deleted": null,
   "variables": [
     {
       "automatic_updates": "off",
       "name": "policy_box_variable",
       "required": false,
       "visibility": "public",
       "value": "381d0fd8-b59e-4be6-afc7-3ee1a0a2db1c",
       "type": "Box"
     }
   ],
   "updated": "2015-10-29 12:05:39.065397",
   "visibility": "workspace",
   "owner": "operations",
   "members": [

   ],
   "claims": [
     "linux"
   ],
   "readme": {
     "url": "/resources/default_box_overview.md",
     "upload_date": "2015-10-21 08:35:50.164926",
     "length": 1302,
     "content_type": "text/x-markdown"
   },
   "organization": "elasticbox",
   "id": "e57466ee-7094-4bd4-9121-a6df4395d493",
   "schema": "http://elasticbox.net/schemas/boxes/policy"
 },
 "updated": "2015-10-29 12:26:20.377029",
 "automatic_updates": "off",
 "name": "ScriptBoxSample",
 "service": {
   "type": "Linux Compute",
   "id": "eb-bbhzh",
   "machines": [

   ]
 },
 "tags": [

 ],
 "deleted": null,
 "variables": [
   {
     "required": true,
     "type": "Text",
     "name": "variable_name",
     "value": "variable_value_overridden",
     "visibility": "public"
   }
 ],
 "created": "2015-10-29 12:26:20.377029",
 "state": "processing",
 "uri": "/services/instances/i-3e43qa",
 "boxes": [
   {
     "updated": "2015-10-29 11:55:23.842461",
     "automatic_updates": "off",
     "requirements": [

     ],
     "description": "sample box",
     "name": "ScriptBoxSample",
     "created": "2015-10-29 10:52:08.446868",
     "deleted": null,
     "variables": [
       {
         "required": true,
         "type": "Text",
         "name": "variable_name",
         "value": "variable_value",
         "visibility": "public"
       }
     ],
     "visibility": "workspace",
     "id": "7a99f75c-30e6-4986-9059-f6889d1ff5f9",
     "members": [

     ],
     "owner": "operations",
     "organization": "elasticbox",
     "events": {
       "configure": {
         "url": "/services/blobs/download/5631fa7614841250525226cc/configure",
         "length": 5,
         "destination_path": "scripts",
         "content_type": "text/x-shellscript"
       },
       "install": {
         "url": "/services/blobs/download/5631fa6614841250525226ca/install",
         "length": 5,
         "destination_path": "scripts",
         "content_type": "text/x-shellscript"
       }
     },
     "schema": "http://elasticbox.net/schemas/boxes/script"
   }
 ],
 "members": [

 ],
 "bindings": [

 ],
 "owner": "operations",
 "operation": {
   "event": "deploy",
   "workspace": "operations",
   "created": "2015-10-29 12:26:20.375582"
 },
 "schema": "http://elasticbox.net/schemas/instance",
 "id": "i-3e43qa",
 "icon": null
}
```

### GET /services/instances/{instance_id}

Fetches an existing instance given its ID.

### URL

#### Structure
```
[GET] /services/instances/{instance_id}
```

#### Example
```
[GET] https://cam.ctl.io/services/instances/i-b1qtkz
```


### Request

#### Headers
```
Content-Type: application/json
Authorization: Bearer your_json_web_token
ElasticBox-Release: 4.0
```

#### URI Parameters
|Parameter |Type |Description | Req. |
|-----------|------|------------| ---- |
| instance_id | string | Instance id | Yes |

### Response
#### Normal Response Codes

- **200** OK

#### Common Error Response Codes

- **400** Invalid Data
- **403** Forbidden
- **404** Not Found


#### Response Parameters

| Parameter | Type |Description |
|-----------|------|------------|
| bindings | array | List of instance bindings. |
| binding | object | Binding contained in the bindings list, each binding object contains the parameters: instance and name. |
| updated |  string | Date of the last update. |
| name | string | Instance name. |
| service | object | Instance service. |
| service.type | string | Required. Can be one of these types: Linux Compute, Windows Compute and CloudFormation Service. |
| service.id | string | Service type. |
| service.machines | array | List of service machines |
| machine | object | Machine contained in the service machines list. |
| machine.state | string | Machine state, there are three possible states: processing , done and unavailable. |
| machine.name | string | Machine name. |
| machine.workflow | array | List of workflow actions, where each workflow action object contains three parameters: box, event, and script. |
| workflow.box | string | Workflow action box. |
| workflow.event | string | Workflow action event. |
| workflow.script | string | Workflow action script uri. |
| tags | array | Instance tags. |
| variables | array | List of instance variables, each variable object contains the parameters: type , name and value. |
| created | string | Creation date. |
| boxes | array | List of boxes |
| box.visibility | string | Indicates at what level the box is visible. By default, boxes are visible to the workspace they’re created in. Can have one of these values:<li>public: Visible to Cloud Application Manager users across all organizations.</li><li>organization: Visible to all users in the organization where the box was created.</li><li>workspace: By default, the box is visible only to members of the workspace where it was created.</li> |
| box.organization | string | Organization to which the box belongs. |
| box.updated | string | Date of the last update. |
| box.description | string | Box description. |
| box.service | string | Required. Can be one of these types: Linux Compute, Windows Compute and CloudFormation Service. |
| box.tags | array | Box tags. |
| box.variables | array | 	List of box variables, each variable object contains the parameters: type , name and value. |
| box.created | string | Creation date. |
| box.uri | string | Box uri. |
| box.id | array | Box unique identifier. |
| box.schema | string | Box schema uri. |
| box.members | array | List of Box members. |
| box.owner | string | Box owner. |
| box.bindings | array | List of Box bindings. |
| box.binding | object | Binding contained in the bindings list, each binding have a box and a name. |
| box.icon | string | Box icon uri. |
| box.events | array | 	List of Box events, there may be nine event lists: configure, dispose, install, post_configure, post_dispose, post_install, post_start, post_stop, start, and stop. |
| box.event | object | Event contained in one of the event lists, each event object contains the parameters: url , upload_date , length and destination_path. |
| box.name | string | Box name. |
| policy_box | object | specific deployment policy for a provider |
| policy_box.provider_id | string | provider id |
| policy_box.automatic_updates | string | One of them: mayor, minor, patch, off |
| policy_box.name | string | Policy box name |
| policy_box.variables | array | List of deployment box policy variables |
| policy_box.claims | array | List of deployment box policy claims |
| policy_box.id | string | Deployment box policy id |
| policy_box.schema | string | Deployment box policy schema |
| policy_box.members | array | 	List of members sharing the deployment policy box |
| policy_box.owner | string | Deployment box policy owner |
| policy_box.readme | object | Readme file for the Deployment policy box |
| uri | string | instance uri. |
| state | string | Instance state, there are three possible states: processing , done and unavailable |
| members | array | Instance members. |
| owner | string | Instance owner. |
| operation | string | Last operation, there are seven types of operations: deploy , shutdown , poweron , reinstall , reconfigure , terminate and terminate_service |
| icon | string | Instance icon uri. |
| id | array | Instance unique identifier. |
| schema | string | Instance schema uri. |



#### Response Body
```
{
    "automatic_updates": "off",
    "variables": [
        {
            "required": true,
            "type": "Text",
            "name": "variable_name",
            "value": "overridden variable value at deployment time",
            "visibility": "public"
        }
    ],
    "automatic_reconfiguration": true,
    "owner": "operations",
    "pricing_history": [
        {
            "pricing_info": {
                "estimated_monthly": 3168000,
                "provider_type": "Amazon Web Services",
                "hourly_price": 4400,
                "factor": 100000
            },
            "from": "2018-12-26 15:18:26.524612"
        }
    ],
    "operation": {
        "event": "deploy",
        "workspace": "operations",
        "created": "2018-12-26 15:18:27.567661"
    },
    "bindings": [],
    "service": {
        "type": "Linux Compute",
        "id": "eb-l2gmi",
        "machines": [
            {
                "state": "done",
                "name": "testserve-eb-l2gmi-1",
                "workflow": []
            }
        ]
    },
    "id": "i-b1qtkz",
    "is_deploy_only": true,
    "state": "done",
    "schema": "http://elasticbox.net/schemas/instance",
    "updated": "2018-12-26 15:21:56.516934",
    "tags": [],
    "deleted": null,
    "boxes": [
        {
            "updated": "2018-12-26 15:17:00.128048",
            "automatic_updates": "off",
            "requirements": [],
            "name": "php-server",
            "created": "2018-12-11 14:29:56.791167",
            "deleted": null,
            "variables": [
                {
                    "required": false,
                    "type": "Text",
                    "name": "variable_name",
                    "value": "value",
                    "visibility": "public"
                }
            ],
            "visibility": "workspace",
            "id": "4f996250-a420-4e44-8e97-4af86328148f",
            "members": [],
            "owner": "operations",
            "organization": "centurylink",
            "events": {
                "pre_install": {
                    "url": "/services/blobs/download/5c0fcb8cc9a9d120195a3f7a/pre_install",
                    "length": 39,
                    "destination_path": "scripts",
                    "content_type": "text/x-shellscript"
                },
                "configure": {
                    "url": "/services/blobs/download/5c0fca3dc9a9d120195a3f71/configure",
                    "length": 23,
                    "destination_path": "scripts",
                    "content_type": "text/x-shellscript"
                }
            },
            "draft_from": "f0023f62-8e43-41d6-a248-691f092d6287",
            "schema": "http://elasticbox.net/schemas/boxes/script"
        }
    ],
    "members": [],
    "box": "4f996250-a420-4e44-8e97-4af86328148f",
    "name": "TestServe",
    "created": "2018-12-26 15:18:26.532799",
    "policy_box": {
        "profile": {
            "subnet": "us-east-1a",
            "security_groups": [
                "Automatic"
            ],
            "pricing_info": {
                "estimated_monthly": 3168000,
                "provider_type": "Amazon Web Services",
                "hourly_price": 4400,
                "factor": 100000
            },
            "image": "Linux Compute",
            "instances": 1,
            "keypair": "None",
            "location": "us-east-1",
            "volumes": [],
            "cloud": "EC2",
            "flavor": "m1.small",
            "managed_os": false,
            "schema": "http://elasticbox.net/schemas/aws/ec2/profile"
        },
        "provider_id": "0669730b-6f01-421b-8a5e-597bca20c1bf",
        "automatic_updates": "off",
        "name": "default-small-us-east-1",
        "created": "2018-12-11 13:53:56.512649",
        "deleted": null,
        "variables": [],
        "updated": "2018-12-11 13:53:56.512649",
        "visibility": "workspace",
        "readme": {
            "url": "services/resources/default_box_overview.md",
            "upload_date": "2018-12-11 13:53:56.512131",
            "length": 1307,
            "content_type": "text/x-markdown"
        },
        "members": [],
        "claims": [
            "small",
            "linux"
        ],
        "owner": "operations",
        "organization": "centurylink",
        "id": "11c8882e-3888-4bdd-bd2d-b92766a423c7",
        "schema": "http://elasticbox.net/schemas/boxes/policy"
    },
    "uri": "/services/instances/i-b1qtkz"
}
```

### PUT /services/instances/{instance_id}

Given the instance ID, updates only these fields of an existing instance: boxes, tags, schedule, members, and variables. The request body should contain an instance object.

### URL

#### Structure
```
[PUT] /services/instances/{instance_id}
```

#### Example
```
[PUT] https://cam.ctl.io/services/instances/eb-bbhzh
```


### Request

#### Headers
```
Content-Type: application/json
Authorization: Bearer your_json_web_token
ElasticBox-Release: 4.0
```

#### URI Parameters

|Parameter |Type |Description | Req. |
|-----------|------|------------| ---- |
| instance_id | string | Instance id | Yes |
| bindings | array | List of instance bindings. |
| binding | object | Binding contained in the bindings list, each binding object contains the parameters: instance and name. |
| updated |  string | Date of the last update. |
| name | string | Instance name. |
| service | object | Instance service. |
| service.type | string | Required. Can be one of these types: Linux Compute, Windows Compute and CloudFormation Service. |
| service.id | string | Service type. |
| service.machines | array | List of service machines |
| machine | object | Machine contained in the service machines list. |
| machine.state | string | Machine state, there are three possible states: processing , done and unavailable. |
| machine.name | string | Machine name. |
| machine.workflow | array | List of workflow actions, where each workflow action object contains three parameters: box, event, and script. |
| workflow.box | string | Workflow action box. |
| workflow.event | string | Workflow action event. |
| workflow.script | string | Workflow action script uri. |
| tags | array | Instance tags. |
| variables | array | List of instance variables, each variable object contains the parameters: type , name and value. |
| created | string | Creation date. |
| boxes | array | List of boxes |
| box.visibility | string | Indicates at what level the box is visible. By default, boxes are visible to the workspace they’re created in. Can have one of these values:<li>public: Visible to Cloud Application Manager users across all organizations.</li><li>organization: Visible to all users in the organization where the box was created.</li><li>workspace: By default, the box is visible only to members of the workspace where it was created.</li> |
| box.organization | string | Organization to which the box belongs. |
| box.updated | string | Date of the last update. |
| box.description | string | Box description. |
| box.service | string | Required. Can be one of these types: Linux Compute, Windows Compute and CloudFormation Service. |
| box.tags | array | Box tags. |
| box.variables | array | 	List of box variables, each variable object contains the parameters: type , name and value. |
| box.created | string | Creation date. |
| box.uri | string | Box uri. |
| box.id | array | Box unique identifier. |
| box.schema | string | Box schema uri. |
| box.members | array | List of Box members. |
| box.owner | string | Box owner. |
| box.bindings | array | List of Box bindings. |
| box.binding | object | Binding contained in the bindings list, each binding have a box and a name. |
| box.icon | string | Box icon uri. |
| box.events | array | 	List of Box events, there may be nine event lists: configure, dispose, install, post_configure, post_dispose, post_install, post_start, post_stop, start, and stop. |
| box.event | object | Event contained in one of the event lists, each event object contains the parameters: url , upload_date , length and destination_path. |
| box.name | string | Box name. |
| policy_box | object | specific deployment policy for a provider |
| policy_box.provider_id | string | provider id |
| policy_box.automatic_updates | string | One of them: mayor, minor, patch, off |
| policy_box.name | string | Policy box name |
| policy_box.variables | array | List of deployment box policy variables |
| policy_box.claims | array | List of deployment box policy claims |
| policy_box.id | string | Deployment box policy id |
| policy_box.schema | string | Deployment box policy schema |
| policy_box.members | array | 	List of members sharing the deployment policy box |
| policy_box.owner | string | Deployment box policy owner |
| policy_box.readme | object | Readme file for the Deployment policy box |
| uri | string | instance uri. |
| state | string | Instance state, there are three possible states: processing , done and unavailable |
| members | array | Instance members. |
| owner | string | Instance owner. |
| operation | string | Last operation, there are seven types of operations: deploy , shutdown , poweron , reinstall , reconfigure , terminate and terminate_service |
| icon | string | Instance icon uri. |
| id | array | Instance unique identifier. |
| schema | string | Instance schema uri. |
| lease | array | Schedules an instance with two parameters:<li>expire. Specifies in UTC format YYYY-MM-DD HH:MM:SS.SSSSSS, the time and date for stopping an instance. It’s required only when an instance is set to terminate or shut down.</li><li>operation. Specifies an instance to stop with **shutdown** or **terminate**. When not scheduled, the instance is set to **alwayson**.</li> |

### Response
#### Normal Response Codes

- **200** OK
- **202** OK

#### Common Error Response Codes

- **400** Invalid Data
- **403** Forbidden
- **404** Not Found


#### Response Parameters

| Parameter | Type |Description |
|-----------|------|------------|
| bindings | array | List of instance bindings. |
| binding | object | Binding contained in the bindings list, each binding object contains the parameters: instance and name. |
| updated | string | Date of the last update. |
|name | string | Instance name. |
| service | Object | Instance service. |
| service.type | string | Required. Can be one of these types: Linux Compute, Windows Compute and CloudFormation Service. |
| service.id | string | Service type. |
| service.machines | array | List of service machines. |
| machine | object | Machine contained in the service machines list. |
| machine.state | string | Machine state, there are three possible states: processing , done and unavailable. |
| machine.name | string | Machine name. |
| machine.workflow | array | 	List of workflow actions, where each workflow action object contains three parameters: box, event, and script. |
| workflow.box | string | Workflow action box. |
| workflow.event | string |	Workflow action event.|
| workflow.script | string | Workflow action script uri. |
| tags | array | Instance tags. |
| variables | array | 	List of instance variables, each variable object contains the parameters: type , name and value. |
| created | string | Creation date. |
| boxes | array | List of boxes |
| box.visibility | string | Indicates at what level the box is visible. By default, boxes are visible to the workspace they’re created in. Can have one of these values:<li>public: Visible to Cloud Application Manager users across all organizations.</li><li>organization: Visible to all users in the organization where the box was created.</li><li>workspace: By default, the box is visible only to members of the workspace where it was created.</li> |
| box.organization | string | Organization to which the box belongs. |
| box.updated | string | Date of the last update. |
| box.description | string | Box description. |
| box.service | string | Required. Can be one of these types: Linux Compute, Windows Compute and CloudFormation Service. |
| box.tags | array | Box tags. |
| box.variables | array | 	List of box variables, each variable object contains the parameters: type , name and value. |
| box.created | string | Creation date. |
| box.uri | string | Box uri. |
| box.id | array | Box unique identifier. |
| box.schema | string | Box schema uri. |
| box.members | array | List of Box members. |
| box.owner | string | Box owner. |
| box.bindings | array | List of Box bindings. |
| box.binding | object | Binding contained in the bindings list, each binding have a box and a name. |
| box.icon | string | Box icon uri. |
| box.events | array | 	List of Box events, there may be nine event lists: configure, dispose, install, post_configure, post_dispose, post_install, post_start, post_stop, start, and stop. |
| box.event | object | Event contained in one of the event lists, each event object contains the parameters: url , upload_date , length and destination_path. |
| box.name | string | Box name. |
| policy_box | object | specific deployment policy for a provider |
| policy_box.provider_id | string | provider id |
| policy_box.automatic_updates | string | One of them: mayor, minor, patch, off |
| policy_box.name | string | Policy box name |
| policy_box.variables | array | List of deployment box policy variables |
| policy_box.claims | array | List of deployment box policy claims |
| policy_box.id | string | Deployment box policy id |
| policy_box.schema | string | Deployment box policy schema |
| policy_box.members | array | 	List of members sharing the deployment policy box |
| policy_box.owner | string | Deployment box policy owner |
| policy_box.readme | object | Readme file for the Deployment policy box |
| uri | string | instance uri. |
| state | string | Instance state, there are three possible states: processing , done and unavailable |
| members | array | Instance members. |
| owner | string | Instance owner. |
| operation | string | Last operation, there are seven types of operations: deploy , shutdown , poweron , reinstall , reconfigure , terminate and terminate_service |
| icon | string | Instance icon uri. |
| id | array | Instance unique identifier. |
| schema | string | Instance schema uri. |
| lease | array | Schedules an instance with two parameters:<li>released. Is a true or false boolean value. False means that the operation scheduled on the instance is not executed yet.</li><li>expire. Specifies in UTC format YYYY-MM-DD HH:MM:SS.SSSSSS, the time and date for stopping an instance. It’s required only when an instance is set to terminate or shut down.</li><li>operation. Specifies an instance to stop with **shutdown** or **terminate**. When not scheduled, the instance is set to **alwayson**.</li> |

#### Response Body
In this sample request, the instance is tagged and scheduled to terminate at a given UTC time.

```
{
   "box": "7a99f75c-30e6-4986-9059-f6889d1ff5f9",
   "bindings": [

   ],
   "updated": "2015-10-29 12:26:24.446893",
   "automatic_updates": "off",
   "name": "ScriptBoxSample",
   "service": {
   "type": "Linux Compute",
   "id": "eb-bbhzh",
   "machines": [
     {
       "state": "done",
       "name": "eb-bbhzh-1",
       "workflow": [

       ]
     }
   ]
   },
   "tags": [

   ],
   "deleted": null,
   "policy_box": {
       "profile": {
         "image": "test",
         "instances": 1,
         "keypair": "test_keypair",
         "location": "Simulated Location",
         "flavor": "test.micro",
         "schema": "http://elasticbox.net/schemas/test/compute/profile"
       },
       "provider_id": "0476718d-2b00-45ce-8a1c-30b10a16cfc7",
       "automatic_updates": "off",
       "name": Linux Compute",
       "created": "2015-10-21 08:35:50.165822",
       "deleted": null,
       "variables": [
         {
           "automatic_updates": "off",
           "name": "policy_box_variable",
           "required": false,
           "visibility": "public",
           "value": "381d0fd8-b59e-4be6-afc7-3ee1a0a2db1c",
           "type": "Box"
         }
       ],
       "updated": "2015-10-29 12:05:39.065397",
       "visibility": "workspace",
       "owner": "operations",
       "members": [

       ],
       "claims": [
         "linux"
       ],
       "readme": {
         "url": "/resources/default_box_overview.md",
         "upload_date": "2015-10-21 08:35:50.164926",
         "length": 1302,
         "content_type": "text/x-markdown"
       },
       "organization": "elasticbox",
       "id": "e57466ee-7094-4bd4-9121-a6df4395d493",
       "schema": "http://elasticbox.net/schemas/boxes/policy"
   },
   "created": "2015-10-29 12:26:20.377029",
   "uri": "/services/instances/i-3e43qa",
   "state": "done",
   "boxes": [
       {
       "updated": "2015-10-29 11:55:23.842461",
       "automatic_updates": "off",
       "requirements": [

       ],
       "description": "sample box",
       "name": "ScriptBoxSample",
       "created": "2015-10-29 10:52:08.446868",
       "deleted": null,
       "variables": [
       {
         "required": true,
         "type": "Text",
         "name": "variable_name",
         "value": "variable_value",
         "visibility": "public"
       }
       ],
       "visibility": "workspace",
       "id": "7a99f75c-30e6-4986-9059-f6889d1ff5f9",
       "members": [

       ],
       "owner": "operations",
       "organization": "elasticbox",
       "events": {
           "configure": {
             "url": "/services/blobs/download/5631fa7614841250525226cc/configure",
             "length": 5,
             "destination_path": "scripts",
             "content_type": "text/x-shellscript"
           },
           "install": {
             "url": "/services/blobs/download/5631fa6614841250525226ca/install",
             "length": 5,
             "destination_path": "scripts",
             "content_type": "text/x-shellscript"
           }
       },
       "schema": "http://elasticbox.net/schemas/boxes/script"
       }
   ],
   "schema": "http://elasticbox.net/schemas/instance",
   "members": [

   ],
   "owner": "operations",
   "variables": [
       {
         "required": true,
         "type": "Text",
         "name": "variable_name",
         "value": "variable_value_overridden",
         "visibility": "public"
       }
   ],
   "operation": {
       "event": "deploy",
       "workspace": "operations",
       "created": "2015-10-29 12:26:20.504356"
   },
   "id": "i-3e43qa",
   "icon": null,
   "lease": {
       "expire": "2015-10-29 19:00:00.000000",
       "operation": "terminate"
   }
}
```


```
{
   "box": "7a99f75c-30e6-4986-9059-f6889d1ff5f9",
   "bindings": [],
   "updated": "2015-10-29 14:16:48.304153",
   "automatic_updates": "off",
   "name": "ScriptBoxSample",
   "service": {
       "type": "Linux Compute",
       "id": "eb-bbhzh",
       "machines": [
           {
               "state": "done",
               "name": "eb-bbhzh-1",
               "workflow": []
           }
       ]
   },
   "tags": [],
   "deleted": null,
   "policy_box": {
       "profile": {
           "image": "test",
           "instances": 1,
           "keypair": "test_keypair",
           "location": "Simulated Location",
           "flavor": "test.micro",
           "schema": "http://elasticbox.net/schemas/test/compute/profile"
       },
       "provider_id": "0476718d-2b00-45ce-8a1c-30b10a16cfc7",
       "automatic_updates": "off",
       "name": "Deploy Policy - Linux Compute",
       "created": "2015-10-21 08:35:50.165822",
       "deleted": null,
       "variables": [
           {
               "automatic_updates": "off",
               "name": "policy_box_variable",
               "required": false,
               "visibility": "public",
               "value": "381d0fd8-b59e-4be6-afc7-3ee1a0a2db1c",
               "type": "Box"
           }
       ],
       "updated": "2015-10-29 12:05:39.065397",
       "visibility": "workspace",
       "owner": "operations",
       "members": [],
       "claims": [
           "linux"
       ],
       "readme": {
           "url": "/resources/default_box_overview.md",
           "upload_date": "2015-10-21 08:35:50.164926",
           "length": 1302,
           "content_type": "text/x-markdown"
       },
       "organization": "elasticbox",
       "id": "e57466ee-7094-4bd4-9121-a6df4395d493",
       "schema": "http://elasticbox.net/schemas/boxes/policy"
   },
   "created": "2015-10-29 12:26:20.377029",
   "uri": "/services/instances/i-3e43qa",
   "state": "done",
   "boxes": [
       {
           "updated": "2015-10-29 11:55:23.842461",
           "automatic_updates": "off",
           "requirements": [],
           "description": "sample box",
           "name": "ScriptBoxSample",
           "created": "2015-10-29 10:52:08.446868",
           "deleted": null,
           "variables": [
               {
                   "required": true,
                   "type": "Text",
                   "name": "variable_name",
                   "value": "variable_value",
                   "visibility": "public"
               }
           ],
           "visibility": "workspace",
           "id": "7a99f75c-30e6-4986-9059-f6889d1ff5f9",
           "members": [],
           "owner": "operations",
           "organization": "elasticbox",
           "events": {
               "configure": {
                   "url": "/services/blobs/download/5631fa7614841250525226cc/configure",
                   "length": 5,
                   "destination_path": "scripts",
                   "content_type": "text/x-shellscript"
               },
               "install": {
                   "url": "/services/blobs/download/5631fa6614841250525226ca/install",
                   "length": 5,
                   "destination_path": "scripts",
                   "content_type": "text/x-shellscript"
               }
           },
           "schema": "http://elasticbox.net/schemas/boxes/script"
       }
   ],
   "schema": "http://elasticbox.net/schemas/instance",
   "members": [],
   "owner": "operations",
   "variables": [
       {
           "required": true,
           "type": "Text",
           "name": "variable_name",
           "value": "variable_value_overridden",
           "visibility": "public"
       }
   ],
   "operation": {
       "event": "deploy",
       "workspace": "operations",
       "created": "2015-10-29 12:26:20.504356"
   },
   "lease": {
       "released": false,
       "operation": "terminate",
       "expire": "2015-10-29 19:00:00.000000"
   },
   "id": "i-3e43qa",
   "icon": null
}
```

### DELETE /services/instances/{instance_id}

Terminates, force-terminates, or deletes an existing instance based on its instance ID.

### URL

#### Structure
```
[DELETE] /services/instances/{instance_id}?operation=value
```

#### Example
```
[DELETE] https://cam.ctl.io/services/instances/eb-bbhzh?operation=force_terminate
```

### Request

#### Headers
```
Content-Type: application/json
Authorization: Bearer your_json_web_token
ElasticBox-Release: 4.0
```
#### URI Parameters
|Parameter |Type |Description | Req. |
|-----------|------|------------| ---- |
| instance_id | string | Instance id | Yes |
| operation | string | Operation type must be one of the following values: terminate, force_terminate and delete |Yes |


### Response
#### Normal Response Codes

- **200** OK

#### Common Error Response Codes

- **400** Invalid Data
- **403** Forbidden
- **404** Not Found
- **409** Operation Conflict



### GET /services/instances/{instance_id}/service
Gets the service on the instance given its instance ID.

### URL

#### Structure
```
[GET] /services/instances/{instance_id}/service
```

#### Example
```
[GET] https://cam.ctl.io/services/instances/i-b1qtkz/service
```

### Request

#### Headers
```
Content-Type: application/json
Authorization: Bearer your_json_web_token
ElasticBox-Release: 4.0
```

#### URI Parameters
|Parameter |Type |Description | Req. |
|-----------|------|------------| ---- |
| instance_id | string | Instance id | Yes |


### Response
#### Normal Response Codes

- **200** OK

#### Common Error Response Codes

- **403** Forbidden
- **404** Not Found

#### Response Parameters

| Parameter | Type |Description |
|-----------|------|------------|
| profile | object | Service profile. |
| profile.subnet | string | Profile subnet. |
| profile.image | string | Profile image. |
| profile.keypair | string | Profile keypair. |
| profile.location | string| Profile location. |
| profile.security_group | string | Profile secruty group. |
| profile.flavor | string | Profile flavor. |
| profile.autoscalable | boolean | Profile autoscalable. |
| profile.cloud | boolean | Cloud type. |
| profile.schema | string | Profile schema uri. |
| provider_id | string | Profile provider unique identifier. |
|created | string | Creation date. |
| tags | array | Service tags. |
| state | string | Service state, there are three possible states: processing , done and unavailable |
| token | string | Service token. |
| operation | string | Service last operation, there are seven types of operations: deploy, shutdown, poweron, reinstall, reconfigure, terminate, and terminate_service. |
| icon | string | Service icon url. |
| type | string | Instance type. |
| id | string | Instance unique identifier. |
| machines | array | List of service machines. |
| machine.token | string | Machine token. |
| machine.name | string | Machine name. |
| machine.address | array | The array contains the public and private address. |
| machine.agent_version | array | Machine agent version. |
| machine.external_id | array | Machine external id. |
| machine.state | string | Machine state, there are three possible states: processing , done and unavailable. |
| machine.schema | array | Machine schema uri. |
| schema | string | Service schema uri. |
| organization | string | The name of the organization that owns this service. |
| deleted | string | Deleted. |




#### Response Body

```
{
    "profile": {
        "subnet": "us-east-1a",
        "pricing_info": {
            "estimated_monthly": 3168000,
            "factor": 100000,
            "hourly_price": 4400,
            "provider_type": "Amazon Web Services"
        },
        "image": "ami-7c807d14",
        "managed_os": false,
        "instances": 1,
        "keypair": "None",
        "location": "us-east-1",
        "volumes": [],
        "cloud": "EC2",
        "flavor": "m1.small",
        "security_groups": [
            "Automatic"
        ],
        "schema": "http://elasticbox.net/schemas/aws/ec2/profile"
    },
    "schema": "http://elasticbox.net/schemas/service",
    "provider_id": "0669730b-6f01-421b-8a5e-597bca20c1bf",
    "tags": [],
    "deleted": null,
    "variables": [],
    "created": "2018-12-26 15:18:26.651731",
    "state_history": [
        {
            "started": "2018-12-26 15:19:12.346533",
            "state": "up",
            "completed": "2018-12-26 15:30:59.280770"
        },
        {
            "started": "2018-12-26 15:30:59.280770",
            "state": "down",
            "completed": "2018-12-26 15:31:27.771582"
        },
        {
            "started": "2018-12-26 15:31:27.771608",
            "state": "up"
        }
    ],
    "updated": "2018-12-26 15:37:03.927659",
    "token": "4b108401-680f-4c12-b972-3c481a852c73",
    "state": "done",
    "clc_alias": "86C7",
    "organization": "centurylink",
    "operation": "poweron",
    "type": "Linux Compute",
    "id": "eb-l2gmi",
    "machines": [
        {
            "last_agent_ping": "2018-12-26 15:33:07.907863",
            "name": "testserve-eb-l2gmi-1",
            "hostname": "ec2-52-90-5-208.compute-1.amazonaws.com",
            "token": "b40e24eb-dc72-4be5-b044-3f0015a28091",
            "support_id": "AWSUSE110715",
            "state": "done",
            "address": {
                "public": "54.208.195.172",
                "private": "10.45.133.57"
            },
            "schema": "http://elasticbox.net/schemas/aws/service-machine",
            "external_id": "i-0fbf9349a5ea5cd36",
            "agent_version": "6.13"
        }
    ],
    "icon": "images/platform/linux.png"
}
```

### GET /services/instances/{instance_id}/activity

Gets all activity logs from operations run on an instance given its instance ID.

### URL

#### Structure
```
[GET] /services/instances/{instance_id}/activity
```


#### Example
```
[GET] https://cam.ctl.io/services/instances/i-b1qtkz/activity
```



### Request

#### Headers
```
Content-Type: application/json
Authorization: Bearer your_json_web_token
ElasticBox-Release: 4.0
```

#### URI Parameters
|Parameter |Type |Description | Req. |
|-----------|------|------------| ---- |
| instance_id | string | Instance id | Yes |
| operation | string | The specific operation id, there are seven types of operations: deploy, shutdown, poweron, reinstall, reconfigure, terminate and terminate_service. | Opt.|

### Response
#### Normal Response Codes

- **200** OK

#### Common Error Response Codes

- **403** Forbidden
- **404** Not Found


#### Response Parameters

| Parameter | Type |Description |
|-----------|------|------------|
|* box | string | Box name. |
| username | string | User who performed the activity. |
|* machine | string | Machine. |
| level | string | Activity type. |
| text | string | Activity description. |
| created | string | Activity creation date. |
|* event | string | Activity event. |



#### Response Body

```
[
    {
        "text": "Deploying instance.",
        "request_id": "6886be9c-cdf8-425f-9392-c6f3bb840e22",
        "created": "2018-12-26 15:18:27.582649",
        "level": "start"
    },
    {
        "text": "Created security group eb-l2gmi.",
        "request_id": "6886be9c-cdf8-425f-9392-c6f3bb840e22",
        "created": "2018-12-26 15:18:28.270143",
        "level": "add"
    },
    {
        "text": "Automatically selected image amzn-ami-pv-2014.03.2.x86_64-ebs.",
        "request_id": "6886be9c-cdf8-425f-9392-c6f3bb840e22",
        "created": "2018-12-26 15:18:29.952413",
        "level": "info"
    },
    {
        "text": "Create in Progress for eb-l2gmi (AWS::CloudFormation::Stack): User Initiated.",
        "request_id": "6886be9c-cdf8-425f-9392-c6f3bb840e22",
        "created": "2018-12-26 15:18:30.693042",
        "level": "info"
    },
    {
        "text": "Create in Progress for testserveebl2gmi1Machine (AWS::EC2::Instance).",
        "request_id": "6886be9c-cdf8-425f-9392-c6f3bb840e22",
        "created": "2018-12-26 15:18:40.934764",
        "level": "info"
    },
    {
        "text": "Create in Progress for testserveebl2gmi1Machine (AWS::EC2::Instance): Resource creation Initiated.",
        "request_id": "6886be9c-cdf8-425f-9392-c6f3bb840e22",
        "created": "2018-12-26 15:18:40.945462",
        "level": "info"
    },
    {
        "text": "Create Complete for testserveebl2gmi1Machine (AWS::EC2::Instance).",
        "request_id": "6886be9c-cdf8-425f-9392-c6f3bb840e22",
        "created": "2018-12-26 15:19:11.677807",
        "level": "info"
    },
    {
        "text": "Create Complete for eb-l2gmi (AWS::CloudFormation::Stack).",
        "request_id": "6886be9c-cdf8-425f-9392-c6f3bb840e22",
        "created": "2018-12-26 15:19:11.687805",
        "level": "info"
    },
    {
        "text": "Waiting to install ElasticBox agent in machine testserve-eb-l2gmi-1.",
        "request_id": "6886be9c-cdf8-425f-9392-c6f3bb840e22",
        "created": "2018-12-26 15:19:12.339171",
        "level": "waiting"
    },
    {
        "box": "",
        "created": "2018-12-26 15:21:52.584981",
        "text": "Executing pre_install:php-server in machine testserve-eb-l2gmi-1.",
        "level": "install",
        "exit_code": 0,
        "machine": "testserve-eb-l2gmi-1",
        "finished": "2018-12-26 15:21:53.200000",
        "request_id": "4a0c69bc-9164-4f51-b313-d2ad46f50443",
        "event": "pre_install"
    },
    {
        "box": "",
        "created": "2018-12-26 15:21:53.592944",
        "text": "Executing configure:php-server in machine testserve-eb-l2gmi-1.",
        "level": "configure",
        "exit_code": 0,
        "machine": "testserve-eb-l2gmi-1",
        "finished": "2018-12-26 15:21:56.190000",
        "request_id": "01e52bb8-a6ba-4f36-8d52-056975fc2e34",
        "event": "configure"
    },
    {
        "text": "Machine testserve-eb-l2gmi-1 successfully deployed.",
        "request_id": "9232da27-2106-46cd-972d-c7014f4ece04",
        "created": "2018-12-26 15:21:56.470664",
        "level": "success"
    },
    {
        "text": "Instance successfully deployed.",
        "request_id": "9232da27-2106-46cd-972d-c7014f4ece04",
        "created": "2018-12-26 15:21:56.483589",
        "level": "success"
    },
    {
        "text": "Shutting-down instance.",
        "request_id": "0af456dd-86d9-49fd-8ff8-16e3017775a8",
        "created": "2018-12-26 15:29:56.584842",
        "level": "stop"
    },
    {
        "text": "Machine testserve-eb-l2gmi-1 successfully stopped.",
        "request_id": "36c4a9f6-78f2-44dc-af3f-2445017571e3",
        "created": "2018-12-26 15:29:57.716319",
        "level": "success"
    },
    {
        "text": "Instance successfully stopped.",
        "request_id": "36c4a9f6-78f2-44dc-af3f-2445017571e3",
        "created": "2018-12-26 15:29:57.727837",
        "level": "success"
    },
    {
        "text": "Shutting-down service eb-l2gmi.",
        "request_id": "615759d1-1461-44b6-96b8-ad4e9671271a",
        "created": "2018-12-26 15:29:57.825175",
        "level": "stop"
    },
    {
        "text": "Waiting for shutting-down machines testserve-eb-l2gmi-1.",
        "request_id": "615759d1-1461-44b6-96b8-ad4e9671271a",
        "created": "2018-12-26 15:29:58.571231",
        "level": "waiting"
    },
    {
        "text": "Service eb-l2gmi successfully shutdown.",
        "request_id": "615759d1-1461-44b6-96b8-ad4e9671271a",
        "created": "2018-12-26 15:30:59.290583",
        "level": "success"
    },
    {
        "text": "Powering-on instance.",
        "request_id": "5d48b218-330b-42bd-b3b0-0349a29c3c58",
        "created": "2018-12-26 15:31:27.556072",
        "level": "start"
    },
    {
        "text": "Powering-on service eb-l2gmi.",
        "request_id": "5d48b218-330b-42bd-b3b0-0349a29c3c58",
        "created": "2018-12-26 15:31:27.603268",
        "level": "start"
    },
    {
        "text": "Booting machine testserve-eb-l2gmi-1.",
        "request_id": "5d48b218-330b-42bd-b3b0-0349a29c3c58",
        "created": "2018-12-26 15:31:27.786126",
        "level": "info"
    },
    {
        "text": "Waiting to install ElasticBox agent in machine testserve-eb-l2gmi-1.",
        "request_id": "5d48b218-330b-42bd-b3b0-0349a29c3c58",
        "created": "2018-12-26 15:31:28.176402",
        "level": "waiting"
    },
    {
        "box": "",
        "created": "2018-12-26 15:33:03.801318",
        "text": "Executing configure:php-server in machine testserve-eb-l2gmi-1.",
        "level": "configure",
        "exit_code": 0,
        "machine": "testserve-eb-l2gmi-1",
        "finished": "2018-12-26 15:33:06.440000",
        "request_id": "7d39719d-236e-4277-bd0f-0c0ca21a941c",
        "event": "configure"
    },
    {
        "text": "Machine testserve-eb-l2gmi-1 successfully powered-on.",
        "request_id": "78d61086-0fdc-4a3a-84c7-2848c88d0bed",
        "created": "2018-12-26 15:33:06.706192",
        "level": "success"
    },
    {
        "text": "Instance successfully powered-on.",
        "request_id": "78d61086-0fdc-4a3a-84c7-2848c88d0bed",
        "created": "2018-12-26 15:33:06.716120",
        "level": "success"
    },
    {
        "text": "Reinstalling instance.",
        "request_id": "162fc44b-c2a0-4873-a42e-0778d4f628ea",
        "created": "2018-12-26 15:34:37.732658",
        "level": "install"
    },
    {
        "box": "",
        "created": "2018-12-26 15:34:39.306274",
        "text": "Executing pre_install:php-server in machine testserve-eb-l2gmi-1.",
        "level": "install",
        "exit_code": 0,
        "machine": "testserve-eb-l2gmi-1",
        "finished": "2018-12-26 15:34:41.870000",
        "request_id": "31be6340-2a11-4cad-9643-8082f44515ac",
        "event": "pre_install"
    },
    {
        "box": "",
        "created": "2018-12-26 15:34:42.177262",
        "text": "Executing configure:php-server in machine testserve-eb-l2gmi-1.",
        "level": "configure",
        "exit_code": 0,
        "machine": "testserve-eb-l2gmi-1",
        "finished": "2018-12-26 15:34:44.700000",
        "request_id": "df7ce1ca-4477-4c41-84de-16476b22e329",
        "event": "configure"
    },
    {
        "text": "Machine testserve-eb-l2gmi-1 successfully reinstalled.",
        "request_id": "a0fccf9e-42ac-4cef-9f6b-9f5b28565cd0",
        "created": "2018-12-26 15:34:44.965676",
        "level": "success"
    },
    {
        "text": "Instance successfully reinstalled.",
        "request_id": "a0fccf9e-42ac-4cef-9f6b-9f5b28565cd0",
        "created": "2018-12-26 15:34:44.979192",
        "level": "success"
    },
    {
        "text": "Reconfiguring instance.",
        "request_id": "98299bd7-e89c-4078-b6c6-51d1134cbaba",
        "created": "2018-12-26 15:37:03.010128",
        "level": "configure"
    },
    {
        "box": "",
        "created": "2018-12-26 15:37:05.022507",
        "text": "Executing configure:php-server in machine testserve-eb-l2gmi-1.",
        "level": "configure",
        "exit_code": 0,
        "machine": "testserve-eb-l2gmi-1",
        "finished": "2018-12-26 15:37:07.540000",
        "request_id": "131c170d-0d76-4bec-a3e8-31877c4cf225",
        "event": "configure"
    },
    {
        "text": "Machine testserve-eb-l2gmi-1 successfully reconfigured.",
        "request_id": "e83e5869-16c3-4a81-9a1f-0e14ff2ca003",
        "created": "2018-12-26 15:37:07.801594",
        "level": "success"
    },
    {
        "text": "Instance successfully reconfigured.",
        "request_id": "e83e5869-16c3-4a81-9a1f-0e14ff2ca003",
        "created": "2018-12-26 15:37:07.812196",
        "level": "success"
    }
]
```

### GET /services/instances/{instance_id}/machine_logs

Gets the logs of one machine for a deployed instance given its instance ID.

### URL

#### Structure

```
[GET] /services/instances/{instance_id}/machine_logs?machine_name={machine}
```

#### Example

```
[GET] https://cam.ctl.io/services/instances/eb-bbhzh/activity?operation=nfs-client1-eb-osw3o-1
```

### Request

#### Headers
```
Content-Type: application/json
Authorization: Bearer your_json_web_token
ElasticBox-Release: 4.0
```

#### URI Parameters
| Parameter | Type |Description |Req. |
|-----------|------|------------| ---- |
| instance_id | string | Instance id | Yes |
| machine_name | string | 	The name of the machine you want to retrieve the log. You can get the name of the machine from the instance document. | Yes |
| box | string | Box name. | Opt. |
| event | string | Event type, there may be nine event lists: configure, dispose, install, post_dispose, post_stop, pre_configure, pre_install, pre_start, start and stop. | Opt. |
| operation | string | The specific operation id, there are seven types of operations: deploy , shutdown , poweron , reinstall , reconfigure, terminate and terminate_service. | Opt. |


### Response
#### Normal Response Codes

- **200** OK

#### Common Error Response Codes

- **403** Forbidden
- **404** Not Found


#### Response Body

```
Executing pre_install-{instance_id} script
...
pre_install-{instance_id} successfully executed.
Executing install-{instance_id} script
...
install-{instance_id} successfully executed.
Executing configure-{instance_id} script
...
configure-{instance_id} successfully executed.
```

### GET /services/instances/{instance_id}/bindings

Gets the binding of an instance when you give the instance ID.

### URL

#### Structure

```
[GET] /services/instances/{instance_id}/bindings
```

#### Example

```
[GET] https://cam.ctl.io/services/instances/eb-bbhzh/bindings
```

### Request

#### Headers
```
Content-Type: application/json
Authorization: Bearer your_json_web_token
ElasticBox-Release: 4.0
```
#### URI Parameters
Parameter |Type |Description | Req. |
|-----------|------|------------| ---- |
| instance_id | string | Instance id | Yes |


### Response
#### Normal Response Codes

- **200** OK

#### Common Error Response Codes

- **403** Forbidden
- **404** Not Found

#### Response Parameters

| Parameter | Type |Description |
|-----------|------|------------|
| updated | string | Date of the last update. |
| operation | string | Last operation, there are seven types of operations: deploy , shutdown , poweron , reinstall , reconfigure , terminate and terminate_service |
| name | string | Instance name. |
| service| Object | Instance service. |
| service.type | string | Required. Can be one of these types: Linux Compute, Windows Compute and CloudFormation Service. |
| service.id | string | Service type. |
| service.machines | array | List of service machines |
| machine | object | Machine contained in the service machines list. |
| machine.state | string | Machine state, there are three possible states: processing , done and unavailable. |
| machine.name | string | Machine name. |
| machine.workflow | array | List of workflow actions, where each workflow action object contains three parameters: box, event, and script. |
| workflow.box | string | Workflow action box. |
| workflow.event | string | Workflow action event. |
| workflow.script | string | Workflow action script uri. |
| tags | array | Instance tags. |
| boxes | array | List of boxes where each box object contains a service parameter. The service parameter can have one of these values: Linux Compute, Windows Compute and CloudFormation Service. |
| uri |  string | Instance uri. |
| state | string | Instance state, there are three possible states: processing , done and unavailable |
| bindings | array | List of instance bindings. |
| binding | object | Binding contained in the bindings list, each binding object contains the parameters: instance and name. |
| id | array | Instance unique identifier |
| icon | string | Instance icon uri. |
| schema | string | Instance schema uri. |


#### Response Body
```
[
  {
     "box":{
        "version":"1186ce20-96f2-458d-ae62-19496036b275",
        "name":"Wordpress"
     },
     "updated":"2014-03-21 18:20:04.921745",
     "name":"profile",
     "created":"2014-03-21 18:20:04.921745",
     "default_stamp":1395426004.921258,
     "uri":"--profile uri--",
     "instances":[
        {
           "box":{
              "version":"1186ce20-96f2-458d-ae62-19496036b275",
              "name":"Wordpress"
           },
           "profile":{
              "subnet":"us-east-1b",
              "image":"Linux Compute",
              "instances":1,
              "keypair":"None",
              "location":"us-east-1",
              "security_group":"Automatic",
              "flavor":"t1.micro",
              "autoscalable":false,
              "cloud":"EC2",
              "schema":"http://elasticbox.net/schemas/aws/ec2/profile"
           },
           "provider":"Amazon",
           "path":"/",
           "variables":[
              {
                 "type":"Port",
                 "name":"http",
                 "value":"80"
              }
           ],
           "bindings":[

           ]
        }
     ],
     "members":[
               "member1","member2"
     ],
     "owner":"workspace1",
     "id":"--profile id--",
     "schema":"http://elasticbox.net/schemas/deployment-profile"
  }
]
```

### GET /services/instances/{instance_id}/operations

Gets all operations run on an instance when you give the instance ID.

### URL

#### Structure

```
[GET] /services/instances/{instance_id}/operations
```

#### Example

```
[GET] https://cam.ctl.io/services/instances/i-b1qtkz/operations
```

### Request

#### Headers
```
Content-Type: application/json
Authorization: Bearer your_json_web_token
ElasticBox-Release: 4.0
```
#### URI Parameters
Parameter |Type |Description | Req. |
|-----------|------|------------| ---- |
| instance_id | string | Instance id | Yes |


### Response
#### Normal Response Codes

- **200** OK

#### Common Error Response Codes

- **403** Forbidden
- **404** Not Found

#### Response Parameters

| Parameter | Type |Description |
|-----------|------|------------|
| username | string | User name. |
| updated | string | Date of the last update. |
| created | string | Creation date. |
| instance | string | Instance unique identifier. |
| state | string | Instance state, there are three possible states: processing , done and unavailable |
| workspace | string | Workspace name. |
| activities | array | List of activities. |
| activity.username | string | User who performed the activity. |
| activity.text | string | Activity description. |
| activity.level | string | Activity type. |
| activity.created | string | Activity date. |
| operation | string | Last operation, there are seven types of operations: deploy, shutdown, poweron, reinstall, reconfigure, terminate and terminate_service. |
| id | string | Operation unique identifier. |
| deleted | string | Removal date. |
| schema | string | Operation schema uri. |


#### Response Body
```
[
    {
        "username": "jorge.torres@centurylink.com",
        "updated": "2018-12-26 15:21:56.509525",
        "created": "2018-12-26 15:18:27.567661",
        "deleted": null,
        "activity": [
            {
                "text": "Deploying instance.",
                "request_id": "6886be9c-cdf8-425f-9392-c6f3bb840e22",
                "created": "2018-12-26 15:18:27.582649",
                "level": "start"
            },
            {
                "text": "Created security group eb-l2gmi.",
                "request_id": "6886be9c-cdf8-425f-9392-c6f3bb840e22",
                "created": "2018-12-26 15:18:28.270143",
                "level": "add"
            },
            {
                "text": "Automatically selected image amzn-ami-pv-2014.03.2.x86_64-ebs.",
                "request_id": "6886be9c-cdf8-425f-9392-c6f3bb840e22",
                "created": "2018-12-26 15:18:29.952413",
                "level": "info"
            },
            {
                "text": "Create in Progress for eb-l2gmi (AWS::CloudFormation::Stack): User Initiated.",
                "request_id": "6886be9c-cdf8-425f-9392-c6f3bb840e22",
                "created": "2018-12-26 15:18:30.693042",
                "level": "info"
            },
            {
                "text": "Create in Progress for testserveebl2gmi1Machine (AWS::EC2::Instance).",
                "request_id": "6886be9c-cdf8-425f-9392-c6f3bb840e22",
                "created": "2018-12-26 15:18:40.934764",
                "level": "info"
            },
            {
                "text": "Create in Progress for testserveebl2gmi1Machine (AWS::EC2::Instance): Resource creation Initiated.",
                "request_id": "6886be9c-cdf8-425f-9392-c6f3bb840e22",
                "created": "2018-12-26 15:18:40.945462",
                "level": "info"
            },
            {
                "text": "Create Complete for testserveebl2gmi1Machine (AWS::EC2::Instance).",
                "request_id": "6886be9c-cdf8-425f-9392-c6f3bb840e22",
                "created": "2018-12-26 15:19:11.677807",
                "level": "info"
            },
            {
                "text": "Create Complete for eb-l2gmi (AWS::CloudFormation::Stack).",
                "request_id": "6886be9c-cdf8-425f-9392-c6f3bb840e22",
                "created": "2018-12-26 15:19:11.687805",
                "level": "info"
            },
            {
                "text": "Waiting to install ElasticBox agent in machine testserve-eb-l2gmi-1.",
                "request_id": "6886be9c-cdf8-425f-9392-c6f3bb840e22",
                "created": "2018-12-26 15:19:12.339171",
                "level": "waiting"
            },
            {
                "box": "",
                "created": "2018-12-26 15:21:52.584981",
                "text": "Executing pre_install:php-server in machine testserve-eb-l2gmi-1.",
                "level": "install",
                "exit_code": 0,
                "machine": "testserve-eb-l2gmi-1",
                "finished": "2018-12-26 15:21:53.200000",
                "request_id": "4a0c69bc-9164-4f51-b313-d2ad46f50443",
                "event": "pre_install"
            },
            {
                "box": "",
                "created": "2018-12-26 15:21:53.592944",
                "text": "Executing configure:php-server in machine testserve-eb-l2gmi-1.",
                "level": "configure",
                "exit_code": 0,
                "machine": "testserve-eb-l2gmi-1",
                "finished": "2018-12-26 15:21:56.190000",
                "request_id": "01e52bb8-a6ba-4f36-8d52-056975fc2e34",
                "event": "configure"
            },
            {
                "text": "Machine testserve-eb-l2gmi-1 successfully deployed.",
                "request_id": "9232da27-2106-46cd-972d-c7014f4ece04",
                "created": "2018-12-26 15:21:56.470664",
                "level": "success"
            },
            {
                "text": "Instance successfully deployed.",
                "request_id": "9232da27-2106-46cd-972d-c7014f4ece04",
                "created": "2018-12-26 15:21:56.483589",
                "level": "success"
            }
        ],
        "instance": "i-b1qtkz",
        "state": "done",
        "instance_state": "done",
        "workspace": "operations",
        "request_id": "6886be9c-cdf8-425f-9392-c6f3bb840e22",
        "operation": "deploy",
        "id": "46e7993d-e259-47a6-a353-fa62128fb288",
        "schema": "http://elasticbox.net/schemas/instance-operation"
    },
    {
        "username": "jorge.torres@centurylink.com",
        "updated": "2018-12-26 15:30:59.323268",
        "created": "2018-12-26 15:29:56.569835",
        "deleted": null,
        "activity": [
            {
                "text": "Shutting-down instance.",
                "request_id": "0af456dd-86d9-49fd-8ff8-16e3017775a8",
                "created": "2018-12-26 15:29:56.584842",
                "level": "stop"
            },
            {
                "text": "Machine testserve-eb-l2gmi-1 successfully stopped.",
                "request_id": "36c4a9f6-78f2-44dc-af3f-2445017571e3",
                "created": "2018-12-26 15:29:57.716319",
                "level": "success"
            },
            {
                "text": "Instance successfully stopped.",
                "request_id": "36c4a9f6-78f2-44dc-af3f-2445017571e3",
                "created": "2018-12-26 15:29:57.727837",
                "level": "success"
            },
            {
                "text": "Shutting-down service eb-l2gmi.",
                "request_id": "615759d1-1461-44b6-96b8-ad4e9671271a",
                "created": "2018-12-26 15:29:57.825175",
                "level": "stop"
            },
            {
                "text": "Waiting for shutting-down machines testserve-eb-l2gmi-1.",
                "request_id": "615759d1-1461-44b6-96b8-ad4e9671271a",
                "created": "2018-12-26 15:29:58.571231",
                "level": "waiting"
            },
            {
                "text": "Service eb-l2gmi successfully shutdown.",
                "request_id": "615759d1-1461-44b6-96b8-ad4e9671271a",
                "created": "2018-12-26 15:30:59.290583",
                "level": "success"
            }
        ],
        "instance": "i-b1qtkz",
        "state": "done",
        "instance_state": "done",
        "workspace": "operations",
        "request_id": "0af456dd-86d9-49fd-8ff8-16e3017775a8",
        "operation": "shutdown",
        "id": "16f0376a-ae1c-4d26-8156-119f5fba3d27",
        "schema": "http://elasticbox.net/schemas/instance-operation"
    },
    {
        "username": "jorge.torres@centurylink.com",
        "updated": "2018-12-26 15:33:06.727051",
        "created": "2018-12-26 15:31:27.539879",
        "deleted": null,
        "activity": [
            {
                "text": "Powering-on instance.",
                "request_id": "5d48b218-330b-42bd-b3b0-0349a29c3c58",
                "created": "2018-12-26 15:31:27.556072",
                "level": "start"
            },
            {
                "text": "Powering-on service eb-l2gmi.",
                "request_id": "5d48b218-330b-42bd-b3b0-0349a29c3c58",
                "created": "2018-12-26 15:31:27.603268",
                "level": "start"
            },
            {
                "text": "Booting machine testserve-eb-l2gmi-1.",
                "request_id": "5d48b218-330b-42bd-b3b0-0349a29c3c58",
                "created": "2018-12-26 15:31:27.786126",
                "level": "info"
            },
            {
                "text": "Waiting to install ElasticBox agent in machine testserve-eb-l2gmi-1.",
                "request_id": "5d48b218-330b-42bd-b3b0-0349a29c3c58",
                "created": "2018-12-26 15:31:28.176402",
                "level": "waiting"
            },
            {
                "box": "",
                "created": "2018-12-26 15:33:03.801318",
                "text": "Executing configure:php-server in machine testserve-eb-l2gmi-1.",
                "level": "configure",
                "exit_code": 0,
                "machine": "testserve-eb-l2gmi-1",
                "finished": "2018-12-26 15:33:06.440000",
                "request_id": "7d39719d-236e-4277-bd0f-0c0ca21a941c",
                "event": "configure"
            },
            {
                "text": "Machine testserve-eb-l2gmi-1 successfully powered-on.",
                "request_id": "78d61086-0fdc-4a3a-84c7-2848c88d0bed",
                "created": "2018-12-26 15:33:06.706192",
                "level": "success"
            },
            {
                "text": "Instance successfully powered-on.",
                "request_id": "78d61086-0fdc-4a3a-84c7-2848c88d0bed",
                "created": "2018-12-26 15:33:06.716120",
                "level": "success"
            }
        ],
        "instance": "i-b1qtkz",
        "state": "done",
        "instance_state": "done",
        "workspace": "operations",
        "request_id": "5d48b218-330b-42bd-b3b0-0349a29c3c58",
        "operation": "poweron",
        "id": "3776fe57-879c-4c93-b1c8-56abbc6757c0",
        "schema": "http://elasticbox.net/schemas/instance-operation"
    },
    {
        "username": "jorge.torres@centurylink.com",
        "updated": "2018-12-26 15:34:44.995543",
        "created": "2018-12-26 15:34:37.718774",
        "deleted": null,
        "activity": [
            {
                "text": "Reinstalling instance.",
                "request_id": "162fc44b-c2a0-4873-a42e-0778d4f628ea",
                "created": "2018-12-26 15:34:37.732658",
                "level": "install"
            },
            {
                "box": "",
                "created": "2018-12-26 15:34:39.306274",
                "text": "Executing pre_install:php-server in machine testserve-eb-l2gmi-1.",
                "level": "install",
                "exit_code": 0,
                "machine": "testserve-eb-l2gmi-1",
                "finished": "2018-12-26 15:34:41.870000",
                "request_id": "31be6340-2a11-4cad-9643-8082f44515ac",
                "event": "pre_install"
            },
            {
                "box": "",
                "created": "2018-12-26 15:34:42.177262",
                "text": "Executing configure:php-server in machine testserve-eb-l2gmi-1.",
                "level": "configure",
                "exit_code": 0,
                "machine": "testserve-eb-l2gmi-1",
                "finished": "2018-12-26 15:34:44.700000",
                "request_id": "df7ce1ca-4477-4c41-84de-16476b22e329",
                "event": "configure"
            },
            {
                "text": "Machine testserve-eb-l2gmi-1 successfully reinstalled.",
                "request_id": "a0fccf9e-42ac-4cef-9f6b-9f5b28565cd0",
                "created": "2018-12-26 15:34:44.965676",
                "level": "success"
            },
            {
                "text": "Instance successfully reinstalled.",
                "request_id": "a0fccf9e-42ac-4cef-9f6b-9f5b28565cd0",
                "created": "2018-12-26 15:34:44.979192",
                "level": "success"
            }
        ],
        "instance": "i-b1qtkz",
        "state": "done",
        "instance_state": "done",
        "workspace": "operations",
        "request_id": "162fc44b-c2a0-4873-a42e-0778d4f628ea",
        "operation": "reinstall",
        "id": "485be288-a545-4cab-8ade-f5b24832ae01",
        "schema": "http://elasticbox.net/schemas/instance-operation"
    },
    {
        "username": "jorge.torres@centurylink.com",
        "updated": "2018-12-26 15:37:07.824425",
        "created": "2018-12-26 15:37:02.998807",
        "deleted": null,
        "activity": [
            {
                "text": "Reconfiguring instance.",
                "request_id": "98299bd7-e89c-4078-b6c6-51d1134cbaba",
                "created": "2018-12-26 15:37:03.010128",
                "level": "configure"
            },
            {
                "box": "",
                "created": "2018-12-26 15:37:05.022507",
                "text": "Executing configure:php-server in machine testserve-eb-l2gmi-1.",
                "level": "configure",
                "exit_code": 0,
                "machine": "testserve-eb-l2gmi-1",
                "finished": "2018-12-26 15:37:07.540000",
                "request_id": "131c170d-0d76-4bec-a3e8-31877c4cf225",
                "event": "configure"
            },
            {
                "text": "Machine testserve-eb-l2gmi-1 successfully reconfigured.",
                "request_id": "e83e5869-16c3-4a81-9a1f-0e14ff2ca003",
                "created": "2018-12-26 15:37:07.801594",
                "level": "success"
            },
            {
                "text": "Instance successfully reconfigured.",
                "request_id": "e83e5869-16c3-4a81-9a1f-0e14ff2ca003",
                "created": "2018-12-26 15:37:07.812196",
                "level": "success"
            }
        ],
        "instance": "i-b1qtkz",
        "state": "done",
        "instance_state": "done",
        "workspace": "operations",
        "request_id": "98299bd7-e89c-4078-b6c6-51d1134cbaba",
        "operation": "reconfigure",
        "id": "3de6477a-5e16-432f-a98a-8ec99f95ac1a",
        "schema": "http://elasticbox.net/schemas/instance-operation"
    }
]
```


### PUT /services/instances/{instance_id}/deploy

Re-deploy an existing instance, requires the specified id instance_id.

### URL

#### Structure

```
[PUT] /services/instances/{instance_id}/deploy
```

#### Example

```
[PUT] https://cam.ctl.io/services/instances/i-ndt46z/deploy
```

### Request

#### Headers
```
Content-Type: application/json
Authorization: Bearer your_json_web_token
ElasticBox-Release: 4.0
```
#### URI Parameters
Parameter |Type |Description | Req. |
|-----------|------|------------| ---- |
| instance_id | string | Instance id | Yes |


### Response
#### Normal Response Codes

- **200** OK

#### Common Error Response Codes

- **409** Operation Conflict


### PUT /services/instances/{instance_id}/poweron

Powers on an existing instance when you give the instance ID.

### URL

#### Structure

```
[PUT] /services/instances/{instance_id}/poweron
```

#### Example

```
[PUT] https://cam.ctl.io/services/instances/i-b1qtkz/poweron
```
### Request

#### Headers
```
Content-Type: application/json
Authorization: Bearer your_json_web_token
ElasticBox-Release: 4.0
```
#### URI Parameters
Parameter |Type |Description | Req. |
|-----------|------|------------| ---- |
| instance_id | string | Instance id | Yes |


### Response
#### Normal Response Codes

- **200** OK

#### Common Error Response Codes

- **409** Operation Conflict


### PUT /services/instances/{instance_id}/shutdown

Shuts down an existing instance when you give the instance ID.

### URL

#### Structure

```
[PUT] /services/instances/{instance_id}/shutdown
```

#### Example

```
[PUT] https://cam.ctl.io/services/instances/i-b1qtkz/shutdown
```
### Request

#### Headers
```
Content-Type: application/json
Authorization: Bearer your_json_web_token
ElasticBox-Release: 4.0
```
#### URI Parameters
Parameter |Type |Description | Req. |
|-----------|------|------------| ---- |
| instance_id | string | Instance id | Yes |


### Response
#### Normal Response Codes

- **200** OK

#### Common Error Response Codes

- **409** Operation Conflict

### PUT /services/instances/{instance_id}/reinstall

Reinstalls an existing instance when you give its ID.


### URL

#### Structure

```
[PUT] /services/instances/{instance_id}/reinstall
```

#### Example

```
[PUT] https://cam.ctl.io/services/instances/i-b1qtkz/reinstall
```
### Request

#### Headers
```
Content-Type: application/json
Authorization: Bearer your_json_web_token
ElasticBox-Release: 4.0
```
#### URI Parameters
Parameter |Type |Description | Req. |
|-----------|------|------------| ---- |
| instance_id | string | Instance id | Yes |


### Response
#### Normal Response Codes

- **200** OK

#### Common Error Response Codes

- **409** Operation Conflict

### PUT /services/instances/{instance_id}/reconfigure

Re-configures an existing instance when you give its ID.

### URL

#### Structure

```
[PUT] /services/instances/{instance_id}/reconfigure
```

#### Example

```
[PUT] https://cam.ctl.io/services/instances/i-b1qtkz/reconfigure
```
### Request

#### Headers
```
Content-Type: application/json
Authorization: Bearer your_json_web_token
ElasticBox-Release: 4.0
```
#### URI Parameters
Parameter |Type |Description | Req. |
|-----------|------|------------| ---- |
| instance_id | string | Instance id | Yes |
| method | string | Operation on the instance. |

### Response
#### Normal Response Codes

- **200** OK

#### Common Error Response Codes

- **409** Operation Conflict
  

#### Response Body
```
{
  "id":"i-4g166v",
  "method":"reconfigure"
}
```


### PUT /services/instances/{instance_id}/import

Retry to import an unregistered instance. when you give its ID.

### URL

#### Structure 

```
[PUT] /services/instances/{instance_id}/import 
```

#### Example

```
[PUT] https://cam.ctl.io/services/instances/i-ndt46z/import
```

### Request

#### Headers
```
Content-Type: application/json
Authorization: Bearer your_json_web_token
ElasticBox-Release: 4.0
```

#### URI Parameters
* None


### Response
#### Normal Response Codes

- **200** OK

#### Common Error Response Codes

- **403** Forbidden
- **404** Not Found 


#### Response Parameters

Parameter |Type |Description | Req. |
|-----------|------|------------| ---- |
| instance_id | string | Instance id | Yes |
| method | string | Operation on the instance (import). |Yes |


#### Response Body

```
{
  "id":"i-eruumb",
  "method":"import"
}
```

### PUT /services/instances/{instance_id}/cancel_import

Cancel a failed import of an unregistered instance when you give its ID.

### URL

#### Structure 

```
[PUT] /services/instances/{instance_id}/cancel_import
```

#### Example

```
[PUT] https://cam.ctl.io/services/instances/i-ndt46z/cancel_import
```

### Request

#### Headers
```
Content-Type: application/json
Authorization: Bearer your_json_web_token
ElasticBox-Release: 4.0
```

#### URI Parameters
* None


### Response
#### Normal Response Codes

- **200** OK

#### Common Error Response Codes

- **403** Forbidden
- **404** Not Found 


#### Response Parameters

| Parameter | Type |Description |Req.|
|-----------|------|------------|----|
| instance_id | string | Instance id | Yes |
| method | string | Operation on the instance (cancel_import). |Yes |

#### Response Body

```
{
  "id":"i-eruumb",
  "method":"cancel_import"
}
```


### Contacting Cloud Application Manager Support

We’re sorry you’re having an issue in [Cloud Application Manager](https://www.ctl.io/cloud-application-manager/). Please review the [troubleshooting tips](https://www.ctl.io/knowledge-base/cloud-application-manager/troubleshooting/troubleshooting-tips/), or contact [Cloud Application Manager support](mailto:incident@CenturyLink.com) with details and screenshots where possible.

For issues related to API calls, send the request body along with details related to the issue.

In the case of a box error, share the box in the workspace that your organization and Cloud Application Manager can access and attach the logs.
* Linux: SSH and locate the log at /var/log/elasticbox/elasticbox-agent.log
* Windows: RDP into the instance to locate the log at ProgramDataElasticBoxLogselasticbox-agent.log
