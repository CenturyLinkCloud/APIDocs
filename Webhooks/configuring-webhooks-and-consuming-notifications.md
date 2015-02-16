{{{
  "title": "Configuring Webhooks and Consuming Notifications",
  "date": "10-13-2014",
  "author": "Richard Seroter",
  "attachments": []
}}}

<h3>Description</h3>
<p>Webhooks make it possible to subscribe to key events that occur in the Tier 3 cloud. In this KB article, we will walk through how to create a Webhook listener, configure a Webhook, and receive a notification. For general details on Webhooks, read the
  KB article on <a href="https://t3n.zendesk.com/entries/22916235-Webhooks-FAQ" target="_blank">Webhook FAQs</a>.</p>
<h3>Audience</h3>
<ul>
  <li>Developers</li>
</ul>
<h3>Prerequisites</h3>
<ul>
  <li>Must have a Tier 3 account</li>
  <li>Must be able to deploy applications to an internet-facing location that has legitimate SSL certificates</li>
</ul>
<h3>Detailed Steps</h3>
<h4>Build the Webhook listener</h4>
<p>A Webhook listener is simply a web application that can receive a JSON message via HTTP POST. A working example application written in Node.js can be <a href="https://github.com/Tier3/Examples/tree/master/Tier3.WebHookListener" target="_blank">downloaded from GitHub</a>.
  When designing a Webhook listener, consider the following activities:</p>
<ol>
  <li>Decide what events to subscribe to. Webhooks support Account, User, and Server events.</li>
  <li>Process HTTP POST requests. In the example Node.js application, <a href="https://github.com/Tier3/Examples/blob/master/Tier3.WebHookListener/app.js" target="_blank">this is done in the app.js file</a>.
    <br />
    <pre>app.post('/webhook/account', function(req, res){



    //extract the signature header

    var signatureHeader = req.get('Tier3-RsaSha1');



    //call function to send webhook data to client browser

    BroadcastAccountWebhook(req.body, signatureHeader);



    //send OK response to Tier 3

    res.send("ok");

})

</pre>
  </li>
  <li>Handle the payload for each message type. In the example project, this is done in<a href="https://github.com/Tier3/Examples/blob/master/Tier3.WebHookListener/public/javascripts/sockethandler.js" target="_blank"> a client-side JavaScript file</a> and
    the entire payload is shown to the user. A listener application that uses typed object definitions must be able to deserialize the following structures:
    <br />
    <br /><strong>Account</strong>
    <br />
    <pre>{ 

     "uri": "/v2/accounts/RLS1", 

     "alias": "RLS1", 

     "businessName": "Seroter Toys, Inc", 

     "addressLine1": "110 110th Ave NE", 

     "addressLine2": "Suite 520", 

     "city": "Bellevue", 

     "stateProvince": "WA", 

     "country": "USA", 

     "postalCode": "98004", 

     "telephone": "800-BUY-TOYS", 

     "fax": null, 

     "status": "Active" 

}

</pre>
    <br /><strong>User</strong>
    <br />
    <pre>{ 

     "uri": "/v2/users/rseroter100", 

     "accountUri": "/v2/accounts/RLS1", 

     "accountAlias": "RLS1", 

     "userName": "rseroter100", 

     "emailAddress": "richard@serotertoys.com", 

     "firstName": "Richard", 

     "lastName": "Seroter", 

     "status": "Active" 

}

</pre>
    <br /><strong>Server</strong>
    <br />
    <pre>{ 

     "accountAlias": "RLS1", 

     "accountUri": "/v2/accounts/RLS1", 

     "cpu": 2, 

     "description": "Production web server for dotcom site", 

     "diskCount": 1, 

     "groupUri": "/v2/serverGroups/WA1/4491", 

     "id": "109945", 

     "ipAddresses": [ 

         { "address": "50.10.160.127" }, 

         { "address": "10.56.118.16" }, 

         { "address": "10.56.118.17" } 

     ], 

     "isTemplate": false, 

     "locationAlias": "WA1", 

     "memoryMB": 4096, 

     "name": "WA1RLS1PWEB0101", 

     "osType": "Windows 2008 64-bit", 

     "powerState": "Started", 

     "status": "Active", 

     "storageGB": 24, 

     "uri": "/v2/servers/WA1/WA1RLS1PWEB0101" 

}

</pre>
  </li>
</ol>
<h4>Deploy the Webhook listener</h4>
<ol>
  <li>Webhooks must be deployed to an internet-facing location that is reachable by the Tier 3 platform.</li>
  <li>Identify a host (public cloud IaaS, public cloud PaaS, or on-premises data center) with a valid (not self-signed) SSL certificate.</li>
  <li>Deploy the application and ensure that it's reachable. For this demonstration, the listener was deployed to a non-Tier 3 public Cloud Foundry environment hosted by Pivotal.
    <br /><img src="https://t3n.zendesk.com/attachments/token/ihqs1tit2aqepwu/?name=webhookwalkthrough01.png" alt="webhookwalkthrough01.png" />
  </li>
</ol>
<h4>Configure a Webhook in the Tier 3 cloud</h4>
<ol>
  <li>Go to the Tier 3 Control Portal, log in, and select the <strong>API&nbsp;</strong>option from the navigation menu.
    <br /><img src="https://t3n.zendesk.com/attachments/token/bdupexlk7hslkje/?name=webhookwalkthrough02.png" alt="webhookwalkthrough02.png" />
  </li>
  <li>&nbsp;Switch to the&nbsp;<strong>Webhooks&nbsp;</strong>sub-tab and review the list of available Webhooks. You can configure unique endpoints for each individual Webhook. In the image below, notice that the&nbsp;<strong>Account.Updated</strong>&nbsp;Webhook
    was set with the URL to the listener web application. A Webhook will respond to events that occur in sub-accounts if the "include sub-accounts" checkbox is selected.
    <br /><img src="https://t3n.zendesk.com/attachments/token/nlc8kanegvoepjq/?name=webhookwalkthrough03.png" alt="webhookwalkthrough03.png" />
  </li>
  <li>Click <strong>Save</strong>&nbsp;when the configuration is complete.</li>
  <li>Add Webhook URLs for any other Webhooks of interest.</li>
</ol>
<h4>Test the Webhook</h4>
<ol>
  <li>Trigger an event in the platform that the Webhook will respond to. View the <a href="https://t3n.zendesk.com/entries/22916235-Webhooks-FAQ" target="_blank">Webhook FAQ</a> for a list of what platform events will trigger a Webhook notification. To get
    the <strong>Account.Updated</strong>&nbsp;Webhook configured above to fire, change an account setting such as the mailing address.
    <br /><img src="https://t3n.zendesk.com/attachments/token/b8ydsawn5xsdanf/?name=webhookwalkthrough04.png" alt="webhookwalkthrough04.png" />
  </li>
  <li>Save the account change. Within seconds, the Webhook listener service should receive the notification message. In <a href="https://github.com/Tier3/Examples/tree/master/Tier3.WebHookListener" target="_blank">the sample application</a>, this information
    is pushed to the browser. Clicking on the updated account's name reveals both the full payload and a portion of the hashed signature value.
    <br /><img src="https://t3n.zendesk.com/attachments/token/84velqvuq9k0cjl/?name=webhookwalkthrough05.png" alt="webhookwalkthrough05.png" />
  </li>
</ol>