{{{
  "title": "Create Server",
  "date": "11-21-2014",
  "author": "Bryan Friedman",
  "attachments": []
}}}


Creates a new server. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to create a new server from a standard or custom template, or clone an existing server.

## URL

### Structure

    POST https://api.ctl.io/v2/servers/{accountAlias}

### Example

    POST https://api.ctl.io/v2/servers/ALIAS/

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | string | Short code for a particular account | Yes |

### Content Properties

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| name | string | Name of the server to create. Alphanumeric characters and dashes only. Must be between 1-7 characters depending on the length of the account alias. (This name will be appended with a two digit number and prepended with the datacenter code and account alias to make up the final server name.) | Yes |
| description | string | User-defined description of this server | No |
| groupId | string | ID of the parent group. Retrieved from query to parent group, or by looking at the URL on the UI pages in the Control Portal. | Yes |
| sourceServerId | string | ID of the server to use a source. May be the ID of a template, or when cloning, an existing server ID. The list of available templates for a given account in a data center can be retrieved from the [Get Data Center Deployment Capabilities](../Data Centers/get-data-center-deployment-capabilities.md) API operation. | Yes |
| isManagedOS | bool | Whether to create the server as managed or not. Default is false. | No |
| primaryDns | string | Primary DNS to set on the server. If not supplied the default value set on the account will be used. | No |
| secondaryDns | string | Secondary DNS to set on the server. If not supplied the default value set on the account will be used. | No |
| networkId | string | ID of the network to which to deploy the server. If not provided, a network will be chosen automatically. If your account has not yet been assigned a network, leave this blank and one will be assigned automatically. The list of available networks for a given account in a data center can be retrieved from the [Get Data Center Deployment Capabilities](../Data Centers/get-data-center-deployment-capabilities.md) API operation.  | No |
| ipAddress | string | IP address to assign to the server. If not provided, one will be assigned automatically. | No |
| password | string | Password of administrator or root user on server. If not provided, one will be generated automatically. | No |
| sourceServerPassword | string | Password of the source server, used only when creating a clone from an existing server. | No |
| cpu | integer | Number of processors to configure the server with (1-16) | Yes |
| cpuAutoscalePolicyId | string | ID of the vertical CPU Autoscale policy to associate the server with. Available IDs can be retrieved from the **Get Autoscale Policies** API operation. | No |
| memoryGB | integer | Number of GB of memory to configure the server with (1-128) | Yes |
| type | string | Whether to create standard or hyperscale server | Yes |
| storageType | string | For standard servers, whether to use standard or premium storage. If not provided, will default to premium storage. For hyperscale servers, storage type must be hyperscale. | No |
| antiAffinityPolicyId | string | ID of the Anti-Affinity policy to associate the server with. Only valid for hyperscale servers. Available IDs can be retrieved from the [Get Anti-Affinity Policies](../Anti-Affinity Policies/get-anti-affinity-policies.md) API operation. | No |
| customFields | complex | Collection of custom field ID-value pairs to set for the server. | No |
| additionalDisks | complex | Collection of disk parameters | No |
| ttl | dateTime | Date/time that the server should be deleted | No |
| packages | complex | Collection of packages to run on the server after it has been built | No |

### CustomFields Definition

| Name | Type | Description |
| --- | --- | --- |
| id | string | ID of the custom field to set. Available custom field IDs can be retrieved from the [Get Custom Fields](../Custom Fields/get-custom-fields.md) API operation. |
| value | string | Value to set the custom field to for this server. |

### AdditionalDisks Definition

| Name | Type | Description |
| --- | --- | --- |
| path | string | File system path for disk (Windows drive letter or Linux mount point). Must not be one of reserved names. |
| sizeGB | integer | Amount in GB to allocate for disk, up to 1024 GB per. |
| type | string | Whether the disk should be raw or partitioned |

### Packages Definition

| Name | Type | Description |
| --- | --- | --- |
| packageId | string | ID of the package to run on the server after it builds. Available package IDs can be retrieved from the **Get Packages** API operation. |
| parameters | complex | Collection of name-value pairs to specify package-specific parameters. |

### Examples

#### JSON

    {
      "name": "web",
      "description": "My web server",
      "groupId": "2a5c0b9662cf4fc8bf6180f139facdc0",
      "sourceServerId": "RHEL-6-64-TEMPLATE",
      "isManagedOS": false,
      "primaryDns": "172.17.1.26",
      "secondaryDns": "172.17.1.27",
      "networkId": "101",
      "ipAddress": "10.123.456.12",
      "password": "Password123",
      "cpu": 2,
      "memoryGB": 4,
      "type": "standard",
      "storageType": "standard",
      "customFields":[
        {
          "id": "90b3c5e28162456781d36ee42c5771a3",
          "value": "custom value"
        }
      ],
      "additionalDisks":[
        {
          "path": "data",
          "sizeGB": 10,
          "type": "partitioned"
        }
      ],
      "ttl": "2014-12-17T01:17:17Z"
    }

## Response

### Entity Definition

| Name | Type | Description |
| --- | --- | --- |
| server | string | ID of the server that the operation was performed on. |
| isQueued | boolean | Boolean indicating whether the operation was successfully added to the queue. |
| links | array | Collection of [entity links](../Getting Started/api-v20-links-framework.md) that point to resources related to this server operation. |
| errorMessage | string | If something goes wrong or the request is not queued, this is the message that contains the details about what happened. |

### Examples

#### JSON

    {
      "server":"web",
      "isQueued":true,
      "links":[
        {
          "rel":"status",
          "href":"/v2/operations/alias/status/wa1-12345",
          "id":"wa1-12345"
        },
        {
          "rel":"self",  "href":"/v2/servers/alias/8134c91a66784c6dada651eba90a5123?uuid=True",
          "id":"8134c91a66784c6dada651eba90a5123",
          "verbs":[
            "GET"
          ]
        }
      ]
    }
