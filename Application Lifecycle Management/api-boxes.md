{{{
"title": "Boxes API",
"date": "12-27-2018",
"author": "Jorge Torres",
"attachments": [],
"contentIsHTML": false,
"keywords": ["cam api", "box", "alm", "get box", "delete box", "box stack", "diff between boxes", "box versions"]
}}}

Manage and perform actions on boxes.

**Create or List Boxes**

| Resource | Description |
|----------|-------------|
| [GET /services/boxes](#get-servicesboxes) | Gets the list of boxes that are accessible in the personal workspace. |
| [POST /services/boxes](#post-servicesboxes) | Creates a new box. |

**Perform Box Operations**

| Resource | Description |
|----------|-------------|
| [GET /services/boxes/{box_id}](#get-servicesboxesbox_id) | Fetches an existing box. |
| [PUT /services/boxes/{box_id}](#put-servicesboxesbox_id) | Updates an existing box. |
| [DELETE /services/box/{box_id}](#delete-servicesboxesbox_id) | Deletes an existing box. |
| [GET /services/boxes/{box_id}/stack](#get-servicesboxesbox_idstack) | Gets the box stack. |
| [GET /services/boxes/{box_id}/bindings](#get-servicesboxesbox_idbindings) | Gets the box bindings. |
| [GET /services/boxes/{box_id}/versions](#get-servicesboxesbox_idversions) | Get the list of box versions. |
| [PUT /services/boxes/{box_id}/diff](#put-servicesboxesbox_iddiff)  | Get the diff between two boxes. |

**CloudFormation Box**

The Cloud Application Manager CloudFormation box runs on the AWS CloudFormation service. It lets you create and customize templates that you can launch as a single stack of combined services in AWS. Manage CloudFormation configurations in Cloud Application Manager using these [API actions](./api-boxes.md).

Some examples include:
| Example |
|----------|
| [Create a CloudFormation box with template](#example-create-a-CloudFormation-box-with-template) |
| [Modify the CloudFormation Template](#example-modify-the-cloudFormation-template) |
| [Launch a CloudFormation Box](#example-launch-a-cloudFormation-box) |
| [Update a CloudFormation Stack in Real-Time](#example-update-a-cloudFormation-stack-in-real-time) |


## GET /services/boxes
Gets boxes that are accessible in the personal workspace of the authenticated user.

### URL

#### Structure
```
[GET] /services/boxes
```

```
[GET] /services/boxes?ids=value
```


#### Example
```
[GET] https://cam.ctl.io/services/boxes
```
An example with parameters to specify a list of boxes IDs.
```
[GET] https://cam.ctl.io/services/boxes?ids=8117657c-572a-4608-a2e2-82204ffa2ba5,540da08f-bbcf-4bb8-95bb-fcb690d44268
```

### Request

#### Headers
```
Content-Type: application/json
Authorization: Bearer your_json_web_token
ElasticBox-Release: 4.0
```
#### URI Parameters

| Parameter | Style | Type | Description | Req. |
|-----------|-------|------|-------------| ---- |
| ids | plain | string | Comma-separate list of boxes IDs | Opt. |

### Response
#### Normal Response Codes

- **200** OK

#### Common Error Response Codes

- **400** Invalid Data


#### Response Parameters

| Parameter | Style | Type | Description |
|--------------|-----------|----------|--------------|
| visibility | plain | string | Indicates at what level the box is visible. By default, boxes are visible to the workspace they’re created in. Can have one of these values: <li>public: Visible to Cloud Application Manager users across all organizations.</li> <li>organization: Visible to all users in the organization where the box was created.</li> <li>workspace: By default, the box is visible only to members of the workspace where it was created.</li> |
| organization | plain | string | Organization to which the box belongs. |
| updated | plain | string | Date of the last update. |
| description | plain | string | Box description. |
| requirements | plain | array | Box requirements. |
| variables | plain | array | List of box variables, each variable object contains the parameters: type, name, value, visibility, required, etc. |
| created | plain | string | Creation date. |
| uri | plain | string | Box uri. |
| id | plain | array | Box unique identificator. |
| schema | plain | string | Box schema uri. |
| members | plain | array | List of Box members. |
| owner | plain | string | Box owner. |
| icon | plain | string | Box icon uri. |
| events | plain | array | List of Box events, there may be nine event lists: configure, dispose, install, pre_configure, pre_dispose, pre_install, pre_start, pre_stop, start and stop. |
| event | plain | object | Event contained in one of the event lists, each event object contains the  parameters: url, upload_date, length and destination_path. |
| name | plain | string | Box name. |


### Response Body
```
[
    {
        "automatic_updates": "off",
        "variables": [
            {
                "required": false,
                "type": "Text",
                "name": "MNESIA_BASE",
                "value": "/var/lib/rabbitmq/mnesia",
                "visibility": "public"
            },
            {
                "required": false,
                "type": "Text",
                "name": "LOG_BASE",
                "value": "/var/log/rabbitmq",
                "visibility": "public"
            },
            {
                "name": "VERSION",
                "required": false,
                "value": "3.2.4",
                "visibility": "public",
                "type": "Options",
                "options": "3.2.4,3.3.5"
            },
            {
                "required": false,
                "type": "Port",
                "name": "mgmt",
                "value": "15672",
                "visibility": "public"
            },
            {
                "required": false,
                "type": "Port",
                "name": "rabbitmq",
                "value": "5672",
                "visibility": "public"
            },
            {
                "required": false,
                "type": "Text",
                "name": "username",
                "value": "",
                "visibility": "public"
            },
            {
                "required": false,
                "type": "Password",
                "name": "password",
                "value": "",
                "visibility": "public"
            },
            {
                "name": "CLONE_URL",
                "required": false,
                "visibility": "public",
                "value": "https://github.com/ElasticBox/rabbitmq.git",
                "scope": "github.git_repo",
                "type": "Text"
            },
            {
                "name": "PUPPET_DEFAULT",
                "required": false,
                "visibility": "public",
                "value": "/services/blobs/download/53550d367d0083337633e563/default.pp",
                "scope": "puppet",
                "type": "File"
            },
            {
                "required": false,
                "type": "Port",
                "name": "ssl_port",
                "value": "5671",
                "visibility": "public"
            },
            {
                "required": false,
                "type": "Text",
                "name": "CA_CERT_PATH",
                "value": "",
                "visibility": "public"
            },
            {
                "required": false,
                "type": "Text",
                "name": "SERVER_CERT_PATH",
                "value": "",
                "visibility": "public"
            },
            {
                "required": false,
                "type": "Text",
                "name": "SERVER_KEY_PATH",
                "value": "",
                "visibility": "public"
            },
            {
                "required": false,
                "type": "File",
                "name": "CA_CERT_FILE",
                "value": "/services/blobs/download/530fc09a3d0a0c698ab6fb78/Blank_file",
                "visibility": "public"
            },
            {
                "required": false,
                "type": "File",
                "name": "SERVER_CERT_FILE",
                "value": "/services/blobs/download/530fc09a3d0a0c698ab6fb78/Blank_file",
                "visibility": "public"
            },
            {
                "required": false,
                "type": "File",
                "name": "SERVER_KEY_FILE",
                "value": "/services/blobs/download/530fc09a3d0a0c698ab6fb78/Blank_file",
                "visibility": "public"
            },
            {
                "automatic_updates": "off",
                "name": "github",
                "required": false,
                "value": "758de981-475a-47fc-b0d9-342edda52a82",
                "visibility": "public",
                "type": "Box"
            },
            {
                "automatic_updates": "off",
                "name": "puppet",
                "required": false,
                "value": "08cc115c-4738-4f69-a8b7-da2e1dfec27c",
                "visibility": "public",
                "type": "Box"
            },
            {
                "name": "CLONE_DIRECTORY",
                "required": false,
                "visibility": "public",
                "value": "/etc/puppet/modules/rabbitmq",
                "scope": "github.git_repo",
                "type": "Text"
            }
        ],
        "friendly_id": "rabbitmq",
        "owner": "elasticbox",
        "id": "540da08f-bbcf-4bb8-95bb-fcb690d44268",
        "requirements": [
            "linux"
        ],
        "deleted": null,
        "version": {
            "box": "be59362e-87d8-4be3-addd-8363b07a2ae4",
            "number": {
                "major": 0,
                "minor": 1,
                "patch": 3
            },
            "workspace": "matt",
            "description": "Updated Icon"
        },
        "readme": {
            "url": "/services/blobs/download/55db2cc60468cd7d5cd7ce04/rabbitmq.mdown",
            "upload_date": "2015-08-24 14:40:06.536836",
            "length": 4415,
            "content_type": "application/octet-stream"
        },
        "events": {
            "pre_install": {
                "url": "/services/blobs/download/53571d577d0083337633e8eb/pre_install",
                "upload_date": "2014-02-14 15:10:18.540864",
                "length": 614,
                "destination_path": "scripts",
                "content_type": "text/x-shellscript"
            }
        },
        "schema": "http://elasticbox.net/schemas/boxes/script",
        "updated": "2015-12-22 22:16:30.618152",
        "description": "Robust and easy-to-use messaging for applications",
        "icon_metadata": {
            "image": "images/platform/technologies/rabbitmq.svg",
            "border": "#EE5715",
            "fill": "#FF6E0D"
        },
        "visibility": "public",
        "members": [],
        "categories": [
            "Message Broker"
        ],
        "icon": "/icons/boxes/be59362e-87d8-4be3-addd-8363b07a2ae4",
        "name": "RabbitMQ",
        "created": "2015-12-22 22:19:13.638201",
        "uri": "/services/boxes/540da08f-bbcf-4bb8-95bb-fcb690d44268",
        "organization": "elasticbox",
        "draft_from": "8698cbcc-d24e-4258-b18a-df9dd526e4d4"
    },
    {
        "schema": "http://elasticbox.net/schemas/boxes/cloudformation",
        "updated": "2015-05-22 20:25:17.104346",
        "automatic_updates": "off",
        "requirements": [
            "oracle"
        ],
        "description": "Oracle Database as a Service",
        "created": "2014-02-14 15:09:53.382579",
        "icon_metadata": {
            "image": "images/platform/oracle.png",
            "border": "#F8F8F9",
            "fill": "#FFFFFF"
        },
        "variables": [
            {
                "required": false,
                "type": "Port",
                "name": "port",
                "value": "1521",
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
            },
            {
                "required": false,
                "type": "Text",
                "name": "database_name",
                "value": "",
                "visibility": "public"
            }
        ],
        "uri": "/services/boxes/8117657c-572a-4608-a2e2-82204ffa2ba5",
        "visibility": "public",
        "name": "Oracle Database Service",
        "deleted": null,
        "members": [],
        "owner": "public",
        "organization": "ebx",
        "type": "Oracle Database Service",
        "id": "8117657c-572a-4608-a2e2-82204ffa2ba5",
        "draft_from": "67695551-7ca9-4f90-bb00-7e8bf774c487",
        "icon": "/icons/boxes/8117657c-572a-4608-a2e2-82204ffa2ba5"
    }
]
```

## POST /services/boxes
Creates a new box in the personal workspace and gets the created box.

### URL

#### Structure
```
[POST] /services/boxes
```

#### Example
```
[POST] https://cam.ctl.io/services/boxes
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


#### Request Body Parameters

| Parameter | Style | Type | Description | Req. | 
|-----------|-------|------|-------------|-----|
| requirements | plain | array | Box requirements. | |  
| owner | plain | string | Box owner, the user name for a personal workspace and the workspace name for a team workspace. | |
| visibility | plain | string | Indicates at what level the box is visible. By default, boxes are visible to the workspace they’re created in. Can have one of these values: <li>public: Visible to Cloud Application Manager users across all organizations.</li> <li>organization: Visible to all users in the organization where the box was created.</li> <li>workspace: By default, the box is visible only to members of the workspace where it was created.</li> | | 
| name | plain | string | Box name. | Yes | 
| description | plain | string | Box description. | |
| icon | plain | string | Icon url. |  | 
| schema | plain | string | Box schema. | Yes | 

#### Request Body

```
{
    "owner": "operation",
    "schema":"http://elasticbox.net/schemas/boxes/script",
    "requirements":["linux","apache"],
    "automatic_updates":"off",
    "name":"Test Starter Box",
    "description":"Test Started for our showcase",
    "variables": [
      {
        "required": false,
        "type": "Text",
        "name": "variable_name",
        "value": ""
      }
    ]
}
```

### Response
#### Normal Response Codes

- **200** OK

#### Common Error Response Codes

- **400** Invalid Data
- **409** Conflict


#### Response Parameters

| Parameter | Style | Type | Description |
|-----------|-------|------|-------------|
| visibility | plain | string | Indicates at what level the box is visible. By default, boxes are visible to the workspace they’re created in. Can have one of these values: <li>public: Visible to Cloud Application Manager users across all organizations.</li> <li>organization: Visible to all users in the organization where the box was created.</li> <li>workspace: By default, the box is visible only to members of the workspace where it was created.</li> |
| organization | plain | string | Organization to which the box belongs. |
| updated | plain | string | Date of the last update. |
| description | plain | string | Box description. |
| requirements | plain | array | Box requirements. |
| variables | plain | array | List of box variables, each variable object contains the parameters: type, name, value, visibility, required, etc. |
| created | plain | string | Creation date. |
| uri | plain | string | Box uri. |
| id | plain | array | Box unique identificator. |
| schema | plain | string | Box schema uri. |
| members | plain | array | List of Box members. |
| owner | plain | string | Box owner. |
| icon | plain | string | Box icon uri. |
| events | plain | array | List of Box events, there may be nine event lists: configure, dispose, install, pre_configure, pre_dispose, pre_install, pre_start, pre_stop, start and stop. |
| event | plain | object | Event contained in one of the event lists, each event object contains the parameters: url, upload_date, length and destination_path. |
| name | plain | string | Box name. |


### Response Body
```
{
    "updated": "2018-12-28 15:05:52.816432",
    "automatic_updates": "off",
    "requirements": [
        "apache",
        "linux"
    ],
    "description": "Test Started for our showcase",
    "created": "2018-12-28 15:05:52.816432",
    "deleted": null,
    "variables": [
        {
            "required": false,
            "type": "Text",
            "name": "variable_name",
            "value": "",
            "visibility": "public"
        }
    ],
    "uri": "/services/boxes/0e725f03-052b-43e2-8c5d-32341bf60a8d",
    "visibility": "workspace",
    "events": {},
    "members": [],
    "owner": "operation",
    "organization": "centurylink",
    "schema": "http://elasticbox.net/schemas/boxes/script",
    "id": "0e725f03-052b-43e2-8c5d-32341bf60a8d",
    "name": "Test Starter Box"
}
```


## GET /services/boxes/{box_id}

Fetches an existing box, requires the specified id box_id.

### URL

#### Structure
```
[GET] /services/boxes/{box_id}
```


#### Example
```
[GET] https://cam.ctl.io/services/boxes/0e725f03-052b-43e2-8c5d-32341bf60a8d
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
| box_id | string | Box id | Yes |


### Response
#### Normal Response Codes

- **200** OK

#### Common Error Response Codes

- **403** Forbidden
- **404** Not Found


#### Response Parameters

| Parameter | Style | Type | Description |
|-----------|-------|------|-------------|
| visibility | plain | string | Indicates at what level the box is visible. By default, boxes are visible to the workspace they’re created in. Can have one of these values: <li>public: Visible to Cloud Application Manager users across all organizations.</li> <li>organization: Visible to all users in the organization where the box was created.</li> <li>workspace: By default, the box is visible only to members of the workspace where it was created.</li> |
| organization | plain | string | Organization to which the box belongs. |
| updated | plain | string | Date of the last update. |
| description | plain | string | Box description. |
| requirements | plain | array | Box requirements. |
| variables | plain | array | List of box variables, each variable object contains the parameters: type, name, value, visibility, required, etc. |
| created | plain | string | Creation date. |
| uri | plain | string | Box uri. |
| id | plain | array | Box unique identificator. |
| schema | plain | string | Box schema uri. |
| members | plain | array | List of Box members. |
| owner | plain | string | Box owner. |
| icon | plain | string | Box icon uri. |
| events | plain | array | List of Box events, there may be nine event lists: configure, dispose, install, pre_configure, pre_dispose, pre_install, pre_start, pre_stop, start and stop. |
| event | plain | object | Event contained in one of the event lists, each event object contains the  parameters: url, upload_date, length and destination_path. |
| name | plain | string | Box name. |


### Response Body
```
{
  "schema": "http://elasticbox.net/schemas/boxes/script",
  "updated": "2015-07-02 16:20:35.534878",
  "automatic_updates": "off",
  "requirements": [
    "linux"
  ],
  "description": "Wordpress Started for our showcase",
  "created": "2015-07-02 16:20:35.534878",
  "deleted": null,
  "variables": [],
  "uri": "/services/boxes/60cef61c-73dc-41d9-a32f-70f49a509c66",
  "visibility": "workspace",
  "events": {},
  "members": [],
  "owner": "project",
  "organization": "elasticbox",
  "id": "60cef61c-73dc-41d9-a32f-70f49a509c66",
  "name": "Wordpress Starter Box"
}
```

## PUT /services/boxes/{box_id}

Requires the box ID to update an existing box. The request body must contain the box object and can only update the following fields: files, variables, ports, requirements, description, icon, name, events, and members.

### URL

#### Structure
```
[PUT] /services/boxes/{box_id}
```


#### Example
```
[PUT] https://cam.ctl.io/services/boxes/{box_id}
```

### Request

#### Headers
```
Content-Type: application/json
Authorization: Bearer your_json_web_token
ElasticBox-Release: 4.0
```

#### URI Parameters

| Parameter | Style | Type | Description | Req. |
|-----------|-------|------|-------------|----|
| box_id | plain | string | Box id | Yes |


#### Request Body Parameters


| Parameter | Style | Type | Description |  Req. |
|-----------|-------|------|-------------|-----|
| updated | plain | string | Date of the last update. | |
| description | plain | string | Box description. |  |
| requirements | plain | array | Box requirements. | |
| variables | plain | array | List of box variables, each variable object contains the parameters: type, name, value, visibility, required, etc. | |
| created | plain | string | Creation date. | |
| uri | plain | string | Box uri. | |
| id | plain | array | Box unique identificator. | |
| schema | plain | string | Box schema uri. | Yes |
| members | plain | array | List of Box members. | |
| owner | plain | string | Box owner. | Yes | |
| organization | plain | string | Organization to which the box belongs. | Yes |
| icon | plain | string | Box icon uri. | |
| events | plain | array | List of Box events, there may be nine event lists: configure, dispose, install, pre_configure, pre_dispose, pre_install, pre_start, pre_stop, start and stop. | |
| event | plain | object | Event contained in one of the event lists, each event object contains the  parameters: url, upload_date, length and destination_path. | |
| name | plain | string | Box name. | Yes |


#### Request Body
```
{
    "schema":"http://elasticbox.net/schemas/boxes/script",
    "updated":"2018-28-12 16:23:46.702968",
    "automatic_updates":"off",
    "requirements":[
        "linux"
    ],
    "description":"New description set",
    "created":"2015-07-02 16:20:15.098554",
    "deleted":null,
    "variables":[
        {
            "required":false,
            "type":"Text",
            "name":"variable_name",
            "value":"Default value",
            "visibility":"public"

        }
        ],
        "uri":"/services/boxes/9192cb3e-04e2-4c50-b8a5-a25c980479d4",
        "visibility":"workspace",
        "events":{},
        "members":[],
        "owner":"operation",
        "organization":"elasticbox",
        "id":"0e725f03-052b-43e2-8c5d-32341bf60a8d",
        "name":"Rename Test Starter Box"
}
```

### Response
#### Normal Response Codes

- **200** OK

#### Common Error Response Codes

- **400** Invalid Data
- **403** Forbidden
- **404** Not Found


#### Response Parameters

| Parameter | Style | Type | Description |
|-----------|-------|------|-------------|
| visibility | plain | string | Indicates at what level the box is visible. By default, boxes are visible to the workspace they’re created in. Can have one of these values: <li>public: Visible to Cloud Application Manager users across all organizations.</li> <li>organization: Visible to all users in the organization where the box was created.</li> <li>workspace: By default, the box is visible only to members of the workspace where it was created.</li> |
| organization | plain | string | Organization to which the box belongs. |
| updated | plain | string | Date of the last update. |
| description | plain | string | Box description. |
| requirements | plain | array | Box requirements. |
| variables | plain | array | List of box variables, each variable object contains the parameters: type, name, value, visibility, required, etc. |
| created | plain | string | Creation date. |
| uri | plain | string | Box uri. |
| id | plain | array | Box unique identificator. |
| schema | plain | string | Box schema uri. |
| members | plain | array | List of Box members. |
| owner | plain | string | Box owner. |
| icon | plain | string | Box icon uri. |
| events | plain | array | List of Box events, there may be nine event lists: configure, dispose, install, pre_configure, pre_dispose, pre_install, pre_start, pre_stop, start and stop. |
| event | plain | object | Event contained in one of the event lists, each event object contains the  parameters: url, upload_date, length and destination_path. |
| name | plain | string | Box name. |


### Response Body
```
{
    "updated": "2018-12-28 16:07:08.238548",
    "automatic_updates": "off",
    "requirements": [
        "linux"
    ],
    "description": "New description",
    "name": "Rename Test Starter Box",
    "created": "2018-12-28 15:05:52.816432",
    "deleted": null,
    "variables": [
        {
            "required": false,
            "type": "Text",
            "name": "variable_name",
            "value": "Default value",
            "visibility": "public"
        }
    ],
    "uri": "/services/boxes/0e725f03-052b-43e2-8c5d-32341bf60a8d",
    "visibility": "workspace",
    "id": "0e725f03-052b-43e2-8c5d-32341bf60a8d",
    "members": [],
    "owner": "operation",
    "organization": "centurylink",
    "events": {},
    "schema": "http://elasticbox.net/schemas/boxes/script"
}
```

## DELETE /services/boxes/{box_id}
Deletes an existing box, requires the specified id box_id.

### URL

#### Structure
```
[DELETE] /services/boxes/{box_id}
```

#### Example
```
[DELETE] https://cam.ctl.io/services/boxes/0e725f03-052b-43e2-8c5d-32341bf60a8d
```

### Request

#### Headers
```
Content-Type: application/json
Authorization: Bearer your_json_web_token
ElasticBox-Release: 4.0
```
#### URI Parameters

| Parameter | Style | Type | Description | Req. |
|-----------|-------|------|-------------| ---- |
| box_id | plain | string | Box id | Yes |

### Response
#### Normal Response Codes

- **204** OK

#### Common Error Response Codes

- **403** Forbidden
- **404** Not Found



## GET /services/boxes/{box_id}/stack

Gets the box stack. The box stack is a list of boxes. All boxes that are a box variable of the given box are included. The first box is always the given box.

### URL

#### Structure
```
[GET] /services/boxes//{box_id}/stack
```

#### Example
```
[GET] https://cam.ctl.io/services/boxes/f4dd017f-4bec-42f4-9614-bd27fd8baf74/stack
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
| box_id | string | Box id | Yes |



### Response
#### Normal Response Codes

- **200** OK

#### Common Error Response Codes

- **400** Bad Request


#### Response Parameters

| Parameter | Style | Type | Description |
|-----------|-------|------|-------------|
| visibility | plain | string | Indicates at what level the box is visible. By default, boxes are visible to the workspace they’re created in. Can have one of these values: <li>public: Visible to Cloud Application Manager users across all organizations.</li> <li>organization: Visible to all users in the organization where the box was created.</li> <li>workspace: By default, the box is visible only to members of the workspace where it was created.</li> |
| organization | plain | string | Organization to which the box belongs. |
| updated | plain | string | Date of the last update. |
| description | plain | string | Box description. |
| tags | plain | array | Box tags. |
| variables | plain | array | List of box variables, each variable object contains the parameters: type, name, value, visibility, required, etc.  |
| created | plain | string | Creation date. |
| uri | plain | string | Box uri. |
| id | plain | array | Box unique identificator. |
| schema | plain | string | Box schema uri. |
| members | plain | array | List of Box members. |
| owner | plain | string | Box owner. |
| icon | plain | string | Box icon uri. |
| events | plain | array | List of Box events, there may be nine event lists: configure, dispose, install, pre_configure, pre_dispose, pre_install, pre_start, pre_stop, start and stop. |
| event | plain | object | Event contained in one of the event lists, each event object contains the  parameters: url, upload_date, length and destination_path. |
| name | plain | string | Box name. |


### Response Body
The following example is of the Box that install and configure Magento using nginx and php-fpm boxes to run the application.


```
[
    {
        "schema": "http://elasticbox.net/schemas/boxes/script",
        "updated": "2015-12-22 23:11:27.168377",
        "automatic_updates": "off",
        "requirements": [
            "linux"
        ],
        "description": "HA proxy for MySQL",
        "created": "2015-11-30 19:51:27.665743",
        "deleted": null,
        "variables": [
            {
                "automatic_updates": "major",
                "name": "haproxy",
                "required": false,
                "visibility": "private",
                "value": "87830b58-ceaf-4790-81d1-4511816b012f",
                "type": "Box"
            },
            {
                "name": "http",
                "required": false,
                "visibility": "internal",
                "value": "3306",
                "scope": "haproxy",
                "type": "Port"
            },
            {
                "name": "fallback_binding_port",
                "required": false,
                "visibility": "internal",
                "value": "3306",
                "scope": "haproxy",
                "type": "Port"
            },
            {
                "name": "CONFIG_FILE",
                "required": false,
                "visibility": "internal",
                "value": "/services/blobs/download/56719884974c520dbaf06db0/haproxy.conf",
                "scope": "haproxy",
                "type": "File"
            },
            {
                "name": "MODE",
                "required": false,
                "visibility": "internal",
                "value": "tcp",
                "scope": "haproxy",
                "type": "Options",
                "options": "http,tcp,health"
            }
        ],
        "uri": "/services/boxes/f6deab86-3744-4be3-bd48-804697859423",
        "visibility": "workspace",
        "name": "MySQL HA Proxy",
        "icon_metadata": {
            "image": "images/platform/technologies/mysql.svg",
            "border": "#227C95",
            "fill": "#ffffff"
        },
        "events": {
            "configure": {
                "url": "/services/blobs/download/565d277217fe944e08464179/configure",
                "length": 1033,
                "destination_path": "scripts",
                "content_type": "text/x-shellscript"
            },
            "install": {
                "url": "/services/blobs/download/565e37a9b1ac9f56ad579a8d/install",
                "length": 634,
                "destination_path": "scripts",
                "content_type": "text/x-shellscript"
            }
        },
        "members": [
            {
                "role": "collaborator",
                "workspace": "rackspace1"
            }
        ],
        "owner": "super",
        "organization": "elasticbox",
        "id": "f6deab86-3744-4be3-bd48-804697859423",
        "icon": "/icons/boxes/f6deab86-3744-4be3-bd48-804697859423"
    },
    {
        "automatic_updates": "off",
        "variables": [
            {
                "required": false,
                "type": "Port",
                "name": "http",
                "value": "80",
                "visibility": "public"
            },
            {
                "required": false,
                "type": "Port",
                "name": "fallback_binding_port",
                "value": "80",
                "visibility": "public"
            },
            {
                "required": false,
                "type": "Text",
                "name": "CONFIG_FILE_NAME",
                "value": "haproxy.cfg",
                "visibility": "public"
            },
            {
                "required": false,
                "type": "File",
                "name": "CONFIG_FILE",
                "value": "/services/blobs/download/55dc3b66b8485e51a2a7d236/haproxy.conf",
                "visibility": "public"
            },
            {
                "name": "MODE",
                "required": false,
                "visibility": "public",
                "value": "http",
                "type": "Options",
                "options": "http,tcp,health"
            },
            {
                "required": false,
                "type": "Binding",
                "name": "servers",
                "value": "AnyBox",
                "visibility": "private"
            }
        ],
        "friendly_id": "haproxy",
        "owner": "elasticbox",
        "id": "87830b58-ceaf-4790-81d1-4511816b012f",
        "requirements": [
            "linux"
        ],
        "icon_metadata": {
            "image": "images/platform/technologies/haproxy.svg",
            "border": "#3F52AA",
            "fill": "#ffffff"
        },
        "version": {
            "box": "fbe1f028-d95e-4bde-958b-00a5d5ca50d6",
            "number": {
                "major": 0,
                "minor": 1,
                "patch": 4
            },
            "workspace": "arnaud-elasticbox",
            "description": "Fix apt-get update"
        },
        "readme": {
            "url": "/services/blobs/download/565e1bedb1ac9f56ad57986a/README.md",
            "upload_date": "2015-12-01 22:15:09.369640",
            "length": 1778,
            "content_type": "text/x-markdown"
        },
        "events": {
            "start": {
                "url": "/services/blobs/download/55dc3b65b8485e51a2a7d234/start",
                "upload_date": "2015-08-25 09:54:45.995814",
                "length": 40,
                "destination_path": "scripts",
                "content_type": null
            },
            "configure": {
                "url": "/services/blobs/download/565cfea1b1ac9f56ad57867b/configure",
                "upload_date": "2015-08-25 09:54:44.800362",
                "length": 102,
                "destination_path": "scripts",
                "content_type": "text/x-shellscript"
            },
            "install": {
                "url": "/services/blobs/download/565e26e017fe944e08465290/install",
                "upload_date": "2015-08-25 09:54:43.653716",
                "length": 524,
                "destination_path": "scripts",
                "content_type": "text/x-shellscript"
            }
        },
        "schema": "http://elasticbox.net/schemas/boxes/script",
        "updated": "2015-12-22 22:30:31.610021",
        "description": "Reliable, High Performance, TCP / HTTP Load Balancer",
        "deleted": null,
        "visibility": "public",
        "members": [],
        "categories": [
            "Load Balancer"
        ],
        "icon": "/services/blobs/download/55e6ca6bdda62a64df899596/haproxy.png",
        "name": "HAProxy",
        "created": "2015-12-01 23:02:07.975395",
        "uri": "/services/boxes/87830b58-ceaf-4790-81d1-4511816b012f",
        "organization": "elasticbox",
        "draft_from": "35b8e7c0-3074-48ed-9b89-28ec6f279830"
    },
    {
        "schema": "http://elasticbox.net/schemas/boxes/script",
        "updated": "2016-12-08 18:22:58.904383",
        "automatic_updates": "off",
        "requirements": [
            "linux"
        ],
        "description": "A free, open-source, high-performance HTTP server and",
        "created": "2015-09-12 19:44:34.159558",
        "deleted": null,
        "variables": [
            {
                "required": false,
                "type": "Port",
                "name": "http",
                "value": "80",
                "visibility": "public"
            },
            {
                "required": false,
                "type": "File",
                "name": "PUBLIC_SSL_CERTIFICATE",
                "value": "/services/blobs/download/55f48216dda62a5eab4a41ca/public.crt",
                "visibility": "internal"
            },
            {
                "required": false,
                "type": "File",
                "name": "PRIVATE_SSL_KEY",
                "value": "/services/blobs/download/55f4822bb1ac9f70ec5d4bb9/private.key",
                "visibility": "internal"
            },
            {
                "required": false,
                "type": "File",
                "name": "NGINX_CONF",
                "value": "/services/blobs/download/57325a5636b43a30a1fb77f7/nginx.conf",
                "visibility": "internal"
            },
            {
                "required": false,
                "type": "Text",
                "name": "NGINX_USER",
                "value": "root",
                "visibility": "internal"
            },
            {
                "required": false,
                "type": "Text",
                "name": "NGINX_GROUP",
                "value": "root",
                "visibility": "internal"
            },
            {
                "required": false,
                "type": "Text",
                "name": "LOG_PATH",
                "value": "/var/log/nginx",
                "visibility": "internal"
            },
            {
                "required": false,
                "type": "Text",
                "name": "CACHE_PATH",
                "value": "/var/nginx/cache",
                "visibility": "internal"
            },
            {
                "required": false,
                "type": "Text",
                "name": "CERTIFICATE_PATH",
                "value": "/var/nginx/certificates",
                "visibility": "internal"
            }
        ],
        "readme": {
            "url": "/services/blobs/download/56297b2fb1ac9f4d02d1c2ab/README.md",
            "upload_date": "2015-10-23 00:11:27.558696",
            "length": 2278,
            "content_type": "text/x-markdown"
        },
        "uri": "/services/boxes/8e176772-5c6c-4d5a-8f6e-cbf342142520",
        "visibility": "workspace",
        "name": "Nginx",
        "icon_metadata": {
            "image": "images/platform/technologies/nginx.svg",
            "border": "#007731",
            "fill": "#00964C"
        },
        "events": {
            "start": {
                "url": "/services/blobs/download/565e31b5b1ac9f56ad57999b/start",
                "length": 91,
                "destination_path": "scripts",
                "content_type": "text/x-shellscript"
            },
            "configure": {
                "url": "/services/blobs/download/56673867dda62a46af5b4275/configure",
                "length": 519,
                "destination_path": "scripts",
                "content_type": "text/x-shellscript"
            },
            "install": {
                "url": "/services/blobs/download/57e55ad5c60625154acebee3/install",
                "length": 1515,
                "destination_path": "scripts",
                "content_type": "text/x-shellscript"
            }
        },
        "members": [
            {
                "role": "collaborator",
                "workspace": "rackspace1"
            }
        ],
        "owner": "super",
        "organization": "elasticbox",
        "id": "8e176772-5c6c-4d5a-8f6e-cbf342142520",
        "draft_from": "790e4791-be29-40fa-85ca-619dd3061ced",
        "icon": "/icons/boxes/8e176772-5c6c-4d5a-8f6e-cbf342142520"
    },
    {
        "schema": "http://elasticbox.net/schemas/boxes/script",
        "updated": "2016-12-08 18:34:39.878898",
        "automatic_updates": "off",
        "requirements": [
            "internal",
            "linux"
        ],
        "name": "Magento",
        "created": "2015-09-12 18:25:43.678013",
        "deleted": null,
        "variables": [
            {
                "name": "LOCAL_PATH",
                "required": true,
                "value": "/mnt/media",
                "visibility": "internal",
                "scope": "nfs",
                "type": "Text"
            },
            {
                "name": "CONFIG_FILE",
                "required": false,
                "value": "/services/blobs/download/565f3c92974c525666cd2f84/haproxy.conf",
                "visibility": "public",
                "scope": "redis.haproxy",
                "type": "File"
            },
            {
                "name": "CONFIG_FILE_NAME",
                "required": false,
                "value": "redis.cfg",
                "visibility": "public",
                "scope": "redis.haproxy",
                "type": "Text"
            },
            {
                "required": false,
                "type": "Text",
                "name": "MAGENTO_URL",
                "value": "https://s3-us-west-1.amazonaws.com/ebx-public/magento-1.9.2.2.tar-2015-10-27-03-19-32.gz",
                "visibility": "internal"
            },
            {
                "required": false,
                "type": "Text",
                "name": "SERVER_NAME",
                "value": "localhost",
                "visibility": "public"
            },
            {
                "required": false,
                "type": "Port",
                "name": "http",
                "value": "80",
                "visibility": "public"
            },
            {
                "required": false,
                "type": "File",
                "name": "MAGENTO_CONF",
                "value": "/services/blobs/download/565ca77d17fe944e08463a45/magento.conf",
                "visibility": "internal"
            },
            {
                "required": false,
                "type": "File",
                "name": "MAGENTO_CONFIG",
                "value": "/services/blobs/download/565f3b1bb1ac9f56ad57b423/local.xml",
                "visibility": "internal"
            },
            {
                "required": false,
                "type": "Text",
                "name": "MAGENTO_PATH",
                "value": "/opt/magento",
                "visibility": "internal"
            },
            {
                "automatic_updates": "major",
                "name": "redis",
                "required": false,
                "value": "053c6467-13e4-47fb-b6cf-46f51e6c2294",
                "visibility": "public",
                "type": "Box"
            },
            {
                "automatic_updates": "major",
                "name": "mysql",
                "required": false,
                "value": "f6deab86-3744-4be3-bd48-804697859423",
                "visibility": "public",
                "type": "Box"
            },
            {
                "automatic_updates": "major",
                "name": "nginx",
                "required": false,
                "visibility": "internal",
                "value": "8e176772-5c6c-4d5a-8f6e-cbf342142520",
                "type": "Box"
            },
            {
                "automatic_updates": "major",
                "name": "php",
                "required": false,
                "value": "ed085cfd-8707-4ef7-9611-6e84498d27c6",
                "visibility": "internal",
                "type": "Box"
            },
            {
                "automatic_updates": "major",
                "name": "nfs",
                "required": false,
                "value": "320e8be7-5d05-4f74-a040-5d74836ae608",
                "visibility": "public",
                "type": "Box"
            }
        ],
        "description": "Magento Web Layer",
        "readme": {
            "url": "/services/blobs/download/563a84b1dda62a1ca8ed5bdb/README.md",
            "upload_date": "2015-11-04 22:20:33.241618",
            "length": 2264,
            "content_type": "text/x-markdown"
        },
        "uri": "/services/boxes/f4dd017f-4bec-42f4-9614-bd27fd8baf74",
        "visibility": "workspace",
        "events": {
            "configure": {
                "url": "/services/blobs/download/566604fcb1ac9f56ad5809bf/configure",
                "length": 702,
                "destination_path": "scripts",
                "content_type": "text/x-shellscript"
            },
            "install": {
                "url": "/services/blobs/download/565e1855dda62a46af5acc97/install",
                "length": 829,
                "destination_path": "scripts",
                "content_type": "text/x-shellscript"
            }
        },
        "icon_metadata": {
            "image": "images/platform/technologies/magento.svg",
            "border": "#191815",
            "fill": "#31302B"
        },
        "members": [
            {
                "role": "collaborator",
                "workspace": "rackspace1"
            },
            {
                "role": "read",
                "workspace": "centurylink"
            }
        ],
        "owner": "super",
        "organization": "elasticbox",
        "id": "f4dd017f-4bec-42f4-9614-bd27fd8baf74",
        "draft_from": "de1841f7-cfbe-4443-a996-d13807271a18",
        "icon": "/icons/boxes/f4dd017f-4bec-42f4-9614-bd27fd8baf74"
    },
    {
        "schema": "http://elasticbox.net/schemas/boxes/script",
        "updated": "2016-12-02 15:27:33.907741",
        "automatic_updates": "off",
        "requirements": [
            "linux"
        ],
        "description": "A simple and robust FastCGI Process Manager for PH",
        "created": "2015-09-12 18:37:50.024980",
        "deleted": null,
        "variables": [
            {
                "required": false,
                "type": "Text",
                "name": "PHP_USER",
                "value": "root",
                "visibility": "internal"
            },
            {
                "required": false,
                "type": "Text",
                "name": "PHP_GROUP",
                "value": "root",
                "visibility": "internal"
            },
            {
                "required": false,
                "type": "Text",
                "name": "LOGS_DIRECTORY",
                "value": "/var/log/php-fpm",
                "visibility": "internal"
            },
            {
                "required": false,
                "type": "File",
                "name": "PHP_INI",
                "value": "/services/blobs/download/565deff917fe944e084647bf/php.ini",
                "visibility": "internal"
            },
            {
                "required": false,
                "type": "File",
                "name": "PHP_FPM_CONF",
                "value": "/services/blobs/download/55f498d917fe94678daaf710/www.conf",
                "visibility": "internal"
            }
        ],
        "uri": "/services/boxes/ed085cfd-8707-4ef7-9611-6e84498d27c6",
        "visibility": "workspace",
        "name": "PHP-FPM",
        "icon_metadata": {
            "image": "images/platform/technologies/php.svg",
            "border": "#484F8C",
            "fill": "#6068A4"
        },
        "events": {
            "start": {
                "url": "/services/blobs/download/584190645939a07e69c92cdc/start",
                "length": 140,
                "destination_path": "scripts",
                "content_type": "text/x-shellscript"
            },
            "configure": {
                "url": "/services/blobs/download/565f491217fe944e08466e01/configure",
                "length": 535,
                "destination_path": "scripts",
                "content_type": "text/x-shellscript"
            },
            "install": {
                "url": "/services/blobs/download/565e173517fe944e084651ea/install",
                "length": 1408,
                "destination_path": "scripts",
                "content_type": "text/x-shellscript"
            }
        },
        "members": [
            {
                "role": "collaborator",
                "workspace": "rackspace1"
            }
        ],
        "organization": "elasticbox",
        "readme": {
            "url": "/services/blobs/download/56297bc9dda62a3b79416cbb/README.md",
            "upload_date": "2015-10-23 00:14:01.384408",
            "length": 2570,
            "content_type": "text/x-markdown"
        },
        "owner": "super",
        "id": "ed085cfd-8707-4ef7-9611-6e84498d27c6",
        "draft_from": "be643a40-e7e8-435a-a857-e06fe5854c3c",
        "icon": "/icons/boxes/ed085cfd-8707-4ef7-9611-6e84498d27c6"
    },
    {
        "schema": "http://elasticbox.net/schemas/boxes/script",
        "updated": "2015-12-22 23:12:59.290608",
        "automatic_updates": "off",
        "requirements": [
            "linux"
        ],
        "description": "HA Proxy for Redis cluster",
        "created": "2015-11-30 19:44:48.523649",
        "deleted": null,
        "variables": [
            {
                "automatic_updates": "major",
                "name": "haproxy",
                "required": false,
                "visibility": "private",
                "value": "87830b58-ceaf-4790-81d1-4511816b012f",
                "type": "Box"
            },
            {
                "name": "CONFIG_FILE",
                "required": false,
                "visibility": "public",
                "value": "/services/blobs/download/565cac16b1ac9f56ad578071/haproxy.conf",
                "scope": "haproxy",
                "type": "File"
            },
            {
                "name": "MODE",
                "required": false,
                "value": "tcp",
                "visibility": "public",
                "scope": "haproxy",
                "type": "Options",
                "options": "http,tcp,health"
            }
        ],
        "uri": "/services/boxes/053c6467-13e4-47fb-b6cf-46f51e6c2294",
        "visibility": "workspace",
        "name": "Redis HA Proxy",
        "icon_metadata": {
            "image": "images/platform/technologies/redis.svg",
            "border": "#18191C",
            "fill": "#2A2C30"
        },
        "events": {
            "install": {
                "url": "/services/blobs/download/565e380bdda62a46af5acef5/install",
                "length": 417,
                "destination_path": "scripts",
                "content_type": "text/x-shellscript"
            }
        },
        "members": [
            {
                "role": "collaborator",
                "workspace": "rackspace1"
            }
        ],
        "owner": "super",
        "organization": "elasticbox",
        "id": "053c6467-13e4-47fb-b6cf-46f51e6c2294",
        "icon": "/icons/boxes/053c6467-13e4-47fb-b6cf-46f51e6c2294"
    },
    {
        "schema": "http://elasticbox.net/schemas/boxes/script",
        "updated": "2016-09-08 16:30:40.026518",
        "automatic_updates": "off",
        "requirements": [
            "linux"
        ],
        "description": "Mounts an NFS endpoint",
        "created": "2015-09-13 20:28:14.119832",
        "deleted": null,
        "variables": [
            {
                "required": true,
                "type": "Text",
                "name": "LOCAL_PATH",
                "value": "",
                "visibility": "public"
            },
            {
                "required": false,
                "type": "Binding",
                "name": "server",
                "value": "894c39a1-169f-4cfb-a377-20fd41ab95d5",
                "visibility": "private"
            }
        ],
        "uri": "/services/boxes/320e8be7-5d05-4f74-a040-5d74836ae608",
        "visibility": "workspace",
        "name": "NFS Client",
        "owner": "super",
        "icon_metadata": {
            "image": "images/platform/abstract/disk.svg",
            "border": "#14427A",
            "fill": "#246099"
        },
        "events": {
            "configure": {
                "url": "/services/blobs/download/5667372db1ac9f56ad580ebc/configure",
                "length": 271,
                "destination_path": "scripts",
                "content_type": "text/x-shellscript"
            },
            "install": {
                "url": "/services/blobs/download/566736f6dda62a46af5b4272/install",
                "length": 213,
                "destination_path": "scripts",
                "content_type": "text/x-shellscript"
            }
        },
        "members": [
            {
                "role": "collaborator",
                "workspace": "rackspace1"
            }
        ],
        "readme": {
            "url": "/services/blobs/download/56297c02b1ac9f4d02d1c2ae/README.md",
            "upload_date": "2015-10-23 00:14:58.186697",
            "length": 1515,
            "content_type": "text/x-markdown"
        },
        "organization": "elasticbox",
        "id": "320e8be7-5d05-4f74-a040-5d74836ae608",
        "draft_from": "7a24d2c7-8e8b-45bb-8a9c-eaf6899d3e85",
        "icon": "/icons/boxes/320e8be7-5d05-4f74-a040-5d74836ae608"
    }
]
```

## GET /services/boxes/{box_id}/bindings

Gets a list of box objects that are bindings of the requested box. Requires the specified box id as a parameter box_id.

### URL

#### Structure
```
[GET] /services/boxes//{box_id}/bindings
```

#### Example
```
[GET] https://cam.ctl.io/services/boxes/f4dd017f-4bec-42f4-9614-bd27fd8baf74/bindings
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
| box_id | string | Box id | Yes |


### Response
#### Normal Response Codes

- **200** OK

#### Common Error Response Codes

- **400** Bad Request



#### Response Parameters

| Parameter | Style | Type | Description |
|-----------|-------|------|-------------|
| uri | plain | string | Box uri. |
| id | plain | array | Box unique identificator. |
| icon | plain | string | Box icon uri. |
| name | plain | string | Box name. |


### Response Body

```
[
    {
        "uri": "/services/boxes/894c39a1-169f-4cfb-a377-20fd41ab95d5",
        "name": "NFS Server",
        "icon": "/icons/boxes/894c39a1-169f-4cfb-a377-20fd41ab95d5",
        "id": "894c39a1-169f-4cfb-a377-20fd41ab95d5"
    }
]
```

## GET /services/boxes/{box_id}/versions

Gets a list of box versions for the requested box. Requires the specified box id as a parameter box_id. If the specified box is unversioned it obtains an empty list.

### URL

#### Structure
```
[GET] /services/boxes//{box_id}/versions
```

#### Example
```
[GET] https://cam.ctl.io/services/boxes/f4dd017f-4bec-42f4-9614-bd27fd8baf74/versions
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
| box_id | string | Box id | Yes |


### Response
#### Normal Response Codes

- **200** OK

#### Common Error Response Codes

- **403** Forbidden
- **404** Not Found

#### Response Parameters

| Parameter | Style | Type | Description |
|-----------|-------|------|-------------|
| updated | plain | string | Date of the last update. |
| description | plain | string | Box description. |
| tags | plain | array | Box tags. |
| variables | plain | array | List of box variables, each variable object contains the parameters: type, name, value, visibility, required, etc. |
| members | plain | array | List of Box members. |
| owner | plain | string | Box owner. |
| id | plain | array | Box unique identificator. |
| icon | plain | string | Box icon uri. |
| visibility | plain | string | Indicates at what level the box is visible. By default, boxes are visible to the workspace they’re created in. Can have one of these values: <li>public: Visible to Cloud Application Manager users across all organizations.</li> <li>organization: Visible to all users in the organization where the box was created.</li> <li>workspace: By default, the box is visible only to members of the workspace where it was created.</li> |
| organization | plain | string | Organization to which the box belongs. |
| name | plain | string | Box name. |
| created | plain | string | Creation date. |
| uri | plain | string | Box uri. |
| version | plain | object | The box version object contains the parameters box, description and workspace. |
| events | plain | array | List of Box events, there may be nine event lists: configure, dispose, install, pre_configure, pre_dispose, pre_install, pre_start, pre_stop, start and stop. |
| event | plain | object | Event contained in one of the event lists, each event object contains the  parameters: url, upload_date, length and destination_path. |
| schema | plain | string | Box schema uri. |


### Response Body

```
[
    {
        "schema": "http://elasticbox.net/schemas/boxes/script",
        "updated": "2016-11-22 13:39:23.680784",
        "automatic_updates": "off",
        "requirements": [
            "internal",
            "linux"
        ],
        "description": "Magento Web Layer",
        "created": "2016-05-10 22:03:20.342575",
        "deleted": null,
        "variables": [
            {
                "name": "LOCAL_PATH",
                "required": true,
                "value": "/mnt/media",
                "visibility": "internal",
                "scope": "nfs",
                "type": "Text"
            },
            {
                "name": "CONFIG_FILE",
                "required": false,
                "value": "/services/blobs/download/565f3c92974c525666cd2f84/haproxy.conf",
                "visibility": "public",
                "scope": "redis.haproxy",
                "type": "File"
            },
            {
                "name": "CONFIG_FILE_NAME",
                "required": false,
                "value": "redis.cfg",
                "visibility": "public",
                "scope": "redis.haproxy",
                "type": "Text"
            },
            {
                "required": false,
                "type": "Text",
                "name": "MAGENTO_URL",
                "value": "https://s3-us-west-1.amazonaws.com/ebx-public/magento-1.9.2.2.tar-2015-10-27-03-19-32.gz",
                "visibility": "internal"
            },
            {
                "required": false,
                "type": "Text",
                "name": "SERVER_NAME",
                "value": "localhost",
                "visibility": "public"
            },
            {
                "required": false,
                "type": "Port",
                "name": "http",
                "value": "80",
                "visibility": "public"
            },
            {
                "required": false,
                "type": "File",
                "name": "MAGENTO_CONF",
                "value": "/services/blobs/download/565ca77d17fe944e08463a45/magento.conf",
                "visibility": "internal"
            },
            {
                "required": false,
                "type": "File",
                "name": "MAGENTO_CONFIG",
                "value": "/services/blobs/download/565f3b1bb1ac9f56ad57b423/local.xml",
                "visibility": "internal"
            },
            {
                "required": false,
                "type": "Text",
                "name": "MAGENTO_PATH",
                "value": "/opt/magento",
                "visibility": "internal"
            },
            {
                "automatic_updates": "major",
                "name": "redis",
                "required": false,
                "value": "053c6467-13e4-47fb-b6cf-46f51e6c2294",
                "visibility": "public",
                "type": "Box"
            },
            {
                "automatic_updates": "major",
                "name": "mysql",
                "required": false,
                "value": "f6deab86-3744-4be3-bd48-804697859423",
                "visibility": "public",
                "type": "Box"
            },
            {
                "automatic_updates": "major",
                "name": "nginx",
                "required": false,
                "visibility": "internal",
                "value": "8e176772-5c6c-4d5a-8f6e-cbf342142520",
                "type": "Box"
            },
            {
                "automatic_updates": "major",
                "name": "php",
                "required": false,
                "value": "ed085cfd-8707-4ef7-9611-6e84498d27c6",
                "visibility": "internal",
                "type": "Box"
            },
            {
                "automatic_updates": "major",
                "name": "nfs",
                "required": false,
                "value": "320e8be7-5d05-4f74-a040-5d74836ae608",
                "visibility": "public",
                "type": "Box"
            }
        ],
        "readme": {
            "url": "/services/blobs/download/563a84b1dda62a1ca8ed5bdb/README.md",
            "upload_date": "2015-11-04 22:20:33.241618",
            "length": 2264,
            "content_type": "text/x-markdown"
        },
        "uri": "/services/boxes/de1841f7-cfbe-4443-a996-d13807271a18",
        "visibility": "workspace",
        "name": "Magento",
        "icon_metadata": {
            "image": "images/platform/technologies/magento.svg",
            "border": "#191815",
            "fill": "#31302B"
        },
        "version": {
            "box": "f4dd017f-4bec-42f4-9614-bd27fd8baf74",
            "number": {
                "major": 0,
                "minor": 1,
                "patch": 1
            },
            "workspace": "alberto",
            "description": "Updated boxes"
        },
        "events": {
            "configure": {
                "url": "/services/blobs/download/566604fcb1ac9f56ad5809bf/configure",
                "length": 702,
                "destination_path": "scripts",
                "content_type": "text/x-shellscript"
            },
            "install": {
                "url": "/services/blobs/download/565e1855dda62a46af5acc97/install",
                "length": 829,
                "destination_path": "scripts",
                "content_type": "text/x-shellscript"
            }
        },
        "members": [
            {
                "role": "collaborator",
                "workspace": "rackspace1"
            },
            {
                "role": "read",
                "workspace": "centurylink"
            }
        ],
        "owner": "super",
        "organization": "elasticbox",
        "id": "de1841f7-cfbe-4443-a996-d13807271a18",
        "icon": "/icons/boxes/f4dd017f-4bec-42f4-9614-bd27fd8baf74"
    },
    {
        "schema": "http://elasticbox.net/schemas/boxes/script",
        "updated": "2016-11-22 13:39:23.680784",
        "automatic_updates": "off",
        "requirements": [
            "internal",
            "linux"
        ],
        "description": "Magento Web Layer",
        "created": "2015-12-10 16:11:01.542052",
        "icon_metadata": {
            "image": "images/platform/technologies/magento.svg",
            "border": "#191815",
            "fill": "#31302B"
        },
        "variables": [
            {
                "name": "LOCAL_PATH",
                "required": true,
                "visibility": "internal",
                "value": "/mnt/media",
                "scope": "nfs",
                "type": "Text"
            },
            {
                "name": "CONFIG_FILE",
                "required": false,
                "visibility": "public",
                "value": "/services/blobs/download/565f3c92974c525666cd2f84/haproxy.conf",
                "scope": "redis.haproxy",
                "type": "File"
            },
            {
                "name": "CONFIG_FILE_NAME",
                "required": false,
                "visibility": "public",
                "value": "redis.cfg",
                "scope": "redis.haproxy",
                "type": "Text"
            },
            {
                "required": false,
                "type": "Text",
                "name": "SERVER_NAME",
                "value": "localhost",
                "visibility": "public"
            },
            {
                "required": false,
                "type": "Port",
                "name": "http",
                "value": "80",
                "visibility": "public"
            },
            {
                "required": false,
                "type": "Text",
                "name": "MAGENTO_URL",
                "value": "https://s3-us-west-1.amazonaws.com/ebx-public/magento-1.9.2.2.tar-2015-10-27-03-19-32.gz",
                "visibility": "internal"
            },
            {
                "required": false,
                "type": "File",
                "name": "MAGENTO_CONF",
                "value": "/services/blobs/download/565ca77d17fe944e08463a45/magento.conf",
                "visibility": "internal"
            },
            {
                "required": false,
                "type": "File",
                "name": "MAGENTO_CONFIG",
                "value": "/services/blobs/download/565f3b1bb1ac9f56ad57b423/local.xml",
                "visibility": "internal"
            },
            {
                "required": false,
                "type": "Text",
                "name": "MAGENTO_PATH",
                "value": "/opt/magento",
                "visibility": "internal"
            },
            {
                "automatic_updates": "major",
                "name": "mysql",
                "required": false,
                "visibility": "public",
                "value": "f6deab86-3744-4be3-bd48-804697859423",
                "type": "Box"
            },
            {
                "automatic_updates": "major",
                "name": "redis",
                "required": false,
                "visibility": "public",
                "value": "053c6467-13e4-47fb-b6cf-46f51e6c2294",
                "type": "Box"
            },
            {
                "automatic_updates": "major",
                "name": "nginx",
                "required": false,
                "value": "8e176772-5c6c-4d5a-8f6e-cbf342142520",
                "visibility": "internal",
                "type": "Box"
            },
            {
                "automatic_updates": "major",
                "name": "php",
                "required": false,
                "visibility": "internal",
                "value": "ed085cfd-8707-4ef7-9611-6e84498d27c6",
                "type": "Box"
            },
            {
                "automatic_updates": "major",
                "name": "nfs",
                "required": false,
                "visibility": "public",
                "value": "320e8be7-5d05-4f74-a040-5d74836ae608",
                "type": "Box"
            }
        ],
        "readme": {
            "url": "/services/blobs/download/563a84b1dda62a1ca8ed5bdb/README.md",
            "upload_date": "2015-11-04 22:20:33.241618",
            "length": 2264,
            "content_type": "text/x-markdown"
        },
        "uri": "/services/boxes/e75f27f6-fded-4647-8630-bd99cf62fcee",
        "visibility": "workspace",
        "name": "Magento",
        "deleted": null,
        "version": {
            "box": "f4dd017f-4bec-42f4-9614-bd27fd8baf74",
            "number": {
                "major": 0,
                "minor": 1,
                "patch": 0
            },
            "workspace": "diego",
            "description": "automatic"
        },
        "events": {
            "configure": {
                "url": "/services/blobs/download/566604fcb1ac9f56ad5809bf/configure",
                "length": 702,
                "destination_path": "scripts",
                "content_type": "text/x-shellscript"
            },
            "install": {
                "url": "/services/blobs/download/565e1855dda62a46af5acc97/install",
                "length": 829,
                "destination_path": "scripts",
                "content_type": "text/x-shellscript"
            }
        },
        "members": [
            {
                "role": "collaborator",
                "workspace": "rackspace1"
            },
            {
                "role": "read",
                "workspace": "centurylink"
            }
        ],
        "owner": "super",
        "organization": "elasticbox",
        "id": "e75f27f6-fded-4647-8630-bd99cf62fcee",
        "icon": "/services/blobs/download/55f46e1c974c52710858afb6/magento.png"
    }
]
```

## PUT /services/boxes/{box_id}/diff

Compares a box to the submitted box. Requires the specified box id as parameter box_id.

### URL

#### Structure
```
[PUT] /services/boxes//{box_id}/diff
```

#### Example
```
[PUT] https://cam.ctl.io/services/boxes/f4dd017f-4bec-42f4-9614-bd27fd8baf74/diff
```

### Request

#### Headers
```
Content-Type: application/json
Authorization: Bearer your_json_web_token
ElasticBox-Release: 4.0
```


#### URI Parameters

| Parameter | Style | Type | Description | Req. |
|-----------|-------|------|-------------| ---- |
| box_id | plain | string | Box id | Yes | 


#### Request Body Parameters

| Parameter | Style | Type | Description | Req. |
|-----------|-------|------|-------------|----| 
| updated | plain | string | Date of the last update. |
| description | plain | string | Box description. |
| tags | plain | array | Box tags. |
| variables | plain | array | List of box variables, each variable object contains the parameters: type, name, value, visibility, required, etc. |
| members | plain | array | List of Box members. |
| owner | plain | string | Box owner. | Yes |
| id | plain | array | Box unique identificator. | Yes |
| icon | plain | string | Box icon uri. |
| visibility | plain | string | Indicates at what level the box is visible. By default, boxes are visible to the workspace they’re created in. Can have one of these values: <li>public: Visible to Cloud Application Manager users across all organizations.</li> <li>organization: Visible to all users in the organization where the box was created.</li> <li>workspace: By default, the box is visible only to members of the workspace where it was created.</li> |
| organization | plain | string | Organization to which the box belongs. | Yes |
| name | plain | string | Box name. | Yes |
| created | plain | string | Creation date. |
| uri | plain | string | Box uri. |
| version | plain | object | The box version object contains the parameters box, description and workspace. |
| events | plain | array | List of Box events, there may be nine event lists: configure, dispose, install, pre_configure, pre_dispose, pre_install, pre_start, pre_stop, start and stop. |
| event | plain | object | Event contained in one of the event lists, each event object contains the  parameters: url, upload_date, length and destination_path. |
| schema | plain | string | Box schema uri. | Yes |


#### Request Body
```
{
  "updated": "2018-07-02 13:36:30.348041",
  "automatic_updates": "off",
  "requirements": [
    "linux",
    "new_requirement"
  ],
  "description": "Test Started for our showcase",
  "name": "Test Starter Box",
  "created": "2018-12-31 11:20:27.349315",
  "deleted": null,
  "variables": [
    {
      "required": false,
      "type": "Text",
      "name": "variable_name",
      "value": "New value",
      "visibility": "public"
    }
  ],
  "uri": "/services/boxes/60cef61c-73dc-41d9-a32f-70f49a509c66",
  "visibility": "workspace",
  "id": "60cef61c-73dc-41d9-a32f-70f49a509c66",
  "members": [],
  "owner": "operation",
  "organization": "elasticbox",
  "events": {},
  "draft_from": "ca197de8-25e1-4e9b-9d45-c99a049249fc",
  "schema": "http://elasticbox.net/schemas/boxes/script"
}
```

### Response
#### Normal Response Codes

- **200** OK

#### Common Error Response Codes

- **403** Forbidden
- **404** Not Found


#### Response Parameters


| Parameter | Style | Type | Description |
|-----------|-------|------|-------------|
| box_variables | plain | object | Differences in the box variables, the object contains a title and three lists: removed, added and changed. |
| box_variables.removed | plain | array | List of box variables removed, each variable object contains the parameters: type, name, value, visibility, required, etc. |
| box_variables.added | plain | array | List of box variables added, each variable object contains the parameters: type, name, value, visibility, required, etc.  |
| box_variables.changed | plain | array | List of box variables changed, each variable object contains the parameters: type, name, value, visibility, required, etc. |
| box_details | plain | object | Differences in the box details, the object contains a title and three lists: removed, added and changed. |
| box_profile_properties | plain | object | Differences in the box profile properties, the object contains a title and three lists: removed, added and changed. Available for Policy boxes. |
| box_events | plain | array | List of box events. |
| changed | plain | boolean | There have been changes between versions. |


```
{
    "changed": true,
    "box_services": {
        "removed": [],
        "added": []
    },
    "box_events": [],
    "box_variables": {
        "title": "Modified Variables",
        "removed": [],
        "changed": [
            [
                {
                    "required": false,
                    "type": "Text",
                    "name": "variable_name",
                    "value": "New value",
                    "visibility": "public"
                },
                {
                    "required": false,
                    "type": "Text",
                    "name": "variable_name",
                    "value": "",
                    "visibility": "public"
                }
            ]
        ],
        "added": [],
        "files_diff": []
    },
    "box_readme": [],
    "box_details": {
        "title": "Modified Box Details",
        "removed": [],
        "added": [],
        "changed": [
            {
                "new": "linux, new_requirement",
                "name": "Requirements",
                "previous": "apache, linux"
            }
        ]
    },
    "box_profile_properties": {
        "removed": [],
        "changed": [],
        "added": [],
        "files_diff": []
    },
    "box_services_variables": {
        "removed": [],
        "added": [],
        "files_diff": []
    }
}
```

## Create and Launch a CloudFormation Box

### Create a CloudFormation box with template

1. [POST /services/boxes](./api-boxes.md)
Creates a box of the CloudFormation service type. See example create a CloudFormation.

2. [GET /services/blobs/download/{file_id}/{file_name}](./api-blobs.md)
Fetches contents from a given file or URL. See example create a CloudFormation, part 2.
Submits a blank JSON template as a blob.

3. [POST /services/blobs/upload/{file_name}](./api-blobs.md)
Creates a blob from template data submitted through a file or URL. Here template data is in the request body. See example create a CloudFormation, part 3.

4. [PUT /services/boxes/{box_id}](./api-boxes.md)
Updates the CloudFormation box with the template. See example create a CloudFormation, part 4.

###  Modify the CloudFormation Template

1. [POST /services/blobs/upload/{file_name}](./api-blobs.md)
Creates a blob from modified template data. See example modify a CloudFormation.

2. [PUT /services/boxes/{box_id}](./api-boxes.md)
Updates the CloudFormation box. See example modify a CloudFormation, part 2.

###  Delete a CloudFormation Box

1. [DELETE /services/box/{box_id}](./api-blobs.md)
Removes the CloudFormation box from the boxes catalog.

### Launch a CloudFormation Box

1. [POST /services/profiles](./api-blobs.md)
This step is optional. Passes deployment settings in a new deployment profile to launch the box in the provider’s infrastructure. See example launch a CloudFormation.

2. [POST /services/instances](./instances-api.md)
Creates a new instance of the CloudFormation box.

### Update a CloudFormation Stack in Real-Time

1. [POST /services/blobs/upload](./api-blobs.md)
Uploads the modified template data. See example update a CloudFormation.

2. [PUT /services/instances/{instance_id}](./instances-api.md)
Updates the instance with the template changes. See example update a CloudFormation part 2.

3. [PUT /services/instances/{instance_id}/reconfigure](./instances-api.md)
Reconfigures the stack based on the changes. See example update a CloudFormation part 3.

## Example: Create a CloudFormation box with template

**1. POST https://cam.ctl.io/services/boxes/**

Creating a box of the CloudFormation service type.

### Request
#### Headers
```
Content-Type: application/json
Authorization: Bearer your_json_web_token
ElasticBox-Release: 4.0
```

#### Request Body
```
{
    "owner": "operations",
    "schema":"http://elasticbox.net/schemas/boxes/cloudformation",
    "automatic_updates":"off",
    "name":"Wordpress Starter CF",
    "description":"Wordpress Started for our showcase"
}
```
### Response
#### Response Body

```
{
    "updated": "2019-01-02 10:57:43.782726",
    "automatic_updates": "off",
    "description": "Wordpress Started for our showcase",
    "deleted": null,
    "variables": [],
    "visibility": "workspace",
    "members": [],
    "owner": "operations",
    "id": "755a09cc-6407-44e2-9993-539c386ee559",
    "requirements": [],
    "name": "Wordpress Starter CF",
    "created": "2019-01-02 10:57:43.782726",
    "uri": "/services/boxes/755a09cc-6407-44e2-9993-539c386ee559",
    "organization": "centurylink",
    "type": "CloudFormation Service",
    "schema": "http://elasticbox.net/schemas/boxes/cloudformation"
}

```

**2. GET https://cam.ctl.io/services/blobs/download/{blob_id}/file_name**

Fetches contents from a given URL. Once we have checked that the template is the right one, we could assign it to the CloudFormation box.

### Request
#### Headers
```
Content-Type: application/json
Authorization: Bearer your_json_web_token
ElasticBox-Release: 4.0
```

### Response
#### Response Body
```
{
   "AWSTemplateFormatVersion":"2010-09-09",
   "Description":"AWS CloudFormation Sample Template WordPress_Single_Instance_With_RDS: WordPress is web software you can use to create a beautiful website or blog. This template installs a single-instance WordPress deployment using an Amazon RDS database instance for storage. It demonstrates using the AWS CloudFormation bootstrap scripts to install packages and files at instance launch time. **WARNING** This template creates an Amazon EC2 instance and an Amazon RDS database instance. You will be billed for the AWS resources used if you create a stack from this template.",
   "Parameters":{
      "KeyName":{
         "Description":"Name of an existing EC2 KeyPair to enable SSH access to the instances",
         "Type":"String",
         "MinLength":"1",
         "MaxLength":"255",
         "AllowedPattern":"[\\x20-\\x7E]*",
         "ConstraintDescription":"can contain only ASCII characters."
      },
    ...
   }
...
...

   "Outputs":{
      "WebsiteURL":{
         "Value":{
            "Fn::Join":[
               "",
               [
                  "http://",
                  {
                     "Fn::GetAtt":[
                        "WebServer",
                        "PublicDnsName"
                     ]
                  },
                  "/wordpress"
               ]
            ]
         },
         "Description":"WordPress Website"
      }
   }
}
```

**3. POST https://cam.ctl.io/services/blobs/upload/template.json**

Another option is to create the template from the data submitted through a URL.

### Request
#### Headers
```
Content-Type: application/json
Authorization: Bearer your_json_web_token
ElasticBox-Release: 4.0
```

#### Request Body
```
{
   "AWSTemplateFormatVersion":"2010-09-09",
   "Description":"AWS CloudFormation Sample Template WordPress_Single_Instance_With_RDS: WordPress is web software you can use to create a beautiful website or blog. This template installs a single-instance WordPress deployment using an Amazon RDS database instance for storage. It demonstrates using the AWS CloudFormation bootstrap scripts to install packages and files at instance launch time. **WARNING** This template creates an Amazon EC2 instance and an Amazon RDS database instance. You will be billed for the AWS resources used if you create a stack from this template.",
   "Parameters":{
      "KeyName":{
         "Description":"Name of an existing EC2 KeyPair to enable SSH access to the instances",
         "Type":"String",
         "MinLength":"1",
         "MaxLength":"255",
         "AllowedPattern":"[\\x20-\\x7E]*",
         "ConstraintDescription":"can contain only ASCII characters."
      },
    ...
   },
...
...
   "Outputs":{
      "WebsiteURL":{
         "Value":{
            "Fn::Join":[
               "",
               [
                  "http://",
                  {
                     "Fn::GetAtt":[
                        "WebServer",
                        "PublicDnsName"
                     ]
                  },
                  "/wordpress"
               ]
            ]
         },
         "Description":"WordPress Website"
      }
   }
}

```

### Response
#### Response Body
```
{
   "url":"/services/blobs/download/536a9e867d0083771808bacd/template.json",
   "upload_date":"2014-05-07 20:58:46.650140",
   "length":9739,
   "content_type":"text/x-shellscript"
}
```

**4. PUT https://cam.ctl.io/services/boxes/{box_id}**

Finally we are going to update the CloudFormation box with one of the templates we have obtained in the last two steps.

### Request
#### Headers
```
Content-Type: application/json
Authorization: Bearer your_json_web_token
ElasticBox-Release: 4.0
```
#### Request Body
```
{
    "schema": "http://elasticbox.net/schemas/boxes/cloudformation",
    "automatic_updates": "off",
    "requirements": [],
    "description": "Wordpress Started for our showcase",
    "deleted": null,
    "variables": [],
    "uri": "/services/boxes/262d4cbe-9ad9-4069-b6a8-76fda70a4d90",
    "visibility": "workspace",
    "members": [],
    "owner": "operations",
    "organization": "elasticbox",
    "type": "CloudFormation Service",
    "id": "262d4cbe-9ad9-4069-b6a8-76fda70a4d90",
    "name": "Wordpress Starter CF",
    "template": {
        "url": "/services/blobs/download/536a9e867d0083771808bacd/template.json"
    }
}
```

### Response
#### Response Body
```
{
    "schema": "http://elasticbox.net/schemas/boxes/cloudformation",
    "updated": "2015-10-28 12:03:32.661399",
    "automatic_updates": "off",
    "requirements": [],
    "description": "Wordpress Started for our showcase",
    "created": "2015-10-28 11:24:01.854958",
    "deleted": null,
    "variables": [
        {
            "value": "",
            "type": "Text",
            "name": "KeyName",
            "visibility": "public"
        },
        {
            "value": "",
            "type": "Text",
            "name": "SourceCidrForRDP",
            "visibility": "public"
        },
        {
            "value": "m1.large",
            "type": "Text",
            "name": "InstanceType",
            "visibility": "public"
        }
    ],
    "uri": "/services/boxes/262d4cbe-9ad9-4069-b6a8-76fda70a4d90",
    "visibility": "workspace",
    "template": {
        "url": "/services/blobs/download/536a9e867d0083771808bacd/template.json"
    },
    "members": [],
    "owner": "operations",
    "organization": "elasticbox",
    "type": "CloudFormation Service",
    "id": "262d4cbe-9ad9-4069-b6a8-76fda70a4d90",
    "name": "Wordpress Starter CF"
}
```

### Example: Modify the CloudFormation Template

**1. POST http://cam.ctl.io/services/blobs/upload/template.json**

Creates a blob from modified template data.

### Request
#### Headers
```
Content-Type: application/json
Authorization: Bearer your_json_web_token
ElasticBox-Release: 4.0
```

#### Request Body
```
{
    "AWSTemplateFormatVersion": "2010-09-09",
    "Description": "AWS CloudFormation Sample Template WordPress_Single_Instance_With_RDS: WordPress is web software you can use to create a beautiful website or blog. This template installs a single-instance WordPress deployment using an Amazon RDS database instance for storage. It demonstrates using the AWS CloudFormation bootstrap scripts to install packages and files at instance launch time. **WARNING** This template creates an Amazon EC2 instance and an Amazon RDS database instance. You will be billed for the AWS resources used if you create a stack from this template.",
    "Parameters": {
        "KeyName": {
            "Description": "Name of an existing EC2 KeyPair to enable SSH access to the instances",
            "Type": "String",
            "MinLength": "1",
            "MaxLength": "255",
            "AllowedPattern": "[\\x20-\\x7E]*",
            "ConstraintDescription": "can contain only ASCII characters."
        },
       ...
    },
…
…
    "Outputs": {
        "WebsiteURL": {
            "Value": {
                "Fn::Join": [
                    "",
                    [
                        "http://",
                        {
                            "Fn::GetAtt": [
                                "WebServer",
                                "PublicDnsName"
                            ]
                        },
                        "/wordpress"
                    ]
                ]
            },
            "Description": "WordPress Website"
        }
    }
}
```

### Response
#### Response Body
```
{
   "url":"/services/blobs/download/536bd5619ac37b2f70318a87/template.json",
   "upload_date":"2014-05-08 19:05:05.761144",
   "length":15922,
   "content_type":"text/x-shellscript"
}
```

**2. PUT http://cam.ctl.io/services/boxes/{box_id}**

Updates the CloudFormation box.

### Request
#### Headers
```
Content-Type: application/json
Authorization: Bearer your_json_web_token
ElasticBox-Release: 4.0
```

#### Request Body
```
{
    "schema": "http://elasticbox.net/schemas/boxes/cloudformation",
    "automatic_updates": "off",
    "requirements": [],
    "description": "Wordpress Started for our showcase",
    "deleted": null,
    "variables": [],
    "uri": "/services/boxes/262d4cbe-9ad9-4069-b6a8-76fda70a4d90",
    "visibility": "workspace",
    "members": [],
    "owner": "operations",
    "organization": "elasticbox",
    "type": "CloudFormation Service",
    "id": "262d4cbe-9ad9-4069-b6a8-76fda70a4d90",
    "name": "Wordpress Starter CF",
    "template": {
        "url": "//services/blobs/download/536bd5619ac37b2f70318a87/template.json"
    }
}
```

### Response
#### Response Body
```
{
    "schema": "http://elasticbox.net/schemas/boxes/cloudformation",
    "updated": "2015-10-28 12:03:32.661399",
    "automatic_updates": "off",
    "requirements": [],
    "description": "Wordpress Started for our showcase",
    "created": "2015-10-28 11:24:01.854958",
    "deleted": null,
    "variables": [
        {
            "value": "",
            "type": "Text",
            "name": "KeyName",
            "visibility": "public"
        },
        {
            "value": "",
            "type": "Text",
            "name": "SourceCidrForRDP",
            "visibility": "public"
        },
        {
            "value": "m1.large",
            "type": "Text",
            "name": "InstanceType",
            "visibility": "public"
        }
    ],
    "uri": "/services/boxes/262d4cbe-9ad9-4069-b6a8-76fda70a4d90",
    "visibility": "workspace",
    "template": {
        "url": "/services/blobs/download/536bd5619ac37b2f70318a87/template.json"
    },
    "members": [],
    "owner": "operations",
    "organization": "elasticbox",
    "type": "CloudFormation Service",
    "id": "262d4cbe-9ad9-4069-b6a8-76fda70a4d90",
    "name": "Wordpress Starter CF"
}
```

### Example: Launch a CloudFormation Box

**1. POST https://cam.ctl.io/services/instances**

Creates a new instance of the CloudFormation box.

### Request
#### Headers

```
Content-Type: application/json
Authorization: Bearer your_json_web_token
ElasticBox-Release: 4.0
```

#### Request Body
```
{
  "schema": "http://elasticbox.net/schemas/deploy-instance-request",
  "owner": "operations",
  "name": "CF WordPress 2",
  "box": {
    "id": "91645eed-173f-4aac-a713-69c6be7582fe",
    "variables": [

    ]
  },
  "instance_tags": [

  ],
  "automatic_updates": "off",
  "policy_box": {
    "id": "91645eed-173f-4aac-a713-69c6be7582fe",
    "variables": [
      {
        "name": "provider_id",
        "value": "7e841966-1dec-4460-a981-1db4e1eec10c",
        "type": "Text"
      },
      {
        "name": "location",
        "value": "ap-northeast-1",
        "type": "Text"
      }
    ]
  }
}
```

### Response
#### Response Body
```
{
  "box": "91645eed-173f-4aac-a713-69c6be7582fe",
  "policy_box": {
    "profile": {
      "location": "ap-northeast-1",
      "schema": "http://elasticbox.net/schemas/aws/cloudformation/profile"
    },
    "schema": "http://elasticbox.net/schemas/boxes/cloudformation",
    "updated": "2015-10-28 13:46:55.247211",
    "automatic_updates": "off",
    "requirements": [

    ],
    "description": "CF test",
    "created": "2015-10-27 12:11:24.734064",
    "deleted": null,
    "variables": [
      {
        "required": false,
        "type": "Binding",
        "name": "Binding",
        "value": "5030fc49-773a-42fa-b569-c551e4f90d77",
        "visibility": "private"
      }
    ],
    "provider_id": "7e841966-1dec-4460-a981-1db4e1eec10c",
    "visibility": "workspace",
    "members": [

    ],
    "template": {
      "url": "/services/blobs/download/5630d1cf14841250525226a6/template.json",
      "upload_date": "2015-10-28 13:46:55.186875",
      "length": 104,
      "content_type": "text/x-shellscript"
    },
    "owner": "operations",
    "organization": "elasticbox",
    "type": "CloudFormation Service",
    "id": "91645eed-173f-4aac-a713-69c6be7582fe",
    "name": "CF WordPress 2"
  },
  "updated": "2015-10-28 13:47:15.567441",
  "automatic_updates": "off",
  "name": "CF WordPress 2",
  "service": {
    "type": "CloudFormation Service",
    "id": "eb-5cn45",
    "machines": [

    ]
  },
  "tags": [

  ],
  "deleted": null,
  "variables": [

  ],
  "created": "2015-10-28 13:47:15.567441",
  "state": "processing",
  "uri": "/services/instances/i-ywf1hu",
  "boxes": [
    {
      "schema": "http://elasticbox.net/schemas/boxes/cloudformation",
      "updated": "2015-10-28 13:46:55.247211",
      "automatic_updates": "off",
      "requirements": [

      ],
      "description": "CF test",
      "created": "2015-10-27 12:11:24.734064",
      "deleted": null,
      "variables": [
        {
          "required": false,
          "type": "Binding",
          "name": "Binding",
          "value": "5030fc49-773a-42fa-b569-c551e4f90d77",
          "visibility": "private"
        }
      ],
      "visibility": "workspace",
      "members": [

      ],
      "template": {
        "url": "/services/blobs/download/5630d1cf14841250525226a6/template.json",
        "upload_date": "2015-10-28 13:46:55.186875",
        "length": 104,
        "content_type": "text/x-shellscript"
      },
      "owner": "operations",
      "organization": "elasticbox",
      "type": "CloudFormation Service",
      "id": "91645eed-173f-4aac-a713-69c6be7582fe",
      "name": "CF WordPress 2"
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
    "created": "2015-10-28 13:47:15.564698"
  },
  "schema": "http://elasticbox.net/schemas/instance",
  "id": "i-ywf1hu",
  "icon": null
}
```

### Example: Update a CloudFormation Stack in Real-Time

**1. POST http://cam.ctl.io/services/blobs/upload/simple_template.json**

Uploads the modified template data.

### Request
#### Headers

```
Content-Type: application/json
Authorization: Bearer your_json_web_token
ElasticBox-Release: 4.0
```

#### Request Body

```
{
    "Resources" : {
        "HelloBucket" : {
            "Type" : "AWS::S3::Bucket"
        }
    }
}

```

### Response
#### Response Body
```
{
    "url": "/services/blobs/download/5630d61d14841250525226aa/simple_template.json",
    "upload_date": "2015-10-28 14:05:17.752627",
    "length": 0,
    "content_type": "application/json"
}
```

**2. PUT http://cam.ctl.io/services/instances/{instance_id}**

Updates the instance with the template changes.

### Request
#### Headers

```
Content-Type: application/json
Authorization: Bearer your_json_web_token
ElasticBox-Release: 4.0
```

#### Request Body

```
{
  "box": "91645eed-173f-4aac-a713-69c6be7582fe",
  "bindings": [

  ],
  "updated": "2015-10-28 13:48:24.367626",
  "automatic_updates": "off",
  "name": "CF WordPress 2",
  "service": {
    "type": "CloudFormation Service",
    "id": "eb-5cn45",
    "machines": [

    ]
  },
  "tags": [

  ],
  "deleted": null,
  "policy_box": {
    "profile": {
      "location": "ap-northeast-1",
      "schema": "http://elasticbox.net/schemas/aws/cloudformation/profile"
    },
    "updated": "2015-10-28 13:46:55.247211",
    "automatic_updates": "off",
    "requirements": [

    ],
    "description": "CF test",
    "created": "2015-10-27 12:11:24.734064",
    "deleted": null,
    "variables": [
      {
        "required": false,
        "type": "Binding",
        "name": "Binding",
        "value": "5030fc49-773a-42fa-b569-c551e4f90d77",
        "visibility": "private"
      }
    ],
    "provider_id": "7e841966-1dec-4460-a981-1db4e1eec10c",
    "visibility": "workspace",
    "template": {
      "url": "/services/blobs/download/5630d1cf14841250525226a6/template.json",
      "upload_date": "2015-10-28 13:46:55.186875",
      "length": 104,
      "content_type": "text/x-shellscript"
    },
    "members": [

    ],
    "owner": "operations",
    "organization": "elasticbox",
    "schema": "http://elasticbox.net/schemas/boxes/cloudformation",
    "type": "CloudFormation Service",
    "id": "91645eed-173f-4aac-a713-69c6be7582fe",
    "name": "CF WordPress 2"
  },
  "created": "2015-10-28 13:47:15.567441",
  "uri": "/services/instances/i-ywf1hu",
  "state": "done",
  "boxes": [
    {
      "updated": "2015-10-28 13:46:55.247211",
      "automatic_updates": "off",
      "requirements": [

      ],
      "description": "CF test",
      "created": "2015-10-27 12:11:24.734064",
      "deleted": null,
      "variables": [
        {
          "required": false,
          "type": "Binding",
          "name": "Binding",
          "value": "5030fc49-773a-42fa-b569-c551e4f90d77",
          "visibility": "private"
        }
      ],
      "visibility": "workspace",
      "template": {
        "url": "/services/blobs/download/5630d61d14841250525226aa/simple_template.json",
        "upload_date": "2015-10-28 13:46:55.186875",
        "length": 104,
        "content_type": "text/x-shellscript"
      },
      "members": [

      ],
      "owner": "operations",
      "organization": "elasticbox",
      "schema": "http://elasticbox.net/schemas/boxes/cloudformation",
      "type": "CloudFormation Service",
      "id": "91645eed-173f-4aac-a713-69c6be7582fe",
      "name": "CF WordPress 2"
    }
  ],
  "schema": "http://elasticbox.net/schemas/instance",
  "members": [

  ],
  "owner": "operations",
  "variables": [

  ],
  "operation": {
    "event": "deploy",
    "workspace": "operations",
    "created": "2015-10-28 13:47:15.746398"
  },
  "id": "i-ywf1hu",
  "icon": null
}
```

### Response
#### Response Body

```
{
  "box": "91645eed-173f-4aac-a713-69c6be7582fe",
  "bindings": [

  ],
  "updated": "2015-10-28 14:44:49.999798",
  "automatic_updates": "off",
  "name": "CF WordPress 2",
  "service": {
    "type": "CloudFormation Service",
    "id": "eb-5cn45",
    "machines": [

    ]
  },
  "tags": [

  ],
  "deleted": null,
  "policy_box": {
    "profile": {
      "location": "ap-northeast-1",
      "schema": "http://elasticbox.net/schemas/aws/cloudformation/profile"
    },
    "updated": "2015-10-28 13:46:55.247211",
    "automatic_updates": "off",
    "requirements": [

    ],
    "description": "CF test",
    "created": "2015-10-27 12:11:24.734064",
    "deleted": null,
    "variables": [
      {
        "required": false,
        "type": "Binding",
        "name": "Binding",
        "value": "5030fc49-773a-42fa-b569-c551e4f90d77",
        "visibility": "private"
      }
    ],
    "provider_id": "7e841966-1dec-4460-a981-1db4e1eec10c",
    "visibility": "workspace",
    "template": {
      "url": "/services/blobs/download/5630d1cf14841250525226a6/template.json",
      "upload_date": "2015-10-28 13:46:55.186875",
      "length": 104,
      "content_type": "text/x-shellscript"
    },
    "members": [

    ],
    "owner": "operations",
    "organization": "elasticbox",
    "schema": "http://elasticbox.net/schemas/boxes/cloudformation",
    "type": "CloudFormation Service",
    "id": "91645eed-173f-4aac-a713-69c6be7582fe",
    "name": "CF WordPress 2"
  },
  "created": "2015-10-28 13:47:15.567441",
  "uri": "/services/instances/i-ywf1hu",
  "state": "done",
  "boxes": [
    {
      "updated": "2015-10-28 13:46:55.247211",
      "automatic_updates": "off",
      "description": "CF test",
      "deleted": null,
      "variables": [
        {
          "required": false,
          "type": "Binding",
          "name": "Binding",
          "value": "5030fc49-773a-42fa-b569-c551e4f90d77",
          "visibility": "private"
        }
      ],
      "visibility": "workspace",
      "members": [

      ],
      "owner": "operations",
      "id": "91645eed-173f-4aac-a713-69c6be7582fe",
      "requirements": [

      ],
      "name": "CF WordPress 2",
      "created": "2015-10-27 12:11:24.734064",
      "template": {
        "url": "/services/blobs/download/5630d61d14841250525226aa/simple_template.json",
        "upload_date": "2015-10-28 13:46:55.186875",
        "length": 104,
        "content_type": "text/x-shellscript"
      },
      "organization": "elasticbox",
      "type": "CloudFormation Service",
      "schema": "http://elasticbox.net/schemas/boxes/cloudformation"
    }
  ],
  "schema": "http://elasticbox.net/schemas/instance",
  "members": [

  ],
  "owner": "operations",
  "variables": [

  ],
  "operation": {
    "event": "deploy",
    "workspace": "operations",
    "created": "2015-10-28 13:47:15.746398"
  },
  "id": "i-ywf1hu",
  "icon": null
}
```

**3. PUT http://cam.ctl.io/services/instances/{instance_id}/reconfigure**

Reconfigures the stack based on the changes.

### Request
#### Headers

```
Content-Type: application/json
Authorization: Bearer your_json_web_token
ElasticBox-Release: 4.0
```

#### Request Body

```

{
   "id":"i-ywf1hu",
   "method":"reconfigure"
}
```

### Response
None.


