{{{ "title": "Configure Intrusion Protection Service Notifications",
        "date": "03-4-2016",
        "author": "Client-Security",
        "attachments": [],
        "contentIsHTML": false,
        "sticky": false }}}

Configures notifications associated with an IPS agent running on a designated host. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation to configure the notifications of an installed IPS agent on CenturyLink Cloud servers.

The calls below will perform all of the operations for configuring, retrieving, updating, and deleting a notification destination.

### Supported Managed Operating Systems
Current supported operating systems can be found here [Operating System Support](https://www.ctl.io/knowledge-base/security/supported-ips-oses/)

## URL

### Structure

#### Create and Update

  PUT https://api.client-security.ctl.io/ips/api/notifications/{accountAlias}/{serverName}

#### Retrieve

  GET https://api.client-security.ctl.io/ips/api/notifications/{accountAlias}/{serverName}

#### Delete

  DELETE https://api.client-security.ctl.io/ips/api/notifications/{accountAlias}/{serverName}

## Example

    PUT https://api.client-security.ctl.io/ips/api/notifications/ALIAS/VA1ALIASTEST04

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| accountAlias | string | Short code for a particular account | Yes |
| serverName | string | The name of the server that has the agent already installed | Yes |

### Content Properties

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| notificationDestinations | array | List of Notification Destinations | Yes |       

#### Notification Destination Definition

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| url | string | The URL endpoint for WEBHOOK or SLACK notification | No |
| typeCode | string | This is the type of destination (either `SYSLOG`, `EMAIL`, or `WEBHOOK`) | Yes |
| sysLogSettings| array |This contains all of the options for SYSLOG | No |
| emailAddress| string |This object will contain options for an EMAIL notification | No |

#### SysLogSettings Definition
| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| ipAddress  | string  | The IP address of customers syslog server | Yes |
| udpPort    | integer | The port the syslog is listening on | Yes |
| facility   | integer | This is an Integer, 16-23, to set the type of [program logging messages](https://en.wikipedia.org/wiki/Syslog). | Yes |

### Example

  PUT http://api.client-security.ctl.io/ips/api/notification/ALIAS/VA1ALIASMYSVR01

    {
        "url": "http://my.slack.webhook",
        "typeCode": "SLACK"
    },
    {
        "url": "http://my.generic.webhook",
        "typeCode": "WEBHOOK"
    },
    {
        "typeCode": "SYSLOG",
        "sysLogSettings":
            {
                "ipAddress": "12345",
                "udpPort": "8081",
                "facility": "16"
            }
    },
    {
        "typeCode": "EMAIL",
        "emailAddress": "youremail@site.com"
    }

## Response

The response will not contain JSON content, but should return the `HTTP 204 No Content` response. For details on what's included in each alert, please refer to [this knowledge base article](https://www.ctl.io/knowledge-base/security/ips-api/).
