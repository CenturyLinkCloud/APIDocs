{{{
  "title": "Delegate Management of an existing Instance",
  "date": "1-10-2018",
  "author": "Ignacio Martin",
  "attachments": [],
  "contentIsHTML": false
}}}

This service allows the user to delegate the management of an existing Instance to CenturyLink.

### When to Use It

Use this API operation if you want CL to be able to manage your instance on your behalf.

NOTE: The following requirements need to be met in order to be able to make an instance managed:

- Only "compute" instances (Linux and Windows) can be managed.
- Terms and conditions need to be accepted. In order to do this, the following url param needs to be set to true:
```json
accept_terms=true
```
- The Instance needs to be in "Done" status.
- The user making the request needs to have admin permissions on the instance.
- The company owning the instance needs to support "Delegate Management".

### Supported Operating Systems

* Linux
* Windows

## URL

### Structure

    [PUT] /services/instances/{instance_id}/make_managed_os

### Example

    POST https://api.ctl.io/v2/instances/my_instance_id/make_managed_os?accept_terms=true

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| InscanceId | string | Id of the Instance | Yes |
| accept_terms | boolean | Indicates that the client accepts the terms and conditions | Yes |