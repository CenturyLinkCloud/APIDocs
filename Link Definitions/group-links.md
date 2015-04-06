{{{
  "title": "Group Links",
  "date": "03-27-2015",
  "author": "Bryan Friedman",
  "attachments": [],
  "sticky": "true"
}}}

### Overview

The following link definitions are related to the groups resource. They may be returned when making a call to [Get Group](../Groups/get-group.md) or other group-related resources.

### Group Link Definition

| Relation (rel) | Description | Verbs |
| --- | --- | --- |
| archiveGroupAction | Archive the given group. | [POST](../Group Actions/archive-group.md)
| billing | Retrieve billing information for the given group. | [GET](../Group/get-group-billing-details.md) |
| createGroup | Create a group. | [POST](../Groups/create-group.md) |
| defaults | Retrieve or modify the default values of the given group. | GET / POST |
| parentGroup | Retrieve the parent group of the given group. | [GET](../Groups/get-group.md) |
| scheduledActivities | Retrieve the list of scheduled activities for the given group. | GET |
| upcomingScheduledActivities | Retrieve the list of upcoming scheduled activities for the given group. | GET |
