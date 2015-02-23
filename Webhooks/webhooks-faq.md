{{{
  "title": "Webhooks FAQ",
  "date": "10-13-2014",
  "author": "Richard Seroter",
  "attachments": []
}}}

<h3><strong>[UPDATED: 6-18-14]</strong></h3>
<h3><strong>Description</strong></h3>
<p>The CenturyLink Cloud supports <strong>Webhooks&nbsp;</strong>which send push notifications to an HTTP endpoint specified by the customer. This FAQ addresses commonly asked questions about the service. For a walkthrough of how to use Webhooks, see the
  KB article called <a href="https://t3n.zendesk.com/entries/22671399-Configuring-Webhooks-and-Consuming-Notifications">Configuring Webhooks&nbsp;and Consuming Notifications</a>.</p>
<p>&nbsp;</p>
<p><strong>Q: What exactly is a Webhook?</strong>
</p>
<p>A: Webhooks make it possible to create push notification solutions. Platform events (e.g. "server created") are sent in real-time to a web endpoint configured for the Webhook. Whenever an event occurs, a JSON message is sent as an HTTP POST request.</p>
<p>&nbsp;</p>
<p><strong>Q: Did CenturyLink Cloud invent the idea of Webhooks?</strong>
</p>
<p>A: No, but we're among the first to use it in an IaaS cloud. Webhooks are in use today for a variety of web properties including <a href="http://en.support.wordpress.com/webhooks/" target="_blank">Wordpress</a>, <a href="https://trello.com/docs/gettingstarted/webhooks.html"
  target="_blank">Trello</a>, and <a href="https://www.zoho.com/crm/extend/webhooks.html" target="_blank">Zoho</a>. CenturyLink Cloud sees value in embracing this model for public cloud customers who want to be more responsive to changes in their cloud
  account.</p>
<p>&nbsp;</p>
<p><strong>Q: In what scenario would I use a Webhook?</strong>
</p>
<p>A: We've identified numerous use cases where Webhooks can replace or augment the components of existing processes:</p>
<ul>
  <li><strong>Replace polling-based synchronization solutions.&nbsp;</strong>Customers often use request-response API operations to retrieve data about their assets in the CenturyLink Cloud. However, polling is fairly inefficient as the caller is simply asking
    "Do you have anything for me?" over and over again. With Webhooks, there's no longer a need to poll for changes. Instead, the CenturyLink Cloud immediately tells customers whenever key events occur in the platform.</li>
  <li><strong>Perform real-time data analytics.&nbsp;</strong>Customers can use this data to assess their cloud usage. For resellers, Webhooks provide an opportunity to observe server provisioning and detect trends. They could use it to watch for fraudulent
    signup scenarios my detecting abnormal combinations of account creation and server provisioning.</li>
  <li><strong>Monitor activities with security, compliance implications.&nbsp;</strong>For customers who closely govern their cloud usage, Webhooks provide the opportunity to immediately see what users are doing. Whether adding public IP addresses, or creating
    new user accounts, customers can quickly monitor and respond to activities that are counter to company policies.</li>
</ul>
<p>&nbsp;</p>
<p><strong>Q: What triggers a Webhook?</strong>
</p>
<p>A: There are currently Webhooks for four major categories: Accounts, Users, Alerts, and Servers.&nbsp;</p>
<ul>
  <li><strong>Accounts.</strong>&nbsp;Triggered on account creation and deletion. Triggered on account changes including account status, business name, address, telephone, fax, and time zone.<strong><br /></strong>
  </li>
  <li><strong>Users</strong>. Triggered on user creation and deletion. Triggered on user changes including user status, password, security PIN, email address, alternative email address, first name, last name, title, office number, mobile number, fax number,
    time zone.</li>
  <li><strong>Alerts.&nbsp;</strong>Triggered when a user-defined alert policy threshold is exceeded, and when the server returns to a utilization level below the alert policy threshold.</li>
  <li><strong>Servers</strong>. Triggered on server creation and deletion. Triggered on server changes including server archive, server restore, convert to template, convert from template, add/delete/edit disks, edit CPU, edit memory, assigned Group, description,
    add/remove IP addresses, power on/off, and shutdown.</li>
