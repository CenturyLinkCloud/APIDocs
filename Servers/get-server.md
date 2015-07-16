{{{
  "title": "Get Server",
  "date": "12-29-2014",
  "author": "Richard Seroter",
  "attachments": [],
  "sticky": "true"
}}}

Gets the details for a individual server. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to find out all the details for a server. It can be used to look for changes, its status, or to retrieve links to associated resources.

## URL

### Structure

    GET https://api.ctl.io/v2/servers/{accountAlias}/{serverId}

### Example

    GET https://api.ctl.io/v2/servers/ALIAS/WA1ACCTSERV0101

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | string | Short code for a particular account | Yes |
| ServerId | string | ID of the server being queried. Retrieved from query to containing group, or by looking at the URL when viewing a server in the Control Portal. | Yes |

## Response

### Server Entity Definition

| Name | Type | Description |
| --- | --- | --- |
| id | string | ID of the server being queried |
| name | string | Name of the server |
| description | string | User-defined description of this server |
| groupId | string | ID of the parent group |
| isTemplate | boolean | Boolean indicating whether this is a custom template or running server |
| locationId | string | Data center that this server resides in |
| osType | string | Friendly name of the Operating System the server is running |
| status | string | Describes whether the server is active or not |
| details | complex | Resource allocations, alert policies, snapshots, and more. |
| type | string | Whether a standard or premium server |
| storageType | string | Whether it uses standard or premium storage |
| changeInfo | complex | Describes "created" and "modified" details |
| links | array | Collection of [entity links](../Getting Started/api-v20-links-framework.md) that point to resources related to this server |

### Details Definition

| Name | Type | Description |
| --- | --- | --- |
| ipAddresses | complex | Details about IP addresses associated with the server |
| alertPolicies | complex | Describe each alert policy applied to the server |
| cpu | integer | How many vCPUs are allocated to the server |
| diskCount | integer | How many disks are attached to the server |
| hostName | string | Fully qualified name of the server |
| inMaintenanceMode | boolean | Indicator of whether server has been placed in maintenance mode |
| memoryMB | integer | How many MB of memory are allocated to the server |
| powerState | string | Whether the server is running or not |
| storageGB | integer | How many total GB of storage are allocated to the server |
| disks | complex | The disks attached to the server |
| partitions | complex | The partitions defined for the server |
| snapshots | complex | Details about any snapshot associated with the server |
| customFields | complex | Details about any custom fields and their values |
| processorDescription | Processor configuration description (for bare metal servers only) |
| storageDescription | Storage configuration description (for bare metal servers only) |

### IPAddresses Definition

| Name | Type | Description |
| --- | --- | --- |
| public | string | If applicable, the public IP |
| internal | string | Private IP address. If associated with a public IP address, then the "public" value is populated |

### AlertPolicies Definition

| Name | Type | Description |
| --- | --- | --- |
| id | string | Unique identifier of the policy |
| name | string | User-defined name of the alert policy |
| links | array | Collection of [entity links](../Getting Started/api-v20-links-framework.md) that point to resources related to this policy |

### Disks Definition

| Name | Type | Description |
| --- | --- | --- |
| id | string | Unique identifier of the disk |
| sizeGB | integer | Size of the disk in GB |
| partitionPaths | array | List of partition paths on the disk |

### Partitions Definition

| Name | Type | Description |
| --- | --- | --- |
| sizeGB | number | Size of the partition in GB |
| path | string | File system location path of the partition |

### Snapshots Definition

| Name | Type | Description |
| --- | --- | --- |
| name | string | Timestamp of the snapshot |
| links | array | Collection of [entity links](../Getting Started/api-v20-links-framework.md) that point to resources related to this snapshot |

### CustomFields Definition

| Name | Type | Description |
| --- | --- | --- |
| id | string | Unique ID of the custom field |
| name | string | Friendly name of the custom field |
| value | string | Underlying value of the field |
| displayValue | string | Shown value of the field |

### ChangeInfo Definition

| Name | Type | Description |
| --- | --- | --- |
| createdDate | dateTime | Date/time that the server was created |
| createdBy | string | Who created the server |
| modifiedDate | dateTime | Date/time that the server was last updated |
| modifiedBy | string | Who modified the server last |

### Examples

