{{{
  "title": "Import Server",
  "date": "03-24-2015",
  "author": "Bryan Friedman",
  "attachments": []
}}}

Imports a new server from an uploaded OVF. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to import a new server from an OVF that has been uploaded to your FTP server. For more information about uploading an OVF for import, see [Using Self-Service VM Import](http://www.ctl.io/knowledge-base/servers/using-self-service-vm-import/) and make sure the OVF meets [these requirements](http://www.ctl.io/knowledge-base/servers/self-service-vm-import-ovf-requirements/) before attempting to import it.

## URL

### Structure

    POST https://api.ctl.io/v2/vmImport/{accountAlias}

### Example

    POST https://api.ctl.io/v2/vmImport/ALIAS/

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
| primaryDns | string | Primary DNS to set on the server. If not supplied the default value set on the account will be used. | No |
| secondaryDns | string | Secondary DNS to set on the server. If not supplied the default value set on the account will be used. | No |
| networkId | string | ID of the network to which to deploy the server. If not provided, a network will be chosen automatically. If your account has not yet been assigned a network, leave this blank and one will be assigned automatically. The list of available networks for a given account in a data center can be retrieved from the [Get Data Center Deployment Capabilities](../Data Centers/get-data-center-deployment-capabilities.md) API operation.  | No |
| password | string | Password of administrator or root user on server. _This password must match the one set on the server being imported or the import will fail._ | Yes |
| cpu | integer | Number of processors to configure the server with (1-16). If this value is different from the one specified in the OVF, the import process will resize the server according to the value specified here. | Yes |
| memoryGB | integer | Number of GB of memory to configure the server with (1-128). If this value is different from the one specified in the OVF, the import process will resize the server according to the value specified here.  | Yes |
| type | string | Whether to create standard or hyperscale server | Yes |
| storageType | string | For standard servers, whether to use standard or premium storage. If not provided, will default to premium storage. For hyperscale servers, storage type must be hyperscale. | No |
| customFields | complex | Collection of custom field ID-value pairs to set for the server. | No |
| ovfId | string | The identifier of the OVF that defines the server to import. This can be retrieved from the [Get Available Server Imports](../Servers/get-available-server-imports.md) API operation. |
| ovfOsType | string | The OS type of the server being imported. Currently, the only supported OS types are `redHat6_64Bit`, `windows2008R2DataCenter_64bit`, and `windows2012R2DataCenter_64Bit`. A list of importable OS types for a given data center can be retrieved from the [Get Data Center Deployment Capabilities](../Data Centers/get-data-center-deployment-capabilities.md) API operation. |

### CustomFields Definition

| Name | Type | Description |
| --- | --- | --- |
| id | string | ID of the custom field to set. Available custom field IDs can be retrieved from the [Get Custom Fields](../Custom Fields/get-custom-fields.md) API operation. |
| value | string | Value to set the custom field to for this server. |

### Examples

#### JSON

    {
      "name": "import",
      "description": "Custom Import Server",
      "groupId": "3d30a6bc6b5443388b7bc966d073e353",
      "primaryDns": "172.17.1.26",
      "secondaryDns": "172.17.1.27",
      "networkId": "d51ef9f58f244205922eab9d240b126f",
      "password": "P@ssw0rd1",
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
      "ovfId": "ALIAS/CUSTOM-OVF-IMPORT",
      "ovfOsType": "redHat6_64Bit"
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
      "server":"import",
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
