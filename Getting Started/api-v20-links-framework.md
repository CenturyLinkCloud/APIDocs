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

Each link entity defines the following properties. For more details about each specific link type, see the [Link Definitions](../Link Definitions/shared-links.md) for each resource type.

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| rel | string | The link type, as described in the table below. | Yes |
| href | string | Address of the resource. | Yes |
| id | string | Unique ID of the resource. | No |
| name | string | Friendly name of the resource. | No |
| verbs | array | Valid HTTP verbs that can act on this resource. If none are explicitly listed, GET is assumed to be the only one. | No |
