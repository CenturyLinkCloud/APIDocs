{{{ "title": "Providers API",
"date": "09-01-2016",
"author": "",
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

- Bad Request (400)

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
        "updated": "2015-10-30 12:18:45.899110",
        "description": "Manage cloud hosting and Linux machines",
        "icon": "images/platform/rackspace.png",
        "created": "2015-10-30 12:16:30.836398",
        "uri": "/services/providers/c6ade25c-cc46-4271-934d-55c75dba821a",
        "name": "RackSpace",
        "services": [
            {
                "locations": [
                    {},
                    {},
                    {},
                    {}
                ],
                "name": "Linux Compute"
            }
        ],
        "state": "ready",
        "members": [],
        "owner": "operations",
        "type": "Rackspace",
        "id": "c6ade25c-cc46-4271-934d-55c75dba821a",
        "schema": "http://elasticbox.net/schemas/openstack/provider"
    },
    {
        "schema": "http://elasticbox.net/schemas/softlayer/provider",
        "updated": "2015-10-30 12:23:01.133330",
        "description": "Manage compute services for Windows and Linux machines",
        "created": "2015-10-30 12:22:57.519720",
        "uri": "/services/providers/8a820dc5-c21e-434f-9ca7-03434d066bd6",
        "name": "SoftlayerProvider",
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
        "owner": "operations",
        "type": "SoftLayer",
        "id": "8a820dc5-c21e-434f-9ca7-03434d066bd6",
        "icon": "images/platform/softlayer.png"
    },
    {
        "updated": "2015-10-30 12:26:23.841387",
        "description": "Manage cloud hosting, Linux and Windows machines",
        "icon": "images/platform/openstack.png",
        "created": "2015-10-30 12:26:14.331420",
        "uri": "/services/providers/57106d2a-ab5d-486a-988f-31a729a0c29d",
        "name": "OpenStackProvider",
        "services": [
            {
                "locations": [
                    {}
                ],
                "name": "Linux Compute"
            },
            {
                "locations": [
                    {}
                ],
                "name": "Windows Compute"
            }
        ],
        "state": "ready",
        "members": [],
        "owner": "operations",
        "type": "Openstack",
        "id": "57106d2a-ab5d-486a-988f-31a729a0c29d",
        "schema": "http://elasticbox.net/schemas/openstack/provider"
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
        "schema": "http://elasticbox.net/schemas/gce/provider",
        "updated": "2015-10-30 12:39:06.518493",
        "description": "Manage cloud hosting and Linux machines",
        "created": "2015-10-30 12:34:09.062710",
        "uri": "/services/providers/d86e3bfe-1edc-45b4-a03b-28d1e2b7eee2",
        "name": "GoogleComputeProvider",
        "owner": "operations",
        "state": "ready",
        "members": [],
        "services": [
            {
                "name": "Linux Compute"
            }
        ],
        "type": "Google Compute",
        "id": "d86e3bfe-1edc-45b4-a03b-28d1e2b7eee2",
        "icon": "images/platform/google.png"
    },
    {
        "schema": "http://elasticbox.net/schemas/vsphere/provider",
        "updated": "2015-10-30 12:52:48.017525",
        "description": "Manage cloud hosting, Linux and Windows machines",
        "created": "2015-10-30 12:51:53.729679",
        "uri": "/services/providers/3afc1c99-dd66-436a-ace4-33979dd5f5ca",
        "name": "VMWareVSphereProvider",
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
        "owner": "operations",
        "type": "VMware vSphere",
        "id": "3afc1c99-dd66-436a-ace4-33979dd5f5ca",
        "icon": "images/platform/vsphere.png"
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
                    {},
                    {},
                    {},
                    {},
                    {},
                    {},
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
                    },
                    {},
                    {
                        "clusters": []
                    },
                    {},
                    {
                        "clusters": [
                            {
                                "name": "scenarios-cluster",
                                "arn": "arn:aws:ecs:us-east-1:729190825118:cluster/scenarios-cluster"
                            }
                        ]
                    },
                    {
                        "clusters": []
                    },
                    {
                        "clusters": []
                    }
                ]
            },
            {
                "name": "Linux Compute",
                "locations": [
                    {},
                    {},
                    {},
                    {},
                    {},
                    {},
                    {},
                    {},
                    {}
                ]
            },
            {
                "name": "Windows Compute",
                "locations": [
                    {},
                    {},
                    {},
                    {},
                    {},
                    {},
                    {},
                    {},
                    {}
                ]
            }
        ],
        "type": "Amazon Web Services",
        "id": "7e841966-1dec-4460-a981-1db4e1eec10c",
        "schema": "http://elasticbox.net/schemas/aws/provider"
    },
    {
        "schema": "http://elasticbox.net/schemas/azure/provider",
        "updated": "2015-10-30 12:49:46.850182",
        "description": "Manage compute services for Windows and Linux machines",
        "created": "2015-10-30 12:49:38.014690",
        "uri": "/services/providers/57b41251-43fd-4a18-9182-c71db30f9035",
        "name": "MicrosoftAzureServiceProvider",
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
        "owner": "operations",
        "type": "Microsoft Azure",
        "id": "57b41251-43fd-4a18-9182-c71db30f9035",
        "icon": "images/platform/azure-storage.png"
    },
    {
        "updated": "2015-10-30 12:54:50.566266",
        "description": "Manage cloud hosting, Linux and Windows machines",
        "icon": "images/platform/vcloud.png",
        "created": "2015-10-30 12:53:55.767875",
        "uri": "/services/providers/51cf6ea7-1edc-42b7-ae96-f7a304060188",
        "name": "VMwareVCloudProvider",
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
        "owner": "operations",
        "type": "VMware vCloud Director",
        "id": "51cf6ea7-1edc-42b7-ae96-f7a304060188",
        "schema": "http://elasticbox.net/schemas/vcloud/provider"
    },
    {
        "schema": "http://elasticbox.net/schemas/aws/provider",
        "updated": "2015-10-30 13:00:29.227885",
        "description": "Manage compute services in an isolated ITAR compliant AWS region",
        "created": "2015-10-30 13:00:24.039492",
        "uri": "/services/providers/b975319b-d5c5-4f8b-8077-0e78a0240efa",
        "name": "AWSGovCloud",
        "services": [
            {
                "locations": [
                    {}
                ],
                "name": "CloudFormation Service"
            },
            {
                "name": "Linux Compute",
                "locations": [
                    {}
                ]
            },
            {
                "name": "Windows Compute",
                "locations": [
                    {}
                ]
            }
        ],
        "state": "ready",
        "members": [],
        "owner": "operations",
        "type": "Amazon Web Services GovCloud",
        "id": "b975319b-d5c5-4f8b-8077-0e78a0240efa",
        "icon": "images/platform/govcloud.png"
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

- Forbidden (403)
- Not Found (404)


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
        },
        {
            "started": "2018-07-26 18:53:27.827179",
            "state": "up",
            "completed": "2018-07-26 19:07:06.443650"
        },
        {
            "started": "2018-07-26 19:07:06.443650",
            "state": "down",
            "completed": "2018-07-26 19:09:30.067475"
        },
        {
            "started": "2018-07-26 19:09:30.067475",
            "state": "up",
            "completed": "2018-08-28 10:08:56.914918"
        },
        {
            "started": "2018-08-28 10:08:56.914918",
            "state": "down",
            "completed": "2018-09-04 21:28:32.573472"
        },
        {
            "started": "2018-09-04 21:28:32.573472",
            "state": "up",
            "completed": "2018-09-24 16:09:01.728550"
        },
        {
            "started": "2018-09-24 16:09:01.728550",
            "state": "down",
            "completed": "2018-09-24 16:21:34.906171"
        },
        {
            "started": "2018-09-24 16:21:34.906171",
            "state": "up"
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
                },
                {
                    "name": "ap-south-1"
                },
                {
                    "name": "ap-southeast-1"
                },
                {
                    "name": "ap-southeast-2"
                },
                {
                    "name": "ca-central-1"
                },
                {
                    "name": "eu-central-1"
                },
                {
                    "name": "eu-west-1"
                },
                {
                    "name": "eu-west-2"
                },
                {
                    "name": "eu-west-3"
                },
                {
                    "name": "sa-east-1"
                },
                {
                    "name": "us-east-1"
                },
                {
                    "name": "us-east-2"
                },
                {
                    "name": "us-west-1"
                },
                {
                    "name": "us-west-2"
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
                },
                {
                    "name": "ap-south-1"
                },
                {
                    "clusters": [],
                    "name": "ap-southeast-1"
                },
                {
                    "clusters": [],
                    "name": "ap-southeast-2"
                },
                {
                    "clusters": [],
                    "name": "ca-central-1"
                },
                {
                    "clusters": [],
                    "name": "eu-central-1"
                },
                {
                    "clusters": [],
                    "name": "eu-west-1"
                },
                {
                    "clusters": [],
                    "name": "eu-west-2"
                },
                {
                    "clusters": [],
                    "name": "eu-west-3"
                },
                {
                    "name": "sa-east-1"
                },
                {
                    "clusters": [],
                    "name": "us-east-1"
                },
                {
                    "clusters": [],
                    "name": "us-east-2"
                },
                {
                    "clusters": [],
                    "name": "us-west-1"
                },
                {
                    "clusters": [],
                    "name": "us-west-2"
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
                },
                {
                    "name": "c3.large"
                },
                {
                    "name": "c3.xlarge"
                },
                {
                    "name": "c3.2xlarge"
                },
                {
                    "name": "c3.4xlarge"
                },
                {
                    "name": "c3.8xlarge"
                },
                {
                    "name": "c4.large"
                },
                {
                    "name": "c4.xlarge"
                },
                {
                    "name": "c4.2xlarge"
                },
                {
                    "name": "c4.4xlarge"
                },
                {
                    "name": "c4.8xlarge"
                },
                {
                    "name": "c5.large"
                },
                {
                    "name": "c5.xlarge"
                },
                {
                    "name": "c5.2xlarge"
                },
                {
                    "name": "c5.4xlarge"
                },
                {
                    "name": "c5.9xlarge"
                },
                {
                    "name": "c5.18xlarge"
                },
                {
                    "name": "c5d.large"
                },
                {
                    "name": "c5d.xlarge"
                },
                {
                    "name": "c5d.2xlarge"
                },
                {
                    "name": "c5d.4xlarge"
                },
                {
                    "name": "c5d.9xlarge"
                },
                {
                    "name": "c5d.18xlarge"
                },
                {
                    "name": "cc2.8xlarge"
                },
                {
                    "name": "cr1.8xlarge"
                },
                {
                    "name": "d2.xlarge"
                },
                {
                    "name": "d2.2xlarge"
                },
                {
                    "name": "d2.4xlarge"
                },
                {
                    "name": "d2.8xlarge"
                },
                {
                    "name": "f1.2xlarge"
                },
                {
                    "name": "f1.16xlarge"
                },
                {
                    "name": "g2.2xlarge"
                },
                {
                    "name": "g2.8xlarge"
                },
                {
                    "name": "g3.4xlarge"
                },
                {
                    "name": "g3.8xlarge"
                },
                {
                    "name": "g3.16xlarge"
                },
                {
                    "name": "h1.2xlarge"
                },
                {
                    "name": "h1.4xlarge"
                },
                {
                    "name": "h1.8xlarge"
                },
                {
                    "name": "h1.16xlarge"
                },
                {
                    "name": "hs1.8xlarge"
                },
                {
                    "name": "i2.xlarge"
                },
                {
                    "name": "i2.2xlarge"
                },
                {
                    "name": "i2.4xlarge"
                },
                {
                    "name": "i2.8xlarge"
                },
                {
                    "name": "i3.large"
                },
                {
                    "name": "i3.metal"
                },
                {
                    "name": "i3.xlarge"
                },
                {
                    "name": "i3.2xlarge"
                },
                {
                    "name": "i3.4xlarge"
                },
                {
                    "name": "i3.8xlarge"
                },
                {
                    "name": "i3.16xlarge"
                },
                {
                    "name": "m1.small"
                },
                {
                    "name": "m1.medium"
                },
                {
                    "name": "m1.large"
                },
                {
                    "name": "m1.xlarge"
                },
                {
                    "name": "m2.xlarge"
                },
                {
                    "name": "m2.2xlarge"
                },
                {
                    "name": "m2.4xlarge"
                },
                {
                    "name": "m3.medium"
                },
                {
                    "name": "m3.large"
                },
                {
                    "name": "m3.xlarge"
                },
                {
                    "name": "m3.2xlarge"
                },
                {
                    "name": "m4.large"
                },
                {
                    "name": "m4.xlarge"
                },
                {
                    "name": "m4.2xlarge"
                },
                {
                    "name": "m4.4xlarge"
                },
                {
                    "name": "m4.10xlarge"
                },
                {
                    "name": "m4.16xlarge"
                },
                {
                    "name": "m5.large"
                },
                {
                    "name": "m5.xlarge"
                },
                {
                    "name": "m5.2xlarge"
                },
                {
                    "name": "m5.4xlarge"
                },
                {
                    "name": "m5.12xlarge"
                },
                {
                    "name": "m5.24xlarge"
                },
                {
                    "name": "m5d.large"
                },
                {
                    "name": "m5d.xlarge"
                },
                {
                    "name": "m5d.2xlarge"
                },
                {
                    "name": "m5d.4xlarge"
                },
                {
                    "name": "m5d.12xlarge"
                },
                {
                    "name": "m5d.24xlarge"
                },
                {
                    "name": "p2.xlarge"
                },
                {
                    "name": "p2.8xlarge"
                },
                {
                    "name": "p2.16xlarge"
                },
                {
                    "name": "r3.large"
                },
                {
                    "name": "r3.xlarge"
                },
                {
                    "name": "r3.2xlarge"
                },
                {
                    "name": "r3.4xlarge"
                },
                {
                    "name": "r3.8xlarge"
                },
                {
                    "name": "r4.large"
                },
                {
                    "name": "r4.xlarge"
                },
                {
                    "name": "r4.2xlarge"
                },
                {
                    "name": "r4.4xlarge"
                },
                {
                    "name": "r4.8xlarge"
                },
                {
                    "name": "r4.16xlarge"
                },
                {
                    "name": "t1.micro"
                },
                {
                    "name": "t2.micro"
                },
                {
                    "name": "t2.small"
                },
                {
                    "name": "t2.medium"
                },
                {
                    "name": "t2.large"
                },
                {
                    "name": "t2.xlarge"
                },
                {
                    "name": "t2.2xlarge"
                },
                {
                    "name": "x1.16xlarge"
                },
                {
                    "name": "x1.32xlarge"
                },
                {
                    "name": "x1e.xlarge"
                },
                {
                    "name": "x1e.2xlarge"
                },
                {
                    "name": "x1e.4xlarge"
                },
                {
                    "name": "x1e.8xlarge"
                },
                {
                    "name": "x1e.16xlarge"
                },
                {
                    "name": "x1e.32xlarge"
                }
            ],
            "name": "Linux Compute",
            "roles": [
                {
                    "name": "None"
                },
                {
                    "name": "AutoScaleS3Access"
                },
                {
                    "name": "MeyerTest"
                },
                {
                    "name": "test-chris"
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
                                },
                                {
                                    "description": "172.31.32.0/20",
                                    "name": "subnet-f2e2bcbb"
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
                },
                {
                    "clouds": [
                        {
                            "subnets": [
                                {
                                    "description": "172.31.0.0/20",
                                    "name": "subnet-d310e69f"
                                },
                                {
                                    "description": "172.31.16.0/20",
                                    "name": "subnet-f855d390"
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
                                    "name": "sg-d39d11b8"
                                }
                            ],
                            "name": "vpc-1585067d"
                        }
                    ],
                    "name": "ap-south-1",
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
                            "name": "ami-48301d27"
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
                                    "description": "172.31.16.0/20",
                                    "name": "subnet-15dc9372"
                                },
                                {
                                    "description": "172.31.0.0/20",
                                    "name": "subnet-2d60776b"
                                },
                                {
                                    "description": "172.31.32.0/20",
                                    "name": "subnet-22b6c96b"
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
                                    "name": "sg-e3a2269a"
                                }
                            ],
                            "name": "vpc-b00a89d7"
                        }
                    ],
                    "name": "ap-southeast-1",
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
                            "name": "ami-da6151a6"
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
                                    "description": "172.31.32.0/20",
                                    "name": "subnet-66492f2f"
                                },
                                {
                                    "description": "172.31.0.0/20",
                                    "name": "subnet-dfc5b0b8"
                                },
                                {
                                    "description": "172.31.16.0/20",
                                    "name": "subnet-3a699f62"
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
                                    "name": "sg-5b299b22"
                                }
                            ],
                            "name": "vpc-65329802"
                        }
                    ],
                    "name": "ap-southeast-2",
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
                            "name": "ami-0d13c26f"
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
                                    "description": "172.31.16.0/20",
                                    "name": "subnet-3119e159"
                                },
                                {
                                    "description": "172.31.0.0/20",
                                    "name": "subnet-823b2cf9"
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
                                    "name": "sg-c09fa1a8"
                                }
                            ],
                            "name": "vpc-9e3fccf6"
                        }
                    ],
                    "name": "ca-central-1",
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
                            "name": "ami-456aea21"
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
                                    "description": "172.31.16.0/20",
                                    "name": "subnet-1557147e"
                                },
                                {
                                    "description": "172.31.32.0/20",
                                    "name": "subnet-454af238"
                                },
                                {
                                    "description": "172.31.0.0/20",
                                    "name": "subnet-07029b4a"
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
                                    "name": "sg-8a14a6e7"
                                }
                            ],
                            "name": "vpc-70e7671b"
                        }
                    ],
                    "name": "eu-central-1",
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
                            "name": "ami-9a183671"
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
                                    "description": "172.31.16.0/20",
                                    "name": "subnet-836db4cb"
                                },
                                {
                                    "description": "172.31.0.0/20",
                                    "name": "subnet-3948835f"
                                },
                                {
                                    "description": "172.31.32.0/20",
                                    "name": "subnet-9b5d49c0"
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
                                    "name": "sg-3e154144"
                                }
                            ],
                            "name": "vpc-2b5fe54d"
                        }
                    ],
                    "name": "eu-west-1",
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
                            "name": "ami-4c457735"
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
                                    "description": "172.31.16.0/20",
                                    "name": "subnet-9f7e9fe5"
                                },
                                {
                                    "description": "172.31.32.0/20",
                                    "name": "subnet-fae6d0b7"
                                },
                                {
                                    "description": "172.31.0.0/20",
                                    "name": "subnet-286fc141"
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
                                    "name": "sg-e98e8581"
                                }
                            ],
                            "name": "vpc-2b1fda43"
                        }
                    ],
                    "name": "eu-west-2",
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
                            "name": "ami-4726cb20"
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
                                    "description": "172.31.16.0/20",
                                    "name": "subnet-d134e3aa"
                                },
                                {
                                    "description": "172.31.32.0/20",
                                    "name": "subnet-c70fe38a"
                                },
                                {
                                    "description": "172.31.0.0/20",
                                    "name": "subnet-b909b4d0"
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
                                    "name": "sg-3d155254"
                                }
                            ],
                            "name": "vpc-ac15aec5"
                        }
                    ],
                    "name": "eu-west-3",
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
                            "name": "ami-6276c71f"
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
                                    "name": "subnet-35133052"
                                },
                                {
                                    "description": "172.31.16.0/20",
                                    "name": "subnet-aa3001f2"
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
                                    "name": "sg-39b32a5f"
                                }
                            ],
                            "name": "vpc-050fa062"
                        }
                    ],
                    "name": "sa-east-1",
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
                            "name": "ami-c2e6baae"
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
                                    "description": "Private subnet",
                                    "name": "subnet-0f4d827f0959c45a4"
                                },
                                {
                                    "description": "Public subnet",
                                    "name": "subnet-0d3033d2b8bf13f12"
                                }
                            ],
                            "description": "VPC1",
                            "target_groups": [],
                            "load_balancers": [],
                            "security_groups": [
                                {
                                    "name": "Automatic"
                                },
                                {
                                    "description": "default VPC security group",
                                    "name": "sg-0c48ef851d23ee3cc"
                                }
                            ],
                            "name": "vpc-0ad1a5959b295f65e"
                        },
                        {
                            "subnets": [
                                {
                                    "description": "172.31.64.0/20",
                                    "name": "subnet-f56242ca"
                                },
                                {
                                    "description": "172.31.0.0/20",
                                    "name": "subnet-32a9bc56"
                                },
                                {
                                    "description": "172.31.16.0/20",
                                    "name": "subnet-09e41a43"
                                },
                                {
                                    "description": "172.31.32.0/20",
                                    "name": "subnet-4ec7ed13"
                                },
                                {
                                    "description": "172.31.48.0/20",
                                    "name": "subnet-772d8978"
                                },
                                {
                                    "description": "172.31.80.0/20",
                                    "name": "subnet-c4f5c1eb"
                                }
                            ],
                            "description": "172.31.0.0/16",
                            "target_groups": [
                                {
                                    "default_port": 80,
                                    "protocol": "HTTP",
                                    "target_type": "instance",
                                    "arn": "arn:aws:elasticloadbalancing:us-east-1:636588615608:targetgroup/partsultdLBRouting/e1031aa116bf033f",
                                    "name": "partsultdLBRouting"
                                }
                            ],
                            "load_balancers": [],
                            "security_groups": [
                                {
                                    "name": "Automatic"
                                },
                                {
                                    "description": "This security group was generated by AWS Marketplace and is based on recommended settings for Red Hat Enterprise Linux (RHEL) 6 (HVM) version 6.7_HVM_20160219 provided by Amazon Web Services",
                                    "name": "sg-06f2b8b511216c8f3"
                                },
                                {
                                    "description": "This security group was generated by AWS Marketplace and is based on recommended settings for CentOS 7 (x86_64) - with Updates HVM version 1805_01 provided by Centos.org",
                                    "name": "sg-0752c07ce1afb7f9a"
                                },
                                {
                                    "description": "Enable SSH access via port 22",
                                    "name": "sg-092de9abb7c435e37"
                                },
                                {
                                    "description": "This security group was generated by AWS Marketplace and is based on recommended settings for Red Hat Enterprise Linux (RHEL) 6 version 6.5_GA provided by Amazon Web Services",
                                    "name": "sg-0db584c264083fbd2"
                                },
                                {
                                    "description": "This security group was generated by AWS Marketplace and is based on recommended settings for CentOS 6 (x86_64) - with Updates HVM version 1805_01 provided by Centos.org",
                                    "name": "sg-0f53c2fa9738d1f55"
                                },
                                {
                                    "description": "default VPC security group",
                                    "name": "sg-6969051f"
                                }
                            ],
                            "name": "vpc-711a9f0a"
                        },
                        {
                            "subnets": [
                                {
                                    "description": "Public Subnet #2",
                                    "name": "subnet-01f48b41fd743c464"
                                },
                                {
                                    "description": "Private subnet",
                                    "name": "subnet-072d27171887b3f3b"
                                },
                                {
                                    "description": "Public subnet",
                                    "name": "subnet-08c8e59037abe931d"
                                },
                                {
                                    "description": "Private subnet #2",
                                    "name": "subnet-00175e924b602a94f"
                                }
                            ],
                            "description": "VPC2",
                            "target_groups": [
                                {
                                    "default_port": 80,
                                    "protocol": "HTTP",
                                    "target_type": "instance",
                                    "arn": "arn:aws:elasticloadbalancing:us-east-1:636588615608:targetgroup/partsultdASGGroup/21bf3b5ba88c8714",
                                    "name": "partsultdASGGroup"
                                }
                            ],
                            "load_balancers": [],
                            "security_groups": [
                                {
                                    "name": "Automatic"
                                },
                                {
                                    "description": "launch-wizard-3 created 2018-03-18T15:37:19.910-05:00",
                                    "name": "sg-00004b4a49e24b9ff"
                                },
                                {
                                    "description": "launch-wizard-4 created 2018-03-20T13:45:11.721-05:00",
                                    "name": "sg-02419971da8f7872e"
                                },
                                {
                                    "description": "SG for AutoScale Group",
                                    "name": "sg-06a3092ac1fdfc419"
                                },
                                {
                                    "description": "launch-wizard-1 created 2018-03-18T14:29:23.439-05:00",
                                    "name": "sg-07a8d5b8803636fcc"
                                },
                                {
                                    "description": "launch-wizard-2 created 2018-03-18T14:32:32.770-05:00",
                                    "name": "sg-081aae6f8f5b4f495"
                                },
                                {
                                    "description": "default VPC security group",
                                    "name": "sg-090fe3844fa6abfb6"
                                },
                                {
                                    "description": "Created from the RDS Management Console: 2018/03/17 01:58:33",
                                    "name": "sg-0a401b0de0f86fcee"
                                },
                                {
                                    "description": "launch-wizard-5 created 2018-03-20T13:50:32.057-05:00",
                                    "name": "sg-0d9aa67d083634708"
                                },
                                {
                                    "description": "launch-wizard-6 created 2018-03-20T20:01:05.847-05:00",
                                    "name": "sg-0dd22da7d662ab2b8"
                                }
                            ],
                            "name": "vpc-e446c29f"
                        }
                    ],
                    "name": "us-east-1",
                    "placement_groups": [],
                    "images": [
                        {
                            "owner": "external",
                            "description": "Ubunut 16.04 USE1",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 8
                            },
                            "name": "ami-759bc50a"
                        },
                        {
                            "owner": "external",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 8
                            },
                            "name": "ami-456b493a",
                            "description": "Ubuntu 14.04 AWSUSE1"
                        },
                        {
                            "owner": "external",
                            "description": "RHEL 7.5 AWSUSE1",
                            "name": "ami-6871a115",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 10
                            }
                        },
                        {
                            "owner": "external",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 10
                            },
                            "name": "ami-f37b4b99",
                            "description": "RHEL6 AWSUSE1"
                        },
                        {
                            "owner": "external",
                            "description": "CentOS7 AWSUSE1",
                            "name": "ami-9887c6e7",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 8
                            }
                        },
                        {
                            "owner": "external",
                            "description": "CentOS6 AWSUSE1",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 8
                            },
                            "name": "ami-1585c46a"
                        },
                        {
                            "owner": "external",
                            "root_disk": null,
                            "name": "ami-b08dd3cf",
                            "description": "Ubuntu16.04 - 2"
                        },
                        {
                            "owner": "external",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 8
                            },
                            "description": "Ubuntu 16.04 - 3",
                            "name": "ami-749bc50b"
                        },
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
                            "name": "ami-d5bf2caa"
                        },
                        {
                            "owner": "external",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 10
                            },
                            "name": "ami-2051294a",
                            "description": "RHEL-7.2"
                        }
                    ],
                    "alarms": [],
                    "keypairs": [
                        {
                            "name": "None"
                        },
                        {
                            "name": "partsultd"
                        },
                        {
                            "name": "partsultdEC2Key"
                        }
                    ]
                },
                {
                    "clouds": [
                        {
                            "subnets": [
                                {
                                    "description": "172.31.32.0/20",
                                    "name": "subnet-6af8c827"
                                },
                                {
                                    "description": "172.31.16.0/20",
                                    "name": "subnet-5746832d"
                                },
                                {
                                    "description": "172.31.0.0/20",
                                    "name": "subnet-c569e4ad"
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
                                    "name": "sg-70f68b1b"
                                }
                            ],
                            "name": "vpc-463cb52e"
                        }
                    ],
                    "name": "us-east-2",
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
                            "name": "ami-77724e12"
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
                                    "description": "172.31.16.0/20",
                                    "name": "subnet-5ac28b3d"
                                },
                                {
                                    "description": "172.31.0.0/20",
                                    "name": "subnet-7b198320"
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
                                    "name": "sg-bc511fc5"
                                }
                            ],
                            "name": "vpc-9561dbf2"
                        }
                    ],
                    "name": "us-west-1",
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
                            "name": "ami-3b89905b"
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
                                    "description": "172.31.32.0/20",
                                    "name": "subnet-4f408404"
                                },
                                {
                                    "description": "172.31.16.0/20",
                                    "name": "subnet-eb872292"
                                },
                                {
                                    "description": "172.31.0.0/20",
                                    "name": "subnet-58cd4c02"
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
                                    "name": "sg-54cac02b"
                                }
                            ],
                            "name": "vpc-f8d0a181"
                        }
                    ],
                    "name": "us-west-2",
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
                            "name": "ami-5490ed2c"
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
        {
            "flavors": [
                {
                    "name": "c1.medium"
                },
                {
                    "name": "c1.xlarge"
                },
                {
                    "name": "c3.large"
                },
                {
                    "name": "c3.xlarge"
                },
                {
                    "name": "c3.2xlarge"
                },
                {
                    "name": "c3.4xlarge"
                },
                {
                    "name": "c3.8xlarge"
                },
                {
                    "name": "c4.large"
                },
                {
                    "name": "c4.xlarge"
                },
                {
                    "name": "c4.2xlarge"
                },
                {
                    "name": "c4.4xlarge"
                },
                {
                    "name": "c4.8xlarge"
                },
                {
                    "name": "c5.large"
                },
                {
                    "name": "c5.xlarge"
                },
                {
                    "name": "c5.2xlarge"
                },
                {
                    "name": "c5.4xlarge"
                },
                {
                    "name": "c5.9xlarge"
                },
                {
                    "name": "c5.18xlarge"
                },
                {
                    "name": "c5d.large"
                },
                {
                    "name": "c5d.xlarge"
                },
                {
                    "name": "c5d.2xlarge"
                },
                {
                    "name": "c5d.4xlarge"
                },
                {
                    "name": "c5d.9xlarge"
                },
                {
                    "name": "c5d.18xlarge"
                },
                {
                    "name": "cc2.8xlarge"
                },
                {
                    "name": "cr1.8xlarge"
                },
                {
                    "name": "d2.xlarge"
                },
                {
                    "name": "d2.2xlarge"
                },
                {
                    "name": "d2.4xlarge"
                },
                {
                    "name": "d2.8xlarge"
                },
                {
                    "name": "f1.2xlarge"
                },
                {
                    "name": "f1.16xlarge"
                },
                {
                    "name": "g2.2xlarge"
                },
                {
                    "name": "g2.8xlarge"
                },
                {
                    "name": "g3.4xlarge"
                },
                {
                    "name": "g3.8xlarge"
                },
                {
                    "name": "g3.16xlarge"
                },
                {
                    "name": "h1.2xlarge"
                },
                {
                    "name": "h1.4xlarge"
                },
                {
                    "name": "h1.8xlarge"
                },
                {
                    "name": "h1.16xlarge"
                },
                {
                    "name": "hs1.8xlarge"
                },
                {
                    "name": "i2.xlarge"
                },
                {
                    "name": "i2.2xlarge"
                },
                {
                    "name": "i2.4xlarge"
                },
                {
                    "name": "i2.8xlarge"
                },
                {
                    "name": "i3.large"
                },
                {
                    "name": "i3.metal"
                },
                {
                    "name": "i3.xlarge"
                },
                {
                    "name": "i3.2xlarge"
                },
                {
                    "name": "i3.4xlarge"
                },
                {
                    "name": "i3.8xlarge"
                },
                {
                    "name": "i3.16xlarge"
                },
                {
                    "name": "m1.small"
                },
                {
                    "name": "m1.medium"
                },
                {
                    "name": "m1.large"
                },
                {
                    "name": "m1.xlarge"
                },
                {
                    "name": "m2.xlarge"
                },
                {
                    "name": "m2.2xlarge"
                },
                {
                    "name": "m2.4xlarge"
                },
                {
                    "name": "m3.medium"
                },
                {
                    "name": "m3.large"
                },
                {
                    "name": "m3.xlarge"
                },
                {
                    "name": "m3.2xlarge"
                },
                {
                    "name": "m4.large"
                },
                {
                    "name": "m4.xlarge"
                },
                {
                    "name": "m4.2xlarge"
                },
                {
                    "name": "m4.4xlarge"
                },
                {
                    "name": "m4.10xlarge"
                },
                {
                    "name": "m4.16xlarge"
                },
                {
                    "name": "m5.large"
                },
                {
                    "name": "m5.xlarge"
                },
                {
                    "name": "m5.2xlarge"
                },
                {
                    "name": "m5.4xlarge"
                },
                {
                    "name": "m5.12xlarge"
                },
                {
                    "name": "m5.24xlarge"
                },
                {
                    "name": "m5d.large"
                },
                {
                    "name": "m5d.xlarge"
                },
                {
                    "name": "m5d.2xlarge"
                },
                {
                    "name": "m5d.4xlarge"
                },
                {
                    "name": "m5d.12xlarge"
                },
                {
                    "name": "m5d.24xlarge"
                },
                {
                    "name": "p2.xlarge"
                },
                {
                    "name": "p2.8xlarge"
                },
                {
                    "name": "p2.16xlarge"
                },
                {
                    "name": "r3.large"
                },
                {
                    "name": "r3.xlarge"
                },
                {
                    "name": "r3.2xlarge"
                },
                {
                    "name": "r3.4xlarge"
                },
                {
                    "name": "r3.8xlarge"
                },
                {
                    "name": "r4.large"
                },
                {
                    "name": "r4.xlarge"
                },
                {
                    "name": "r4.2xlarge"
                },
                {
                    "name": "r4.4xlarge"
                },
                {
                    "name": "r4.8xlarge"
                },
                {
                    "name": "r4.16xlarge"
                },
                {
                    "name": "t1.micro"
                },
                {
                    "name": "t2.micro"
                },
                {
                    "name": "t2.small"
                },
                {
                    "name": "t2.medium"
                },
                {
                    "name": "t2.large"
                },
                {
                    "name": "t2.xlarge"
                },
                {
                    "name": "t2.2xlarge"
                },
                {
                    "name": "x1.16xlarge"
                },
                {
                    "name": "x1.32xlarge"
                },
                {
                    "name": "x1e.xlarge"
                },
                {
                    "name": "x1e.2xlarge"
                },
                {
                    "name": "x1e.4xlarge"
                },
                {
                    "name": "x1e.8xlarge"
                },
                {
                    "name": "x1e.16xlarge"
                },
                {
                    "name": "x1e.32xlarge"
                }
            ],
            "name": "Windows Compute",
            "roles": [
                {
                    "name": "None"
                },
                {
                    "name": "AutoScaleS3Access"
                },
                {
                    "name": "MeyerTest"
                },
                {
                    "name": "test-chris"
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
                                },
                                {
                                    "description": "172.31.32.0/20",
                                    "name": "subnet-f2e2bcbb"
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
                            "name": "Windows Compute"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k08 Std-Win2k8 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-c57de7a3"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k14 Std-Win2k12 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-c671eba0"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k12 Std-Win2k12",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-3e6ef458"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k12 Ent-Win2k8 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-5e7ce638"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k14 Ent-Win2k12 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-7b2eb41d"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k12 Std-Win2k8 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-2572e843"
                        },
                        {
                            "owner": "user",
                            "description": "Microsoft Windows Server 2016 with Desktop Experience Locale",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 30
                            },
                            "name": "ami-ec279c8a"
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
                            "name": "Windows Compute"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k08 Std-Win2k8 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-fc4ded92"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k12 Std-Win2k8 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-b34fefdd"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k12 Std-Win2k12",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-c64fefa8"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k12 Ent-Win2k8 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-e34fef8d"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k14 Ent-Win2k12 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-2b55f545"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k14 Std-Win2k12 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-cd4deda3"
                        },
                        {
                            "owner": "user",
                            "description": "Microsoft Windows Server 2016 with Desktop Experience Locale",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 30
                            },
                            "name": "ami-e8ef4986"
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
                                    "name": "subnet-d310e69f"
                                },
                                {
                                    "description": "172.31.16.0/20",
                                    "name": "subnet-f855d390"
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
                                    "name": "sg-d39d11b8"
                                }
                            ],
                            "name": "vpc-1585067d"
                        }
                    ],
                    "name": "ap-south-1",
                    "placement_groups": [],
                    "images": [
                        {
                            "owner": "user",
                            "description": "Latest Amazon AMI",
                            "name": "Windows Compute"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k08 Std-Win2k8 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-5fb4e330"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k12 Std-Win2k8 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-35b6e15a"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k12 Ent-Win2k8 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-edb3e482"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k14 Ent-Win2k12 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-a6bcebc9"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k12 Std-Win2k12",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-69b3e406"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k14 Std-Win2k12 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-8cb5e2e3"
                        },
                        {
                            "owner": "user",
                            "description": "Microsoft Windows Server 2016 with Desktop Experience Locale",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 30
                            },
                            "name": "ami-100f467f"
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
                                    "description": "172.31.16.0/20",
                                    "name": "subnet-15dc9372"
                                },
                                {
                                    "description": "172.31.0.0/20",
                                    "name": "subnet-2d60776b"
                                },
                                {
                                    "description": "172.31.32.0/20",
                                    "name": "subnet-22b6c96b"
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
                                    "name": "sg-e3a2269a"
                                }
                            ],
                            "name": "vpc-b00a89d7"
                        }
                    ],
                    "name": "ap-southeast-1",
                    "placement_groups": [],
                    "images": [
                        {
                            "owner": "user",
                            "description": "Latest Amazon AMI",
                            "name": "Windows Compute"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k08 Std-Win2k8 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-39364b45"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k14 Ent-Win2k12 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-0d097471"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k12 Std-Win2k12",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-11275a6d"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k12 Ent-Win2k8 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-95304de9"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k14 Std-Win2k12 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-9d2c51e1"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k12 Std-Win2k8 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-93334eef"
                        },
                        {
                            "owner": "user",
                            "description": "Microsoft Windows Server 2016 with Desktop Experience Locale",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 30
                            },
                            "name": "ami-870855e4"
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
                                    "description": "172.31.32.0/20",
                                    "name": "subnet-66492f2f"
                                },
                                {
                                    "description": "172.31.0.0/20",
                                    "name": "subnet-dfc5b0b8"
                                },
                                {
                                    "description": "172.31.16.0/20",
                                    "name": "subnet-3a699f62"
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
                                    "name": "sg-5b299b22"
                                }
                            ],
                            "name": "vpc-65329802"
                        }
                    ],
                    "name": "ap-southeast-2",
                    "placement_groups": [],
                    "images": [
                        {
                            "owner": "user",
                            "description": "Latest Amazon AMI",
                            "name": "Windows Compute"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k12 Std-Win2k8 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-cda15daf"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k08 Std-Win2k8 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-85a65ae7"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k12 Ent-Win2k8 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-01a75b63"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k14 Ent-Win2k12 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-0d8d716f"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k12 Std-Win2k12",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-9b9965f9"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k14 Std-Win2k12 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-629e6200"
                        },
                        {
                            "owner": "user",
                            "description": "Microsoft Windows Server 2016 with Desktop Experience Locale",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 30
                            },
                            "name": "ami-de5eabbc"
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
                                    "description": "172.31.16.0/20",
                                    "name": "subnet-3119e159"
                                },
                                {
                                    "description": "172.31.0.0/20",
                                    "name": "subnet-823b2cf9"
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
                                    "name": "sg-c09fa1a8"
                                }
                            ],
                            "name": "vpc-9e3fccf6"
                        }
                    ],
                    "name": "ca-central-1",
                    "placement_groups": [],
                    "images": [
                        {
                            "owner": "user",
                            "description": "Latest Amazon AMI",
                            "name": "Windows Compute"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k08 Std-Win2k8 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-3fb5305b"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k12 Ent-Win2k8 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-aab431ce"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k12 Std-Win2k12",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-bab431de"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k12 Std-Win2k8 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-3bb5305f"
                        },
                        {
                            "owner": "user",
                            "description": "Microsoft Windows Server 2016 with Desktop Experience Locale",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 30
                            },
                            "name": "ami-5e3b803a"
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
                                    "description": "172.31.16.0/20",
                                    "name": "subnet-1557147e"
                                },
                                {
                                    "description": "172.31.32.0/20",
                                    "name": "subnet-454af238"
                                },
                                {
                                    "description": "172.31.0.0/20",
                                    "name": "subnet-07029b4a"
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
                                    "name": "sg-8a14a6e7"
                                }
                            ],
                            "name": "vpc-70e7671b"
                        }
                    ],
                    "name": "eu-central-1",
                    "placement_groups": [],
                    "images": [
                        {
                            "owner": "user",
                            "description": "Latest Amazon AMI",
                            "name": "Windows Compute"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k12 Std-Win2k8 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-e3079a8c"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k08 Std-Win2k8 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-98079af7"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k12 Ent-Win2k8 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-3c039e53"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k12 Std-Win2k12",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-c53ca1aa"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k14 Std-Win2k12 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-f1039e9e"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k14 Ent-Win2k12 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-1a31ac75"
                        },
                        {
                            "owner": "user",
                            "description": "Microsoft Windows Server 2016 with Desktop Experience Locale",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 30
                            },
                            "name": "ami-da9b14b5"
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
                                    "description": "172.31.16.0/20",
                                    "name": "subnet-836db4cb"
                                },
                                {
                                    "description": "172.31.0.0/20",
                                    "name": "subnet-3948835f"
                                },
                                {
                                    "description": "172.31.32.0/20",
                                    "name": "subnet-9b5d49c0"
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
                                    "name": "sg-3e154144"
                                }
                            ],
                            "name": "vpc-2b5fe54d"
                        }
                    ],
                    "name": "eu-west-1",
                    "placement_groups": [],
                    "images": [
                        {
                            "owner": "user",
                            "description": "Latest Amazon AMI",
                            "name": "Windows Compute"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k08 Std-Win2k8 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-17b62a6e"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k12 Std-Win2k8 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-0db72b74"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k12 Ent-Win2k8 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-76b62a0f"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k14 Std-Win2k12 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-61ad3118"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k12 Std-Win2k12",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-b9a935c0"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k14 Ent-Win2k12 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-c558c4bc"
                        },
                        {
                            "owner": "user",
                            "description": "Microsoft Windows Server 2016 with Desktop Experience Locale",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 30
                            },
                            "name": "ami-e055e899"
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
                                    "description": "172.31.16.0/20",
                                    "name": "subnet-9f7e9fe5"
                                },
                                {
                                    "description": "172.31.32.0/20",
                                    "name": "subnet-fae6d0b7"
                                },
                                {
                                    "description": "172.31.0.0/20",
                                    "name": "subnet-286fc141"
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
                                    "name": "sg-e98e8581"
                                }
                            ],
                            "name": "vpc-2b1fda43"
                        }
                    ],
                    "name": "eu-west-2",
                    "placement_groups": [],
                    "images": [
                        {
                            "owner": "user",
                            "description": "Latest Amazon AMI",
                            "name": "Windows Compute"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k08 Std-Win2k8 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-87667de3"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k12 Std-Win2k8 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-58677c3c"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k12 Std-Win2k12",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-0b647f6f"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k12 Ent-Win2k8 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-c0677ca4"
                        },
                        {
                            "owner": "user",
                            "description": "Microsoft Windows Server 2016 with Desktop Experience Locale",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 30
                            },
                            "name": "ami-78657b1c"
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
                                    "description": "172.31.16.0/20",
                                    "name": "subnet-d134e3aa"
                                },
                                {
                                    "description": "172.31.32.0/20",
                                    "name": "subnet-c70fe38a"
                                },
                                {
                                    "description": "172.31.0.0/20",
                                    "name": "subnet-b909b4d0"
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
                                    "name": "sg-3d155254"
                                }
                            ],
                            "name": "vpc-ac15aec5"
                        }
                    ],
                    "name": "eu-west-3",
                    "placement_groups": [],
                    "images": [
                        {
                            "owner": "user",
                            "description": "Latest Amazon AMI",
                            "name": "Windows Compute"
                        },
                        {
                            "owner": "user",
                            "description": "Microsoft Windows Server 2016 with Desktop Experience Locale",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 30
                            },
                            "name": "ami-2e67d053"
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
                                    "name": "subnet-35133052"
                                },
                                {
                                    "description": "172.31.16.0/20",
                                    "name": "subnet-aa3001f2"
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
                                    "name": "sg-39b32a5f"
                                }
                            ],
                            "name": "vpc-050fa062"
                        }
                    ],
                    "name": "sa-east-1",
                    "placement_groups": [],
                    "images": [
                        {
                            "owner": "user",
                            "description": "Latest Amazon AMI",
                            "name": "Windows Compute"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k08 Std-Win2k8 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-f5c58799"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k12 Std-Win2k8 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-5bca8837"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k14 Std-Win2k12 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-faca8896"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k14 Ent-Win2k12 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-bdc98bd1"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k12 Ent-Win2k8 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-89c587e5"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k12 Std-Win2k12",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-accb89c0"
                        },
                        {
                            "owner": "user",
                            "description": "Microsoft Windows Server 2016 with Desktop Experience Locale",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 30
                            },
                            "name": "ami-41bffb2d"
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
                                    "description": "Private subnet",
                                    "name": "subnet-0f4d827f0959c45a4"
                                },
                                {
                                    "description": "Public subnet",
                                    "name": "subnet-0d3033d2b8bf13f12"
                                }
                            ],
                            "description": "VPC1",
                            "target_groups": [],
                            "load_balancers": [],
                            "security_groups": [
                                {
                                    "name": "Automatic"
                                },
                                {
                                    "description": "default VPC security group",
                                    "name": "sg-0c48ef851d23ee3cc"
                                }
                            ],
                            "name": "vpc-0ad1a5959b295f65e"
                        },
                        {
                            "subnets": [
                                {
                                    "description": "172.31.64.0/20",
                                    "name": "subnet-f56242ca"
                                },
                                {
                                    "description": "172.31.0.0/20",
                                    "name": "subnet-32a9bc56"
                                },
                                {
                                    "description": "172.31.16.0/20",
                                    "name": "subnet-09e41a43"
                                },
                                {
                                    "description": "172.31.32.0/20",
                                    "name": "subnet-4ec7ed13"
                                },
                                {
                                    "description": "172.31.48.0/20",
                                    "name": "subnet-772d8978"
                                },
                                {
                                    "description": "172.31.80.0/20",
                                    "name": "subnet-c4f5c1eb"
                                }
                            ],
                            "description": "172.31.0.0/16",
                            "target_groups": [
                                {
                                    "default_port": 80,
                                    "protocol": "HTTP",
                                    "target_type": "instance",
                                    "arn": "arn:aws:elasticloadbalancing:us-east-1:636588615608:targetgroup/partsultdLBRouting/e1031aa116bf033f",
                                    "name": "partsultdLBRouting"
                                }
                            ],
                            "load_balancers": [],
                            "security_groups": [
                                {
                                    "name": "Automatic"
                                },
                                {
                                    "description": "This security group was generated by AWS Marketplace and is based on recommended settings for Red Hat Enterprise Linux (RHEL) 6 (HVM) version 6.7_HVM_20160219 provided by Amazon Web Services",
                                    "name": "sg-06f2b8b511216c8f3"
                                },
                                {
                                    "description": "This security group was generated by AWS Marketplace and is based on recommended settings for CentOS 7 (x86_64) - with Updates HVM version 1805_01 provided by Centos.org",
                                    "name": "sg-0752c07ce1afb7f9a"
                                },
                                {
                                    "description": "Enable SSH access via port 22",
                                    "name": "sg-092de9abb7c435e37"
                                },
                                {
                                    "description": "This security group was generated by AWS Marketplace and is based on recommended settings for Red Hat Enterprise Linux (RHEL) 6 version 6.5_GA provided by Amazon Web Services",
                                    "name": "sg-0db584c264083fbd2"
                                },
                                {
                                    "description": "This security group was generated by AWS Marketplace and is based on recommended settings for CentOS 6 (x86_64) - with Updates HVM version 1805_01 provided by Centos.org",
                                    "name": "sg-0f53c2fa9738d1f55"
                                },
                                {
                                    "description": "default VPC security group",
                                    "name": "sg-6969051f"
                                }
                            ],
                            "name": "vpc-711a9f0a"
                        },
                        {
                            "subnets": [
                                {
                                    "description": "Public Subnet #2",
                                    "name": "subnet-01f48b41fd743c464"
                                },
                                {
                                    "description": "Private subnet",
                                    "name": "subnet-072d27171887b3f3b"
                                },
                                {
                                    "description": "Public subnet",
                                    "name": "subnet-08c8e59037abe931d"
                                },
                                {
                                    "description": "Private subnet #2",
                                    "name": "subnet-00175e924b602a94f"
                                }
                            ],
                            "description": "VPC2",
                            "target_groups": [
                                {
                                    "default_port": 80,
                                    "protocol": "HTTP",
                                    "target_type": "instance",
                                    "arn": "arn:aws:elasticloadbalancing:us-east-1:636588615608:targetgroup/partsultdASGGroup/21bf3b5ba88c8714",
                                    "name": "partsultdASGGroup"
                                }
                            ],
                            "load_balancers": [],
                            "security_groups": [
                                {
                                    "name": "Automatic"
                                },
                                {
                                    "description": "launch-wizard-3 created 2018-03-18T15:37:19.910-05:00",
                                    "name": "sg-00004b4a49e24b9ff"
                                },
                                {
                                    "description": "launch-wizard-4 created 2018-03-20T13:45:11.721-05:00",
                                    "name": "sg-02419971da8f7872e"
                                },
                                {
                                    "description": "SG for AutoScale Group",
                                    "name": "sg-06a3092ac1fdfc419"
                                },
                                {
                                    "description": "launch-wizard-1 created 2018-03-18T14:29:23.439-05:00",
                                    "name": "sg-07a8d5b8803636fcc"
                                },
                                {
                                    "description": "launch-wizard-2 created 2018-03-18T14:32:32.770-05:00",
                                    "name": "sg-081aae6f8f5b4f495"
                                },
                                {
                                    "description": "default VPC security group",
                                    "name": "sg-090fe3844fa6abfb6"
                                },
                                {
                                    "description": "Created from the RDS Management Console: 2018/03/17 01:58:33",
                                    "name": "sg-0a401b0de0f86fcee"
                                },
                                {
                                    "description": "launch-wizard-5 created 2018-03-20T13:50:32.057-05:00",
                                    "name": "sg-0d9aa67d083634708"
                                },
                                {
                                    "description": "launch-wizard-6 created 2018-03-20T20:01:05.847-05:00",
                                    "name": "sg-0dd22da7d662ab2b8"
                                }
                            ],
                            "name": "vpc-e446c29f"
                        }
                    ],
                    "name": "us-east-1",
                    "placement_groups": [],
                    "images": [
                        {
                            "owner": "external",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 30
                            },
                            "description": "Win2k12 R2 Base",
                            "name": "ami-60093e1f"
                        },
                        {
                            "owner": "user",
                            "description": "Latest Amazon AMI",
                            "name": "Windows Compute"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k08 Std-Win2k8 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-f3052289"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k12 Std-Win2k8 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-2e0b2c54"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k12 Std-Win2k12",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-211c3b5b"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k14 Std-Win2k12 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-d91334a3"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k12 Ent-Win2k8 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-42391e38"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k14 Ent-Win2k12 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-f2f0d788"
                        },
                        {
                            "owner": "user",
                            "description": "Microsoft Windows Server 2016 with Desktop Experience Locale",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 30
                            },
                            "name": "ami-08910872"
                        }
                    ],
                    "alarms": [],
                    "keypairs": [
                        {
                            "name": "None"
                        },
                        {
                            "name": "partsultd"
                        },
                        {
                            "name": "partsultdEC2Key"
                        }
                    ]
                },
                {
                    "clouds": [
                        {
                            "subnets": [
                                {
                                    "description": "172.31.32.0/20",
                                    "name": "subnet-6af8c827"
                                },
                                {
                                    "description": "172.31.16.0/20",
                                    "name": "subnet-5746832d"
                                },
                                {
                                    "description": "172.31.0.0/20",
                                    "name": "subnet-c569e4ad"
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
                                    "name": "sg-70f68b1b"
                                }
                            ],
                            "name": "vpc-463cb52e"
                        }
                    ],
                    "name": "us-east-2",
                    "placement_groups": [],
                    "images": [
                        {
                            "owner": "user",
                            "description": "Latest Amazon AMI",
                            "name": "Windows Compute"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k08 Std-Win2k8 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-da476dbf"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k12 Std-Win2k8 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-d9476dbc"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k14 Std-Win2k12 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-c7466ca2"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k14 Ent-Win2k12 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-27597342"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k12 Std-Win2k12",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-da446ebf"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k12 Ent-Win2k8 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-3b476d5e"
                        },
                        {
                            "owner": "user",
                            "description": "Microsoft Windows Server 2016 with Desktop Experience Locale",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 30
                            },
                            "name": "ami-21587144"
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
                                    "description": "172.31.16.0/20",
                                    "name": "subnet-5ac28b3d"
                                },
                                {
                                    "description": "172.31.0.0/20",
                                    "name": "subnet-7b198320"
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
                                    "name": "sg-bc511fc5"
                                }
                            ],
                            "name": "vpc-9561dbf2"
                        }
                    ],
                    "name": "us-west-1",
                    "placement_groups": [],
                    "images": [
                        {
                            "owner": "user",
                            "description": "Latest Amazon AMI",
                            "name": "Windows Compute"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k08 Std-Win2k8 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-55838035"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k12 Std-Win2k12",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-9d8083fd"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k14 Ent-Win2k12 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-a08586c0"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k12 Ent-Win2k8 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-1b82817b"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k12 Std-Win2k8 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-19828179"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k14 Std-Win2k12 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-ed81828d"
                        },
                        {
                            "owner": "user",
                            "description": "Microsoft Windows Server 2016 with Desktop Experience Locale",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 30
                            },
                            "name": "ami-406d5720"
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
                                    "description": "172.31.32.0/20",
                                    "name": "subnet-4f408404"
                                },
                                {
                                    "description": "172.31.16.0/20",
                                    "name": "subnet-eb872292"
                                },
                                {
                                    "description": "172.31.0.0/20",
                                    "name": "subnet-58cd4c02"
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
                                    "name": "sg-54cac02b"
                                }
                            ],
                            "name": "vpc-f8d0a181"
                        }
                    ],
                    "name": "us-west-2",
                    "placement_groups": [],
                    "images": [
                        {
                            "owner": "user",
                            "description": "Latest Amazon AMI",
                            "name": "Windows Compute"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k08 Std-Win2k8 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-add061d5"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k12 Std-Win2k8 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-bed160c6"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k12 Ent-Win2k8 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-2cd36254"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k12 Std-Win2k12",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-aedd6cd6"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k14 Ent-Win2k12 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-04c9787c"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k14 Std-Win2k12 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-90d160e8"
                        },
                        {
                            "owner": "user",
                            "description": "Microsoft Windows Server 2016 with Desktop Experience Locale",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 30
                            },
                            "name": "ami-f6d8008e"
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
            "appliance_id": "i-q428yw",
            "name": "us-east-1",
            "vpc": "vpc-e446c29f"
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
  - Invalid Data (400)
  - Conflict (409)

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
        },
        {
            "started": "2018-07-26 18:53:27.827179",
            "state": "up",
            "completed": "2018-07-26 19:07:06.443650"
        },
        {
            "started": "2018-07-26 19:07:06.443650",
            "state": "down",
            "completed": "2018-07-26 19:09:30.067475"
        },
        {
            "started": "2018-07-26 19:09:30.067475",
            "state": "up",
            "completed": "2018-08-28 10:08:56.914918"
        },
        {
            "started": "2018-08-28 10:08:56.914918",
            "state": "down",
            "completed": "2018-09-04 21:28:32.573472"
        },
        {
            "started": "2018-09-04 21:28:32.573472",
            "state": "up",
            "completed": "2018-09-24 16:09:01.728550"
        },
        {
            "started": "2018-09-24 16:09:01.728550",
            "state": "down",
            "completed": "2018-09-24 16:21:34.906171"
        },
        {
            "started": "2018-09-24 16:21:34.906171",
            "state": "up"
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
                },
                {
                    "name": "ap-south-1"
                },
                {
                    "name": "ap-southeast-1"
                },
                {
                    "name": "ap-southeast-2"
                },
                {
                    "name": "ca-central-1"
                },
                {
                    "name": "eu-central-1"
                },
                {
                    "name": "eu-west-1"
                },
                {
                    "name": "eu-west-2"
                },
                {
                    "name": "eu-west-3"
                },
                {
                    "name": "sa-east-1"
                },
                {
                    "name": "us-east-1"
                },
                {
                    "name": "us-east-2"
                },
                {
                    "name": "us-west-1"
                },
                {
                    "name": "us-west-2"
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
                },
                {
                    "name": "ap-south-1"
                },
                {
                    "clusters": [],
                    "name": "ap-southeast-1"
                },
                {
                    "clusters": [],
                    "name": "ap-southeast-2"
                },
                {
                    "clusters": [],
                    "name": "ca-central-1"
                },
                {
                    "clusters": [],
                    "name": "eu-central-1"
                },
                {
                    "clusters": [],
                    "name": "eu-west-1"
                },
                {
                    "clusters": [],
                    "name": "eu-west-2"
                },
                {
                    "clusters": [],
                    "name": "eu-west-3"
                },
                {
                    "name": "sa-east-1"
                },
                {
                    "clusters": [],
                    "name": "us-east-1"
                },
                {
                    "clusters": [],
                    "name": "us-east-2"
                },
                {
                    "clusters": [],
                    "name": "us-west-1"
                },
                {
                    "clusters": [],
                    "name": "us-west-2"
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
                },
                {
                    "name": "c3.large"
                },
                {
                    "name": "c3.xlarge"
                },
                {
                    "name": "c3.2xlarge"
                },
                {
                    "name": "c3.4xlarge"
                },
                {
                    "name": "c3.8xlarge"
                },
                {
                    "name": "c4.large"
                },
                {
                    "name": "c4.xlarge"
                },
                {
                    "name": "c4.2xlarge"
                },
                {
                    "name": "c4.4xlarge"
                },
                {
                    "name": "c4.8xlarge"
                },
                {
                    "name": "c5.large"
                },
                {
                    "name": "c5.xlarge"
                },
                {
                    "name": "c5.2xlarge"
                },
                {
                    "name": "c5.4xlarge"
                },
                {
                    "name": "c5.9xlarge"
                },
                {
                    "name": "c5.18xlarge"
                },
                {
                    "name": "c5d.large"
                },
                {
                    "name": "c5d.xlarge"
                },
                {
                    "name": "c5d.2xlarge"
                },
                {
                    "name": "c5d.4xlarge"
                },
                {
                    "name": "c5d.9xlarge"
                },
                {
                    "name": "c5d.18xlarge"
                },
                {
                    "name": "cc2.8xlarge"
                },
                {
                    "name": "cr1.8xlarge"
                },
                {
                    "name": "d2.xlarge"
                },
                {
                    "name": "d2.2xlarge"
                },
                {
                    "name": "d2.4xlarge"
                },
                {
                    "name": "d2.8xlarge"
                },
                {
                    "name": "f1.2xlarge"
                },
                {
                    "name": "f1.16xlarge"
                },
                {
                    "name": "g2.2xlarge"
                },
                {
                    "name": "g2.8xlarge"
                },
                {
                    "name": "g3.4xlarge"
                },
                {
                    "name": "g3.8xlarge"
                },
                {
                    "name": "g3.16xlarge"
                },
                {
                    "name": "h1.2xlarge"
                },
                {
                    "name": "h1.4xlarge"
                },
                {
                    "name": "h1.8xlarge"
                },
                {
                    "name": "h1.16xlarge"
                },
                {
                    "name": "hs1.8xlarge"
                },
                {
                    "name": "i2.xlarge"
                },
                {
                    "name": "i2.2xlarge"
                },
                {
                    "name": "i2.4xlarge"
                },
                {
                    "name": "i2.8xlarge"
                },
                {
                    "name": "i3.large"
                },
                {
                    "name": "i3.metal"
                },
                {
                    "name": "i3.xlarge"
                },
                {
                    "name": "i3.2xlarge"
                },
                {
                    "name": "i3.4xlarge"
                },
                {
                    "name": "i3.8xlarge"
                },
                {
                    "name": "i3.16xlarge"
                },
                {
                    "name": "m1.small"
                },
                {
                    "name": "m1.medium"
                },
                {
                    "name": "m1.large"
                },
                {
                    "name": "m1.xlarge"
                },
                {
                    "name": "m2.xlarge"
                },
                {
                    "name": "m2.2xlarge"
                },
                {
                    "name": "m2.4xlarge"
                },
                {
                    "name": "m3.medium"
                },
                {
                    "name": "m3.large"
                },
                {
                    "name": "m3.xlarge"
                },
                {
                    "name": "m3.2xlarge"
                },
                {
                    "name": "m4.large"
                },
                {
                    "name": "m4.xlarge"
                },
                {
                    "name": "m4.2xlarge"
                },
                {
                    "name": "m4.4xlarge"
                },
                {
                    "name": "m4.10xlarge"
                },
                {
                    "name": "m4.16xlarge"
                },
                {
                    "name": "m5.large"
                },
                {
                    "name": "m5.xlarge"
                },
                {
                    "name": "m5.2xlarge"
                },
                {
                    "name": "m5.4xlarge"
                },
                {
                    "name": "m5.12xlarge"
                },
                {
                    "name": "m5.24xlarge"
                },
                {
                    "name": "m5d.large"
                },
                {
                    "name": "m5d.xlarge"
                },
                {
                    "name": "m5d.2xlarge"
                },
                {
                    "name": "m5d.4xlarge"
                },
                {
                    "name": "m5d.12xlarge"
                },
                {
                    "name": "m5d.24xlarge"
                },
                {
                    "name": "p2.xlarge"
                },
                {
                    "name": "p2.8xlarge"
                },
                {
                    "name": "p2.16xlarge"
                },
                {
                    "name": "r3.large"
                },
                {
                    "name": "r3.xlarge"
                },
                {
                    "name": "r3.2xlarge"
                },
                {
                    "name": "r3.4xlarge"
                },
                {
                    "name": "r3.8xlarge"
                },
                {
                    "name": "r4.large"
                },
                {
                    "name": "r4.xlarge"
                },
                {
                    "name": "r4.2xlarge"
                },
                {
                    "name": "r4.4xlarge"
                },
                {
                    "name": "r4.8xlarge"
                },
                {
                    "name": "r4.16xlarge"
                },
                {
                    "name": "t1.micro"
                },
                {
                    "name": "t2.micro"
                },
                {
                    "name": "t2.small"
                },
                {
                    "name": "t2.medium"
                },
                {
                    "name": "t2.large"
                },
                {
                    "name": "t2.xlarge"
                },
                {
                    "name": "t2.2xlarge"
                },
                {
                    "name": "x1.16xlarge"
                },
                {
                    "name": "x1.32xlarge"
                },
                {
                    "name": "x1e.xlarge"
                },
                {
                    "name": "x1e.2xlarge"
                },
                {
                    "name": "x1e.4xlarge"
                },
                {
                    "name": "x1e.8xlarge"
                },
                {
                    "name": "x1e.16xlarge"
                },
                {
                    "name": "x1e.32xlarge"
                }
            ],
            "name": "Linux Compute",
            "roles": [
                {
                    "name": "None"
                },
                {
                    "name": "AutoScaleS3Access"
                },
                {
                    "name": "MeyerTest"
                },
                {
                    "name": "test-chris"
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
                                },
                                {
                                    "description": "172.31.32.0/20",
                                    "name": "subnet-f2e2bcbb"
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
                },
                {
                    "clouds": [
                        {
                            "subnets": [
                                {
                                    "description": "172.31.0.0/20",
                                    "name": "subnet-d310e69f"
                                },
                                {
                                    "description": "172.31.16.0/20",
                                    "name": "subnet-f855d390"
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
                                    "name": "sg-d39d11b8"
                                }
                            ],
                            "name": "vpc-1585067d"
                        }
                    ],
                    "name": "ap-south-1",
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
                            "name": "ami-48301d27"
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
                                    "description": "172.31.16.0/20",
                                    "name": "subnet-15dc9372"
                                },
                                {
                                    "description": "172.31.0.0/20",
                                    "name": "subnet-2d60776b"
                                },
                                {
                                    "description": "172.31.32.0/20",
                                    "name": "subnet-22b6c96b"
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
                                    "name": "sg-e3a2269a"
                                }
                            ],
                            "name": "vpc-b00a89d7"
                        }
                    ],
                    "name": "ap-southeast-1",
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
                            "name": "ami-da6151a6"
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
                                    "description": "172.31.32.0/20",
                                    "name": "subnet-66492f2f"
                                },
                                {
                                    "description": "172.31.0.0/20",
                                    "name": "subnet-dfc5b0b8"
                                },
                                {
                                    "description": "172.31.16.0/20",
                                    "name": "subnet-3a699f62"
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
                                    "name": "sg-5b299b22"
                                }
                            ],
                            "name": "vpc-65329802"
                        }
                    ],
                    "name": "ap-southeast-2",
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
                            "name": "ami-0d13c26f"
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
                                    "description": "172.31.16.0/20",
                                    "name": "subnet-3119e159"
                                },
                                {
                                    "description": "172.31.0.0/20",
                                    "name": "subnet-823b2cf9"
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
                                    "name": "sg-c09fa1a8"
                                }
                            ],
                            "name": "vpc-9e3fccf6"
                        }
                    ],
                    "name": "ca-central-1",
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
                            "name": "ami-456aea21"
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
                                    "description": "172.31.16.0/20",
                                    "name": "subnet-1557147e"
                                },
                                {
                                    "description": "172.31.32.0/20",
                                    "name": "subnet-454af238"
                                },
                                {
                                    "description": "172.31.0.0/20",
                                    "name": "subnet-07029b4a"
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
                                    "name": "sg-8a14a6e7"
                                }
                            ],
                            "name": "vpc-70e7671b"
                        }
                    ],
                    "name": "eu-central-1",
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
                            "name": "ami-9a183671"
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
                                    "description": "172.31.16.0/20",
                                    "name": "subnet-836db4cb"
                                },
                                {
                                    "description": "172.31.0.0/20",
                                    "name": "subnet-3948835f"
                                },
                                {
                                    "description": "172.31.32.0/20",
                                    "name": "subnet-9b5d49c0"
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
                                    "name": "sg-3e154144"
                                }
                            ],
                            "name": "vpc-2b5fe54d"
                        }
                    ],
                    "name": "eu-west-1",
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
                            "name": "ami-4c457735"
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
                                    "description": "172.31.16.0/20",
                                    "name": "subnet-9f7e9fe5"
                                },
                                {
                                    "description": "172.31.32.0/20",
                                    "name": "subnet-fae6d0b7"
                                },
                                {
                                    "description": "172.31.0.0/20",
                                    "name": "subnet-286fc141"
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
                                    "name": "sg-e98e8581"
                                }
                            ],
                            "name": "vpc-2b1fda43"
                        }
                    ],
                    "name": "eu-west-2",
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
                            "name": "ami-4726cb20"
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
                                    "description": "172.31.16.0/20",
                                    "name": "subnet-d134e3aa"
                                },
                                {
                                    "description": "172.31.32.0/20",
                                    "name": "subnet-c70fe38a"
                                },
                                {
                                    "description": "172.31.0.0/20",
                                    "name": "subnet-b909b4d0"
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
                                    "name": "sg-3d155254"
                                }
                            ],
                            "name": "vpc-ac15aec5"
                        }
                    ],
                    "name": "eu-west-3",
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
                            "name": "ami-6276c71f"
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
                                    "name": "subnet-35133052"
                                },
                                {
                                    "description": "172.31.16.0/20",
                                    "name": "subnet-aa3001f2"
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
                                    "name": "sg-39b32a5f"
                                }
                            ],
                            "name": "vpc-050fa062"
                        }
                    ],
                    "name": "sa-east-1",
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
                            "name": "ami-c2e6baae"
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
                                    "description": "Private subnet",
                                    "name": "subnet-0f4d827f0959c45a4"
                                },
                                {
                                    "description": "Public subnet",
                                    "name": "subnet-0d3033d2b8bf13f12"
                                }
                            ],
                            "description": "VPC1",
                            "target_groups": [],
                            "load_balancers": [],
                            "security_groups": [
                                {
                                    "name": "Automatic"
                                },
                                {
                                    "description": "default VPC security group",
                                    "name": "sg-0c48ef851d23ee3cc"
                                }
                            ],
                            "name": "vpc-0ad1a5959b295f65e"
                        },
                        {
                            "subnets": [
                                {
                                    "description": "172.31.64.0/20",
                                    "name": "subnet-f56242ca"
                                },
                                {
                                    "description": "172.31.0.0/20",
                                    "name": "subnet-32a9bc56"
                                },
                                {
                                    "description": "172.31.16.0/20",
                                    "name": "subnet-09e41a43"
                                },
                                {
                                    "description": "172.31.32.0/20",
                                    "name": "subnet-4ec7ed13"
                                },
                                {
                                    "description": "172.31.48.0/20",
                                    "name": "subnet-772d8978"
                                },
                                {
                                    "description": "172.31.80.0/20",
                                    "name": "subnet-c4f5c1eb"
                                }
                            ],
                            "description": "172.31.0.0/16",
                            "target_groups": [
                                {
                                    "default_port": 80,
                                    "protocol": "HTTP",
                                    "target_type": "instance",
                                    "arn": "arn:aws:elasticloadbalancing:us-east-1:636588615608:targetgroup/partsultdLBRouting/e1031aa116bf033f",
                                    "name": "partsultdLBRouting"
                                }
                            ],
                            "load_balancers": [],
                            "security_groups": [
                                {
                                    "name": "Automatic"
                                },
                                {
                                    "description": "This security group was generated by AWS Marketplace and is based on recommended settings for Red Hat Enterprise Linux (RHEL) 6 (HVM) version 6.7_HVM_20160219 provided by Amazon Web Services",
                                    "name": "sg-06f2b8b511216c8f3"
                                },
                                {
                                    "description": "This security group was generated by AWS Marketplace and is based on recommended settings for CentOS 7 (x86_64) - with Updates HVM version 1805_01 provided by Centos.org",
                                    "name": "sg-0752c07ce1afb7f9a"
                                },
                                {
                                    "description": "Enable SSH access via port 22",
                                    "name": "sg-092de9abb7c435e37"
                                },
                                {
                                    "description": "This security group was generated by AWS Marketplace and is based on recommended settings for Red Hat Enterprise Linux (RHEL) 6 version 6.5_GA provided by Amazon Web Services",
                                    "name": "sg-0db584c264083fbd2"
                                },
                                {
                                    "description": "This security group was generated by AWS Marketplace and is based on recommended settings for CentOS 6 (x86_64) - with Updates HVM version 1805_01 provided by Centos.org",
                                    "name": "sg-0f53c2fa9738d1f55"
                                },
                                {
                                    "description": "default VPC security group",
                                    "name": "sg-6969051f"
                                }
                            ],
                            "name": "vpc-711a9f0a"
                        },
                        {
                            "subnets": [
                                {
                                    "description": "Public Subnet #2",
                                    "name": "subnet-01f48b41fd743c464"
                                },
                                {
                                    "description": "Private subnet",
                                    "name": "subnet-072d27171887b3f3b"
                                },
                                {
                                    "description": "Public subnet",
                                    "name": "subnet-08c8e59037abe931d"
                                },
                                {
                                    "description": "Private subnet #2",
                                    "name": "subnet-00175e924b602a94f"
                                }
                            ],
                            "description": "VPC2",
                            "target_groups": [
                                {
                                    "default_port": 80,
                                    "protocol": "HTTP",
                                    "target_type": "instance",
                                    "arn": "arn:aws:elasticloadbalancing:us-east-1:636588615608:targetgroup/partsultdASGGroup/21bf3b5ba88c8714",
                                    "name": "partsultdASGGroup"
                                }
                            ],
                            "load_balancers": [],
                            "security_groups": [
                                {
                                    "name": "Automatic"
                                },
                                {
                                    "description": "launch-wizard-3 created 2018-03-18T15:37:19.910-05:00",
                                    "name": "sg-00004b4a49e24b9ff"
                                },
                                {
                                    "description": "launch-wizard-4 created 2018-03-20T13:45:11.721-05:00",
                                    "name": "sg-02419971da8f7872e"
                                },
                                {
                                    "description": "SG for AutoScale Group",
                                    "name": "sg-06a3092ac1fdfc419"
                                },
                                {
                                    "description": "launch-wizard-1 created 2018-03-18T14:29:23.439-05:00",
                                    "name": "sg-07a8d5b8803636fcc"
                                },
                                {
                                    "description": "launch-wizard-2 created 2018-03-18T14:32:32.770-05:00",
                                    "name": "sg-081aae6f8f5b4f495"
                                },
                                {
                                    "description": "default VPC security group",
                                    "name": "sg-090fe3844fa6abfb6"
                                },
                                {
                                    "description": "Created from the RDS Management Console: 2018/03/17 01:58:33",
                                    "name": "sg-0a401b0de0f86fcee"
                                },
                                {
                                    "description": "launch-wizard-5 created 2018-03-20T13:50:32.057-05:00",
                                    "name": "sg-0d9aa67d083634708"
                                },
                                {
                                    "description": "launch-wizard-6 created 2018-03-20T20:01:05.847-05:00",
                                    "name": "sg-0dd22da7d662ab2b8"
                                }
                            ],
                            "name": "vpc-e446c29f"
                        }
                    ],
                    "name": "us-east-1",
                    "placement_groups": [],
                    "images": [
                        {
                            "owner": "external",
                            "description": "Ubunut 16.04 USE1",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 8
                            },
                            "name": "ami-759bc50a"
                        },
                        {
                            "owner": "external",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 8
                            },
                            "name": "ami-456b493a",
                            "description": "Ubuntu 14.04 AWSUSE1"
                        },
                        {
                            "owner": "external",
                            "description": "RHEL 7.5 AWSUSE1",
                            "name": "ami-6871a115",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 10
                            }
                        },
                        {
                            "owner": "external",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 10
                            },
                            "name": "ami-f37b4b99",
                            "description": "RHEL6 AWSUSE1"
                        },
                        {
                            "owner": "external",
                            "description": "CentOS7 AWSUSE1",
                            "name": "ami-9887c6e7",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 8
                            }
                        },
                        {
                            "owner": "external",
                            "description": "CentOS6 AWSUSE1",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 8
                            },
                            "name": "ami-1585c46a"
                        },
                        {
                            "owner": "external",
                            "root_disk": null,
                            "name": "ami-b08dd3cf",
                            "description": "Ubuntu16.04 - 2"
                        },
                        {
                            "owner": "external",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 8
                            },
                            "description": "Ubuntu 16.04 - 3",
                            "name": "ami-749bc50b"
                        },
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
                            "name": "ami-d5bf2caa"
                        },
                        {
                            "owner": "external",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 10
                            },
                            "name": "ami-2051294a",
                            "description": "RHEL-7.2"
                        }
                    ],
                    "alarms": [],
                    "keypairs": [
                        {
                            "name": "None"
                        },
                        {
                            "name": "partsultd"
                        },
                        {
                            "name": "partsultdEC2Key"
                        }
                    ]
                },
                {
                    "clouds": [
                        {
                            "subnets": [
                                {
                                    "description": "172.31.32.0/20",
                                    "name": "subnet-6af8c827"
                                },
                                {
                                    "description": "172.31.16.0/20",
                                    "name": "subnet-5746832d"
                                },
                                {
                                    "description": "172.31.0.0/20",
                                    "name": "subnet-c569e4ad"
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
                                    "name": "sg-70f68b1b"
                                }
                            ],
                            "name": "vpc-463cb52e"
                        }
                    ],
                    "name": "us-east-2",
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
                            "name": "ami-77724e12"
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
                                    "description": "172.31.16.0/20",
                                    "name": "subnet-5ac28b3d"
                                },
                                {
                                    "description": "172.31.0.0/20",
                                    "name": "subnet-7b198320"
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
                                    "name": "sg-bc511fc5"
                                }
                            ],
                            "name": "vpc-9561dbf2"
                        }
                    ],
                    "name": "us-west-1",
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
                            "name": "ami-3b89905b"
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
                                    "description": "172.31.32.0/20",
                                    "name": "subnet-4f408404"
                                },
                                {
                                    "description": "172.31.16.0/20",
                                    "name": "subnet-eb872292"
                                },
                                {
                                    "description": "172.31.0.0/20",
                                    "name": "subnet-58cd4c02"
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
                                    "name": "sg-54cac02b"
                                }
                            ],
                            "name": "vpc-f8d0a181"
                        }
                    ],
                    "name": "us-west-2",
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
                            "name": "ami-5490ed2c"
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
        {
            "flavors": [
                {
                    "name": "c1.medium"
                },
                {
                    "name": "c1.xlarge"
                },
                {
                    "name": "c3.large"
                },
                {
                    "name": "c3.xlarge"
                },
                {
                    "name": "c3.2xlarge"
                },
                {
                    "name": "c3.4xlarge"
                },
                {
                    "name": "c3.8xlarge"
                },
                {
                    "name": "c4.large"
                },
                {
                    "name": "c4.xlarge"
                },
                {
                    "name": "c4.2xlarge"
                },
                {
                    "name": "c4.4xlarge"
                },
                {
                    "name": "c4.8xlarge"
                },
                {
                    "name": "c5.large"
                },
                {
                    "name": "c5.xlarge"
                },
                {
                    "name": "c5.2xlarge"
                },
                {
                    "name": "c5.4xlarge"
                },
                {
                    "name": "c5.9xlarge"
                },
                {
                    "name": "c5.18xlarge"
                },
                {
                    "name": "c5d.large"
                },
                {
                    "name": "c5d.xlarge"
                },
                {
                    "name": "c5d.2xlarge"
                },
                {
                    "name": "c5d.4xlarge"
                },
                {
                    "name": "c5d.9xlarge"
                },
                {
                    "name": "c5d.18xlarge"
                },
                {
                    "name": "cc2.8xlarge"
                },
                {
                    "name": "cr1.8xlarge"
                },
                {
                    "name": "d2.xlarge"
                },
                {
                    "name": "d2.2xlarge"
                },
                {
                    "name": "d2.4xlarge"
                },
                {
                    "name": "d2.8xlarge"
                },
                {
                    "name": "f1.2xlarge"
                },
                {
                    "name": "f1.16xlarge"
                },
                {
                    "name": "g2.2xlarge"
                },
                {
                    "name": "g2.8xlarge"
                },
                {
                    "name": "g3.4xlarge"
                },
                {
                    "name": "g3.8xlarge"
                },
                {
                    "name": "g3.16xlarge"
                },
                {
                    "name": "h1.2xlarge"
                },
                {
                    "name": "h1.4xlarge"
                },
                {
                    "name": "h1.8xlarge"
                },
                {
                    "name": "h1.16xlarge"
                },
                {
                    "name": "hs1.8xlarge"
                },
                {
                    "name": "i2.xlarge"
                },
                {
                    "name": "i2.2xlarge"
                },
                {
                    "name": "i2.4xlarge"
                },
                {
                    "name": "i2.8xlarge"
                },
                {
                    "name": "i3.large"
                },
                {
                    "name": "i3.metal"
                },
                {
                    "name": "i3.xlarge"
                },
                {
                    "name": "i3.2xlarge"
                },
                {
                    "name": "i3.4xlarge"
                },
                {
                    "name": "i3.8xlarge"
                },
                {
                    "name": "i3.16xlarge"
                },
                {
                    "name": "m1.small"
                },
                {
                    "name": "m1.medium"
                },
                {
                    "name": "m1.large"
                },
                {
                    "name": "m1.xlarge"
                },
                {
                    "name": "m2.xlarge"
                },
                {
                    "name": "m2.2xlarge"
                },
                {
                    "name": "m2.4xlarge"
                },
                {
                    "name": "m3.medium"
                },
                {
                    "name": "m3.large"
                },
                {
                    "name": "m3.xlarge"
                },
                {
                    "name": "m3.2xlarge"
                },
                {
                    "name": "m4.large"
                },
                {
                    "name": "m4.xlarge"
                },
                {
                    "name": "m4.2xlarge"
                },
                {
                    "name": "m4.4xlarge"
                },
                {
                    "name": "m4.10xlarge"
                },
                {
                    "name": "m4.16xlarge"
                },
                {
                    "name": "m5.large"
                },
                {
                    "name": "m5.xlarge"
                },
                {
                    "name": "m5.2xlarge"
                },
                {
                    "name": "m5.4xlarge"
                },
                {
                    "name": "m5.12xlarge"
                },
                {
                    "name": "m5.24xlarge"
                },
                {
                    "name": "m5d.large"
                },
                {
                    "name": "m5d.xlarge"
                },
                {
                    "name": "m5d.2xlarge"
                },
                {
                    "name": "m5d.4xlarge"
                },
                {
                    "name": "m5d.12xlarge"
                },
                {
                    "name": "m5d.24xlarge"
                },
                {
                    "name": "p2.xlarge"
                },
                {
                    "name": "p2.8xlarge"
                },
                {
                    "name": "p2.16xlarge"
                },
                {
                    "name": "r3.large"
                },
                {
                    "name": "r3.xlarge"
                },
                {
                    "name": "r3.2xlarge"
                },
                {
                    "name": "r3.4xlarge"
                },
                {
                    "name": "r3.8xlarge"
                },
                {
                    "name": "r4.large"
                },
                {
                    "name": "r4.xlarge"
                },
                {
                    "name": "r4.2xlarge"
                },
                {
                    "name": "r4.4xlarge"
                },
                {
                    "name": "r4.8xlarge"
                },
                {
                    "name": "r4.16xlarge"
                },
                {
                    "name": "t1.micro"
                },
                {
                    "name": "t2.micro"
                },
                {
                    "name": "t2.small"
                },
                {
                    "name": "t2.medium"
                },
                {
                    "name": "t2.large"
                },
                {
                    "name": "t2.xlarge"
                },
                {
                    "name": "t2.2xlarge"
                },
                {
                    "name": "x1.16xlarge"
                },
                {
                    "name": "x1.32xlarge"
                },
                {
                    "name": "x1e.xlarge"
                },
                {
                    "name": "x1e.2xlarge"
                },
                {
                    "name": "x1e.4xlarge"
                },
                {
                    "name": "x1e.8xlarge"
                },
                {
                    "name": "x1e.16xlarge"
                },
                {
                    "name": "x1e.32xlarge"
                }
            ],
            "name": "Windows Compute",
            "roles": [
                {
                    "name": "None"
                },
                {
                    "name": "AutoScaleS3Access"
                },
                {
                    "name": "MeyerTest"
                },
                {
                    "name": "test-chris"
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
                                },
                                {
                                    "description": "172.31.32.0/20",
                                    "name": "subnet-f2e2bcbb"
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
                            "name": "Windows Compute"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k08 Std-Win2k8 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-c57de7a3"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k14 Std-Win2k12 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-c671eba0"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k12 Std-Win2k12",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-3e6ef458"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k12 Ent-Win2k8 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-5e7ce638"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k14 Ent-Win2k12 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-7b2eb41d"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k12 Std-Win2k8 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-2572e843"
                        },
                        {
                            "owner": "user",
                            "description": "Microsoft Windows Server 2016 with Desktop Experience Locale",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 30
                            },
                            "name": "ami-ec279c8a"
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
                            "name": "Windows Compute"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k08 Std-Win2k8 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-fc4ded92"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k12 Std-Win2k8 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-b34fefdd"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k12 Std-Win2k12",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-c64fefa8"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k12 Ent-Win2k8 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-e34fef8d"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k14 Ent-Win2k12 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-2b55f545"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k14 Std-Win2k12 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-cd4deda3"
                        },
                        {
                            "owner": "user",
                            "description": "Microsoft Windows Server 2016 with Desktop Experience Locale",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 30
                            },
                            "name": "ami-e8ef4986"
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
                                    "name": "subnet-d310e69f"
                                },
                                {
                                    "description": "172.31.16.0/20",
                                    "name": "subnet-f855d390"
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
                                    "name": "sg-d39d11b8"
                                }
                            ],
                            "name": "vpc-1585067d"
                        }
                    ],
                    "name": "ap-south-1",
                    "placement_groups": [],
                    "images": [
                        {
                            "owner": "user",
                            "description": "Latest Amazon AMI",
                            "name": "Windows Compute"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k08 Std-Win2k8 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-5fb4e330"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k12 Std-Win2k8 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-35b6e15a"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k12 Ent-Win2k8 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-edb3e482"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k14 Ent-Win2k12 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-a6bcebc9"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k12 Std-Win2k12",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-69b3e406"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k14 Std-Win2k12 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-8cb5e2e3"
                        },
                        {
                            "owner": "user",
                            "description": "Microsoft Windows Server 2016 with Desktop Experience Locale",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 30
                            },
                            "name": "ami-100f467f"
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
                                    "description": "172.31.16.0/20",
                                    "name": "subnet-15dc9372"
                                },
                                {
                                    "description": "172.31.0.0/20",
                                    "name": "subnet-2d60776b"
                                },
                                {
                                    "description": "172.31.32.0/20",
                                    "name": "subnet-22b6c96b"
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
                                    "name": "sg-e3a2269a"
                                }
                            ],
                            "name": "vpc-b00a89d7"
                        }
                    ],
                    "name": "ap-southeast-1",
                    "placement_groups": [],
                    "images": [
                        {
                            "owner": "user",
                            "description": "Latest Amazon AMI",
                            "name": "Windows Compute"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k08 Std-Win2k8 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-39364b45"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k14 Ent-Win2k12 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-0d097471"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k12 Std-Win2k12",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-11275a6d"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k12 Ent-Win2k8 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-95304de9"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k14 Std-Win2k12 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-9d2c51e1"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k12 Std-Win2k8 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-93334eef"
                        },
                        {
                            "owner": "user",
                            "description": "Microsoft Windows Server 2016 with Desktop Experience Locale",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 30
                            },
                            "name": "ami-870855e4"
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
                                    "description": "172.31.32.0/20",
                                    "name": "subnet-66492f2f"
                                },
                                {
                                    "description": "172.31.0.0/20",
                                    "name": "subnet-dfc5b0b8"
                                },
                                {
                                    "description": "172.31.16.0/20",
                                    "name": "subnet-3a699f62"
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
                                    "name": "sg-5b299b22"
                                }
                            ],
                            "name": "vpc-65329802"
                        }
                    ],
                    "name": "ap-southeast-2",
                    "placement_groups": [],
                    "images": [
                        {
                            "owner": "user",
                            "description": "Latest Amazon AMI",
                            "name": "Windows Compute"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k12 Std-Win2k8 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-cda15daf"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k08 Std-Win2k8 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-85a65ae7"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k12 Ent-Win2k8 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-01a75b63"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k14 Ent-Win2k12 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-0d8d716f"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k12 Std-Win2k12",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-9b9965f9"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k14 Std-Win2k12 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-629e6200"
                        },
                        {
                            "owner": "user",
                            "description": "Microsoft Windows Server 2016 with Desktop Experience Locale",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 30
                            },
                            "name": "ami-de5eabbc"
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
                                    "description": "172.31.16.0/20",
                                    "name": "subnet-3119e159"
                                },
                                {
                                    "description": "172.31.0.0/20",
                                    "name": "subnet-823b2cf9"
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
                                    "name": "sg-c09fa1a8"
                                }
                            ],
                            "name": "vpc-9e3fccf6"
                        }
                    ],
                    "name": "ca-central-1",
                    "placement_groups": [],
                    "images": [
                        {
                            "owner": "user",
                            "description": "Latest Amazon AMI",
                            "name": "Windows Compute"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k08 Std-Win2k8 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-3fb5305b"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k12 Ent-Win2k8 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-aab431ce"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k12 Std-Win2k12",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-bab431de"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k12 Std-Win2k8 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-3bb5305f"
                        },
                        {
                            "owner": "user",
                            "description": "Microsoft Windows Server 2016 with Desktop Experience Locale",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 30
                            },
                            "name": "ami-5e3b803a"
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
                                    "description": "172.31.16.0/20",
                                    "name": "subnet-1557147e"
                                },
                                {
                                    "description": "172.31.32.0/20",
                                    "name": "subnet-454af238"
                                },
                                {
                                    "description": "172.31.0.0/20",
                                    "name": "subnet-07029b4a"
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
                                    "name": "sg-8a14a6e7"
                                }
                            ],
                            "name": "vpc-70e7671b"
                        }
                    ],
                    "name": "eu-central-1",
                    "placement_groups": [],
                    "images": [
                        {
                            "owner": "user",
                            "description": "Latest Amazon AMI",
                            "name": "Windows Compute"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k12 Std-Win2k8 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-e3079a8c"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k08 Std-Win2k8 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-98079af7"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k12 Ent-Win2k8 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-3c039e53"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k12 Std-Win2k12",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-c53ca1aa"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k14 Std-Win2k12 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-f1039e9e"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k14 Ent-Win2k12 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-1a31ac75"
                        },
                        {
                            "owner": "user",
                            "description": "Microsoft Windows Server 2016 with Desktop Experience Locale",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 30
                            },
                            "name": "ami-da9b14b5"
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
                                    "description": "172.31.16.0/20",
                                    "name": "subnet-836db4cb"
                                },
                                {
                                    "description": "172.31.0.0/20",
                                    "name": "subnet-3948835f"
                                },
                                {
                                    "description": "172.31.32.0/20",
                                    "name": "subnet-9b5d49c0"
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
                                    "name": "sg-3e154144"
                                }
                            ],
                            "name": "vpc-2b5fe54d"
                        }
                    ],
                    "name": "eu-west-1",
                    "placement_groups": [],
                    "images": [
                        {
                            "owner": "user",
                            "description": "Latest Amazon AMI",
                            "name": "Windows Compute"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k08 Std-Win2k8 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-17b62a6e"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k12 Std-Win2k8 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-0db72b74"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k12 Ent-Win2k8 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-76b62a0f"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k14 Std-Win2k12 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-61ad3118"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k12 Std-Win2k12",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-b9a935c0"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k14 Ent-Win2k12 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-c558c4bc"
                        },
                        {
                            "owner": "user",
                            "description": "Microsoft Windows Server 2016 with Desktop Experience Locale",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 30
                            },
                            "name": "ami-e055e899"
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
                                    "description": "172.31.16.0/20",
                                    "name": "subnet-9f7e9fe5"
                                },
                                {
                                    "description": "172.31.32.0/20",
                                    "name": "subnet-fae6d0b7"
                                },
                                {
                                    "description": "172.31.0.0/20",
                                    "name": "subnet-286fc141"
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
                                    "name": "sg-e98e8581"
                                }
                            ],
                            "name": "vpc-2b1fda43"
                        }
                    ],
                    "name": "eu-west-2",
                    "placement_groups": [],
                    "images": [
                        {
                            "owner": "user",
                            "description": "Latest Amazon AMI",
                            "name": "Windows Compute"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k08 Std-Win2k8 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-87667de3"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k12 Std-Win2k8 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-58677c3c"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k12 Std-Win2k12",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-0b647f6f"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k12 Ent-Win2k8 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-c0677ca4"
                        },
                        {
                            "owner": "user",
                            "description": "Microsoft Windows Server 2016 with Desktop Experience Locale",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 30
                            },
                            "name": "ami-78657b1c"
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
                                    "description": "172.31.16.0/20",
                                    "name": "subnet-d134e3aa"
                                },
                                {
                                    "description": "172.31.32.0/20",
                                    "name": "subnet-c70fe38a"
                                },
                                {
                                    "description": "172.31.0.0/20",
                                    "name": "subnet-b909b4d0"
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
                                    "name": "sg-3d155254"
                                }
                            ],
                            "name": "vpc-ac15aec5"
                        }
                    ],
                    "name": "eu-west-3",
                    "placement_groups": [],
                    "images": [
                        {
                            "owner": "user",
                            "description": "Latest Amazon AMI",
                            "name": "Windows Compute"
                        },
                        {
                            "owner": "user",
                            "description": "Microsoft Windows Server 2016 with Desktop Experience Locale",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 30
                            },
                            "name": "ami-2e67d053"
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
                                    "name": "subnet-35133052"
                                },
                                {
                                    "description": "172.31.16.0/20",
                                    "name": "subnet-aa3001f2"
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
                                    "name": "sg-39b32a5f"
                                }
                            ],
                            "name": "vpc-050fa062"
                        }
                    ],
                    "name": "sa-east-1",
                    "placement_groups": [],
                    "images": [
                        {
                            "owner": "user",
                            "description": "Latest Amazon AMI",
                            "name": "Windows Compute"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k08 Std-Win2k8 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-f5c58799"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k12 Std-Win2k8 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-5bca8837"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k14 Std-Win2k12 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-faca8896"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k14 Ent-Win2k12 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-bdc98bd1"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k12 Ent-Win2k8 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-89c587e5"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k12 Std-Win2k12",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-accb89c0"
                        },
                        {
                            "owner": "user",
                            "description": "Microsoft Windows Server 2016 with Desktop Experience Locale",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 30
                            },
                            "name": "ami-41bffb2d"
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
                                    "description": "Private subnet",
                                    "name": "subnet-0f4d827f0959c45a4"
                                },
                                {
                                    "description": "Public subnet",
                                    "name": "subnet-0d3033d2b8bf13f12"
                                }
                            ],
                            "description": "VPC1",
                            "target_groups": [],
                            "load_balancers": [],
                            "security_groups": [
                                {
                                    "name": "Automatic"
                                },
                                {
                                    "description": "default VPC security group",
                                    "name": "sg-0c48ef851d23ee3cc"
                                }
                            ],
                            "name": "vpc-0ad1a5959b295f65e"
                        },
                        {
                            "subnets": [
                                {
                                    "description": "172.31.64.0/20",
                                    "name": "subnet-f56242ca"
                                },
                                {
                                    "description": "172.31.0.0/20",
                                    "name": "subnet-32a9bc56"
                                },
                                {
                                    "description": "172.31.16.0/20",
                                    "name": "subnet-09e41a43"
                                },
                                {
                                    "description": "172.31.32.0/20",
                                    "name": "subnet-4ec7ed13"
                                },
                                {
                                    "description": "172.31.48.0/20",
                                    "name": "subnet-772d8978"
                                },
                                {
                                    "description": "172.31.80.0/20",
                                    "name": "subnet-c4f5c1eb"
                                }
                            ],
                            "description": "172.31.0.0/16",
                            "target_groups": [
                                {
                                    "default_port": 80,
                                    "protocol": "HTTP",
                                    "target_type": "instance",
                                    "arn": "arn:aws:elasticloadbalancing:us-east-1:636588615608:targetgroup/partsultdLBRouting/e1031aa116bf033f",
                                    "name": "partsultdLBRouting"
                                }
                            ],
                            "load_balancers": [],
                            "security_groups": [
                                {
                                    "name": "Automatic"
                                },
                                {
                                    "description": "This security group was generated by AWS Marketplace and is based on recommended settings for Red Hat Enterprise Linux (RHEL) 6 (HVM) version 6.7_HVM_20160219 provided by Amazon Web Services",
                                    "name": "sg-06f2b8b511216c8f3"
                                },
                                {
                                    "description": "This security group was generated by AWS Marketplace and is based on recommended settings for CentOS 7 (x86_64) - with Updates HVM version 1805_01 provided by Centos.org",
                                    "name": "sg-0752c07ce1afb7f9a"
                                },
                                {
                                    "description": "Enable SSH access via port 22",
                                    "name": "sg-092de9abb7c435e37"
                                },
                                {
                                    "description": "This security group was generated by AWS Marketplace and is based on recommended settings for Red Hat Enterprise Linux (RHEL) 6 version 6.5_GA provided by Amazon Web Services",
                                    "name": "sg-0db584c264083fbd2"
                                },
                                {
                                    "description": "This security group was generated by AWS Marketplace and is based on recommended settings for CentOS 6 (x86_64) - with Updates HVM version 1805_01 provided by Centos.org",
                                    "name": "sg-0f53c2fa9738d1f55"
                                },
                                {
                                    "description": "default VPC security group",
                                    "name": "sg-6969051f"
                                }
                            ],
                            "name": "vpc-711a9f0a"
                        },
                        {
                            "subnets": [
                                {
                                    "description": "Public Subnet #2",
                                    "name": "subnet-01f48b41fd743c464"
                                },
                                {
                                    "description": "Private subnet",
                                    "name": "subnet-072d27171887b3f3b"
                                },
                                {
                                    "description": "Public subnet",
                                    "name": "subnet-08c8e59037abe931d"
                                },
                                {
                                    "description": "Private subnet #2",
                                    "name": "subnet-00175e924b602a94f"
                                }
                            ],
                            "description": "VPC2",
                            "target_groups": [
                                {
                                    "default_port": 80,
                                    "protocol": "HTTP",
                                    "target_type": "instance",
                                    "arn": "arn:aws:elasticloadbalancing:us-east-1:636588615608:targetgroup/partsultdASGGroup/21bf3b5ba88c8714",
                                    "name": "partsultdASGGroup"
                                }
                            ],
                            "load_balancers": [],
                            "security_groups": [
                                {
                                    "name": "Automatic"
                                },
                                {
                                    "description": "launch-wizard-3 created 2018-03-18T15:37:19.910-05:00",
                                    "name": "sg-00004b4a49e24b9ff"
                                },
                                {
                                    "description": "launch-wizard-4 created 2018-03-20T13:45:11.721-05:00",
                                    "name": "sg-02419971da8f7872e"
                                },
                                {
                                    "description": "SG for AutoScale Group",
                                    "name": "sg-06a3092ac1fdfc419"
                                },
                                {
                                    "description": "launch-wizard-1 created 2018-03-18T14:29:23.439-05:00",
                                    "name": "sg-07a8d5b8803636fcc"
                                },
                                {
                                    "description": "launch-wizard-2 created 2018-03-18T14:32:32.770-05:00",
                                    "name": "sg-081aae6f8f5b4f495"
                                },
                                {
                                    "description": "default VPC security group",
                                    "name": "sg-090fe3844fa6abfb6"
                                },
                                {
                                    "description": "Created from the RDS Management Console: 2018/03/17 01:58:33",
                                    "name": "sg-0a401b0de0f86fcee"
                                },
                                {
                                    "description": "launch-wizard-5 created 2018-03-20T13:50:32.057-05:00",
                                    "name": "sg-0d9aa67d083634708"
                                },
                                {
                                    "description": "launch-wizard-6 created 2018-03-20T20:01:05.847-05:00",
                                    "name": "sg-0dd22da7d662ab2b8"
                                }
                            ],
                            "name": "vpc-e446c29f"
                        }
                    ],
                    "name": "us-east-1",
                    "placement_groups": [],
                    "images": [
                        {
                            "owner": "external",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 30
                            },
                            "description": "Win2k12 R2 Base",
                            "name": "ami-60093e1f"
                        },
                        {
                            "owner": "user",
                            "description": "Latest Amazon AMI",
                            "name": "Windows Compute"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k08 Std-Win2k8 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-f3052289"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k12 Std-Win2k8 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-2e0b2c54"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k12 Std-Win2k12",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-211c3b5b"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k14 Std-Win2k12 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-d91334a3"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k12 Ent-Win2k8 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-42391e38"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k14 Ent-Win2k12 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-f2f0d788"
                        },
                        {
                            "owner": "user",
                            "description": "Microsoft Windows Server 2016 with Desktop Experience Locale",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 30
                            },
                            "name": "ami-08910872"
                        }
                    ],
                    "alarms": [],
                    "keypairs": [
                        {
                            "name": "None"
                        },
                        {
                            "name": "partsultd"
                        },
                        {
                            "name": "partsultdEC2Key"
                        }
                    ]
                },
                {
                    "clouds": [
                        {
                            "subnets": [
                                {
                                    "description": "172.31.32.0/20",
                                    "name": "subnet-6af8c827"
                                },
                                {
                                    "description": "172.31.16.0/20",
                                    "name": "subnet-5746832d"
                                },
                                {
                                    "description": "172.31.0.0/20",
                                    "name": "subnet-c569e4ad"
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
                                    "name": "sg-70f68b1b"
                                }
                            ],
                            "name": "vpc-463cb52e"
                        }
                    ],
                    "name": "us-east-2",
                    "placement_groups": [],
                    "images": [
                        {
                            "owner": "user",
                            "description": "Latest Amazon AMI",
                            "name": "Windows Compute"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k08 Std-Win2k8 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-da476dbf"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k12 Std-Win2k8 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-d9476dbc"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k14 Std-Win2k12 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-c7466ca2"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k14 Ent-Win2k12 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-27597342"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k12 Std-Win2k12",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-da446ebf"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k12 Ent-Win2k8 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-3b476d5e"
                        },
                        {
                            "owner": "user",
                            "description": "Microsoft Windows Server 2016 with Desktop Experience Locale",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 30
                            },
                            "name": "ami-21587144"
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
                                    "description": "172.31.16.0/20",
                                    "name": "subnet-5ac28b3d"
                                },
                                {
                                    "description": "172.31.0.0/20",
                                    "name": "subnet-7b198320"
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
                                    "name": "sg-bc511fc5"
                                }
                            ],
                            "name": "vpc-9561dbf2"
                        }
                    ],
                    "name": "us-west-1",
                    "placement_groups": [],
                    "images": [
                        {
                            "owner": "user",
                            "description": "Latest Amazon AMI",
                            "name": "Windows Compute"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k08 Std-Win2k8 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-55838035"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k12 Std-Win2k12",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-9d8083fd"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k14 Ent-Win2k12 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-a08586c0"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k12 Ent-Win2k8 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-1b82817b"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k12 Std-Win2k8 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-19828179"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k14 Std-Win2k12 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-ed81828d"
                        },
                        {
                            "owner": "user",
                            "description": "Microsoft Windows Server 2016 with Desktop Experience Locale",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 30
                            },
                            "name": "ami-406d5720"
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
                                    "description": "172.31.32.0/20",
                                    "name": "subnet-4f408404"
                                },
                                {
                                    "description": "172.31.16.0/20",
                                    "name": "subnet-eb872292"
                                },
                                {
                                    "description": "172.31.0.0/20",
                                    "name": "subnet-58cd4c02"
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
                                    "name": "sg-54cac02b"
                                }
                            ],
                            "name": "vpc-f8d0a181"
                        }
                    ],
                    "name": "us-west-2",
                    "placement_groups": [],
                    "images": [
                        {
                            "owner": "user",
                            "description": "Latest Amazon AMI",
                            "name": "Windows Compute"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k08 Std-Win2k8 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-add061d5"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k12 Std-Win2k8 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-bed160c6"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k12 Ent-Win2k8 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-2cd36254"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k12 Std-Win2k12",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-aedd6cd6"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k14 Ent-Win2k12 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-04c9787c"
                        },
                        {
                            "owner": "user",
                            "description": "SQL Srv 2k14 Std-Win2k12 R2",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 50
                            },
                            "name": "ami-90d160e8"
                        },
                        {
                            "owner": "user",
                            "description": "Microsoft Windows Server 2016 with Desktop Experience Locale",
                            "root_disk": {
                                "device": "/dev/sda1",
                                "iops": null,
                                "type": "gp2",
                                "size": 30
                            },
                            "name": "ami-f6d8008e"
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
            "appliance_id": "i-q428yw",
            "name": "us-east-1",
            "vpc": "vpc-e446c29f"
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
- Invalid Data (400)
- Forbidden (403)
- Active service using the provider (400)


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
- Forbidden (403)
- Not Found (404)


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
- Forbidden (403)
- Not Found (404)

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
- Forbidden (403)
- Not Found (404)

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

### POST /services/providers/{provider_id}/images

Adds a new machine image to a provider when you give the provider ID.

### URL
#### Structure
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
- Invalid Data (400)
- Forbidden (403)
- Not Found (404)


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
- Location query parameter is missing (400)
- Forbidden (403)
- Not Found (404)


### Contacting Cloud Application Manager Support

We’re sorry you’re having an issue in [Cloud Application Manager](https://www.ctl.io/cloud-application-manager/). Please review the [troubleshooting tips](https://www.ctl.io/knowledge-base/cloud-application-manager/troubleshooting/troubleshooting-tips/), or contact [Cloud Application Manager support](mailto:incident@CenturyLink.com) with details and screenshots where possible.

For issues related to API calls, send the request body along with details related to the issue.

In the case of a box error, share the box in the workspace that your organization and Cloud Application Manager can access and attach the logs.
* Linux: SSH and locate the log at /var/log/elasticbox/elasticbox-agent.log
* Windows: RDP into the instance to locate the log at ProgramDataElasticBoxLogselasticbox-agent.log
