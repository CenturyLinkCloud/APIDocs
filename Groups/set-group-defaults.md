{{{
  "title": "Group Defaults",
  "date": "02-27-2015",
  "author": "Bryan Friedman",
  "attachments": []
}}}

Set group defaults. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to set group defaults.

## URL

### Structure

    POST https://api.ctl.io/v2/groups/{accountAlias}/{groupId}

### Example

    POST https://api.ctl.io/v2/groups/ALIAS/2a5c0b9662cf4fc8bf6180f139facdc0

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | string | Short code for a particular account | Yes |
| GroupID | string | ID of the group being queried. Retrieved from query to parent group, or by looking at the URL on the new UI pages in the Control Portal | Yes |

### Content Properties

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| cpu | integer | Number of processors to configure the server with (1-16) (ignored for bare metal servers) | No |
| memoryGB | integer | Number of GB of memory to configure the server with (1-128) (ignored for bare metal servers) | No |
| networkId | string |ID of the Network. This can be retrieved from the Get Network List API operation. | No |
| primaryDns | string | Primary DNS to set on the server. If not supplied the default value set on the account will be used. | No |
| secondaryDns | string | Secondary DNS to set on the server. If not supplied the default value set on the account will be used. | No |
| templateName | string | Name of the template to use as the source. The list of available templates for a given account in a data center can be retrieved from the [Get Data Center Deployment Capabilities](../Data Centers/get-data-center-deployment-capabilities.md) API operation. (Ignored for bare metal servers.) | No |

### Examples

#### JSON
```
{
  "cpu": "1",
  "memoryGB": "2",
  "networkId": "fb46f06f8278421d8e94d78cf6409ba5",
  "primaryDns": "8.8.8.8",
  "secondaryDns": "8.8.4.4",
  "templateName": "UBUNTU-10-64-TEMPLATE"
}
```
## Response

### Cpu Definition

| Name | Type | Description |
| --- | --- | --- |
| value | int | How many vCPUs are allocated to the server |
| inherited | bool | Whether the value is set explicitly (false) or by its parent (true) |

### Memory Definition

| Name | Type | Description |
| --- | --- | --- |
| value | int | How many GB of memory are allocated to the server |
| inherited | bool | Whether the value is set explicitly (false) or by its parent (true) |

### Network Definition

| Name | Type | Description |
| --- | --- | --- |
| value | string | ID of the Network |
| inherited | bool | Whether the value is set explicitly (false) or by its parent (true) |

### PrimaryDNS Definition

| Name | Type | Description |
| --- | --- | --- |
| value | string | Primary DNS set on the server |
| inherited | bool | Whether the value is set explicitly (false) or by its parent (true) |

### SecondaryDNS Definition

| Name | Type | Description |
| --- | --- | --- |
| value | string | Secondary DNS set on the server |
| inherited | bool | Whether the value is set explicitly (false) or by its parent (true) |

### TemplateName Definition

| Name | Type | Description |
| --- | --- | --- |
| value | string | ID  | Name of the default template |
| inherited | bool | Whether the value is set explicitly (false) or by its parent (true) |

### Examples

#### JSON
```
{
  "cpu": {
    "value": 1,
    "inherited": false
  },
  "memoryGB": {
    "value": 2,
    "inherited": false
  },
  "networkId": {
    "value": "ee600a2b4b734aac8ab0de2642597433",
    "inherited": true
  },
  "primaryDns": {
    "value": "8.8.8.8",
    "inherited": false
  },
  "secondaryDns": {
    "value": "8.8.4.4",
    "inherited": false
  },
  "templateName": {
    "value": "UBUNTU-10-64-TEMPLATE",
    "inherited": false
  }
}
```
