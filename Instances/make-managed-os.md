{{{
  "title": "Delegate Management of an existing Instance",
  "date": "9-12-2018",
  "author": "Guillermo Sanchez",
  "keywords": ["managed", "instance", "msa"],
  "attachments": [],
  "contentIsHTML": false
}}}

This service allows the user to delegate the management of an existing Instance to CenturyLink.

### When to Use It

Use this API operation if you want CL to be able to manage your instance on your behalf.

**NOTE**: The following requirements need to be met in order to be able to make an instance managed:

- Only "compute" instances (Linux and Windows) can be managed.
- Terms and conditions need to be accepted. In order to do this, the following url param needs to be set to true:
    ```json
    accept_terms=true
    ```
- The Instance needs to be in "Done" status.
- The user making the request needs to have **write** permissions on the instance.
- The company owning the instance needs to support "Delegate Management".

### Supported Operating Systems

- Linux
- Windows

### URL

#### Structure

    [PUT] /services/instances/{instance_id}/make_managed_os

#### Example

    PUT https://cam.ctl.io/services/instances/i-fbs9ow/make_managed_os?accept_terms=true

### Request

#### Headers

```
Content-Type: application/json
Authorization: Bearer your_json_web_token
ElasticBox-Release: 4.0
```

#### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| InscanceId | string | Id of the Instance | Yes |
| accept_terms | boolean | Indicates that the client accepts the terms and conditions | Yes |

### Response

#### Normal Response Codes

- **202** Accepted

#### Common Error Response Codes

- Bad Request (**400**) - Request includes invalid, incomplete or missing parameters (details provided inside body)
- Unauthorized (**401**) - Invalid access token/cookie
- Forbidden (**403**) - User doesn’t belong to the organization
- Not Found (**404**) - Organization not found
