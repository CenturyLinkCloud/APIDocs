{{{ "title": "Providers API",
"date": "10-30-2018",
"author": "Arya Roudi",
"keywords": ["api", "cam api", "cam", "api providers", "providers", "manage api"],
"attachments": [],
"contentIsHTML": false
}}}

Manage and perform provider actions.

### Manage Providers

|  Resource  |  Description |
|------------|--------------|
| POST /services/providers | Creates a new provider account in Cloud Application Manager and gets the status of the provider. |
| GET /services/providers | Gets the list of providers. |
| GET /services/providers/{provider_id} | Fetches an existing provider. |
| PUT /services/providers/{provider_id} | Updates an existing provider. |
| DELETE /services/providers/{provider_id}| Deletes an existing provider.|

### Provider Operations

|  Resource  |  Description |
|------------|--------------|
| PUT /services/providers/{provider_id}/sync |Syncs an existing provider.|
| GET /services/providers/{provider_id}/logs | Gets the logs of a provider. |
| GET /services/providers/{provider_id}/unregisted-instances | Gets the unregistered instances of a provider. |
| POST /services/providers/{provider_id}/images | Adds a new machine image to a provider. |
| DELETE /services/providers/{provider_id}/images/{machine_image_id} | Updates an existing provider. |


### POST /services/providers

Creates a new provider account in Cloud Application Manager and gets the status of the provider.

### URL

#### Structure

    [POST] /services/providers

#### Example

    POST https://cam.ctl.io/services/providers

### Request

#### Headers
```
content-type:application/json
Authorization: Bearer your_json_web_token
ElasticBox-Release: 4.0
```

#### Request parameters for all providers

|  Parameter  |      Type     |   Description   |
|-------------|---------------|-----------------|
| icon | string | Specify an icon URI for the provider account. |
| type | string | Required. Specify the account type as one of the following: Amazon Web Services, Rackspace, Openstack, VMware vSphere, Google Compute, Microsoft Azure, Cloudstack, SoftLayer. |
| description | string | Describe the services from the provider. |
| schema | string | Required. Provide the schema for the request. |
| name | string | Required. Give the provider account a name in Cloud Application Manager. |
| owner | string | Specify the user in Cloud Application Manager who owns the provider account. |

#### Amazon Web Services request parameters

|  Parameter  |      Type     |   Description   |
|-------------|---------------|-----------------|
| credentials | object | Required. Contains the credential object, which is either the AWS role ARN name if using Cloud Application Manager as a SaaS or the key and secret if using Cloud Application Manager as an appliance. |

#### Amazon Web Services request body
```
{
   "icon": "images/platform/aws.png",
   "type": "Amazon Web Services",
   "description": "Manage EC2, ECS and Cloudformation instances",
   "schema": "http://elasticbox.net/schemas/aws/provider",
   "name": "example account",
   "credentials": {
      "role": "role_ARN_that_gives_Cloud_Application_Manager_access"
   },
   "owner": "mrina"
}
```

