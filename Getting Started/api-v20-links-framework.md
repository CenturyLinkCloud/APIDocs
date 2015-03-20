{{{
  "title": "API v2.0 Links Framework",
  "date": "03-19-2015",
  "author": "Bryan Friedman",
  "attachments": []
}}}

### Overview

The CenturyLink Cloud v2 REST API utilizes the concept of "linking" to reference other related entities from within JSON response payloads. Many of the JSON response entities include a `links` attribute which contains an array of link entities for resources that are related the object that was just acted upon.

This link model helps with both discoverability as well as use-case scalability. In addition, it provides a mechanism for exposing only those endpoints that are available to a user based on their role. In other words, a user will only see links and associated actions that they have access to. Each link entity contains a URL in the `href` attribute so the API user may simply follow the link to perform a followup action.

### Link Entity

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| rel | string | The link type, as described in the table below. | Yes |
| href | string | Address of the resource. | Yes |
| id | string | Unique ID of the resource. | No |
| name | string | Friendly name of the resource. | No |
| verbs | array | Valid HTTP verbs that can act on this resource. If none are explicitly listed, GET is assumed to be the only one. | No |

### Link Definitions

#### Shared

| Relation (rel) | Description | Verbs |
| --- | --- | --- |
| self | A special link that references the resource itself. Useful if the API users wishes to act on the same resource again. | - |
| account | Retrieve the account for the given resource. | GET |
| group | Retrieve a group related to the resource (such as the group for a given server). | [GET](../Groups/get-group.md) |
| status | Retrieve the status information for the given job in the queue. | [GET](../Queue/get-status.md) |
| server | Retrieve a server related to the resource (such as servers in the given group). | [GET](../Servers/get-server.md) |


#### Groups

| Relation (rel) | Description | Verbs |
| --- | --- | --- |
| archiveGroupAction | Archive the given group. | [POST](../Group Actions/archive-group.md)
| billing | Retrieve billing information for the given group. | [GET](../Group/get-group-billing-details.md) |
| createGroup | Create a group. | [POST](../Groups/create-group.md) |
| defaults | Retrieve or modify the default values of the given group. | GET / POST |
| parentGroup | Retrieve the parent group of the given group. | [GET](../Groups/get-group.md) |
| scheduledActivities | Retrieve the list of scheduled activities for the given group. | GET |
| statistics | Retrieve resource consumption information for servers within the given group hierarchy. | [GET](../Group/get-group-monitoring-statistics.md) |
| upcomingScheduledActivities | Retrieve the list of upcoming scheduled activities for the given group. | GET |

#### Servers

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
| publicIPAddress | Retrieve or modify a public IP address of the specific server. | [GET](../Public IP/get-public-ip-address.md) / [DELETE](../Public IP/remove-public-ip-address.md) / [PUT](../Public IP/update-public-ip-address.md) |
| publicIPAddresses | Add a public IP address for the given server. | [POST](../Public IP/add-public-ip-address.md) |
| scheduledActivities | Retrieve the list of scheduled activities for the given server. | GET |
| statistics | Retrieve resource consumption information for the given server. | GET |

#### Server Snapshots

| Relation (rel) | Description | Verbs |
| --- | --- | --- |
| delete | Delete the snapshot for the given server. | DELETE |
| restore | Restore the snapshot for the given server. | POST |
