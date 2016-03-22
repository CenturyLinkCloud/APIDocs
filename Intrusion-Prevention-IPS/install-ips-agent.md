{{{ "title": "Install Intrusion Protection Service Agent",
        "date": "03-4-2016",
        "author": "Client-Security",
        "attachments": [],
        "contentIsHTML": false,
        "sticky": false }}}

Installs an IPS agent on the designated host. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation to install an IPS agent on CenturyLink Cloud servers.

### Supported Managed Operating Systems
Current supported operating systems can be found here [Operating System Support](https://www.ctl.io/knowledge-base/security/supported-ips-oses/)

## URL

### Structure

    POST https://api.client-security.ctl.io/ips/api/app/

### Example

    POST https://api.client-security.ctl.io/ips/api/app/

## Request

### Content Properties

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| hostName | string | The name of the server that will ha Data center location of the anti-affinity policy. | Yes |
| accountAlias | string | Short code for a particular account | Yes |

### Example

#### JSON

    {
        "hostName":"VA1ALIASTEST04",
        "accountAlias":"ALIAS"
    }

## Response

The response will not contain JSON content, but should return the `HTTP 204 No Content` response upon the install of the agent.
