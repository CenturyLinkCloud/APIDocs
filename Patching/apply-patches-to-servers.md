{{{
  "title": "Applying Patches to Operating Systems",
  "date": "3-14-2016",
  "author": "Benjamin Swoboda",
  "attachments": [],
  "contentIsHTML": false
}}}

This service allows the user to patch virtual machines to the latest available patches provided by the OS vendor, using the [Execute Package API](../Server Actions/execute-package.md). It does not discriminate patches based on patch severity or any other vendor categorization. The package will kick off one or multiple attempts to apply patches, including a series of reboots. Reboots will cease and the execution will complete when there are no more patches to apply. Additional information on this capability is in [this knowledge base article](https://www.ctl.io/knowledge-base/servers/patching-as-a-service/).

Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation to patch operating systems with updates from OS vendors.

NOTE: Servers require Internet access to be patched. It is also recommended to place servers in Maintenance Mode before patching. Further, an API request can deploy against all VMs a user is authorized to administer under a single alias.

### Supported Operating Systems

Currently, the Operating Systems that may be updated with this service are show below:

* CentOS 5
* CentOS 6
* Red Hat Enterprise Linux 6
* Red Hat Enterprise Linux 5
* Red Hat Enterprise Linux 7
* Windows 2012
* Windows 2012R2

#### Exceptions

* Red Hat Enterprise Linux and CentOS: This service will exclude some updates. It will exclude kernel patches and `nss` packages.

### Package Details

| Operating Systems | Blueprint Name | Script Package Name | Package ID |
| --- | --- | --- | --- |
| Windows 2012 and 2012R2 | Auto Patching Windows 2012 | Auto Patching Windows 2012 | b229535c-a313-4a31-baf8-6aa71ff4b9ed |
| Red Hat Enterprise Linux 5, 6, and 7 OR CentOS 5 and 6 | Yum Update Script | Yum Update | c3c6642e-24e1-4c37-b56a-1cf1476ee360 |

### Example

#### JSON

```json
{
    "servers": [
        "WA1ALIASSERV0101"
    ],
    "package": {
        "packageId": "c3c6642e-24e1-4c37-b56a-1cf1476ee360",
        "parameters": {"patch.debug.mode": "false"

        }
    }
}
```

### Response

The response will be an array containing one entity for each server that the operation was performed on.

In addition, you will receive an email confirming that the patch was requested. A second email will be sent upon the successful application of the auto-patch capability.