</ul>
<p>&nbsp;</p>
<p><strong>Q: What data is sent in the Webhook event notification?</strong>
</p>
<p>A: Some push notification systems only send a bare minimum of information and ask the user to call-back for the full data payload. CenturyLink Cloud Webhooks send a full JSON-encoded payload AND include a URL to the referenced resource.&nbsp;<strong>Note that since Webhooks are in beta, not all URLs resolve to resources yet.</strong>
</p>
<p>The Account event payload:</p>
<pre>{
    "addressLine1": "112 112th Ave NE",
    "addressLine2": "Ste 300",
    "city": "Bellevue",
    "stateProvince": "WA",
    "country": "USA",
    "postalCode": "98004",
    "telephone": "800-buy-cloud",
    "status": "Active",
    "isManaged": true,
    "links": [
        {
         "rel": "self",
         "href": "/v2/accounts/DEMO"
        },
        {
         "rel": "parentAccount",
         "href": "/v2/accounts/T3N"
         } ],
     "accountAlias": "DEMO",
     "businessName": "Seroter Industries",
     "parentAlias": "T3N",
     "primaryDataCenter": "WA1"
}
</pre>
<p>&nbsp;</p>
<p>The User event payload:</p>
<pre>{
     "uri": "/v2/users/demo@user.com",
     "accountUri": "/v2/accounts/DEMO",
     "accountAlias": "DEMO",
     "userName": "demo@user.com",
     "emailAddress": "demo@user.com",
     "firstName": "Richard",
     "lastName": "Seroter",
     "status": "Active"
}

