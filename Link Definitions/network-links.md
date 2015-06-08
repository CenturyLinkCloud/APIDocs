{{{
  "title": "Network Links",
  "date": "05-22-2015",
  "author": "Jared Ruckle",
  "attachments": [],
  "sticky": "true"
}}}

### Overview

The following link definitions are related to the network resource. They may be returned when making a call to [Get Network List](../Networks/get-network-list.md) or other network-related resources.

### Network Link Definitions

| Relation (rel) | Description | Verbs |
| --- | --- | --- |
| ipAddresses | Retrieves the list of IP Addresses associated with a network | [GET](../Networks/get-ip-address-list.md) |
| release | Releases a given network in a given data center; the network may then be claimed | [POST] |
| firewallPolicies | Retrieves the list of firewall policies associated with an account | [GET](../Networks/get-firewall-policy.md) |
