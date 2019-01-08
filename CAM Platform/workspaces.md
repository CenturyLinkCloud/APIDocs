{{{
"title": "Workspaces API",
"date": "09-01-2016",
"author": "",
"attachments": [],
"contentIsHTML": false,
"sticky": true
}}}

Manage and perform actions on workspaces.

**Create or List Workspaces**

| Resource |Description |
|----------|------------|
| [GET /services/workspaces](#get-servicesworkspaces) | Gets the list of workspaces |
| [POST /services/workspace](#post-servicesworkspace) | Creates a new team workspace |

**Perform Other Workspace Operations**

| Parameter | Description |
|-----------|-------------|
| [GET /services/workspaces/{workspace_id}](#get-servicesworkspacesworkspace_id) | Fetches an existing workspace |
| [PUT /services/workspaces/{workspace_id}](#put-servicesworkspacesworkspace_id) | Updates an existing workspace |
| [DELETE /services/workspaces/{workspace_id}](#delete-servicesworkspacesworkspace_id) | Deletes an existing workspace |
| [GET /services/workspaces/{workspace_id}/providers](#get-servicesworkspacesworkspace_idproviders) | Gets the cloud providers registered in a workspace |
| [GET /services/workspaces/{workspace_id}/boxes](#get-servicesworkspacesworkspace_idboxes) | Gets the boxes in a workspace |
| [GET /services/workspaces/{workspace_id}/instances](#get-servicesworkspacesworkspace_idinstances) | Gets the instances in a workspace |


## GET /services/workspaces
Gets the default workspace if no parameter is provided and user has no other privilege. If ids parameter (a list of workspace ids) is provided then it fetches all the workspaces corresponding to that list and user has access to.

### URL

#### Structure
```
[GET] /services/workspaces
```
#### Example
```
[GET] https://cam.ctl.io/services/workspaces
```
### Request

#### Headers
```
Content-Type: application/json
Authorization: Bearer your_json_web_token
ElasticBox-Release: 4.0
```
#### URI Parameters
| NAME | TYPE | DESCRIPTION | REQ. |
|------| ---- | ----------- | ---- |
| ids | string | Fetches the workspaces corresponding to each workspace id in the string. The ids will be separated by commas. For example: workspace4,operations,workspace5. | No |
| limit | integer | It limits the number of workspaces listed in the reply. | No |

#### Request body parameters

* None

### Response
#### Normal Response Codes

- **200** OK

#### Common Error Response Codes

- **400** Bad Request
- **401** Unauthorized
- **404** Not Found

#### Response Parameters

| Parameter | Type |Description |
|-----------|------|------------|
| add_provider | boolean | Indicates true if a personal workspace has a provider |
| billing_notice | boolean | If the flag is False we don't show the billing notice to the user |
| clc_alias | string | (optional) Account Id for billing customers that have an account at CL |
| clc_username | string | If user has CLC authentication |
| created | string | Creation date |
| costcenter | string | Cost center id |
| dashboard_notice | boolean | If the flag is False we don't show the dashboard notice to the user |
| deleted | string | It will be null if the resource is valid or a string with the time and date of deletion if it was deleted. End users will always see this parameter as null | |
| deploy_instance | boolean | Indicates if the workspace has deployed an instance |
| email | string | User email |
| email_validated_at | string | Email validation date. |
| favorites | array | List of user's favourite workspaces. User set a workspace as favourite when he clicks on a star. |
| group_dns | array | List of fully qualified names of LDAP groups to which a user’s personal workspace belongs. You can’t update this field. Present in Personal Workspaces |
| icon | string | Relative URL to a file that is stored as a blob in CAM and represents the workspace icon|
| id | string | Workspace unique identifier |
| last_login | string | Date of the last login. Example “2015-07-02 10:23:47.748740” |
| last_name | string | User last name |
| ldap_groups | array | List of fully qualified names of LDAP groups that are members of a workspace. Present in Team Workspaces |
| members | array | Lists members of a team workspace |
| name | string | User (Workspace) name |
| organization | string | (Personal Workspaces) Organization of the workspace |
| organizations | array | (Team Workspaces) List of the organizations' name of the workspace |
| owner | string | Refers to the username that owns the workspace. Present in Team Workspaces |
| saml_id | string | (optional) Account id if user logged in with SAML |
| schema | string | Schema URI. For personal workspace:  “http://elasticbox.net/schemas/workspaces/personal” For team workspace:  “http://elasticbox.net/schemas/workspaces/team” |
| support_user_created | boolean | True if support CAM user for this workspace has been created and is ready |
| take_tour | boolean | If true, the user has dismissed the tour popup |
| type | string | Workspace type. Can be personal or team. Users can edit personal workspace as long as schemas are valid and the user has privileges. |
| updated | string | Date of the last update |
| uri | string | Workspace uri |


#### Response Body

* Response to request without parameters
```
[
    {
        "last_name": "ElasticBox",
        "costcenter": "3ef6e6e0-a08d-40f1-98bf-4a7fc9b9c63a",
        "clc_alias": "CTLX",
        "id": "operations",
        "billing_notice": true,
        "last_login": "2018-12-11 12:53:11.636462",
        "add_provider": true,
        "deploy_instance": true,
        "type": "personal",
        "email": "operations@elasticbox.com",
        "schema": "http://elasticbox.net/schemas/workspaces/personal",
        "updated": "2018-12-11 12:53:11.636781",
        "take_tour": true,
        "deleted": null,
        "dashboard_notice": true,
        "email_validated_at": "2018-10-11 12:10:03.468280",
        "favorites": [],
        "icon": null,
        "group_dns": [],
        "clc_username": null,
        "name": "Operations",
        "created": "2018-10-11 12:10:03.468280",
        "support_user_created": false,
        "uri": "/services/workspaces/operations",
        "organization": "elasticbox"
    }
]
```
* Response to request with parameter
```
[
    {
        "uri": "/services/workspaces/operations",
        "icon": null,
        "id": "operations",
        "name": "Operations",
        "schema": "http://elasticbox.net/schemas/workspaces/personal"
    },
    {
        "uri": "/services/workspaces/workspace4",
        "icon": "/services/blobs/download/5bcf2c5c1862a312d7ac3c37/Screen-Shot-2018-10-23-at-16.12.23.png",
        "id": "workspace4",
        "name": "WORKSPACE A",
        "schema": "http://elasticbox.net/schemas/workspaces/team"
    },
    {
        "uri": "/services/workspaces/workspace5",
        "icon": "/services/blobs/download/5bcf2c5c1862a312d7ac3c37/Screen-Shot-2018-10-23-at-16.12.23.png",
        "id": "workspace5",
        "name": "WORKSPACE B",
        "schema": "http://elasticbox.net/schemas/workspaces/team"
    }
]
```
## POST /services/workspaces
Creates a workspace and gets the created workspace.

### URL

#### Structure
```
[POST] /services/workspaces
```
#### Example
```
[POST] https://cam.ctl.io/services/workspaces
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

#### Request body parameters

| NAME | TYPE | DESCRIPTION | REQ. |
|------| ---- | ----------- | ---- |
| costcenter | string | Cost center id | Yes |
| name | string | Workspace name | Yes |
| schema | string | Schema Url. For example, http://elasticbox.net/schemas/workspaces/team | Yes |

### Response
#### Normal Response Codes
- **201** Created

#### Common Error Response Codes
- **400** Invalid Data
- **401** Unauthorized

#### Response Parameters

| Parameter | Type |Description |
|-----------|------|------------|
| costcenter | string | Cost center id |
| created | string | Creation date |
| deleted | string | It will be null if the resource is valid or a string with the time and date of deletion if it was deleted. End users will always see this parameter as null |
| id | string | Workspace id |
| members | array | Lists members of a team workspace. |
| name | string | Workspace name |
| organizations | array | List of organization names |
| schema | string | Schema URI. Either “http://elasticbox.net/schemas/workspaces/personal” or “http://elasticbox.net/schemas/workspaces/team” |
| type | string | Workspace type. Can be personal or team. Users can edit personal workspace as long as schemas are valid and the user has privileges. |
| updated | string | Update date |
| uri | string | Url to access the workspace |


#### Response Body

```
{
    "organizations": [
        "elasticbox"
    ],
    "updated": "2018-10-24 14:52:42.302338",
    "name": "WORKSPACE C",
    "created": "2018-10-24 14:52:42.302338",
    "deleted": null,
    "uri": "/services/workspaces/workspace6",
    "members": [],
    "costcenter": "3ef6e6e0-a08d-40f1-98bf-4a7fc9b9c63a",
    "type": "team",
    "id": "workspace6",
    "schema": "http://elasticbox.net/schemas/workspaces/team"
}
```
## GET /services/workspaces/{workspace_id}
Fetches an existing workspace for the specified workspace ID.

### URL
#### Structure
```
[GET] /services/workspaces/{workspace_id}
```
#### Example
```
[GET] https://cam.ctl.io//services/workspaces/workspace4
```
### Request

#### Headers
```
Content-Type: application/json
Authorization: Bearer your_json_web_token
ElasticBox-Release: 4.0
```
#### URI Parameters

| NAME | TYPE | DESCRIPTION | REQ. |
|------| ---- | ----------- | ---- |
| workspace_id | string | Workspace id. | Yes |
#### Request body parameters

* None

### Response
#### Normal Response Codes

- **200** OK

#### Common Error Response Codes

- **401** Unauthorized
- **404** Not Found

#### Response Parameters

| Parameter | Type |Description |
|-----------|------|------------|
| costcenter | string | Cost center id |
| created | string | Creation date |
| deleted | string | It will be null if the resource is valid or a string with the time and date of deletion if it was deleted. End users will always see this parameter as null |
| icon | string | Url to Workspace avatar |
| id | string | Workspace id |
| members | array | Lists members of a team workspace |
| name | string | Workspace name |
| organizations | array | List of organization names |
| schema | string | Schema URI. Either “http://elasticbox.net/schemas/workspaces/personal” or “http://elasticbox.net/schemas/workspaces/team” |
| type | string | Workspace type. Can be personal or team. Users can edit personal workspace as long as schemas are valid and the user has privileges. |
| updated | string | Update date |
| uri | string | Url to access the workspace |


#### Response Body

```
{
    "organizations": [
        "elasticbox"
    ],
    "updated": "2018-10-23 14:13:21.375854",
    "name": "WORKSPACE C",
    "created": "2018-10-23 14:13:21.375854",
    "deleted": null,
    "uri": "/services/workspaces/workspace4",
    "schema": "http://elasticbox.net/schemas/workspaces/team",
    "costcenter": "3ef6e6e0-a08d-40f1-98bf-4a7fc9b9c63a",
    "members": [],
    "type": "team",
    "id": "workspace4",
    "icon": "/services/blobs/download/5bcf2c5c1862a312d7ac3c37/Screen-Shot-2018-10-23-at-16.12.23.png"
}
```

## PUT /services/workspaces/{workspace_id}
Updates an existing workspace.

### URL

#### Structure
```
[PUT] /services/workspaces/{workspace_id}
```
#### Example
```
[PUT] https://cam.ctl.io/services/workspaces/workspace4
```
### Request

#### Headers
```
Content-Type: application/json
Authorization: Bearer your_json_web_token
ElasticBox-Release: 4.0
```
#### URI Parameters

| NAME | TYPE | DESCRIPTION | REQ. |
|------| ---- | ----------- | ---- |
| workspace_id | string | Workspace id. | Yes |

#### Request body parameters

| NAME | TYPE | DESCRIPTION | REQ. |
|------| ---- | ----------- | ---- |
| costcenter | string | Cost center id | Yes |
| created | string | Workspace creation date | No |
| deleted | string | It will be null if the resource is valid or a string with the time and date of deletion if it was deleted. End users will always see this parameter as null | No |
| icon | string | Icon url | No |
| id | string | Workspace id | Yes |
| members | array | List of objects representing the members (other workspaces) added to this workspace | No |
| name | string | New workspace name | Yes |
| organizations | array | List of organization names  | Yes |
| schema | string | Workspace schema uri. Schema URI. Either “http://elasticbox.net/schemas/workspaces/personal” or “http://elasticbox.net/schemas/workspaces/team” | Yes |
| type | string | Workspace type. Can be personal or team. Users can edit personal workspace as long as schemas are valid and the user has privileges. | No |
| updated | string | Workspace update date | No |
```
{
    "organizations":["elasticbox"],
    "updated": "2018-10-25 07:26:50.016849",
    "name": "WORKSPACE E",
    "icon": "/services/blobs/download/5bcf2c5c1862a312d7ac3c37/Screen-Shot-2018-10-23-at-16.12.23.png",
    "created": "2018-10-23 14:15:29.294888",
    "deleted": null,
    "members":[
        {
            "id": "operations",
            "type": "workspace",
            "role": "user"
        }
    ],
    "costcenter": "3ef6e6e0-a08d-40f1-98bf-4a7fc9b9c63a",
    "type": "team",
    "id": "workspace5",
    "schema": "http://elasticbox.net/schemas/workspaces/team"
}
```

### Response
#### Normal Response Codes

- **200** OK

#### Common Error Response Codes

- **400** Bad Request
- **401** Unauthorized
- **404** Not Found

#### Response Parameters
| Parameter | Type |Description |
|-----------|------|------------|
| costcenter | string | Cost center id |
| created | string | Workspace creation date |
| deleted | string | It will be null if the resource is valid or a string with the time and date of deletion if it was deleted. End users will always see this parameter as null | No |
| icon | string | Icon url |
| id | string | Workspace id |
| members | array | List of objects representing the members (other workspaces) added to this workspace |
| name | string | New workspace name |
| organizations | array | List of organization names  |
| schema | string | Workspace schema uri. Schema URI. Either “http://elasticbox.net/schemas/workspaces/personal” or “http://elasticbox.net/schemas/workspaces/team” |
| type | string | Workspace type. Can be personal or team. Users can edit personal workspace as long as schemas are valid and the user has privileges. |
| updated | string | Workspace update date |
| uri | string | Url to access the updated workspace view |

#### Response Body

```
{
    "organizations": [
        "elasticbox"
    ],
    "updated": "2018-10-26 12:16:11.763338",
    "name": "WORKSPACE A",
    "created": "2018-10-26 12:15:44.433381",
    "deleted": null,
    "uri": "/services/workspaces/workspace7",
    "costcenter": "3ef6e6e0-a08d-40f1-98bf-4a7fc9b9c63a",
    "members":
        [
            {
                "type": "workspace",
                "role": "user",
                "id": "operations",
                "workspace": "operations"
            }
        ],
    "icon": null,
    "type": "team",
    "id": "workspace7",
    "schema": "http://elasticbox.net/schemas/workspaces/team"
}
```


## DELETE /services/workspaces/{workspace_id}
Deletes a workspace.

### URL

#### Structure
```
[DELETE] /services/workspaces/{workspace_id}
```
#### Example
```
[DELETE] https://cam.ctl.io/services/workspaces/workspace4
```
### Request

#### Headers
```
Content-Type: application/json
Authorization: Bearer your_json_web_token
ElasticBox-Release: 4.0
```
#### URI Parameters
| NAME | TYPE | DESCRIPTION | REQ. |
|------| ---- | ----------- | ---- |
| workspace_id | string | Workspace id. | Yes |

#### Request body parameters

* None

### Response
#### Normal Response Codes

- **204** No Content

#### Common Error Response Codes

- **401** Unauthorized
- **404** Not Found

#### Response Parameters

* None

#### Response Body

* None

## GET /services/workspaces/{workspace_id}/providers
Gets the providers registered in a workspace.

### URL

#### Structure
```
[GET] /services/workspaces/{workspace_id}/providers
```
#### Example
```
[GET] https://cam.ctl.io/services/workspaces/workspace4/providers
```
### Request

#### Headers
```
Content-Type: application/json
Authorization: Bearer your_json_web_token
ElasticBox-Release: 4.0
```
#### URI Parameters
| NAME | TYPE | DESCRIPTION | REQ. |
|------| ---- | ----------- | ---- |
| workspace_id | string | Workspace id | Yes |

#### Request body parameters
* None

### Response
#### Normal Response Codes

- **200** OK

#### Common Error Response Codes

- **401** Unauthorized
- **404** Not found

#### Response Parameters

| Parameter | Type |Description |
|-----------|------|------------|
| created | string | Provider creation date |
| description | string | Provider description |
| icon | string | Provider icon url |
| id | string | Provider id |
| members | array | List of members with access to the provider |
| name | string | Provider name |
| owner | string | Workspace id where the provider belongs to |
| schema | string | Provider schema uri. For example, "http://elasticbox.net/schemas/aws/provider" [See provider API documentation for a full list of schema types](./api-providers.md)|
| services | array | List of services associated to the provider |
| state | string | Provider state |
| type | string | Provider type |
| updated | string | Provider update date |
| uri | string | Url to access the provider view |

#### Response Body

```
[
    {
        "updated": "2018-11-20 12:23:10.654685",
        "description": null,
        "icon": "images/platform/aws.svg",
        "created": "2018-11-19 12:20:44.788595",
        "uri": "/services/providers/5b98633e-31d5-46ed-b530-f959d2898eef",
        "name": "My Amazon Web Services Provider",
        "services": [...],
        "state": "ready",
        "members": [],
        "owner": "operations",
        "credentials": {},
        "type": "Amazon Web Services",
        "id": "5b98633e-31d5-46ed-b530-f959d2898eef",
        "schema": "http://elasticbox.net/schemas/aws/provider"
    },
    {
        "updated": "2018-11-20 12:23:11.057875",
        "name": "My Centurly Link Provider",
        "icon": "images/platform/centurylink.svg",
        "created": "2018-11-20 08:57:43.926910",
        "uri": "/services/providers/ca33877a-6ade-4d28-8ed1-8c5e455148fa",
        "services": [...],
        "state": "ready",
        "members": [],
        "owner": "operations",
        "type": "CenturyLink",
        "id": "ca33877a-6ade-4d28-8ed1-8c5e455148fa",
        "schema": "http://elasticbox.net/schemas/centurylink/provider"
    }
]
```
## GET /services/workspaces/{workspace_id}/boxes
Gets the all the boxes in a workspace.

### URL
#### Structure
```
[GET] /services/workspaces/{workspace_id}/boxes
```
#### Example
```
[GET] https://cam.ctl.io/services/workspaces/workspace4/boxes
```
### Request

#### Headers
```
Content-Type: application/json
Authorization: Bearer your_json_web_token
ElasticBox-Release: 4.0
```
#### URI Parameters
| NAME | TYPE | DESCRIPTION | REQ. |
|------| ---- | ----------- | ---- |
| workspace_id | string | Workspace id | Yes |

#### Request body parameters

* None

### Response
#### Normal Response Codes

- **200** OK

#### Common Error Response Codes

- **401** Unauthorized
- **404** Not Found

#### Response Parameters

| Parameter | Type |Description |
|-----------|------|------------|
| automatic_updates | string | Type of automatic update |
| created | string | Box creation date |
| deleted | string | It will be null if the resource is valid or a string with the time and date of deletion if it was deleted. End users will always see this parameter as null |
| description | string | Box description |
| event | object | Event contained in one of the event lists, each event object contains the parameters: url, upload_date, length and destination_path |
| events | object | List of Box events, there may be nine event lists: configure, dispose, install, pre_configure, pre_dispose, pre_install, pre_start, pre_stop, start and stop. |
| icon | string | Box icon url |
| id | string | Box id |
| members | array | List of members with access to the box |
| name | string | Box name |
| organization | string | Organization name |
| owner | string | Workspace owner id |
| requirements | array | List of requirements of the box |
| schema | string | Box schema uri |
| type | string | Box type |
| updated | string | Box update date |
| uri | string | Url to access the box view |
| variables | array | List of variables associated to the box |
| visibility | string | Type of visibility the provider has |

#### Response Body

```
[
    {
        "updated": "2018-10-11 12:09:18.184974",
        "automatic_updates": "off",
        "requirements": [
            "linux"
        ],
        "name": "Oracle Database Service",
        "icon": "images/platform/oracle.png",
        "created": "2018-10-11 12:09:18.184974",
        "deleted": null,
        "variables": [
            {
                "required": false,
                "type": "Port",
                "name": "port",
                "value": "1521",
                "visibility": "public"
            },
            {
                "required": false,
                "type": "Text",
                "name": "database_name",
                "value": "",
                "visibility": "public"
            },
            {
                "required": true,
                "type": "Text",
                "name": "username",
                "value": "",
                "visibility": "public"
            },
            {
                "required": true,
                "type": "Password",
                "name": "password",
                "value": "",
                "visibility": "public"
            }
        ],
        "description": "Oracle Database as a Service",
        "uri": "/services/boxes/ce709ff9-69a7-4d95-bf14-97f069910be8",
        "visibility": "public",
        "id": "ce709ff9-69a7-4d95-bf14-97f069910be8",
        "friendly_id": "oracle-database-service",
        "members": [],
        "owner": "elasticbox",
        "organization": "public",
        "events": {},
        "schema": "http://elasticbox.net/schemas/boxes/script"
    },

    ... MORE BOXES ...

    {
        "updated": "2018-10-26 09:39:10.156446",
        "automatic_updates": "off",
        "requirements": [],
        "name": "Container A",
        "created": "2018-10-26 09:39:10.156446",
        "deleted": null,
        "variables": [
            {
                "required": false,
                "type": "Box",
                "name": "DOCKER_BOX",
                "value": "14c6d2c0-a1ea-436c-862b-c63d60acc53b",
                "visibility": "public"
            }
        ],
        "uri": "/services/boxes/bcc27232-4c44-470c-a329-30e45931b523",
        "visibility": "workspace",
        "events": {},
        "members": [],
        "owner": "workspace5",
        "organization": "elasticbox",
        "id": "bcc27232-4c44-470c-a329-30e45931b523",
        "schema": "http://elasticbox.net/schemas/boxes/docker"
    }
]
```
## GET /services/workspaces/{workspace_id}/instances
Gets the all the instances in a workspace.

### URL

#### Structure
```
[GET] /services/workspaces/{workspace_id}/instances
```
#### Example
```
[GET] https://cam.ctl.io/services/workspaces/myworkspace/instances
```
### Request

#### Headers
```
Content-Type: application/json
Authorization: Bearer your_json_web_token
ElasticBox-Release: 4.0
```
#### URI Parameters
| NAME | TYPE | DESCRIPTION | REQ. |
|------| ---- | ----------- | ---- |
| workspace_id | string | Workspace id | Yes |

#### Request body parameters

* None

### Response
#### Normal Response Codes

- **200** OK

#### Common Error Response Codes

- **401** Unauthorized
- **404** Not Found

#### Response Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| automatic_updates | string | Type of automatic update |
| bindings | array | List of instance bindings |
| boxes | array | List of boxes where each box object contains a service parameter. The service parameter can have one of these values: Linux Compute, Windows Compute and CloudFormation Service |
| icon | string | Instance icon uri |
| id | string | Instance id |
| is_deploy_only | boolean | If the instance is deploy only |
| machine | object | Machine contained in the service machines list |
| machine.name | string | Machine name |
| machine.state | string | Machine state, there are three possible states: processing, done and unavailable |
| machine.workflow | array | List of workflow actions, each workflow action object contains three parameters: box, event and script |
| members | array | List of members with access to the instance |
| name | string | Instance name |
| operation | object | Last operation, there are several types of operations: deploy, shutdown, poweron, reinstall, reconfigure, terminate, terminate_service |
| policy_box | object | Instance policy box |
| schema | string | Instance schema uri |
| service | object | Instance service |
| service.id | string | Service id |
| service.machines | array | List of service machines |
| service.type | string | Required. Can be one of these types: Linux Compute, Windows Compute and CloudFormation Service |
| state | string | Instance state, there are three possible states: processing, done and unavailable |
| tags | array | List of Instance tags |
| updated | string | Date of the last update |
| uri | string | Instance uri |
| variables | array | List of instance variables |

**Response Body**

```
[
    {
        "box": "29a9fe00-517a-4635-a77c-6eb473f4d7a1",
        "lease": {
            "released": false,
            "operation": "terminate",
            "expire": "2018-12-12 11:20:48.751000"
        },
        "updated": "2018-12-12 10:30:56.151018",
        "automatic_updates": "off",
        "policy_box": {
            "profile": {
                "subnet": "subnet-3412a250",
                "volumes": [],
                "pricing_info": {
                    "estimated_monthly": 417600,
                    "factor": 100000,
                    "hourly_price": 580,
                    "provider_type": "Amazon Web Services"
                },
                "image": "Linux Compute",
                "elastic_ip": false,
                "managed_os": false,
                "instances": 1,
                "keypair": "None",
                "role": "None",
                "location": "us-west-2",
                "placement_group": "",
                "cloud": "vpc-c52e9aa1",
                "flavor": "t2.nano",
                "security_groups": [
                    "Automatic"
                ],
                "schema": "http://elasticbox.net/schemas/aws/ec2/profile"
            },
            "provider_id": "cdcb8062-c792-4f92-9099-fc77831f5e0f",
            "automatic_updates": "off",
            "name": "My Deployment Policy",
            "created": "2018-12-12 10:19:21.170223",
            "deleted": null,
            "variables": [],
            "updated": "2018-12-12 10:20:25.788933",
            "lifespan": {
                "operation": "terminate",
                "interval": "hours",
                "quantity": 1
            },
            "visibility": "workspace",
            "members": [],
            "claims": [],
            "owner": "myworkspace",
            "organization": "elasticbox",
            "id": "0e37ec16-ac46-4fd6-a7d4-343b65982828",
            "schema": "http://elasticbox.net/schemas/boxes/policy"
        },
        "name": "My Script Box",
        "service": {
            "type": "Linux Compute",
            "id": "eb-e1uyz",
            "machines": [
                {
                    "state": "done",
                    "name": "my-script-box-eb-e1uyz-1",
                    "workflow": []
                }
            ]
        },
        "tags": [],
        "variables": [],
        "created": "2018-12-12 10:21:48.709303",
        "boxes": [
            {
                "updated": "2018-12-12 10:16:51.895046",
                "automatic_updates": "off",
                "requirements": [],
                "name": "My Script Box",
                "created": "2018-12-12 10:16:51.895046",
                "deleted": null,
                "variables": [],
                "visibility": "workspace",
                "id": "29a9fe00-517a-4635-a77c-6eb473f4d7a1",
                "members": [],
                "owner": "myworkspace",
                "organization": "elasticbox",
                "events": {},
                "schema": "http://elasticbox.net/schemas/boxes/script"
            }
        ],
        "id": "i-8jo5n5",
        "is_deploy_only": true,
        "state": "done",
        "members": [],
        "owner": "myworkspace",
        "bindings": [],
        "uri": "/services/instances/i-8jo5n5",
        "operation": {
            "event": "deploy",
            "workspace": "operations",
            "created": "2018-12-12 10:27:53.778494"
        },
        "schema": "http://elasticbox.net/schemas/instance"
    }
]
```

### Contacting Cloud Application Manager Support

We’re sorry you’re having an issue in [Cloud Application Manager](https://www.ctl.io/cloud-application-manager/). Please review the [troubleshooting tips](https://www.ctl.io/knowledge-base/cloud-application-manager/troubleshooting/troubleshooting-tips/), or contact [Cloud Application Manager support](mailto:incident@CenturyLink.com) with details and screenshots where possible.

For issues related to API calls, send the request body along with details related to the issue.

In the case of a box error, share the box in the workspace that your organization and Cloud Application Manager can access and attach the logs.
* Linux: SSH and locate the log at /var/log/elasticbox/elasticbox-agent.log
* Windows: RDP into the instance to locate the log at ProgramDataElasticBoxLogselasticbox-agent.log