</pre>
<p>&nbsp;</p>
<p>The Server event payload:&nbsp;</p>
<pre>{
    "id": "WA1DEMOSERVER01",
    "name": "WA1DEMOSERVER01",
    "description": "My web server",
    "groupId": "wa1-0000",
    "isTemplate": false,
    "locationId": "WA1",
    "osType": "Windows 2008 64-bit",
    "status": "active",
    "details": {
        "ipAddresses": [
            {
                "internal": "10.81.123.11"
            },
            {
                "public": "74.41.155.112",
                "internal": "10.81.123.14"
            }
        ],
        "alertPolicies": [
            {
                "id": "45866e6219e84ab786d07d4f570ba960",
                "name": "Production Web Servers - RAM",
                "links": [
                    {
                        "rel": "self",
                        "href": "/v2/alertPolicies/DEMO/45866e6219e84ab786d07d4f570ba960"
                    },
                    {
                        "rel": "alertPolicyMap",
                        "href": "/v2/servers/DEMO/WA1DEMOSERVER01/alertPolicies/45866e6219e84ab786d07d4f570ba960",
                        "verbs": [
                            "DELETE"
                        ]
                    }
                ]
            },
            {
                "id": "1aec88dd90ad4757937548c8c25e7431",
                "name": "Production Web Servers - Disk",
                "links": [
                    {
                        "rel": "self",
                        "href": "/v2/alertPolicies/DEMO/1aec88dd90ad4757937548c8c25e7431"
                    },
                    {
                        "rel": "alertPolicyMap",
                        "href": "/v2/servers/DEMO/WA1DEMOSERVER01/alertPolicies/1aec88dd90ad4757937548c8c25e7431",
                        "verbs": [
                            "DELETE"
                        ]
                    }
                ]
            },
            {
                "id": "cdab476a61884af9ab4840827f9e4b6f",
                "name": "Production Web Servers - CPU",
                "links": [
                    {
                        "rel": "self",
                        "href": "/v2/alertPolicies/DEMO/cdab476a61884af9ab4840827f9e4b6f"
                    },
                    {
                        "rel": "alertPolicyMap",
                        "href": "/v2/servers/DEMO/WA1DEMOSERVER01/alertPolicies/cdab476a61884af9ab4840827f9e4b6f",
                        "verbs": [
                            "DELETE"
                        ]
                    }
                ]
            }
        ],
        "cpu": 1,
        "diskCount": 1,
        "inMaintenanceMode": false,
        "memoryMB": 4096,
        "powerState": "started",
        "storageGB": 50,
        "disks": [
            {
                "id": "0:0",
                "sizeGB": 50,
                "partitionPaths": []
            }
        ],
        "partitions": [],
        "snapshots": [],
        "customFields": [
            {
                "id": 22,
                "name": "Cost Center",
                "value": "IT-DEV",
                "displayValue": "IT-DEV"
            },
            {
                "id": 237,
                "name": "CMDB ID",
                "value": "1100003",
                "displayValue": "1100003"
            }
        ]
    },
    "type": "standard",
    "storageType": "standard",
    "changeInfo": {
        "createdBy": "demo@user.com",
        "createdDate": "2012-12-17T01:17:17Z",
        "modifiedBy": "demo@user.com",
        "modifiedDate": "2014-06-18T18:28:54Z"
    },
    "links": [
        {
            "rel": "self",
            "href": "/v2/servers/DEMO/WA1DEMOSERVER01",
            "id": "WA1DEMOSERVER01",
            "verbs": [
                "GET",
                "PATCH",
                "DELETE"
            ]
        },
        {
            "rel": "group",
            "href": "/v2/groups/DEMO/wa1-0000",
            "id": "wa1-3728"
        },
        {
            "rel": "account",
            "href": "/v2/accounts/DEMO",
            "id": "btdi"
        },
        {
            "rel": "billing",
            "href": "/v2/billing/DEMO/serverPricing/WA1DEMOSERVER01"
        },
        {
            "rel": "statistics",
            "href": "/v2/servers/DEMO/WA1DEMOSERVER01/statistics"
        },
        {
            "rel": "scheduledActivities",
            "href": "/v2/servers/DEMO/WA1DEMOSERVER01/scheduledActivities"
        },
        {
            "rel": "publicIPAddresses",
            "href": "/v2/servers/DEMO/WA1DEMOSERVER01/publicIPAddresses",
            "verbs": [
                "POST"
            ]
        },
        {
            "rel": "alertPolicyMappings",
            "href": "/v2/servers/DEMO/WA1DEMOSERVER01/alertPolicies",
            "verbs": [
                "POST"
            ]
        },
        {
            "rel": "antiAffinityPolicyMapping",
            "href": "/v2/servers/DEMO/WA1DEMOSERVER01/antiAffinityPolicy",
            "verbs": [
                "DELETE",
                "PUT"
            ]
        },
        {
            "rel": "cpuAutoscalePolicyMapping",
            "href": "/v2/servers/DEMO/WA1DEMOSERVER01/cpuAutoscalePolicy",
            "verbs": [
                "DELETE",
                "PUT"
            ]
        },
        {
            "rel": "capabilities",
            "href": "/v2/servers/DEMO/WA1DEMOSERVER01/capabilities"
        },
        {
            "rel": "credentials",
            "href": "/v2/servers/DEMO/WA1DEMOSERVER01/credentials"
        },
        {
            "rel": "publicIPAddress",
            "href": "/v2/servers/DEMO/WA1DEMOSERVER01/publicIPAddresses/74.41.155.112",
            "id": "74.41.155.112",
            "verbs": [
                "GET",
                "PUT",
                "DELETE"
            ]
        }
    ]
}
</pre>
<p>&nbsp;* note that server delete events will only contain the accountAlias and name fields as the server has been deleted and any other information is no longer available.</p>
<p>The Alert event payload:&nbsp;</p>
<pre>{

    "accountAlias": "DEMO",
    "serverName": "WA1DEMOSERVER01",
    "triggers": [
        {
            "data": {
                "cpu": 2,
                "cpuPercent": 39.34
            },
            "duration": "00:05:00",
            "metric": "cpu",
            "stateEndTime": "2014-06-18T18:23:46Z",
            "stateStartTime": "2014-06-18T18:20:00Z",
            "state": "notTriggered"
        }
    ]
}

