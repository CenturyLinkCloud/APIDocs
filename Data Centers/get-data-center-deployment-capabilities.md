{{{
  "title": "Get Data Center Deployment Capabilities",
  "date": "11-21-2014",
  "author": "Bryan Friedman",
  "attachments": []
}}}

Gets the list of capabilities that a specific data center supports for a given account, including the deployable networks, OS templates, and whether features like premium storage and shared load balancer configuration are available. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to discover the available capabilities of a data center for your account. Specifically, this operation is helpful for retrieving network identifiers and OS template names to use when creating a server.

## URL

### Structure

    GET https://api.ctl.io/v2/datacenters/{accountAlias}/{dataCenter}/deploymentCapabilities

### Example

    GET https://api.ctl.io/v2/datacenters/ALIAS/UC1/deploymentCapabilities

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | string | Short code for a particular account | Yes |
| DataCenter | string | Short string representing the data center you are querying. Valid codes can be retrieved from the [Get Data Center List](get-data-center.md) API operation. | Yes |

## Response

### Entity Definition

| Name | Type | Description |
| --- | --- | --- |
| supportsPremiumStorage | boolean | Whether or not this data center provides support for servers with premium storage |
| supportsSharedLoadBalancer | boolean | Whether or not this data center provides support for shared load balancer configuration |
| deployableNetworks | array | Collection of networks that can be used for deploying servers |
| templates | array | Collection of available templates in the data center that can be used to create servers |

### DeployableNetworks Definition

| Name | Type | Description |
| --- | --- | --- |
| name | string | User-defined name of the network |
| networkId | string | Unique identifier of the network |
| type | string | Network type, usually "private" for networks created by the user |
| accountID | string | Account alias for the account in which the network exists |

### Templates Definition

| Name | Type | Description |
| --- | --- | --- |
| name | string | Underlying unique name for the template |
| description | string | Description of the template at it appears in the Control Portal UI |
| storageSizeGB | integer | The amount of storage allocated for the primary OS root drive |
| capabilities | array | List of capabilities supported by this specific OS template (example: whether adding CPU or memory requires a reboot or not) |
| reservedDrivePaths | array | List of drive path names reserved by the OS that can't be used to name user-defined drives |
| drivePathLength | integer | Length of the string for naming a drive path, if applicable |

### Examples

#### JSON

    {
      "supportsPremiumStorage":true,
      "supportsSharedLoadBalancer":true,
      "deployableNetworks":[
        {
          "name":"My Network",
          "networkId":"a933432bd8894e84b6c4fb123e48cb8b",
          "type":"private",
          "accountID":"ACCT"
        }
      ],
      "templates":[
        {
          "name":"UBUNTU-14-64-TEMPLATE",
          "description":"Ubuntu 14 | 64-bit",
          "storageSizeGB":17,
          "capabilities":[
            "cpuAutoscale"
          ],
          "reservedDrivePaths":[
            "bin",
            "boot",
            "build",
            "cdrom",
            "compat",
            "dist",
            "dev",
            "entropy",
            "etc",
            "home",
            "initrd.img",
            "lib",
            "lib64",
            "libexec",
            "lost+found",
            "media",
            "mnt",
            "opt",
            "proc",
            "root",
            "sbin",
            "selinux",
            "srv",
            "sys",
            "tmp",
            "usr",
            "var",
            "vmlinuz"
          ]
        },
        {
          "name":"WIN2012R2DTC-64",
          "description":"Windows 2012 R2 Datacenter Edition | 64-bit",
          "storageSizeGB":60,
          "capabilities":[
            "cpuAutoscale"
          ],
          "reservedDrivePaths":[
            "a",
            "b",
            "c",
            "d"
          ],
          "drivePathLength":1
        },
        {
          "name":"WA1ACCTCUST01",
          "description":"My Custom Template",
          "storageSizeGB":16,
          "capabilities":[
            "cpuAutoscale"
          ],
          "reservedDrivePaths":[
            "bin",
            "boot",
            "build",
            "cdrom",
            "compat",
            "dist",
            "dev",
            "entropy",
            "etc",
            "home",
            "initrd.img",
            "lib",
            "lib64",
            "libexec",
            "lost+found",
            "media",
            "mnt",
            "opt",
            "proc",
            "root",
            "sbin",
            "selinux",
            "srv",
            "sys",
            "tmp",
            "usr",
            "var",
            "vmlinuz"
          ]
        }
      ]
    }
