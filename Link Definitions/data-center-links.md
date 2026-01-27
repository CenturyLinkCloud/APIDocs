{{{
  "title": "Data Center Links",
  "date": "03-27-2015",
  "author": "Bryan Friedman",
  "attachments": [],
  "sticky": "true"
}}}

### Overview

The following link definitions are related to the data center resource. They may be returned when making a call to [Get Data Center List](../Data Centers/get-data-center-list.md) or other data center-related resources.

### Data Center Link Definitions

| Relation (rel) | Description | Verbs |
| --- | --- | --- |
| availableOvfs | Retrieve the list of available servers that can be imported. These are OVFs that have been uploaded to the FTP server. | [GET](../Servers/get-available-server-imports.md) |
| computeLimits | Retrieve or modify the limits for CPU, memory, storage allowed in the data center for the account. | GET / POST |
| deploymentCapabilities | Retrieve the list of capabilities that a specific data center supports, including the deployable networks and OS templates. | [GET](../Data Centers/get-data-center-deployment-capabilities.md) |
| loadBalancers | Retrieve the list of shared load balancers in the data center for the account. | [GET](../Shared Load Balancers/get-shared-load-balancers.md) / [POST](../Shared Load Balancers/create-shared-load-balancer.md) |
| networkLimits | Retrieve the limits for number of networks allowed in the data center for the account. | GET |
