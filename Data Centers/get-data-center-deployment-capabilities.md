{{{
  "title": "Get Data Center Deployment Capabilities",
  "date": "11-21-2014",
  "author": "Bryan Friedman",
  "attachments": []
}}}

Gets the list of capabilities that a specific data center supports for a given account, including the deployable networks, OS templates, and whether features like premium storage and shared load balancer configuration are available. Calls to this operation must include a token acquired from the authentication endpoint. See the <a href="/api-docs/v2#authentication-login">Login API</a> for information on acquiring this token.

### When to Use It

Use this API operation when you want to discover the available capabilities of a data center for your account. Specifically, this operation is helpful for retrieving network identifiers and OS template names to use when creating a server.

### Supported HTTP Verbs

Requests to this endpoint are done via HTTP GET.

## URL

### Structure

    https://api.tier3.com/v2/datacenters/{accountAlias}/{dataCenter}/deploymentCapabilities

### Example

    https://api.tier3.com/v2/datacenters/ALIAS/UC1/deploymentCapabilities

## Request

### URI Parameters

<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
      <th>Description</th>
      <th>Req.</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>AccountAlias</td>
      <td>string</td>
      <td>Short code for a particular account</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>DataCenter</td>
      <td>string</td>
      <td>Short string representing the data center you are querying. Valid codes can be retrieved from the&nbsp;<a href="https://t3n.zendesk.com/entries/31303140-Get-Data-Center-List">List Data Centers</a> API operation.</td>
      <td>Yes</td>
    </tr>
  </tbody>
</table>

## Response

### Entity Definition

<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>supportsPremiumStorage</td>
      <td>boolean</td>
      <td>Whether or not this data center provides support for servers with premium storage</td>
    </tr>
    <tr>
      <td>supportsSharedLoadBalancer</td>
      <td>boolean</td>
      <td>Whether or not this data center provides support for shared load balancer configuration</td>
    </tr>
    <tr>
      <td>deployableNetworks</td>
      <td>array</td>
      <td>Collection of networks that can be used for deploying servers</td>
    </tr>
    <tr>
      <td>templates</td>
      <td>array</td>
      <td>Collection of available templates in the data center that can be used to create servers</td>
    </tr>
  </tbody>
</table>

### DeployableNetworks Definition

<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>name</td>
      <td>string</td>
      <td>User-defined name of the network</td>
    </tr>
    <tr>
      <td>networkId</td>
      <td>string</td>
      <td>Unique identifier of the network</td>
    </tr>
    <tr>
      <td>type</td>
      <td>string</td>
      <td>Network type, usually "private" for networks created by the user</td>
    </tr>
    <tr>
      <td>accountID</td>
      <td>string</td>
      <td>Account alias for the account in which the network exists</td>
    </tr>
  </tbody>
</table>

### Templates Definition

<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>name</td>
      <td>string</td>
      <td>Underlying unique name for the template</td>
    </tr>
    <tr>
      <td>description</td>
      <td>string</td>
      <td>Description of the template at it appears in the Control Portal UI</td>
    </tr>
    <tr>
      <td>storageSizeGB</td>
      <td>int</td>
      <td>The amount of storage allocated for the primary OS root drive</td>
    </tr>
    <tr>
      <td>capabilities</td>
      <td>array</td>
      <td>List of capabilities supported by this specific OS template (example: whether adding CPU or memory requires a reboot or not)</td>
    </tr>
    <tr>
      <td>reservedDrivePaths</td>
      <td>array</td>
      <td>List of drive path names reserved by the OS that can't be used to name user-defined drives</td>
    </tr>
    <tr>
      <td>drivePathLength</td>
      <td>int</td>
      <td>Length of the string for naming a drive path, if applicable</td>
    </tr>
  </tbody>
</table>

### Examples

### JSON

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
          "name":"CENTOS-6-64-TEMPLATE",
          "description":"CentOS 6 | 64-bit",
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
        },
        {
          "name":"RHEL-6-64-TEMPLATE",
          "description":"RedHat Enterprise Linux 6 | 64-bit",
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
          "name":"WIN2008R2ENT-64",
          "description":"Windows 2008 R2 Enterprise | 64-bit",
          "storageSizeGB":60,
          "capabilities":[],
          "reservedDrivePaths":[
            "a",
            "b",
            "c",
            "d"
          ],
          "drivePathLength":1
        },
        {
          "name":"WIN2008R2STD-64",
          "description":"Windows 2008 R2 Standard | 64-bit",
          "storageSizeGB":60,
          "capabilities":[],
          "reservedDrivePaths":[
            "a",
            "b",
            "c",
            "d"
          ],
          "drivePathLength":1
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
        }
      ]
    }
