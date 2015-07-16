{{{
  "title": "Get Data Center Bare Metal Capabilities",
  "date": "07-15-2015",
  "author": "Bryan Friedman",
  "attachments": []
}}}

Gets the list of bare metal capabilities that a specific data center supports for a given account, including the list of configuration types and the list of supported operating systems. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to discover the available capabilities of related to provisioning bare metal servers in a data center for your account. Specifically, this operation is helpful for retrieving the list of configuration identifiers and OS types to use when creating a bare metal server.

## URL

### Structure

    GET https://api.ctl.io/v2/datacenters/{accountAlias}/{dataCenter}/bareMetalCapabilities

### Example

    GET https://api.ctl.io/v2/datacenters/ALIAS/VA1/bareMetalCapabilities

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
| skus | array | Collection of available bare metal configuration types to pass in to configurationId when creating a bare metal server |
| operatingSystems | array | Collection of available operating systems when creating a bare metal server |

### SKUs Definition

| Name | Type | Description |
| --- | --- | --- |
| id | string | The configurationId to pass to the [Create Server](../Server/create-server.md) API operation when creating a bare metal server. |
| hourlyRate | number | Price per hour for the given configuration. |
| availability | string | The level of availability for the given configuration: either `high`, `low`, or `none `. |
| memory | complex | Information about the memory on the server. |
| processor | complex | Information about the physical processors on the server. |
| storage | complex | Collection of disk information, each item representing one physical disk on the server. |

### Memory Definition
| Name | Type | Description |
| --- | --- | --- |
| capacityGB | number | Memory capacity in gigabytes |

### Processor Definition
| Name | Type | Description |
| --- | --- | --- |
| coresPerSocket | number | Number of cores for each processor socket |
| description | string | Description of the processor including model and clock speed |
| sockets | number | Number of sockets |

### Storage Definition
| Name | Type | Description |
| --- | --- | --- |
| type | string | Drive capacity in gigabytes |
| description | string | Friendly description for the OS type |
| hourlyRatePerSocket | number | Price per hour per socket for the OS type.  |

### OperatingSystems Definition

| Name | Type | Description |
| --- | --- | --- |
| capacityGB | number | Underlying unique name for the OS type |
| speedRpm | number | RPM (revolutions per minutes) speed of the disk |
| type | string | Disk type. Only `Hdd` currently supported. |

### Examples

#### JSON

    {
      "skus": [
        {
          "id": "529e2592a3e640a7c2617b5e8bc8feaed95eab22",
          "hourlyRate": 0.56,
          "availability": "high",
          "memory": [
            {
              "capacityGB": 16
            }
          ],
          "processor": {
            "coresPerSocket": 4,
            "description": "Intel(R) Xeon(R) CPU E3-1271 v3 @ 3.60GHz",
            "sockets": 1
          },
          "storage": [
            {
              "capacityGB": 1000,
              "speedRpm": 7200,
              "type": "Hdd"
            },
            {
              "capacityGB": 1000,
              "speedRpm": 7200,
              "type": "Hdd"
            }
          ]
        },
        {
          "id": "f24b18ba2ce23657657444601649c7b8b7f9b60c",
          "hourlyRate": 1.65,
          "availability": "none",
          "memory": [
            {
              "capacityGB": 64
            }
          ],
          "processor": {
            "coresPerSocket": 6,
            "description": "Intel(R) Xeon(R) CPU E5-2620 v3 @ 2.40GHz",
            "sockets": 2
          },
          "storage": [
            {
              "capacityGB": 2000,
              "speedRpm": 7200,
              "type": "Hdd"
            },
            {
              "capacityGB": 2000,
              "speedRpm": 7200,
              "type": "Hdd"
            },
            {
              "capacityGB": 2000,
              "speedRpm": 7200,
              "type": "Hdd"
            },
            {
              "capacityGB": 2000,
              "speedRpm": 7200,
              "type": "Hdd"
            }
          ]
        }
      ],
      "operatingSystems": [
        {
          "type": "centOS6_64Bit",
          "description": "CentOS 6 64-bit",
          "hourlyRatePerSocket": 0
        },
        {
          "type": "redHat6_64Bit",
          "description": "RedHat Enterprise Linux 6 64-bit",
          "hourlyRatePerSocket": 0.075
        },
        {
          "type": "windows2012R2Standard_64bit",
          "description": "Windows 2012 R2 Standard 64-bit",
          "hourlyRatePerSocket": 0.04
        }
      ]
    }
