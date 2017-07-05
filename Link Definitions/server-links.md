{{{
  "title": "Server Links",
  "date": "03-27-2015",
  "author": "Bryan Friedman",
  "attachments": [],
  "sticky": "true"
}}}

### Overview

The following link definitions are related to the servers resource. They may be returned when making a call to [Get Server](../Servers/get-server.md) or other server-related resources.

### Server Link Definitions

| Relation (rel) | Description | Verbs |
| --- | --- | --- |
| alertPolicyMap | Retrieve or modify the given alert policy for the given server. | GET / DELETE |
| alertPolicyMappings | Retrieve or modify the list of alert policies for the given server. | GET / PUT / DELETE |
| antiAffinityPolicyMapping | Retrieve or modify the anti-affinity policy for the given server. | GET / PUT / DELETE |
| billing | Retrieve billing information for the given server. | GET |
| capabilities | Retrieve the supported capabilities listing for the given server. | GET |
| cpuAutoscalePolicyMapping | Retrieve or modify the vertical autoscale policy for the given server. | GET / PUT / DELETE |
| createServer | Create a server. | [POST](../Servers/create-server.md) |
| credentials | Retrieve credentials for the given server. | [GET](../Servers/get-server-credentials.md)
| publicIPAddress | Retrieve or modify a public IP address of the specific server. | [GET](../Firewall/get-public-ip-address.md) / [DELETE](../Firewall/remove-public-ip-address.md) / [PUT](../Firewall/update-public-ip-address.md) |
| publicIPAddresses | Add a public IP address for the given server. | [POST](../Firewall/add-public-ip-address.md) |
| scheduledActivities | Retrieve the list of scheduled activities for the given server. | GET |

### Server Snapshot Definitions

| Relation (rel) | Description | Verbs |
| --- | --- | --- |
| delete | Delete the snapshot for the given server. | DELETE |
| restore | Restore the snapshot for the given server. | POST |
