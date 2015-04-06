{{{
  "title": "Shared Links",
  "date": "03-27-2015",
  "author": "Bryan Friedman",
  "attachments": [],
  "sticky": "true"
}}}

### Overview

The following link definitions are related to all types of resources. 

### Shared Link Definitions

| Relation (rel) | Description | Verbs |
| --- | --- | --- |
| self | A special link that references the resource itself. Useful if the API users wishes to act on the same resource again. | - |
| account | Retrieve the account for the given resource. | GET |
| group | Retrieve a group related to the resource (such as the group for a given server). | [GET](../Groups/get-group.md) |
| status | Retrieve the status information for the given job in the queue. | [GET](../Queue/get-status.md) |
| server | Retrieve a server related to the resource (such as servers in the given group). | [GET](../Servers/get-server.md) |
