{{{
"title": "Organizations API",
"date": "09-01-2016",
"author": "",
"attachments": [],
"contentIsHTML": false,
"keywords": ["api", "organization api", "manage api", "manage organization"]
}}}

### Manage an Organization

| Resource | Description |
|----------|-------------|
| GET /services/organizations/{organization_name} | Get the schema of the given organization. |
| GET /services/organizations/{organization_name}/boxes | Get the boxes of the given organization. |
| GET /services/organizations/{organization_name}/instances | Get the instances of the given organization. |
| GET /services/organizations/{organization_name}/providers | Get the providers of the given organization. |
| GET /services/organizations/{organization_name}/workspaces | Get the workspaces of the given organization. |
| PUT /services/organizations/{organization_name} | Updates an existing organization. |
| PUT /organizations/{organization_name}/sync_groups | Queues a request to sync LDAP groups. |

### GET /services/organizations/{organization_name}

Gets the schema of a given organization.

### URL
#### Structure

    [GET] /services/organizations/{organization_name}

#### Example

    GET https://cam.ctl.io/services/organizations/centurylink

### Request
#### Headers
```
Content-Type: application/json
Authorization: Bearer your_json_web_token
ElasticBox-Release: 4.0
```

#### URI Parameters
| Parameter | Type | Description | Req. |
| --- | --- | --- | --- |
| Organization name | string | the name of the organization | Yes |

### Response
#### Normal Response Codes
- **200** Accepted

#### Common Error Response Codes
- 401: Unauthorized - Invalid access token/cookie
- 403: Forbidden - User doesn’t belong to the organization
- Not Found (404)