#### Amazon Web Services Gov request parameters
|  Parameter  |      Type     |   Description   |
|-------------|---------------|-----------------|
| credentials | object | Required. Contains the credential object, which is either the [AWS role ARN name](https://www.ctl.io/knowledge-base/cloud-application-manager/deploying-anywhere/using-your-aws-account/) if using Cloud Application Manager as a SaaS or the key and secret if using Cloud Application Manager as an appliance. |

#### Amazon Web Services Gov request body
```
{
  "icon": "images/platform/govcloud.png",
  "type": "Amazon Web Services GovCloud",
  "description": "Manage compute services in an isolated ITAR compliant AWS region",
  "schema": "http://elasticbox.net/schemas/aws/provider",
  "name": "AWSGovCloud",
  "credentials": {
    "key": "_the_key",
    "secret": "_the_secret"
  },
  "owner": "operations"
}
```

#### Rackspace and OpenStack request parameters
|  Parameter  |      Type     |   Description   |
|-------------|---------------|-----------------|
| identity_url | string |Required. Specify the identity service endpoint.|
| project | string | Required. Specify the project ID for Rackspace or the tenant for OpenStack. |
| username | string | Required. Specify the username. |
| password | string | Required. Specify the password. |

#### Rackspace request body
```
{
   "icon": "images/platform/rackspace.png",
   "type": "Rackspace",
   "description": "Manage cloud hosting and Linux machines",
   "schema": "http://elasticbox.net/schemas/openstack/provider",
   "identity_url": "https://identity.api.rackspacecloud.com/v2.0",
   "name": "example rackspace",
   "project": "your_project_ID",
   "username": "your_Rackspace_username",
   "password": "your_Rackspace_password",
   "owner": "mrina"
}
```

#### OpenStack request body
```
{
   "icon": "images/platform/openstack.png",
   "type": "Openstack",
   "description": "Manage cloud hosting, Linux and Windows machines",
   "schema": "http://elasticbox.net/schemas/openstack/provider",
   "name": "example openstack",
   "identity_url": "http://openstack-26.cam.ctl.io:5000/v2.0",
   "project": "your_OpenStack_tenant",
   "username": "your_OpenStack_username",
   "password": "your_OpenStack_password",
   "owner": "mrina"
}
```

#### VSphere request parameters
|  Parameter  |      Type     |   Description   |
|-------------|---------------|-----------------|
| username | string | Required. Specify a vCenter username. |
| secret | string | Required. Specify the user’s password. |
| endpoint | string | Required. Specify the vCenter server URL. |

#### VSphere request body
```
{
   "icon": "images/platform/vsphere.png",
   "type": "VMware vSphere",
   "description": "Manage cloud hosting, Linux and Windows machines",
   "schema": "http://elasticbox.net/schemas/vsphere/provider",
   "name": "example vcenter",
   "username": "your_Vspherer_username",
   "secret": "your_Vsphere_user_password",
   "endpoint": "your_vCenter_server_URL",
   "owner": "mrina"
}
```

#### VCloud request parameters
|  Parameter  |      Type     |   Description   |
|-------------|---------------|-----------------|
| username | string | Required. Specify a vCenter username. |
| password | string | Required. Specify the user’s password. |
| url | string | Required. Specify the vCenter server URL. |
| organization | string | Required. Organization. |

#### VCloud request body
```
{
  "icon": "images/platform/vcloud.png",
  "type": "VMware vCloud Director",
  "description": "Manage cloud hosting, Linux and Windows machines",
  "schema": "http://elasticbox.net/schemas/vcloud/provider",
  "name": "VMwareVCloudProvider",
  "url": "https://v-cloud.cam.ctl.io",
  "vorg": "system",
  "username": "_the_username",
  "password": "_the_password",
  "owner": "operations"
}
```

#### Google Cloud request parameters
|  Parameter  |      Type     |   Description   |
|-------------|---------------|-----------------|
| project_id | string | Required. Specify a project ID in Google Cloud that has billing and the Google Compute Engine API enabled. |
| email | string | Required. Specify your Gmail account associated with Google Cloud. |
| credentials | object | Required. Specify either the refresh_token object or the key. You can get the refresh_token from Google OAuth 2.0 to allow Cloud Application Manager to make API requests on your behalf. Or you can provide the JSON key for the project service account. |

#### Google Cloud request body
```
{
   "icon": "images/platform/google.png",
   "type": "Google Compute",
   "description": "Manage cloud hosting and Linux machines",
   "name": "example google cloud account",
   "project_id": "your_GoogleCloud_projectID",
   "email": "your_gmailaccount_for_GoogleCloud",
   "credentials": {
      "refresh_token": "Google_OAuth_2.0_refresh_token"
   },
   "schema": "http://elasticbox.net/schemas/gce/provider",
   "owner": "mrina"
}
```

#### Azure request parameter
To add an Azure subscription in Cloud Application Manager, you first have to upload the Cloud Application Manager management certificate to your subscription in Azure.

|  Parameter  |      Type     |   Description   |
|-------------|---------------|-----------------|
| subscription | string | Required. Specify the Azure subscription ID.|

#### Azure request body
```
{
   "icon": "images/platform/azure-storage.png",
   "type": "Microsoft Azure",
   "description": "Manage compute services for Windows and Linux machines.",
   "schema": "http://elasticbox.net/schemas/azure/provider",
   "name": "example azure",
   "subscription_id": "your_Azure_subscription_ID",
   "owner": "mrina"
}
```

#### CloudStack request parameters
|  Parameter  |      Type     |   Description   |
|-------------|---------------|-----------------|
| url | string | Required. Specify the API endpoint to the CloudStack management server. |
| api_key | string | Required. Specify the API key for the CloudStack user account. |
| secret_key | string | Required. Specify the API secret for the CloudStack user account. |

#### CloudStack request body
```
{
   "icon": "images/platform/cloudstack.png",
   "type": "Cloudstack",
   "description": "Manage cloud hosting, Linux and Windows machines",
   "schema": "http://elasticbox.net/schemas/cloudstack/provider",
   "name": "example CloudStack",
   "url": "CloudStack_management_server_endpoint",
   "api_key": "CloudStack_API_key",
   "secret_key": "CloudStack_secret_key",
   "owner": "mrina"
}
```

#### SoftLayer request parameters
|  Parameter  |      Type     |   Description   |
|-------------|---------------|-----------------|
| username | string | Required. Specify a SoftLayer account username. |
| api_key | string | Required. Specify the API key for the SoftLayer user. |

#### SoftLayer request body
```
{
   "icon": "images/platform/softlayer.png",
   "type": "SoftLayer",
   "description": "Manage compute services for Windows and Linux machines.",
   "schema": "http://elasticbox.net/schemas/softlayer/provider",
   "name": "example softlayer",
   "username": "your_SoftLayer_username",
   "api_key": "SoftLayer_API_key_for_username",
   "owner": "mrina"
}
```

### Response

#### Normal Code

- **202** accepted

#### Error Codes

- No error code

#### Response parameters for all providers

|  Parameter  |      Type     |   Description   |
|-------------|---------------|-----------------|
| updated | string | Returns the date the provider was updated. |
| description | string | Returns the description for the provider. |
| deleted | object | Identifies whether the provider is deleted. |
| services | array | Returns the available services from the provider.|
| members | array | Returns users with whom the provider is shared. |
| owner | string | Returns the provider account owner in Cloud Application Manager. |
| id | string | Returns the ID of the provider account in Cloud Application Manager. |
| icon | string | Returns the icon used for the provider account. |
| name | string | Returns the name used to identify the provider account in Cloud Application Manager. |
| created | string | Returns the date that the provider was added. |
| uri | string | Returns the unique resource identifier path to the provider account. |
| admin_boxes | string | Lists the admin boxes attached to the provider. |
| organization | string | Identifies the name of the organization. |
| type | string | Identifies the provider as one of the following: Amazon Web Services, Rackspace, Openstack, VMware vSphere, Google Compute, Microsoft Azure, Cloudstack, SoftLayer. |
| schema | string | Returns the schema URL. |

#### AWS response parameters

|  Parameter  |      Type     |   Description   |
|-------------|---------------|-----------------|
| credentials | object | Returns the Amazon Web Services role ARN if using Cloud Application Manager as a SaaS or identifies the key and secret if using Cloud Application Manager as an appliance. |

#### AWS response body
```
{
   "updated": "2015-01-05 18:36:26.227970",
   "description": "Manage EC2, ECS and Cloudformation instances",
   "deleted": null,
   "services": [],
   "members": [],
   "owner": "mrina",
   "credentials": {
      "role": "your_ARN_role_that_allows_Cloud_Application_Manager_access"
   },
   "id": "aefc3f24-74af-414d-98ae-d6ee05997610",
   "icon": "images/platform/aws.png",
   "name": "example account",
   "created": "2015-01-05 18:36:26.227970",
   "uri": "/services/providers/aefc3f24-74af-414d-98ae-d6ee05997610",
   "state": "initializing",
   "admin_boxes": [],
   "organization": "elasticbox",
   "type": "Amazon Web Services",
   "schema": "http://elasticbox.net/schemas/aws/provider"
}
```

#### Rackspace and OpenStack response parameters
|  Parameter  |      Type     |   Description   |
|-------------|---------------|-----------------|
| username | string | Returns the username. |
| password | string | Masks the password for the provider account. |
| project | string | Returns the Rackspace project ID or the OpenStack tenant. |
| identity_url | string | Returns the OpenStack identity service endpoint. |

#### Rackspace response example
```
{
  "username": "_the_username",
  "updated": "2015-10-30 12:16:30.836398",
  "password": "_the_password",
  "description": "Manage cloud hosting and Linux machines",
  "created": "2015-10-30 12:16:30.836398",
  "deleted": null,
  "type": "Rackspace",
  "uri": "/services/providers/c6ade25c-cc46-4271-934d-55c75dba821a",
  "name": "RackSpace",
  "project": "937535",
  "services": [

  ],
  "state": "initializing",
  "admin_boxes": [

  ],
  "members": [

  ],
  "owner": "operations",
  "organization": "elasticbox",
  "icon": "images/platform/rackspace.png",
  "identity_url": "https://identity.api.rackspacecloud.com/v2.0",
  "id": "c6ade25c-cc46-4271-934d-55c75dba821a",
  "schema": "http://elasticbox.net/schemas/openstack/provider"
}
```

#### Openstack response example
```
{
  "username": "_the_username",
  "updated": "2015-10-30 12:26:14.331420",
  "password": "_the_password",
  "description": "Manage cloud hosting, Linux and Windows machines",
  "created": "2015-10-30 12:26:14.331420",
  "deleted": null,
  "identity_url": "http://openstack-36.cam.ctl.io:5000/v2.0",
  "uri": "/services/providers/57106d2a-ab5d-486a-988f-31a729a0c29d",
  "name": "OpenStackProvider",
  "project": "admin",
  "services": [

  ],
  "state": "initializing",
  "admin_boxes": [

  ],
  "members": [

  ],
  "owner": "operations",
  "organization": "elasticbox",
  "icon": "images/platform/openstack.png",
  "type": "Openstack",
  "id": "57106d2a-ab5d-486a-988f-31a729a0c29d",
  "schema": "http://elasticbox.net/schemas/openstack/provider"
}
```

#### VSphere response parameters
|  Parameter  |      Type     |   Description   |
|-------------|---------------|-----------------|
| username | string | Returns the vCenter username. |
| secret | string | Masks the user’s password. |
| endpoint | string | Returns the vCenter server URL. |

#### VSphere response example
```
{
  "username": "_the_username",
  "updated": "2015-10-30 12:51:53.729679",
  "endpoint": "https://10.0.128.2",
  "description": "Manage cloud hosting, Linux and Windows machines",
  "state": "initializing",
  "deleted": null,
  "created": "2015-10-30 12:51:53.729679",
  "uri": "/services/providers/3afc1c99-dd66-436a-ace4-33979dd5f5ca",
  "name": "VMWareVSphereProvider",
  "services": [

  ],
  "secret": "_the_secret",
  "admin_boxes": [

  ],
  "members": [

  ],
  "owner": "operations",
  "organization": "elasticbox",
  "icon": "images/platform/vsphere.png",
  "type": "VMware vSphere",
  "id": "3afc1c99-dd66-436a-ace4-33979dd5f5ca",
  "schema": "http://elasticbox.net/schemas/vsphere/provider"
}
```

#### Google Cloud response parameters

|  Parameter  |      Type     |   Description   |
|-------------|---------------|-----------------|
| project_id | string | Returns the project ID in Google Cloud that the provider account uses. |
| email | string | Returns the Gmail account associated with Google Cloud for the provider account. |
| credentials | object | Returns either the access_token and refresh_token objects or the key. Returns a key if you provided a JSON key for the project service account. |

#### Google Cloud response example

```
{
  "updated": "2015-10-30 12:34:09.062710",
  "description": "Manage cloud hosting and Linux machines",
  "icon": "images/platform/google.png",
  "created": "2015-10-30 12:34:09.062710",
  "deleted": null,
  "id": "d86e3bfe-1edc-45b4-a03b-28d1e2b7eee2",
  "uri": "/services/providers/d86e3bfe-1edc-45b4-a03b-28d1e2b7eee2",
  "name": "GoogleComputeProvider",
  "services": [

  ],
  "state": "initializing",
  "admin_boxes": [

  ],
  "members": [

  ],
  "organization": "elasticbox",
  "owner": "operations",
  "credentials": {
    "key": "_the_key"
  },
  "project_id": "_project_id",
  "type": "Google Compute",
  "email": "email@company.com",
  "schema": "http://elasticbox.net/schemas/gce/provider"
}
```

#### Azure response parameters

|  Parameter  |      Type     |   Description   |
|-------------|---------------|-----------------|
| subscription_id | string | Returns the Azure subscription ID that the provider account uses. |

#### Azure response example
```
{
  "updated": "2015-10-30 12:49:38.014690",
  "description": "Manage compute services for Windows and Linux machines",
  "created": "2015-10-30 12:49:38.014690",
  "deleted": null,
  "uri": "/services/providers/57b41251-43fd-4a18-9182-c71db30f9035",
  "name": "MicrosoftAzureServiceProvider",
  "services": [

  ],
  "state": "initializing",
  "admin_boxes": [

  ],
  "members": [

  ],
  "owner": "operations",
  "organization": "elasticbox",
  "subscription_id": "_the_subscription_id",
  "icon": "images/platform/azure-storage.png",
  "type": "Microsoft Azure",
  "id": "57b41251-43fd-4a18-9182-c71db30f9035",
  "schema": "http://elasticbox.net/schemas/azure/provider"
}
```

#### CloudStack response parameters
|  Parameter  |      Type     |   Description   |
|-------------|---------------|-----------------|
| url | string | Returns the API endpoint to the CloudStack management server. |
| api_key | string | Returns the API key for the CloudStack user account. |
| secret_key | string | Returns the API secret for the CloudStack user account. |

#### CloudStack response example
```
{
  "updated": "2015-10-30 12:28:22.315749",
  "api_key": "the_api_key",
  "description": "Manage cloud hosting, Linux and Windows machines",
  "created": "2015-10-30 12:28:22.315749",
  "url": "http://10.0.128.21:8080/client/api",
  "uri": "/services/providers/e50e4612-74a5-40b9-8aa0-b82631782c10",
  "name": "CloudStack",
  "deleted": null,
  "state": "initializing",
  "admin_boxes": [

  ],
  "members": [

  ],
  "organization": "elasticbox",
  "owner": "operations",
  "services": [

  ],
  "secret_key": "_the_secret_key",
  "icon": "images/platform/cloudstack.png",
  "type": "Cloudstack",
  "id": "e50e4612-74a5-40b9-8aa0-b82631782c10",
  "schema": "http://elasticbox.net/schemas/cloudstack/provider"
}
```

#### SoftLayer response parameters
|  Parameter  |      Type     |   Description   |
|-------------|---------------|-----------------|
| username | string | Returns the SoftLayer username the provider account uses. |
| api_key | string | Returns the API key for the SoftLayer user. |

#### SoftLayer response example
```
{
  "username": "_the_username",
  "updated": "2015-10-30 12:22:57.519720",
  "api_key": "_the_apikey",
  "description": "Manage compute services for Windows and Linux machines",
  "created": "2015-10-30 12:22:57.519720",
  "deleted": null,
  "uri": "/services/providers/8a820dc5-c21e-434f-9ca7-03434d066bd6",
  "name": "SoftlayerProvider",
  "services": [

  ],
  "state": "initializing",
  "admin_boxes": [

  ],
  "members": [

  ],
  "owner": "operations",
  "organization": "elasticbox",
  "icon": "images/platform/softlayer.png",
  "type": "SoftLayer",
  "id": "8a820dc5-c21e-434f-9ca7-03434d066bd6",
  "schema": "http://elasticbox.net/schemas/softlayer/provider"
}
```


### GET /services/providers

Gets available providers from the personal workspace of the authenticated user.

### URL
#### Structure

    [GET] /services/providers

#### Example

    GET https://cam.ctl.io/services/providers

### Request

#### Headers
```
content-type:application/json
Authorization: Bearer your_json_web_token
ElasticBox-Release: 4.0
```

#### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| -------- | ------- | --------------- | ----- |


### Response

#### Normal Code

- **200** accepted

#### Error Codes

- 400: Bad Request

#### Response parameters
|Parameter | Type | Description |
|----------|------|-------------|
|updated | string | Date of the last update.|
|description | string | Provider description.|
|created | string | Creation date.|
|uri | string | Provider uri.|
|name | string | Provider name.|
|services | array | List of services associated to the provider, each service has a name.|
|state | string | Provider state, there are five possible states: initializing , processing , ready , deleting or unavailable.|
|members | array | List of members with access to the provider.|
|owner | string | Provider owner.|
|type | string | Provider type, there are the available providers: Amazon Web Services (AWS), VShpere, VCloud, RackSpace, Openstack, Google Compute, Azure, CloudStack, Softlayer, AWS Gov.|
|id | string | Provider unique identificator.|
|icon | string | Provider Icon uri.|
|schema | string | The uri schema of the right provider.|

#### Response body
```
[
    {
        "updated": "2015-10-30 12:28:38.312157",
        "description": "Manage cloud hosting, Linux and Windows machines",
        "icon": "images/platform/cloudstack.png",
        "created": "2015-10-30 12:28:22.315749",
        "uri": "/services/providers/e50e4612-74a5-40b9-8aa0-b82631782c10",
        "name": "CloudStack",
        "services": [],
        "state": "unavailable",
        "members": [],
        "owner": "operations",
        "type": "Cloudstack",
        "id": "e50e4612-74a5-40b9-8aa0-b82631782c10",
        "schema": "http://elasticbox.net/schemas/cloudstack/provider"
    },
    {
        "schema": "http://elasticbox.net/schemas/vsphere/provider",
        "updated": "2015-10-30 12:25:42.135998",
        "description": "Manage cloud hosting, Linux and Windows machines",
        "created": "2015-10-09 07:35:00.273473",
        "uri": "/services/providers/cac26e4c-16f8-46ad-83ae-52a2b1ba4fca",
        "name": "vSphere",
        "owner": "operations",
        "state": "ready",
        "members": [],
        "services": [
            {
                "name": "Linux Compute"
            },
            {
                "name": "Windows Compute"
            }
        ],
        "type": "VMware vSphere",
        "id": "cac26e4c-16f8-46ad-83ae-52a2b1ba4fca",
        "icon": "images/platform/vsphere.png"
    },
    {
        "schema": "http://elasticbox.net/schemas/dimension-data/provider",
        "updated": "2015-10-30 12:58:20.228258",
        "description": "Manage compute services in DD",
        "created": "2015-10-30 12:58:19.078758",
        "uri": "/services/providers/052211ae-096a-44e7-b88c-27d8dcac3971",
        "name": "DimensionDataProvider",
        "services": [
            {
                "locations": [],
                "name": "Linux Compute"
            },
            {
                "locations": [],
                "name": "Windows Compute"
            }
        ],
        "state": "unavailable",
        "members": [],
        "owner": "operations",
        "type": "Dimension Data",
        "id": "052211ae-096a-44e7-b88c-27d8dcac3971",
        "icon": "images/platform/dimension-data.png"
    },
    {
        "updated": "2015-10-27 20:54:28.739422",
        "description": "Manage EC2, ECS and Cloudformation instances",
        "icon": "images/platform/aws.png",
        "created": "2015-10-27 16:25:58.448390",
        "uri": "/services/providers/7e841966-1dec-4460-a981-1db4e1eec10c",
        "name": "AWSProvider",
        "owner": "operations",
        "state": "ready",
        "members": [],
        "services": [
            {
                "locations": [
                    {},
                    {}
                ],
                "name": "CloudFormation Service"
            },
            {
                "name": "ECS Service",
                "locations": [
                    {
                        "clusters": []
                    },
                    {},
                    {
                        "clusters": []
                    }
                    {
                        "clusters": [
                            {
                                "name": "scenarios-cluster",
                                "arn": "arn:aws:ecs:us-east-1:729190825118:cluster/scenarios-cluster"
                            }
                        ]
                    }
                ]
            },
            {
                "name": "Linux Compute",
                "locations": [
                    {},
                    {}
                ]
            },
            {
                "name": "Windows Compute",
                "locations": [
                    {},
                    {}
                ]
            }
        ],
        "type": "Amazon Web Services",
        "id": "7e841966-1dec-4460-a981-1db4e1eec10c",
        "schema": "http://elasticbox.net/schemas/aws/provider"
    }
]
```

### GET /services/providers/{provider_id}

Fetches an existing provider when you give the provider ID.

### URL

#### Structure

    [GET] /services/providers/{provider_id}

#### Example

    GET https://cam.ctl.io/services/providers/338f38dc-e667-47e0-9026-b253138f109e


### Request

#### Headers

```
content-type:application/json
Authorization: Bearer your_json_web_token
ElasticBox-Release: 4.0
```

#### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| Provider id | string | The id of the provider | Yes |

### Response

#### Normal Code

- **202** accepted

#### Error Codes

- 403: Forbidden
- 404: Not Found


#### Response parameters

| Parameter | Type | Description |
|----------------|--------|-----------------|
| updated | string | Date of the last update. |
| description | string | Provider description. |
| created | string | Creation date. |
| uri | string | Provider uri. |
| name | string | Provider name. |
| services | array | List of services associated to the provider, each service has a name. |
| state | string | Provider state, there are five possible states: initializing , processing , ready , deleting or unavailable. |
| members | array | List of members with access to the provider. |
| owner | string | Provider owner. |
| type | string | Provider type, there are the available providers: Amazon Web Services (AWS), VShpere, VCloud, RackSpace, Openstack, Google Compute, Azure, CloudStack, Softlayer, AWS Gov. |
| id | string | Provider unique identificator. |
| schema | string | The provider type schema uri. |
| icon | string | Provider Icon uri. |

#### Response Body
```
{
    "costcenter": "c3195962-4c70-4ad6-a17a-189a5579a45a",
    "owner": "dryrun",
    "default_managed_iis_policies_created": true,
    "clc_alias": "DA4",
    "management_state": true,
    "id": "8132cc1d-38b0-4867-b7a3-1af7b83d4792",
    "state": "ready",
    "admin_boxes": [],
    "type": "Amazon Web Services",
    "managed_os": true,
    "schema": "http://elasticbox.net/schemas/aws/provider",
    "updated": "2018-10-15 19:10:57.749750",
    "description": null,
    "management_state_history": [
        {
            "started": "2018-04-06 00:29:28.414938",
            "state": "up",
            "completed": "2018-07-26 18:43:46.867016"
        },
        {
            "started": "2018-07-26 18:43:46.867016",
            "state": "down",
            "completed": "2018-07-26 18:53:27.827179"
        }
    ],
    "default_sql_server_policies_created": true,
    "deleted": null,
    "default_management_appliance_policies_created": true,
    "default_policies_created": true,
    "members": [
        {
            "role": "read",
            "workspace": "mission5"
        }
    ],
    "services": [
        {
            "icon": "images/platform/aws-cloudformation.png",
            "locations": [
                {
                    "name": "ap-northeast-1"
                },
                {
                    "name": "ap-northeast-2"
                }
            ],
            "name": "CloudFormation Service",
            "schema": "http://elasticbox.net/schemas/aws/cloudformation/cloudformation"
        },
        {
            "locations": [
                {
                    "clusters": [],
                    "name": "ap-northeast-1"
                },
                {
                    "name": "ap-northeast-2"
                }
            ],
            "icon": "images/platform/amazon-ecs.png",
            "name": "Container Service",
            "roles": [
                {
                    "name": "None"
                }
            ],
            "schema": "http://elasticbox.net/schemas/aws/ecs/container"
        },
        {
            "flavors": [
                {
                    "name": "c1.medium"
                },
                {
                    "name": "c1.xlarge"
                }
            ],
            "name": "Linux Compute",
            "roles": [
                {
                    "name": "None"
                },
                {
                    "name": "AutoScaleS3Access"
                }
            ],
            "locations": [
                {
                    "clouds": [
                        {
                            "subnets": [
                                {
                                    "description": "172.31.16.0/20",
                                    "name": "subnet-231b2d0b"
                                },
                                {
                                    "description": "172.31.0.0/20",
                                    "name": "subnet-af8e04f4"
                                }
                            ],
                            "description": "172.31.0.0/16",
                            "target_groups": [],
                            "load_balancers": [],
                            "security_groups": [
                                {
                                    "name": "Automatic"
                                },
                                {
                                    "description": "default VPC security group",
                                    "name": "sg-40c1ea39"
                                }
                            ],
                            "name": "vpc-9ff879f8"
                        }
                    ],
                    "name": "ap-northeast-1",
                    "placement_groups": [],
                    "images": [
                        {
                            "owner": "user",
                            "description": "Latest Amazon AMI",
                            "name": "Linux Compute"
                        },
                        {
                            "owner": "user",
                            "description": "CentOS 7 for Management Appliance",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 8
                            },
                            "name": "ami-3185744e"
                        }
                    ],
                    "alarms": [],
                    "keypairs": [
                        {
                            "name": "None"
                        }
                    ]
                }
            ],
            "certificates": [],
            "schema": "http://elasticbox.net/schemas/aws/compute/linux",
            "icon": "images/platform/linux.png"
        },
    ],
    "credentials": {
        "role": "arn:aws:iam::636588615608:role/ElasticBox_Access"
    },
    "icon": "images/platform/aws.svg",
    "target_regions": [
        {
            "appliance_id": "***********",
            "name": "us-east-1",
            "vpc": "************"
        }
    ],
    "name": "Dry-Run AWS",
    "reseller": false,
    "created": "2018-03-16 16:17:59.531589",
    "uri": "/services/providers/8132cc1d-38b0-4867-b7a3-1af7b83d4792",
    "organization": "mission-field"
}
```

### PUT /services/providers/{provider_id}

Updates an existing provider when you give the provider ID. Pass the provider object in the request body to update these fields: name, description, and members.

For AWS, you can also update the key and secret. For VMware vShpere, you can also update the username, secret, and endpoint.

### URL
#### Structure

    [PUT] /services/providers/{provider_id}

#### Example

    PUT https://cam.ctl.io/services/providers/338f38dc-e667-47e0-9026-b253138f109e

### Request
#### Headers
```
Content-Type: application/json
Authorization: Bearer your_json_web_token
ElasticBox-Release: 4.0
```

#### URI Parameters
| Parameter | Type | Description | Req. |
| Provider id | string | The unique id of the created provider | Yes |

### Response

#### Normal Response Codes
- **200** Accepted

#### Common Error Response Codes
- 400: Bad Request - Invalid Data
- 409: Conflict

#### Response Parameters
|Parameter | Type | Description |
|----------|------|-------------|
|updated | string | Date of the last update.|
|description | string | Provider description.|
|created | string | Creation date.|
|uri | string | Provider uri.|
|name | string | Provider name.|
|services | array | List of services associated to the provider, each service has a name.|
|state | string | Provider state, there are five possible states: initializing , processing , ready , deleting or unavailable .|
|members | array | List of members with access to the provider.|
|owner | string | Provider owner.|
|type | string | Provider type, there are two possible providers: Amazon Web Services or VMware vShpere. |
|id | string | Provider unique identifier.|
|icon | string | Provider Icon uri.|

#### Response Body
```
{
    "costcenter": "c3195962-4c70-4ad6-a17a-189a5579a45a",
    "owner": "dryrun",
    "default_managed_iis_policies_created": true,
    "clc_alias": "DA4",
    "management_state": true,
    "id": "8132cc1d-38b0-4867-b7a3-1af7b83d4792",
    "state": "ready",
    "admin_boxes": [],
    "type": "Amazon Web Services",
    "managed_os": true,
    "schema": "http://elasticbox.net/schemas/aws/provider",
    "updated": "2018-10-15 19:10:57.749750",
    "description": null,
    "management_state_history": [
        {
            "started": "2018-04-06 00:29:28.414938",
            "state": "up",
            "completed": "2018-07-26 18:43:46.867016"
        },
        {
            "started": "2018-07-26 18:43:46.867016",
            "state": "down",
            "completed": "2018-07-26 18:53:27.827179"
        }
    ],
    "default_sql_server_policies_created": true,
    "deleted": null,
    "default_management_appliance_policies_created": true,
    "default_policies_created": true,
    "members": [
        {
            "role": "read",
            "workspace": "mission5"
        }
    ],
    "services": [
        {
            "icon": "images/platform/aws-cloudformation.png",
            "locations": [
                {
                    "name": "ap-northeast-1"
                },
                {
                    "name": "ap-northeast-2"
                }
            ],
            "name": "CloudFormation Service",
            "schema": "http://elasticbox.net/schemas/aws/cloudformation/cloudformation"
        },
        {
            "locations": [
                {
                    "clusters": [],
                    "name": "ap-northeast-1"
                },
                {
                    "name": "ap-northeast-2"
                }
            ],
            "icon": "images/platform/amazon-ecs.png",
            "name": "Container Service",
            "roles": [
                {
                    "name": "None"
                }
            ],
            "schema": "http://elasticbox.net/schemas/aws/ecs/container"
        },
        {
            "flavors": [
                {
                    "name": "c1.medium"
                },
                {
                    "name": "c1.xlarge"
                }
            ],
            "name": "Linux Compute",
            "roles": [
                {
                    "name": "None"
                },
                {
                    "name": "AutoScaleS3Access"
                }
            ],
            "locations": [
                {
                    "clouds": [
                        {
                            "subnets": [
                                {
                                    "description": "172.31.16.0/20",
                                    "name": "subnet-231b2d0b"
                                },
                                {
                                    "description": "172.31.0.0/20",
                                    "name": "subnet-af8e04f4"
                                }
                            ],
                            "description": "172.31.0.0/16",
                            "target_groups": [],
                            "load_balancers": [],
                            "security_groups": [
                                {
                                    "name": "Automatic"
                                },
                                {
                                    "description": "default VPC security group",
                                    "name": "sg-40c1ea39"
                                }
                            ],
                            "name": "vpc-9ff879f8"
                        }
                    ],
                    "name": "ap-northeast-1",
                    "placement_groups": [],
                    "images": [
                        {
                            "owner": "user",
                            "description": "Latest Amazon AMI",
                            "name": "Linux Compute"
                        },
                        {
                            "owner": "user",
                            "description": "CentOS 7 for Management Appliance",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 8
                            },
                            "name": "ami-3185744e"
                        }
                    ],
                    "alarms": [],
                    "keypairs": [
                        {
                            "name": "None"
                        }
                    ]
                },
                {
                    "clouds": [
                        {
                            "subnets": [
                                {
                                    "description": "172.31.0.0/20",
                                    "name": "subnet-9ecc86f6"
                                },
                                {
                                    "description": "172.31.16.0/20",
                                    "name": "subnet-1dee5651"
                                }
                            ],
                            "description": "172.31.0.0/16",
                            "target_groups": [],
                            "load_balancers": [],
                            "security_groups": [
                                {
                                    "name": "Automatic"
                                },
                                {
                                    "description": "default VPC security group",
                                    "name": "sg-ff282394"
                                }
                            ],
                            "name": "vpc-08296b60"
                        }
                    ],
                    "name": "ap-northeast-2",
                    "placement_groups": [],
                    "images": [
                        {
                            "owner": "user",
                            "description": "Latest Amazon AMI",
                            "name": "Linux Compute"
                        },
                        {
                            "owner": "user",
                            "description": "CentOS 7 for Management Appliance",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 8
                            },
                            "name": "ami-46963e28"
                        }
                    ],
                    "alarms": [],
                    "keypairs": [
                        {
                            "name": "None"
                        }
                    ]
                }
            ],
            "certificates": [],
            "schema": "http://elasticbox.net/schemas/aws/compute/windows",
            "icon": "images/platform/windows.png"
        }
    ],
    "credentials": {
        "role": "arn:aws:iam::636588615608:role/ElasticBox_Access"
    },
    "icon": "images/platform/aws.svg",
    "target_regions": [
        {
            "appliance_id": "*********",
            "name": "us-east-1",
            "vpc": "**************"
        }
    ],
    "name": "Dry-Run AWS",
    "reseller": false,
    "created": "2018-03-16 16:17:59.531589",
    "uri": "/services/providers/8132cc1d-38b0-4867-b7a3-1af7b83d4792",
    "organization": "mission-field"
}
```

### DELETE /services/providers/{provider_id}

Deletes an existing provider when you give the provider ID.

### URL

#### Structure

    [DELETE] /services/providers/{provider_id}

#### Example

    DELETE https://cam.ctl.io/services/providers/338f38dc-e667-47e0-9026-b253138f109e

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
| Provider id | string | The unique id that given to each provider | Yes |

### Response
#### Normal Response Codes
- **202** Accepted

#### Common Error Response Codes
- 400: Bad Request - Invalid Data
- 400: Bad Request - Active service using the provider
- 403: Forbidden


### PUT /services/providers/{provider_id}/sync

Syncs an existing provider when you give the provider ID.

### URL
#### Structure

    [PUT] /services/providers/{provider_id}/sync

#### Example

    PUT https://cam.ctl.io/services/providers/338f38dc-e667-47e0-9026-b253138f109e/sync


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
| Provider id | string | The unique id that given to each provider | Yes |

### Response
#### Normal Response Codes
- **202** Accepted

#### Common Error Response Codes
- 403: Forbidden - User doesn’t belong to the organization
- 404: Not Found


### GET /services/providers/{provider_id}/logs

Retrieves the logs of a provider when you give the provider ID.

### URL
#### Structure
    [GET] /services/providers/{provider_id}/logs

#### Example
    GET https://cam.ctl.io/services/providers/338f38dc-e667-47e0-9026-b253138f109e/logs

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
| Provider id | string | The unique id that given to each provider | Yes |

### Response
#### Normal Response Codes
- **200** Accepted

#### Common Error Response Codes
- 403: Forbidden - User doesn’t belong to the organization
- 404: Not Found

#### Response Parameters

|Parameter | Type | Description |
|----------|------|-------------|
|workspace | string | Id of the workspace who perform the action.|
|provider_id | string | Provider unique identifier.|
|created | string | Creation date.|
|text | string | Profiver-log action description.|
|level | integer | Provider-log action level.|
|updated | array | Date of the update.|
|id | string | Provider unique identifier.|
|schema | string | Provider-log schema url.|


#### Response Body
```
 [
    {
       provider_id: "8132cc1d-38b0-4867-b7a3-1af7b83d4792",
       level: 40,
       text: "Amazon Web Services Management Console was accessed",
       created: "2018-10-22 07:30:47.808486",
       updated: "2018-10-22 07:30:47.808621",
       role: "arn:aws:iam::636588615608:role/ElasticBox_Access",
       workspace: "thomasbroadwell",
       request_id: "e09360e1-7738-4cd9-91f2-cdd3c9f83a91",
       operation: "console_access",
       id: "231373e4-ab8f-4c28-8ba6-d91f331fae2c",
       schema: "http://elasticbox.net/schemas/provider-log"
    },
    {
       provider_id: "8132cc1d-38b0-4867-b7a3-1af7b83d4792",
       level: 40,
       text: "Image ami-2051294a in location us-east-1 added successfully.",
       created: "2018-10-15 19:10:57.765608",
       updated: "2018-10-15 19:10:57.766848",
       workspace: "msa_service_account1",
       request_id: "3ee09e46-1655-4e09-a500-0ccf83161eec",
       operation: "sync",
       id: "b79820d6-64c4-4103-ac0b-97cdfe672893",
       schema: "http://elasticbox.net/schemas/provider-log"
    }
 ]
```

### GET /services/providers/{provider_id}/unregisted-instances

Retrieves a list of unregistered instances found in a provider when you give the provider ID.

### URL
#### Structure
    [GET] /services/providers/{provider_id}/unregisted-instances

#### Example
    GET https://cam.ctl.io/services/providers/338f38dc-e667-47e0-9026-b253138f109e/unregisted-instances

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
| Provider id | string | The unique id that given to each provider | Yes |

### Response

#### Normal Response Codes
- **200** Accepted

#### Common Error Response Codes
- 403: Forbidden - User doesn’t belong to the organization
- 404: Not Found

#### Response Parameters
|Parameter | Type | Description |
|----------|------|-------------|
|profile | object | Instance profile. |
| profile.subnet | string | Instance subnet. |
| profile.image | string | Instance image. |
| profile.keypair | string | Instance keypair. |
| profile.location | string| Instance location. |
| profile.security_groups | string | Instance security groups. |
| profile.flavor | string | Instance flavor. |
| profile.manageos | boolean | Instance Manage. |
| profile.autoscalable | boolean | Instance autoscalable. |
| profile.cloud | boolean | Cloud type. |
| profile.schema | string | Instance schema uri. |
|provider_id | string | Instance provider unique identifier. |
|name | string | Instance name. |
|created | string | Creation date.|
|deleted | string | Logical deletion date. |
|type | string | Can be one of these types: Linux Compute, Windows Compute and CloudFormation Service. |
|server_info | object | Instance public and private ips and public dns.|
|updated | array | Date of the update.|
|power_state | string | Can be running or stopped.|
|organization | string | Organization to which instance belongs.|
|external_id | string | Instance external id. |
|id | string | Instance unique identifier.|
|schema | string | Unregistered-instance schema url.|

#### Response Body
```
  [
     {
       profile: {
       location: "us-west-2",
       service: "cloudtrail",
       schema: "http://elasticbox.net/schemas/aws/native-service/profile"
       },
       schema: "http://elasticbox.net/schemas/unregistered-instance",
       provider_id: "8132cc1d-38b0-4867-b7a3-1af7b83d4792",
       description: "S3 Bucket: partsultd-cloudtrail",
       created: "2018-09-24 16:10:06.198406",
       deleted: null,
       type: "Native Service",
       server_info: { },
       updated: "2018-09-24 16:22:18.000760",
       stack_id: null,
       autoscaling_group: null,
       power_state: "running",
       organization: "mission-field",
       external_id: "PartsUltdAPILogs-Mgmt",
       id: "451873d3-07cb-450d-b20d-12b4ba3ec343",
       name: "PartsUltdAPILogs-Mgmt"
     }
  ]
```


Adds a new machine image to a provider when you give the provider ID.

### URL
#### Structure
### POST /services/providers/{provider_id}/images
    [POST] /services/providers/{provider_id}/images

#### Example
    POST https://cam.ctl.io/services/providers/338f38dc-e667-47e0-9026-b253138f109e/images

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
| Provider id | string | The unique id that given to each provider | Yes |

#### Request Body Parameters
|Parameter | Type | Description|
|----------|------|------------|
|location | string | Image location. |
|name | string | Image name. |
|description | string | Image description. |

#### Request Body
```
{
   "location":"us-east-1",
   "name":"ami-3275ee5b",
   "description":"New Image Description"
}
```

### Response
#### Normal Response Codes
- **202** Accepted

#### Common Error Response Codes
- 400: Bad Request - Request missing, incomplete or includes invalid properties (details provided inside body)
- 403: Forbidden - User doesn’t belong to the organization
- 404: Not Found


### DELETE /services/providers/{provider_id}/images/{machine_image_id}

Deletes an existing machine image when you give the provider ID and the machine image ID.

### URL
#### Structure
    [DELETE] /services/providers/{provider_id}/images/{machine_image_id}

#### Example
    DELETE https://cam.ctl.io/services/providers/338f38dc-e667-47e0-9026-b253138f109e/images/b253138f109e?location=us-east-1

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
| Provider id | string | The unique id that given to each provider | Yes |

#### Request Body Parameters
| Parameter | Type | Description |
|-----------|------|-------------|
|location | string | Location of the machine image to be deleted. |


### Response
#### Normal Response Codes
- **202** Accepted

#### Common Error Response Codes
- 400: Bad Request - Request missing, incomplete or includes invalid properties (details provided inside body)
- 403: Forbidden - User doesn’t belong to the organization
- 404: Not Found

### Contacting Cloud Application Manager Support

We’re sorry you’re having an issue in [Cloud Application Manager](https://www.ctl.io/cloud-application-manager/). Please review the [troubleshooting tips](https://www.ctl.io/knowledge-base/cloud-application-manager/troubleshooting/troubleshooting-tips/), or contact [Cloud Application Manager support](mailto:incident@CenturyLink.com) with details and screenshots where possible.

For issues related to API calls, send the request body along with details related to the issue.

In the case of a box error, share the box in the workspace that your organization and Cloud Application Manager can access and attach the logs.
* Linux: SSH and locate the log at /var/log/elasticbox/elasticbox-agent.log
* Windows: RDP into the instance to locate the log at ProgramDataElasticBoxLogselasticbox-agent.log