#### JSON

    {
      "id": "WA1ALIASWB01",
      "name": "WA1ALIASWB01",
      "description": "My web server",
      "groupId": "2a5c0b9662cf4fc8bf6180f139facdc0",
      "isTemplate": false,
      "locationId": "WA1",
      "osType": "Windows 2008 64-bit",
      "status": "active",
      "details": {
        "ipAddresses": [
          {
            "internal": "10.82.131.44"
          },
          {
            "public": "91.14.111.101",
            "internal": "10.82.131.45"
          }
        ],
        "alertPolicies": [
          {
            "id": "15836e6219e84ac736d01d4e571bb950",
            "name": "Production Web Servers - RAM",
            "links": [
              {
                "rel": "self",
                "href": "/v2/alertPolicies/alias/15836e6219e84ac736d01d4e571bb950"
              },
              {
                "rel": "alertPolicyMap",
                "href": "/v2/servers/alias/WA1ALIASWB01/alertPolicies/15836e6219e84ac736d01d4e571bb950",
                "verbs": [
                  "DELETE"
                ]
              }
            ]
          },
          {
            "id": "2bec81dd90aa4217887548c3c20d7421",
            "name": "Production Web Servers - Disk",
            "links": [
              {
                "rel": "self",
                "href": "/v2/alertPolicies/alias/2bec81dd90aa4217887548c3c20d7421"
              },
              {
                "rel": "alertPolicyMap",
                "href": "/v2/servers/alias/WA1ALIASWB01/alertPolicies/2bec81dd90aa4217887548c3c20d7421",
                "verbs": [
                  "DELETE"
                ]
              }
            ]
          }
        ],
        "cpu": 2,
        "diskCount": 1,
        "hostName": "WA1ALIASWB01.customdomain.com",
        "inMaintenanceMode": false,
        "memoryMB": 4096,
        "powerState": "started",
        "storageGB": 60,
        "disks":[
          {
            "id":"0:0",
            "sizeGB":60,
            "partitionPaths":[]
          }
        ],
        "partitions":[
          {
            "sizeGB":59.654,
            "path":"C:\\"
          }
        ],
        "snapshots": [
          {
            "name": "2014-05-16.23:45:52",
            "links": [
              {
                "rel": "self",
                "href": "/v2/servers/alias/WA1ALIASWB01/snapshots/40"
              },
              {
                "rel": "delete",
                "href": "/v2/servers/alias/WA1ALIASWB01/snapshots/40"
              },
              {
                "rel": "restore",
                "href": "/v2/servers/alias/WA1ALIASWB01/snapshots/40/restore"
              }
            ]
          }
        ],
        "customFields": [
          {
            "id": "22f002123e3b46d9a8b38ecd4c6df7f9",
            "name": "Cost Center",
            "value": "IT-DEV",
            "displayValue": "IT-DEV"
          },
          {
            "id": "58f83af6123846769ee6cb091ce3561e",
            "name": "CMDB ID",
            "value": "1100003",
            "displayValue": "1100003"
          }
        ]
      },
      "type": "standard",
      "storageType": "standard",
      "changeInfo": {
        "createdDate": "2012-12-17T01:17:17Z",
        "createdBy": "user@domain.com",
        "modifiedDate": "2014-05-16T23:49:25Z",
        "modifiedBy": "user@domain.com"
      },
      "links": [
        {
          "rel": "self",
          "href": "/v2/servers/alias/WA1ALIASWB01",
          "id": "WA1ALIASWB01",
          "verbs": [
            "GET",
            "PATCH",
            "DELETE"
          ]
        },
        {
          "rel": "group",
          "href": "/v2/groups/alias/2a5c0b9662cf4fc8bf6180f139facdc0",
          "id": "2a5c0b9662cf4fc8bf6180f139facdc0"
        },
        {
          "rel": "account",
          "href": "/v2/accounts/alias",
          "id": "alias"
        },
        {
          "rel": "billing",
          "href": "/v2/billing/alias/estimate-server/WA1ALIASWB01"
        },
        {
          "rel": "statistics",
          "href": "/v2/servers/alias/WA1ALIASWB01/statistics"
        },
        {
          "rel": "scheduledActivities",
          "href": "/v2/servers/alias/WA1ALIASWB01/scheduledActivities"
        },
        {
          "rel": "publicIPAddresses",
          "href": "/v2/servers/alias/WA1ALIASWB01/publicIPAddresses",
          "verbs": [
            "POST"
          ]
        },
        {
          "rel": "alertPolicyMappings",
          "href": "/v2/servers/alias/WA1ALIASWB01/alertPolicies",
          "verbs": [
            "POST"
          ]
        },
        {
          "rel": "antiAffinityPolicyMapping",
          "href": "/v2/servers/alias/WA1ALIASWB01/antiAffinityPolicy",
          "verbs": [
            "DELETE",
            "PUT"
          ]
        },
        {
          "rel": "cpuAutoscalePolicyMapping",
          "href": "/v2/servers/alias/WA1ALIASWB01/cpuAutoscalePolicy",
          "verbs": [
            "DELETE",
            "PUT"
          ]
        },
        {
          "rel": "capabilities",
          "href": "/v2/servers/alias/WA1ALIASWB01/capabilities"
        },
        {
          "rel": "credentials",
          "href": "/v2/servers/alias/WA1ALIASWB01/credentials"
        },
        {
          "rel": "publicIPAddress",
          "href": "/v2/servers/alias/WA1ALIASWB01/publicIPAddresses/91.14.111.101",
          "id": "91.14.111.101",
          "verbs": [
            "GET",
            "PUT",
            "DELETE"
          ]
        }
      ]
    }