</pre>
<p><strong>Q: Where do I go to set a Webhook?</strong>
</p>
<p>A: Webhooks are available at the Account-level under the&nbsp;<strong>API&nbsp;</strong>menu. There is now a sub-menu called "Webhooks." Customers can set a target URL for each Webhook event listed.</p>
<p><img src="https://t3n.zendesk.com/attachments/token/mezgqvekji9zh06/?name=webhookfaq01.png" alt="webhookfaq01.png" />
</p>
<p>&nbsp;</p>
<p><strong>Q: Can notifications be sent for events that occur within sub-accounts?</strong>
</p>
<p>&nbsp;A: Yes. For each individual Webhook event, customers can specify whether they want sub-account events to ALSO be sent to the designated endpoint. If a parent account has the "include sub-accounts" checkbox selected, and a sub-account has specified
  their own Webhook endpoint for the same event, then a copy of the event notification is sent to both endpoints.</p>
<p><img src="https://t3n.zendesk.com/attachments/token/tslhcvncdhf0xar/?name=webhookfaq02.png" alt="webhookfaq02.png" />
</p>
<p>&nbsp;</p>
<p><strong>Q: Are there any requirements for the service that receives the Webhook notification?</strong>
</p>
<p>&nbsp;A: All Webhook listener services <strong>must</strong> support secure HTTP transport via HTTPS. The data transmitted in the event may be sensitive and shouldn't travel over unprotected channels. Secondly, listener services must be on the public
  internet in a location reachable by the CenturyLink CLoud platform. If a customer plans on consuming this data within an internal system, consider using a reverse proxy or another mechanism to forward traffic from a public-facing web service to an internal
  system.</p>
<p>&nbsp;</p>
<p><strong>Q: How can listener services be sure that it was CenturyLink Cloud that sent the message and not someone spoofing you?</strong>
</p>
<p>A: While SSL ensures that the message cannot be read in transit, it doesn't protect you from rogue callers who target your public endpoint. Each Webhook notification includes a signature hash of the message payload. The "Tier3-RsaSha1" header is signed with our private key, leveraging the json payload as input. This signature can be verified with the following public key and the received json body. Customers can use this process to ensure that the message wasn't tampered with.</p>

Public Key:

```
-----BEGIN PUBLIC KEY-----
MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAnmwsVLJ22Y8lmnk+1fI/
JKkm4bM1GvggI7DN10KIoPDgBbNcePZqcFayDdmVuq/jL9MFBrqFSfVszgdq8OWF
G9lEB5vP29K/N+0kRg5V2NDXddI5AOzx6jDjkNM/jjb45UXeDcPzMMdMOl/ds6uT
p6mbfG3U8dWqM/if7mzjEbbhYkBM3OuacEFk38Tkm49IJ4jHnC0p9qWO2iaxJqRc
08M2cJ+yKcFudCVKX8ANE6g6YKK+5aSabxfHX83Vjr4I0kpqo0cfP4aSW/CPDUZ7
yR4bFiy5Wv2de2V+FOGVBQF+/viSzrtrwQjUOJViuxEnifc06xuDF0QFta9anz4d
LQIDAQAB
-----END PUBLIC KEY-----
```

<p><strong>Q: How soon after an event occurs does a Webhook notification get sent?</strong>
</p>
<p>&nbsp;A: As soon as the event occurs in the CenturyLink Cloud platform, it is routed through our messaging infrastructure and sent to each Webhook endpoint. In reality, this means that messages are often received within 5 seconds of the event occurring.</p>
<p>&nbsp;</p>
<p><strong>Q: What happens if the destination is unreachable?</strong>
</p>
<p>&nbsp;A: There is no guaranteed delivery with CenturyLink Cloud Webhooks. We make a single attempt to send a message to the designated endpoint and if it fails, it is not retried. This means two things: (1) design your endpoints to be highly available
  and withstand failures of any single component in the solution, and (2) rely on a combination of Webhooks and daily web service API calls to ensure that your local repositories stay in sync.</p>
<p>&nbsp;</p>
<p><strong>Q: Are there more Webhooks on the way?</strong>
</p>
<p>A: Yes! We have ideas for additional Webhooks to add to the platform, but would like to hear from you. If you have suggestions for other Webhooks, send an email to <a href="mailto:Features@tier3.com">Features@tier3.com</a>.&nbsp;</p>