#### Response Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| schema |  string| Organization schema URI: **//elasticbox.net/schemas/organization** |
| name |    string   |  Organization name |
| icon | string |   Organization icon URI |
| updated | string | Date of the last update |
| created | string | Creation date |
| setup | boolean | This is read-only. It indicates that the Cloud Application Manager appliance is set up and ready for use. |
| administrators | array | List of users who can administer the organization |
| domains | string | Domains that are a part of the organization |
| authentication | object | List of the authentication methods to allow single sign-on in the organization. Contains the following properties:<li>github: Boolean. If enabled, it is true, else false.</li><li>google: Boolean. If enabled, it is true, else false.</li><li>password: Boolean. If enabled, it is true, else false.</li><li>ldap: Boolean. If enabled, it is true, else false.</li><li>ldap_config: Object that contains the LDAP service settings:</li><ul><li>ldap_group_sync: Boolean. By default it’s false. Specify as true to enable synchronizing with LDAP groups.</li><li>sources: Array of [LDAP sources](https://www.ctl.io/knowledge-base/cloud-application-manager/administering-your-organization/user-authentication/). Each source has the following properties:</li><ul><li>host: Required. String identifies the hostname or IP address of the LDAP service.</li><li>groups_dn: String specifies a fully qualified group name.</li><li>group_dn_filter: String defines an entity on the LDAP server. All groups are synchronised as children of this entity.</li><li>email_field: String specifies the email field name by which to look up users. Typically, this field is called email.</li><li>ldap_search_password: String specifies the password for the LDAP service account to look up users who try to log in</li><li>ldap_search_user: String specifies the username of the LDAP service account to look up users who try to log in.</li></ul></ul> |
| ldap_last_sync_completed | string | Timestamp of the last successful LDAP group sync, for example, 2015-04-06 14:28:12.874910. Value is null if ldap_group_sync is set to false. |
| ldap_groups | array | List of objects, each of which is an LDAP group. Each group has two properties:<li>dn: String identifier for the group.</li><li>name: String name shown in the workspace web interface.</li> |
| providers | array | List of cloud providers the organization can enable to register and deploy. Each provider type has the following properties enabled:<li>Boolean value of true if enabled, else false.</li><li>type: String values of the supported cloud providers: Amazon Web Services, Openstack, VMWare vSphere, Google Compute, Microsoft Azure, Cloudstack, SoftLayer, VMware vCloud Director, Amazon Web Services GovCloud, Rackspace.</li><li>description: String that briefly enumerates the services from the cloud provider.</li><li>pricing: Array of pricing information for Linux and Windows compute instance types. Only available for Amazon Web Services.</li> |
| tags | array | List of [tags](https://www.ctl.io/knowledge-base/cloud-application-manager/administering-your-organization/resource-tags/) applied on instances deployed to cloud providers from the organization. Each tag has three properties:<li>name: String you apply as a tag.</li><li>type: String identifies the type of tag whether an Cloud Application Manager object or a custom one. Allowed values are Box, Workspace, Provider, Environment, Email, User ID, Service Instance ID, Service ID, Workspace ID, Instance ID, Custom.</li><li>value: String value of null for Cloud Application Manager objects. For custom tags, set its value using this property.</li> |
| webhooks | array | List of webhooks that integrate with the organization. |
| cost_centers | array | List of cost centers. Each cost center contains the following properties:<li>enforce: Boolean. If true, an instance cannot be deployed if it is over the quota.</li><li>name: String. Name of the cost center</li><li>workspaces: Array. List of the names that belongs to the cost center.</li><li>quotas: List of quotas. Each quota contains an object with the following properties:</li><ul><li>cost: Required. Boolean. By default it’s false. Specify as true to enable synchronizing with LDAP groups.</li><li>provider: Required. Boolean. By default it’s false. Specify as true to enable synchronizing with LDAP groups.</li><li>allocated: Array. List of instances which are contributing to the current quota. Each allocated instance has these properties:</li> <ul><li>instance_id: Required. String. Id of the instance.</li><li>instances: Required. Int. Number of instances.</li><li>started: Required. String. Date when this instance was deployed.</li><li>flavor: Required. String. Type of instance.</li><li>region: Required. String. Region where it was deployed.</li><li>service_type: Required. String. Type of the service.</li><li>terminated: String specifies the username of the LDAP service account to look up users who try to log in.</li></ul><li>resources: Object. Resources of the quota.</li><ul><li>cpu: Required. Int. Number of cpu units.</li><li>disk: Required. Object. A disk with these properties:</li><ul><li>quantity: Required. String. Amount of storage.</li><li>unit: Required. String. Mb, Gb or Tb.</li></ul><li>ram: Required. String. Ram of the quota.</li><ul><li>quantity: Required. String. Amount of storage.</li><li>unit: Required. String. Mb or Gb.</li> </ul>|

#### Response Body
```
{
    "remedy_account_id": "CPY000000115554",
    "features": {
        "net_x": true,
        "alm": true,
        "monitoring": true,
        "managed_provider": true,
        "show_unregistered_resources": true,
        "sync_corporate_groups": false,
        "aws_reseller": true,
        "ignore_velocity_templates": true,
        "safehaven_dr": false,
        "reporting": false,
        "ucpe": false,
        "managed_clc_provider": true,
        "delegate_managed_os": true,
        "custom_pricing": false,
        "analytics": true,
        "provider_sharing": true,
        "validate_emails": true,
        "safehaven_migration": false,
        "azure_reseller": true,
        "onboard_checklist": false,
        "aware_duplicate_arns": false
    },
    "providers": [
        {
            "enabled": true,
            "type": "CenturyLink",
            "description": "Manage cloud hosting, Linux and Windows machines",
            "pricing": []
        },
        {
            "enabled": true,
            "type": "CenturyLink DCC Foundation",
            "description": "Manage cloud hosting, Linux and Windows machines.",
            "pricing": []
        }
    ],
    "account_installed_product": "******",
    "clc_alias": "*****",
    "plugins": [],
    "account_status": "Active",
    "vantive_id": "S626423",
    "display_name": "MissionField LLC",
    "billing_account_number": "*******",
    "theme": {
        "logo": "/services/blobs/download/58888fc42364025f58d42b9a/mission-field.png",
        "accent": null,
        "css": "/services/blobs/download/58888fd3c571007a8af06207/mission-field.css"
    },
    "authentication": {
        "password": true,
        "google": true,
        "saml": false,
        "saml_config": {},
        "github": true,
        "ldap": true,
        "clc": false,
        "ldap_config": {
            "ldap_group_sync": true,
            "sources": [
                {
                    "host": "ldap://ldap.***********.com",
                    "ldap_search_password": "************"
                }
            ]
        }
    },
    "itsm": {
        "servicenow": {
            "enabled": false
        }
    },
    "default_costcenter": "c3195962-4c70-4ad6-a17a-189a5579a45a",
    "ldap_groups": [],
    "schema": "http://elasticbox.net/schemas/organization",
    "updated": "2018-10-25 15:48:03.290547",
    "account_type": "Billable",
    "tags": [
        {
            "type": "Box",
            "name": "box",
            "value": null
        },
        {
            "type": "Email",
            "name": "email",
            "value": null
        }
    ],
    "deleted": null,
    "ldap_last_sync_completed": null,
    "domains": [
        "**************"
    ],
    "members": [
        {
            "role": "administrator",
            "type": "workspace",
            "id": "********"
        },
        {
            "type": "workspace",
            "role": "administrator",
            "id": "**************"
        },
        {
            "role": "administrator",
            "type": "ldap",
            "id": "CN=Cloud Application Manager Support,OU=Internal Server Security Groups,OU=Protected,OU=EmployeeAccts,OU=ManagedHosting,DC=na,DC=msmps,DC=net"
        }
    ],
    "icon": "/services/blobs/download/58888fc42364025f58d42b9a/mission-field.png",
    "federated_to": [
        "elasticbox",
        "centurylink",
        "contoso",
        "ctlops"
    ],
    "name": "mission-field",
    "created": "2017-01-25 11:11:13.254512",
    "setup": true,
    "release": "4.0"
}
```

### GET /services/organizations/{organization_name}/boxes

Get the schema of boxes in the given organization.

### URL

#### Structure

    [GET] /services/organizations/{organization_name}/boxes

#### Example

    GET https://cam.ctl.io/services/organizations/centurylink/boxes

### Request
#### Headers
```
Content-Type: application/json
Authorization: Bearer your_json_web_token
ElasticBox-Release: 4.0
```

#### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| Organization name |  String  |  The name of the organization | Yes |

### Response
#### Normal Code
- **200** accepted

#### Error Codes
- Unauthorized (401) - Invalid access token/cookie
- User doesn’t belong to the organization (403)
- Not Found (404)

#### Response Parameters
| Parameter | Type | Description |
|-----------|------|-------------|
| schema |  string| Box schema URI: **//elasticbox.net/schemas/boxes** |
| name |    string   |  Organization's Box name |
| id | string |  Organization's Box identification number. |
| auto_update | boolean |   Auto update the box if any related requirement get updated. |
| updated | string | Date of the last update. |
| created | string | Creation date. |
| deleted | string | Deletion date. |
| profile | array | It shows the profile information of the box. |
| members | array | List of users who can access this box. |
| organization | string | It shows the name of the organization. |
| provider_id | string | It says to what provider is belonged this box. |
| uri | string | A url to the API service that makes a possibility to fetch the data of this box directly by a GET request. |
| readme | array | List of the information about the documentation for this API service. |
| owner | string | It shows the owner of this box. |
| visibility | strings | It indicates the visibility of the box for public or workspace or only organization. |
| variables | array | A list of the variables that defined in the box |
| claims | array | A list of the claims that defined in the box |

#### Response Body
```
  {
    "profile": {
      "datacenter": "va1",
      "group": [
        "Default Group"
      ],
      "network": "vlan_3135_10.128.235",
      "server_type": "Standard",
      "pricing_info": {
        "estimated_monthly": 2592000000,
        "provider_type": "CenturyLink",
        "hourly_price": 3600000,
        "factor": 100000000
      },
      "disks": [],
      "cpus": 1,
      "public_ip": false,
      "instances": 1,
      "template": "CENTOS-7-64-TEMPLATE",
      "memory": 2,
      "managed_os": false,
      "schema": "http://elasticbox.net/schemas/centurylink/compute/profile"
    },
    "provider_id": "338f38dc-e667-47e0-9026-b253138f109e",
    "automatic_updates": "off",
    "name": "default-small-va1",
    "created": "2018-08-21 20:26:17.273033",
    "deleted": null,
    "variables": [],
    "updated": "2018-08-21 20:26:17.273033",
    "visibility": "workspace",
    "uri": "/services/boxes/55c6aad7-393c-439e-94a0-88108ae1ee76",
    "readme": {
      "url": "services/resources/default_box_overview.md",
      "upload_date": "2018-08-21 20:26:17.272359",
      "length": 1307,
      "content_type": "text/x-markdown"
    },
    "members": [],
    "claims": [
      "small",
      "linux"
    ],
    "owner": "cam3",
    "organization": "mission-field",
    "id": "55c6aad7-393c-439e-94a0-88108ae1ee76",
    "schema": "http://elasticbox.net/schemas/boxes/policy"
  }
```

### GET /services/organizations/{organization_name}/instances

Get the schema of instances in the given organization.

### URL
#### Structure
    [GET] /services/organizations/{organization_name}/instances

#### Example
    GET https://cam.ctl.io/services/organizations/centurylink/instances

### Request
#### Headers
```
Content-Type: application/json
Authorization: Bearer your_json_web_token
ElasticBox-Release: 4.0
```

#### URI Parameters
| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| Organization name |  String  |  The name of the organization | Yes |

### Response
#### Normal Code
- **200** accepted

#### Error Codes
- Unauthorized (401) - Invalid access token/cookie
- User doesn’t belong to the organization (403)
- Not Found (404)

#### Response Parameters
| Parameter | Type | Description |
|-----------|------|-------------|
| schema |  string| Organization schema URI: **//elasticbox.net/schemas/instance** |
| name |    string   |  Instance name |
| id | string |  Instance Identifier |
| updated | string | Date of the last update |
| created | string | Creation date |
| auto_update | boolean |   Auto update the box if any related requirement get updated. |
| box | string | The identifier of the last deployed box. |
| boxes | array | A list of the boxes that defined in the lifecycle of the instance |
| bindings | array | List of specified bindings of the instance |
| uri | string | A url to the API service that makes a possibility to fetch the data of this box directly by a GET request. |
| owner | string | It shows the owner of this box. |
| state | string | The last state of the instance |
| members | array | List of users who can access this box. |
| service | object | An object that contains information about the instance's service |
| policy_box | object | An object that includes the policy of the box that is defined for the instance. |

#### Response Body
```
    {
        "box": "c2be22d3-22bf-4694-8a6d-e2efe3dceebd",
        "bindings": [],
        "updated": "2018-08-22 13:32:51.728997",
        "automatic_updates": "off",
        "policy_box": {
            "profile": {
                "datacenter": "va1",
                "group": [
                    "Default Group"
                ],
                "network": "vlan_3135_10.128.235",
                "server_type": "Standard",
                "pricing_info": {
                    "estimated_monthly": 5388004080,
                    "factor": 100000000,
                    "hourly_price": 7483339,
                    "provider_type": "CenturyLink"
                },
                "disks": [],
                "cpus": 2,
                "public_ip": false,
                "instances": 1,
                "template": "CENTOS-7-64-TEMPLATE",
                "memory": 4,
                "managed_os": false,
                "schema": "http://elasticbox.net/schemas/centurylink/compute/profile"
            },
            "provider_id": "338f38dc-e667-47e0-9026-b253138f109e",
            "automatic_updates": "off",
            "name": "management-appliance-va1",
            "deleted": null,
            "variables": [],
            "visibility": "workspace",
            "owner": "cam3",
            "members": [],
            "organization": "mission-field",
            "readme": {
                "url": "services/resources/default_box_overview.md",
                "upload_date": "2018-08-22 13:16:15.650210",
                "length": 1307,
                "content_type": "text/x-markdown"
            },
            "claims": [
                "centos7",
                "linux"
            ],
            "id": "01bf237e-2e73-416c-a72b-d94ea10d1c2e",
            "schema": "http://elasticbox.net/schemas/boxes/policy"
        },
        "name": "managed-provider-appliance-va1",
        "service": {
            "type": "Linux Compute",
            "id": "eb-6okdo",
            "machines": [
                {
                    "state": "done",
                    "name": "managed-provider-appliance-va1-6okdo-1",
                    "workflow": []
                }
            ]
        },
        "tags": [
            "managed",
            "appliance"
        ],
        "variables": [
            {
                "scope": "gateway.constants",
                "type": "Text",
                "value": "https://gateway.managedos.ctl.io",
                "visibility": "internal",
                "name": "managed_os_api_url"
            },
            {
                "scope": "gateway.constants",
                "type": "Text",
                "visibility": "internal",
                "value": "https://api.watcher.ctl.io/",
                "name": "watcher_reg_url"
            }
        ],
        "created": "2018-08-22 13:16:15.687975",
        "boxes": [
            {
                "schema": "http://elasticbox.net/schemas/boxes/script",
                "updated": "2018-08-07 23:20:02.898885",
                "automatic_updates": "off",
                "requirements": [
                    "centos7",
                    "linux"
                ],
                "description": "CenturyLink Management Appliance",
                "created": "2018-08-08 16:43:02.151411",
                "icon_metadata": {
                    "image": "/services/blobs/download/58a21fb465eca605038edc67/centurylink-logo.svg",
                    "border": "#8CC63F",
                    "fill": "#ffffff"
                },
                "variables": [
                    {
                        "name": "WaitForCMDBRecon",
                        "required": true,
                        "visibility": "internal",
                        "value": "true",
                        "type": "Options",
                        "options": "true,false"
                    },
                    {
                        "required": true,
                        "type": "Text",
                        "name": "CMDB_MaxTries",
                        "value": "120",
                        "visibility": "internal"
                    }
                ],
                "visibility": "workspace",
                "name": "CenturyLink Management Appliance",
                "deleted": null,
                "version": {
                    "box": "c2be22d3-22bf-4694-8a6d-e2efe3dceebd",
                    "number": {
                        "major": 0,
                        "minor": 5,
                        "patch": 5
                    },
                    "workspace": "keithhomco",
                    "description": "Limited support for no outbound connectivity scenarios (contact cam-msa@centurylink.com for details)"
                },
                "id": "fe257f92-2808-4c1a-aa1d-310a87e228b9",
                "categories": [
                    "managed"
                ],
                "members": [
                    {
                        "role": "read",
                        "workspace": "mgd"
                    },
                    {
                        "role": "read",
                        "workspace": "managed6"
                    }
                ],
                "owner": "managed1",
                "organization": "centurylink",
                "readme": {
                    "url": "/services/blobs/download/593843b76d4c585793fe1fb9/README.md",
                    "upload_date": "2017-06-07 18:19:35.185072",
                    "length": 2962,
                    "content_type": "text/x-markdown"
                },
                "events": {
                    "pre_install": {
                        "url": "/services/blobs/download/5b6a26565fc39f10a99fefaa/pre_install",
                        "length": 2170,
                        "destination_path": "scripts",
                        "content_type": "text/x-shellscript"
                    }
                },
                "draft_from": "7f1bd23f-14cf-4e44-a831-53716e0f20a8",
                "icon": "/icons/boxes/c2be22d3-22bf-4694-8a6d-e2efe3dceebd"
            }
        ],
        "uri": "/services/instances/i-k2tj0y",
        "is_deploy_only": true,
        "state": "done",
        "members": [],
        "owner": "cam3",
        "operation": {
            "event": "deploy",
            "workspace": "cam3",
            "created": "2018-08-22 13:16:15.857029"
        },
        "id": "i-k2tj0y",
        "schema": "http://elasticbox.net/schemas/instance"
    }
```

### GET /services/organizations/{organization_name}/providers

Get the schema of providers in the given organization.

### URL
#### Structure

    [GET] /services/organizations/{organization_name}/providers

#### Example

    GET https://cam.ctl.io/services/organizations/centurylink/providers

### Request
#### Headers
```
Content-Type: application/json
Authorization: Bearer your_json_web_token
ElasticBox-Release: 4.0
```

#### URI Parameters
| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| Organization name |  String  |  The name of the organization | Yes |

### Response
#### Normal Code
- **200** accepted

#### Error Codes
- Unauthorized (401) - Invalid access token/cookie
- User doesn’t belong to the organization (403)
- Not Found (404)


#### Response Parameters
| Parameter | Type | Description |
|-----------|------|-------------|
| schema |  string| Provider schema URI: **//elasticbox.net/schemas/providers** |
| name |    string   |  It defines the provider name |
| icon | string |   Provider icon URI |
| updated | string | Date of the last update |
| created | string | Creation date |
| description | string | Short description about the provider |
| uri | string | A url to the API service that makes a possibility to fetch the data of this box directly by a GET request. |
| state | string | It shows the last state of the provider |
| members | array | List of users who can access this box. |
| type | string | Indicates the type of the provider. |
| id | string | Contains the id of provider |
| providers | array | List of cloud providers the organization can enable to register and deploy. Each provider type has the following properties enabled:<li>Boolean value of true if enabled, else false.</li><li>type: String values of the supported cloud providers: Amazon Web Services, Openstack, VMWare vSphere, Google Compute, Microsoft Azure, Cloudstack, SoftLayer, VMware vCloud Director, Amazon Web Services GovCloud, Rackspace.</li><li>description: String that briefly enumerates the services from the cloud provider.</li><li>pricing: Array of pricing information for Linux and Windows compute instance types. Only available for Amazon Web Services.</li> |
| owner | string | It shows the owner of this box. |
| service | object | An object that contains information about the instance's service |

#### Response Body
```
  {
    "updated": "2018-09-28 21:18:17.691311",
    "description": "UMW Lab Account for CAM MSA Testing",
    "icon": "images/platform/centurylink.svg",
    "created": "2018-08-21 20:03:15.901180",
    "deleted": null,
    "uri": "/services/providers/338f38dc-e667-47e0-9026-b253138f109e",
    "name": "UMWC",
    "services": [
      {
        "name": "Linux Compute"
      },
      {
        "name": "Windows Compute"
      }
    ],
    "state": "ready",
    "members": [],
    "owner": "cam3",
    "type": "CenturyLink",
    "id": "338f38dc-e667-47e0-9026-b253138f109e",
    "schema": "http://elasticbox.net/schemas/centurylink/provider"
  }
```

### GET /services/organizations/{organization_name}/workspaces

Get the schema of workspaces in the given organization.

### URL
#### Structure
    [GET] /services/organizations/{organization_name}/workspaces

#### Example
    GET https://cam.ctl.io/services/organizations/centurylink/workspaces

### Request
#### Headers
```
Content-Type: application/json
Authorization: Bearer your_json_web_token
ElasticBox-Release: 4.0
```

#### URI Parameters
| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| Organization name |  String  |  The name of the organization | Yes |

### Response
#### Normal Code
- **200** accepted

#### Error Codes
- Unauthorized (401) - Invalid access token/cookie
- User doesn’t belong to the organization (403)
- Not Found (404)

#### Response Parameters
| Parameter | Type | Description |
|-----------|------|-------------|
| last_name | string | The last name of the user. |
| favorites | array | List of the users or organizations that has been selected as favorite.
| clc_alias | string | Indicates the CenturyLink billing alias if it exists for the workspace. |
| id | string | The user name in this workspace. |
| last_login | string | The date of the last login. |
| add_provider | boolean |
| deploy_instance | boolean |
| type | string | The type of the user. |
| email | string | The email of the user. |
| schema |  string| Provider schema URI: **//elasticbox.net/schemas/providers** |
| updated | string | Date of the last update |
| take_tour | boolean | Indicates if had the first login tour or not. |
| deleted | string | The Deletion date of the user. |
| costcenter | string | The given name of the cost center when the user got created. |
| icon | string | The user icon URI |
| group_dns | array | The list of the users that have been configured by AD in a local network. |
| email_validated_at | string | The date that user got validated. |
| validate_email_id | string | The validation id that generated for the user. |
| reset_password_id | string | The reset id that generated for the user. |
| name | string | The given name of the user. |
| created | string | The creation date of the user |
| uri | string | A url to the API service that makes a possibility to fetch the data of this box directly by a GET request. |
| members | array | If the user type be a "team" then it shows the workspaces that this user is belonged to |
| organization | string | The name of the organization that user belongs to it. |

#### Response Body
```
  {
    "last_name": "1",
    "favorites": [
      {
        "type": "team_workspace",
        "id": "insightglobal4"
      }
    ],
    "clc_alias": "DMFC",
    "id": "missionfields1",
    "last_login": "2018-07-25 14:18:22.323786",
    "add_provider": true,
    "deploy_instance": true,
    "type": "personal",
    "email": "*****@*************.com",
    "schema": "http://elasticbox.net/schemas/workspaces/personal",
    "updated": "2018-07-25 14:24:05.510205",
    "take_tour": true,
    "deleted": null,
    "clc_username": null,
    "costcenter": "c3195962-4c70-4ad6-a17a-189a5579a45a",
    "icon": null,
    "group_dns": [],
    "email_validated_at": "2017-02-01 15:03:54.087863",
    "name": "MF User",
    "created": "2017-02-01 15:03:54.087863",
    "support_user_created": true,
    "uri": "/services/workspaces/missionfields1",
    "organization": "mission-field"
  }
```

### PUT /services/organizations/{organization_name}

Updates an existing organization given its name. Only the organization administrator can update.

### URL
#### Structure
    [PUT] /services/organizations/{organization_name}

#### Example
    PUT https://cam.ctl.io/services/organizations/{organization_name}

### Request
#### Headers
```
Content-Type: application/json
Authorization: Bearer your_json_web_token
ElasticBox-Release: 4.0
```

#### URI Parameters
| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| Organization name |  String  |  The name of the organization | Yes |

#### Request Body
```
{
   "schema":"http://elasticbox.net/schemas/organization",
   "name":"elasticbox",
   "icon":"/services/blobs/download/5452705c3bbd224ef9541c41/elasticbox.png",
   "theme":null,
   "updated":"2015-04-06 14:28:12.874910",
   "created":"2014-02-14 15:12:21.526672",
   "setup":true,
   "administrators":[
      "ad",
      "al"
   ],
   "domains":[
      "cam.ctl.io"
   ],
   "authentication":{
      "github":false,
      "google":true,
      "ldap":true,
      "password":false,
      "username":null,
      "ldap_config":{
         "sources":[
            {
               "host":"ldap://ldap.cam.ctl.io",
               "email_field":"mail"
            }
         ]
      }
   },
   "features":{
      "admin_boxes":true,
      "cost_center":true,
      "custom_pricing":false,
      "onboard_checklist":false,
      "provider_sharing":true,
      "reporting":true
   },
   "providers":[
      {
         "enabled":true,
         "type":"Amazon Web Services",
         "description":"Manage EC2, ECS and Cloudformation instances",
         "pricing":[
            {
               "platform":"Linux Compute",
               "price":7000,
               "region":"ap-southeast-2",
               "flavor":"i2.8xlarge",
               "schema":"http://elasticbox.net/schemas/aws/compute/pricing"
            },
            {
               "platform":"Linux Compute",
               "price":5,
               "region":"us-east-1",
               "flavor":"t2.micro",
               "schema":"http://elasticbox.net/schemas/aws/compute/pricing"
            }
         ]
      },
      {
         "enabled":true,
         "type":"Openstack",
         "description":"Manage cloud hosting, Linux and Windows machines",
         "pricing":[

         ]
      },
      {
         "enabled":true,
         "type":"VMware vSphere",
         "description":"Manage cloud hosting, Linux and Windows machines",
         "pricing":[

         ]
      }
   ],
   "tags":[
      {
         "name":"workspace",
         "type":"Workspace",
         "value":null
      },
      {
         "name":"box",
         "type":"Box",
         "value":null
      }
   ],
   "cost_centers":[
      {
         "name":"test",
         "enforce":false,
         "quotas":[
            {
               "allocated":[

               ],
               "cost":0,
               "provider":"2bf1bd2c-b03d-460f-80da-647d26bdbcfe"
            },
            {
               "cost":3000,
               "provider":"5908ee9b-0c0a-4af6-8eef-2dc9f95d033a"
            }
         ],
         "workspaces":[
            "operations"
         ]
      }
   ],
   "webhooks":[

   ]
}
```

#### Request Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| schema |  string| Organization schema URI: **//elasticbox.net/schemas/organization** |
| name |    string   |  Organization name |
| icon | string |   Organization icon URI |
| updated | string | Date of the last update |
| created | string | Creation date |
| setup | boolean | This is read-only. It indicates that the Cloud Application Manager appliance is set up and ready for use. |
| administrators | array | List of users who can administer the organization |
| domains | string | Domains that are a part of the organization |
| authentication | object | List of the authentication methods to allow single sign-on in the organization. Contains the following properties:<li>github: Boolean. If enabled, it is true, else false.</li><li>google: Boolean. If enabled, it is true, else false.</li><li>password: Boolean. If enabled, it is true, else false.</li><li>ldap: Boolean. If enabled, it is true, else false.</li><li>ldap_config: Object that contains the LDAP service settings:</li><ul><li>ldap_group_sync: Boolean. By default it’s false. Specify as true to enable synchronizing with LDAP groups.</li><li>sources: Array of [LDAP](https://www.ctl.io/knowledge-base/cloud-application-manager/administering-your-organization/user-authentication/) sources. Each source has the following properties:</li><ul><li>host: Required. String identifies the hostname or IP address of the LDAP service.</li><li>groups_dn: String specifies a fully qualified group name.</li><li>group_dn_filter: String defines an entity on the LDAP server. All groups are synchronized as children of this entity.</li><li>email_field: String specifies the email field name by which to look up users. Typically, this field is called email.</li><li>ldap_search_password: String specifies the password for the LDAP service account to look up users who try to log in</li><li>ldap_search_user: String specifies the username of the LDAP service account to look up users who try to log in.</li></ul></ul> |
| ldap_last_sync_completed | string | Timestamp of the last successful LDAP group sync, for example, 2015-04-06 14:28:12.874910. Value is null if ldap_group_sync is set to false. |
| ldap_groups | array | List of objects, each of which is an LDAP group. Each group has two properties:<li>dn: String identifier for the group.</li><li>name: String name shown in the workspace web interface.</li> |
| providers | array | List of cloud providers the organization can enable to register and deploy. Each provider type has the following properties:<li>enabled: Boolean value of true if enabled, else false.</li><li>type: String values of the supported cloud providers: Amazon Web Services, Openstack, VMWare vSphere, Google Compute, Microsoft Azure, Cloudstack, SoftLayer, VMware vCloud Director, Amazon Web Services GovCloud, Rackspace.</li><li>description: String that briefly enumerates the services from the cloud provider.</li><li>pricing: Array of pricing information for Linux and Windows compute instance types. Only available for Amazon Web Services.</li> |
| tags | array | List of [tags](https://www.ctl.io/knowledge-base/cloud-application-manager/administering-your-organization/resource-tags/) applied on instances deployed to cloud providers from the organization. Each tag has three properties:<li>name: String you apply as a tag.</li><li>type: String identifies the type of tag whether an Cloud Application Manager object or a custom one. Allowed values are Box, Workspace, Provider, Environment, Email, User ID, Service Instance ID, Service ID, Workspace ID, Instance ID, Custom.</li><li>value: String value of null for Cloud Application Manager objects. For custom tags, set its value using this property.</li> |
| webhooks | array | List of webhooks that integrate with the organization. |
| cost_centers | array | List of cost centers. Each cost center contains the following properties:<li>enforce: Boolean. If true, an instance cannot be deployed if it is over the quota.</li><li>name: String. Name of the cost center</li><li>workspaces: Array. List of the names that belongs to the cost center.</li><li>quotas: List of quotas. Each quota contains an object with the following properties:</li><ul><li>cost: Required. Boolean. By default it’s false. Specify as true to enable synchronizing with LDAP groups.</li><li>provider: Required. Boolean. By default it’s false. Specify as true to enable synchronizing with LDAP groups.</li><li>allocated: Array. List of instances which are contributing to the current quota. Each allocated instance has these properties:</li><ul><li>instance_id: Required. String. Id of the instance.</li><li>instances: Required. Int. Number of instances.</li><li>started: Required. String. Date when this instance was deployed.</li><li>flavor: Required. String. Type of instance.</li><li>region: Required. String. Region where it was deployed.</li><li>service_type: Required. String. Type of the service.</li><li>terminated: String specifies the username of the LDAP service account to look up users who try to log in.</li></ul><li>resources: Object. Resources of the quota.</li><ul><li>cpu: Required. Int. Number of cpu units.</li><li>disk: Required. Object. A disk with these properties:</li><ul><li>quantity: Required. String. Amount of storage.</li><li>unit: Required. String. Mb, Gb or Tb.</li></ul><li>ram: Required. String. Ram of the quota.</li><ul><li>quantity: Required. String. Amount of storage.</li><li>unit: Required. String. Mb or Gb.</li> </ul>|

### Response
#### Normal Code
- **200** accepted

#### Error Codes
- Bad Request (400) - Request missing, incomplete or includes invalid properties (details provided inside body)
- Unauthorized (401) - Invalid access token/cookie
- User doesn’t belong to the organization (403)
- Not Found (404) - Organization not found
- Conflict (409) - 'updated' property mismatch. (Make a GET call to API to fetch the current 'updated' property and use it in a new PUT request)

#### Response Parameters
|  Parameter  |     Type      |	Description |
|----------|:-------------|-----|
| schema |  string| Organization schema URI: **http://elasticbox.net/schemas/organization** |
| name |    string   |  Organization name |
| icon | string |   Organization icon URI |
| updated | string | Date of the last update |
| created | string | Creation date |
| setup | boolean | This is read-only. It indicates that the Cloud Application Manager appliance is set up and ready for use. |
| administrators | array | List of users who can administer the organization |
| domains | string | Domains that are a part of the organization |
| authentication | object | List of the authentication methods to allow single sign-on in the organization. Contains the following properties:<li>github: Boolean. If enabled, it is true, else false.</li><li>google: Boolean. If enabled, it is true, else false.</li><li>password: Boolean. If enabled, it is true, else false.</li><li>ldap: Boolean. If enabled, it is true, else false.</li><li>ldap_config: Object that contains the LDAP service settings:</li><ul><li>ldap_group_sync: Boolean. By default it’s false. Specify as true to enable synchronizing with LDAP groups.</li><li>sources: Array of [LDAP sources](https://www.ctl.io/knowledge-base/cloud-application-manager/administering-your-organization/user-authentication/). Each source has the following properties:</li><ul><li>host: Required. String identifies the hostname or IP address of the LDAP service.</li><li>groups_dn: String specifies a fully qualified group name.</li><li>group_dn_filter: String defines an entity on the LDAP server. All groups are synchronized as children of this entity.</li><li>email_field: String specifies the email field name by which to look up users. Typically, this field is called email.</li><li>ldap_search_password: String specifies the password for the LDAP service account to look up users who try to log in</li><li>ldap_search_user: String specifies the username of the LDAP service account to look up users who try to log in.</li></ul></ul> |
| ldap_last_sync_completed | string | Timestamp of the last successful LDAP group sync, for example, 2015-04-06 14:28:12.874910. Value is null if ldap_group_sync is set to false. |
| ldap_groups | array | List of objects, each of which is an LDAP group. Each group has two properties:<li>dn: String identifier for the group.</li><li>name: String name shown in the workspace web interface.</li> |
| providers | array | List of cloud providers the organization can enable to register and deploy. Each provider type has the following properties enabled:<li>Boolean value of true if enabled, else false.</li><li>type: String values of the supported cloud providers: Amazon Web Services, Openstack, VMWare vSphere, Google Compute, Microsoft Azure, Cloudstack, SoftLayer, VMware vCloud Director, Amazon Web Services GovCloud, Rackspace.</li><li>description: String that briefly enumerates the services from the cloud provider.</li><li>pricing: Array of pricing information for Linux and Windows compute instance types. Only available for Amazon Web Services.</li> |
| tags | array | List of [tags](https://www.ctl.io/knowledge-base/cloud-application-manager/administering-your-organization/resource-tags/) applied on instances deployed to cloud providers from the organization. Each tag has three properties:<li>name: String you apply as a tag.</li><li>type: String identifies the type of tag whether an Cloud Application Manager object or a custom one. Allowed values are Box, Workspace, Provider, Environment, Email, User ID, Service Instance ID, Service ID, Workspace ID, Instance ID, Custom.</li><li>value: String value of null for Cloud Application Manager objects. For custom tags, set its value using this property.</li> |
| webhooks | array | List of webhooks that integrate with the organization. |
| cost_centers | array | List of cost centers. Each cost center contains the following properties:<li>enforce: Boolean. If true, an instance cannot be deployed if it is over the quota.</li><li>name: String. Name of the cost center</li><li>workspaces: Array. List of the names that belongs to the cost center.</li><li>quotas: List of quotas. Each quota contains an object with the following properties:</li><ul><li>cost: Required. Boolean. By default it’s false. Specify as true to enable synchronizing with LDAP groups.</li><li>provider: Required. Boolean. By default it’s false. Specify as true to enable synchronizing with LDAP groups.</li><li>allocated: Array. List of instances which are contributing to the current quota. Each allocated instance has these properties:</li><ul><li>instance_id: Required. String. Id of the instance.</li><li>instances: Required. Int. Number of instances.</li><li>started: Required. String. Date when this instance was deployed.</li><li>flavor: Required. String. Type of instance.</li><li>region: Required. String. Region where it was deployed.</li><li>service_type: Required. String. Type of the service.</li><li>terminated: String specifies the username of the LDAP service account to look up users who try to log in.</li></ul><li>resources: Object. Resources of the quota.</li><ul><li>cpu: Required. Int. Number of cpu units.</li><li>disk: Required. Object. A disk with these properties:</li><ul><li>quantity: Required. String. Amount of storage.</li><li>unit: Required. String. Mb, Gb or Tb.</li></ul><li>ram: Required. String. Ram of the quota.</li><ul><li>quantity: Required. String. Amount of storage.</li><li>unit: Required. String. Mb or Gb.</li> </ul>|

#### Response Body
```
{
   "schema":"http://elasticbox.net/schemas/organization",
   "name":"elasticbox",
   "icon":"/services/blobs/download/5452705c3bbd224ef9541c41/elasticbox.png",
   "theme":null,
   "updated":"2015-04-06 20:38:46.060399",
   "created":"2014-02-14 15:12:21.526672",
   "setup":true,
   "administrators":[
      "ad",
      "al",
      "ar"
   ],
   "domains":[
      "cam.ctl.io"
   ],
   "authentication":{
      "github":false,
      "google":true,
      "ldap":true,
      "password":false,
      "username":null,
      "ldap_config":{
         "sources":[
            {
               "host":"ldap://ldap.cam.ctl.io",
               "email_field":"mail"
            }
         ]
      }
   },
   "features":{
      "admin_boxes":true,
      "cost_center":true,
      "custom_pricing":false,
      "onboard_checklist":false,
      "provider_sharing":true,
      "reporting":true
   },
   "providers":[
      {
         "enabled":true,
         "type":"Amazon Web Services",
         "description":"Manage EC2, ECS and Cloudformation instances",
         "pricing":[
            {
               "platform":"Linux Compute",
               "price":7000,
               "region":"ap-southeast-2",
               "flavor":"i2.8xlarge",
               "schema":"http://elasticbox.net/schemas/aws/compute/pricing"
            },
            {
               "platform":"Linux Compute",
               "price":5,
               "region":"us-east-1",
               "flavor":"t2.micro",
               "schema":"http://elasticbox.net/schemas/aws/compute/pricing"
            }
         ]
      },
      {
         "enabled":true,
         "type":"Amazon Web Services GovCloud",
         "description":"Manage compute services in an isolated ITAR compliant AWS region.",
         "pricing":[

         ]
      },
      {
         "enabled":true,
         "type":"Rackspace",
         "description":"Manage cloud hosting and Linux machines.",
         "pricing":[

         ]
      }
   ],
   "tags":[
      {
         "name":"workspace",
         "type":"Workspace",
         "value":null
      },
      {
         "name":"box",
         "type":"Box",
         "value":null
      }
   ],
   "cost_centers":[
      {
         "name":"test",
         "enforce":false,
         "quotas":[
            {
               "allocated":[

               ],
               "cost":0,
               "provider":"2bf1bd2c-b03d-460f-80da-647d26bdbcfe"
            },
            {
               "cost":3000,
               "provider":"5908ee9b-0c0a-4af6-8eef-2dc9f95d033a"
            }
         ],
         "workspaces":[
            "operations"
         ]
      }
   ],
   "webhooks":[

   ]
}
```

### PUT /organizations/{organization_name}/sync_groups

Queues a request to sync LDAP groups. The sync request, depending on the amount of data from the LDAP service, can take a few minutes. The ldap_last_sync_completed property updates when the request finishes successfully.

### URL
#### Structure
    [PUT] /organizations/{organization_name}/sync_groups

#### Example
    PUT https://cam.ctl.io/organizations/{organization_name}/sync_groups

### Request
#### Headers
```
Content-Type: application/json
Authorization: Bearer your_json_web_token
ElasticBox-Release: 4.0
```
#### URI Parameters
| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| Organization name |  String  |  The name of the organization | Yes |

### Response
#### Normal Code
- **202** accepted

#### Error Codes
- Unauthorized (401) - Invalid access token/cookie
- Not Found (404) - Organization not found


#### Response Parameters
| Parameter | Type | Description |
|-----------|------|-------------|
| schema |  string| Organization schema URI: **//elasticbox.net/schemas/organization** |
| name |    string   |  Organization name |
| icon | string |   Organization icon URI |
| updated | string | Date of the last update |
| created | string | Creation date |
| setup | boolean | This is read-only. It indicates that the Cloud Application Manager appliance is set up and ready for use. |
| administrators | array | List of users who can administer the organization |
| domains | string | Domains that are a part of the organization |
| authentication | object | List of the authentication methods to allow single sign-on in the organization. Contains the following properties:<li>github: Boolean. If enabled, it is true, else false.</li><li>google: Boolean. If enabled, it is true, else false.</li><li>password: Boolean. If enabled, it is true, else false.</li><li>ldap: Boolean. If enabled, it is true, else false.</li><li>ldap_config: Object that contains the LDAP service settings:</li><ul><li>ldap_group_sync: Boolean. By default it’s false. Specify as true to enable synchronizing with LDAP groups.</li><li>sources: Array of [LDAP sources](https://www.ctl.io/knowledge-base/cloud-application-manager/administering-your-organization/user-authentication/). Each source has the following properties:</li><ul><li>host: Required. String identifies the hostname or IP address of the LDAP service.</li><li>groups_dn: String specifies a fully qualified group name.</li><li>group_dn_filter: String defines an entity on the LDAP server. All groups are synchronised as children of this entity.</li><li>email_field: String specifies the email field name by which to look up users. Typically, this field is called email.</li><li>ldap_search_password: String specifies the password for the LDAP service account to look up users who try to log in</li><li>ldap_search_user: String specifies the username of the LDAP service account to look up users who try to log in.</li></ul></ul> |
| ldap_last_sync_completed | string | Timestamp of the last successful LDAP group sync, for example, 2015-04-06 14:28:12.874910. Value is null if ldap_group_sync is set to false. |
| ldap_groups | array | List of objects, each of which is an LDAP group. Each group has two properties:<li>dn: String identifier for the group.</li><li>name: String name shown in the workspace web interface.</li> |
| providers | array | List of cloud providers the organization can enable to register and deploy. Each provider type has the following properties enabled:<li>Boolean value of true if enabled, else false.</li><li>type: String values of the supported cloud providers: Amazon Web Services, Openstack, VMWare vSphere, Google Compute, Microsoft Azure, Cloudstack, SoftLayer, VMware vCloud Director, Amazon Web Services GovCloud, Rackspace.</li><li>description: String that briefly enumerates the services from the cloud provider.</li><li>pricing: Array of pricing information for Linux and Windows compute instance types. Only available for Amazon Web Services.</li> |
| tags | array | List of [tags](https://www.ctl.io/knowledge-base/cloud-application-manager/administering-your-organization/resource-tags/) applied on instances deployed to cloud providers from the organization. Each tag has three properties:<li>name: String you apply as a tag.</li><li>type: String identifies the type of tag whether an Cloud Application Manager object or a custom one. Allowed values are Box, Workspace, Provider, Environment, Email, User ID, Service Instance ID, Service ID, Workspace ID, Instance ID, Custom.</li><li>value: String value of null for Cloud Application Manager objects. For custom tags, set its value using this property.</li> |
| webhooks | array | List of webhooks that integrate with the organization. |
| cost_centers | array | List of cost centers. Each cost center contains the following properties:<li>enforce: Boolean. If true, an instance cannot be deployed if it is over the quota.</li><li>name: String. Name of the cost center</li><li>workspaces: Array. List of the names that belongs to the cost center.</li><li>quotas: List of quotas. Each quota contains an object with the following properties:</li><ul><li>cost: Required. Boolean. By default it’s false. Specify as true to enable synchronizing with LDAP groups.</li><li>provider: Required. Boolean. By default it’s false. Specify as true to enable synchronizing with LDAP groups.</li><li>allocated: Array. List of instances which are contributing to the current quota. Each allocated instance has these properties:</li><ul><li>instance_id: Required. String. Id of the instance.</li><li>instances: Required. Int. Number of instances.</li><li>started: Required. String. Date when this instance was deployed.</li><li>flavor: Required. String. Type of instance.</li><li>region: Required. String. Region where it was deployed.</li><li>service_type: Required. String. Type of the service.</li><li>terminated: String specifies the username of the LDAP service account to look up users who try to log in.</li></ul><li>resources: Object. Resources of the quota.</li><ul><li>cpu: Required. Int. Number of cpu units.</li><li>disk: Required. Object. A disk with these properties:</li><ul><li>quantity: Required. String. Amount of storage.</li><li>unit: Required. String. Mb, Gb or Tb.</li></ul><li>ram: Required. String. Ram of the quota.</li><ul><li>quantity: Required. String. Amount of storage.</li><li>unit: Required. String. Mb or Gb.</li></ul> |

#### Response Body

```
{
   "schema":"http://elasticbox.net/schemas/organization",
   "name":"organization_name",
   "icon":null,
   "theme":null,
   "updated":"2015-04-06 16:59:02.486606",
   "created":"2015-03-25 10:41:15.098256",
   "setup":true,
   "administrators":[
      "operations"
   ],
   "domains":[
      "cam.ctl.io"
   ],
   "authentication":{
      "ldap_config":{
         "ldap_group_sync":false,
         "sources":[
            {
               "host":"ldap://test_ldap"
            }
         ]
      },
      "github":true,
      "google":true,
      "ldap":true,
      "password":true,
   },
   "ldap_groups":[

   ],
   "providers":[
      {
         "enabled":true,
         "type":"Amazon Web Services",
         "description":"Manage EC2, ECS and Cloudformation instances",
         "pricing":[

         ]
      },
      {
         "enabled":true,
         "type":"Google Compute",
         "description":"Manage cloud hosting and Linux machines.",
         "pricing":[

         ]
      }
   ],
   "ldap_last_sync_completed":null,
   "tags":[
      {
         "name":"box",
         "type":"Box name",
         "value":null
      },
      {
         "name":"environment",
         "type":"Environment",
         "value":null
      }
   ],
   "cost_centers":[
      {
         "name":"test",
         "enforce":false,
         "quotas":[
            {
               "allocated":[

               ],
               "cost":0,
               "provider":"2bf1bd2c-b03d-460f-80da-647d26bdbcfe"
            },
            {
               "cost":3000,
               "provider":"5908ee9b-0c0a-4af6-8eef-2dc9f95d033a"
            }
         ],
         "workspaces":[
            "operations"
         ]
      }
   ],
   "webhooks":[

   ]
}
```

### Contacting Cloud Application Manager Support

We’re sorry you’re having an issue in [Cloud Application Manager](https://www.ctl.io/cloud-application-manager/). Please review the [troubleshooting tips](https://www.ctl.io/knowledge-base/cloud-application-manager/troubleshooting/troubleshooting-tips/), or contact [Cloud Application Manager support](mailto:incident@CenturyLink.com) with details and screenshots where possible.

For issues related to API calls, send the request body along with details related to the issue.

In the case of a box error, share the box in the workspace that your organization and Cloud Application Manager can access and attach the logs.
* Linux: SSH and locate the log at /var/log/elasticbox/elasticbox-agent.log
* Windows: RDP into the instance to locate the log at ProgramDataElasticBoxLogselasticbox-agent.log
