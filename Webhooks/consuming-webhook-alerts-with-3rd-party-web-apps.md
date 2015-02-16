{{{
  "title": "Consuming Webhook Alerts with 3rd party web apps",
  "date": "11-24-2014",
  "author": "Chris Little",
  "attachments": []
}}}

<p>Customers may wish to leverage the alert notification webhook services built into CenturyLink Cloud with 3rd party web apps or services. &nbsp;While clients could <a href="https://t3n.zendesk.com/entries/22671399-Configuring-Webhooks-and-Consuming-Notifications"
  target="_blank">build their own webhook listener platform</a>&nbsp;there are various services on the market that make consuming webhooks and sending them into other web app or services point and click. &nbsp;In this example we are going to leverage
  <a href="http://zapier.com" target="_blank">Zapier</a>&nbsp;in conjunction with <a href="http://slack.com/" target="_blank">Slack</a>. &nbsp; &nbsp;</p>
<h3>Sample Use Case</h3>
<p>The Operations team wishes to integrate alert notifications from the CenturyLink cloud into their real time Slack chat system used by the NOC. &nbsp;Slack provides the NOC teams&nbsp;one-on-one messaging, private groups, persistent chat rooms, direct
  messaging as well as group chats organized by topic. &nbsp;By pushing alerts into slack the operations organization hopes to be more responsive and collaborative to events occurring in the CenturyLink Cloud. &nbsp;</p>
<p>The organization does not wish to build an integration system from scratch to consume and push notifications into slack. &nbsp;Instead they choose Zapier&nbsp;which connects web apps to easily move your data and automate tedious tasks. &nbsp;In this case
  zapier will consume an alert webhook from CenturyLink Cloud and move that data into the NOC slack channel for immediate action.</p>
<h3>Prerequisites</h3>
<ul>
  <li>A CenturyLink Cloud Account</li>
  <li><a href="http://www.zapier.com" target="_blank">A Zapier Account</a>
  </li>
  <li><a href="http://www.slack.com" target="_blank">A Slack Account&nbsp;</a>
  </li>
</ul>
<h3>Exceptions</h3>
<p>This sample use case will not detail the process to setup a #slack domain and associated #channels. &nbsp;We will simply illustrate the events being pushed into these respective areas after Zapier configuration.</p>
<h3>Configuring Zapier</h3>
<p>1. &nbsp;Login to the Zapier dashboard and select <strong>Make a New Zap</strong>
</p>
<p><strong><img src="https://t3n.zendesk.com/attachments/token/OK4lR5ujJXXROLpMShvuZMq8n/?name=00.png" alt="00.png" /></strong>
</p>
<p>2. &nbsp;Choose a trigger and action. &nbsp;For this use case we want to catch a webhook and send a message to Slack.</p>
<p><img src="https://t3n.zendesk.com/attachments/token/kSgv8yaBXVSkK3d1JoB8silkK/?name=01.png" alt="01.png" />
</p>
<p>3. &nbsp;Zapier will generate a unique webhook URL for this new Zap. &nbsp;Copy this to clipboard.</p>
<p><img src="https://t3n.zendesk.com/attachments/token/tS6zWlON1SuoGr2zHAxvEZAaV/?name=02.png" alt="02.png" />
</p>
<p>4. &nbsp;Open the CenturyLink Cloud Control Portal, navigate to API, Webhooks. &nbsp;Input the Zapier URL provided previously into the Alert Notifications field. &nbsp;Optionally, cloud administrators can choose to include any sub accounts in this webhook
  configuration. &nbsp;</p>
<p><img src="https://t3n.zendesk.com/attachments/token/zUbmvzFwXjdzxkntKqWoVsbzD/?name=webhook.png" alt="webhook.png" />
</p>
<p>5. &nbsp;Select a slack account for the webhook event to be sent to. &nbsp;If you are setting up your first Zap to Slack you will need to connect and authorize Zapier to connect to your slack account. &nbsp;These steps are not shown.</p>
<p><img src="https://t3n.zendesk.com/attachments/token/i9pvEQVTxNLoTZHFChjxojHvu/?name=03.png" alt="03.png" />
</p>
<p>6. &nbsp;Optional: &nbsp;Add key or filters (not required)</p>
<p><img src="https://t3n.zendesk.com/attachments/token/3ipLnDTLacNGaNS2m6C5owKPk/?name=04.png" alt="04.png" />
</p>
<p>7. &nbsp;Input the slack channel or user you wish to send Alert Notifications. &nbsp;Typically, if pushing to an operations group you'd want to use a channel (i.e. #operations) as the destination for events. &nbsp;However, events can be pushed via the
  slack bot to individual users as well (i.e. @username). &nbsp;</p>
<p>In the Text area of the form select the 'Insert Fields' button. &nbsp;</p>
<p><img src="https://t3n.zendesk.com/attachments/token/6jdOLv9Eb73vQ57IhiVx0l61E/?name=07a.png" alt="07a.png" />
</p>
<p>If this is the first time you've added an alert notification webhook from CenturyLink Cloud a dialog box will pop up saying "We Couldn't get any samples from Web Hook. &nbsp;As you have already 1) taken the URL and added it to control 2) are creating
  a new hook you can skip right to #3. &nbsp;The Zapier interface will wait until a valid Alert Webhook (don't close browser) arrives from CenturyLink Cloud.&nbsp;</p>
<p><img src="https://t3n.zendesk.com/attachments/token/U5stj1xY7cjRYwWOh6VWBMb2g/?name=05.png" alt="05.png" />
</p>
<p>8. &nbsp;In order to generate an Alert Notification from CenturyLink Cloud you can use various tools to max out a CPU, fill disk space etc on a test VM with an <a href="https://t3n.zendesk.com/entries/27202824-Cloud-Server-Alerting-FAQ" target="_blank">alert policy configured</a>.
  &nbsp;In this example, I used <a href="http://sourceforge.net/projects/max-cpu/" target="_blank">Max CPU</a>&nbsp;on a Windows 2012 VM to max out the CPU for the 5 minute duration configured in the alert policy. Windows users can also use the fsutil
  (i.e.&nbsp;fsutil file createnew &lt;filename&gt; &lt;length&gt;) to generate a large file to fill up disk space. &nbsp;</p>
<p><img src="https://t3n.zendesk.com/attachments/token/BjgoVoLsdu4GVSDXruLdCECiK/?name=alert.png" alt="alert.png" />&nbsp;</p>
<p><img src="https://t3n.zendesk.com/attachments/token/oxlbPAKqHWna6BO8PUj500LmO/?name=13.png" alt="13.png" />
</p>
<p>&nbsp;9. &nbsp;Once the webhook from CenturyLink Cloud fires to Zapier the Zap configuration tool will state 'We found your changes!</p>
<p><img src="https://t3n.zendesk.com/attachments/token/Ek0aNEaCD55VqoIOsVtkEzoGf/?name=06.png" alt="06.png" />
</p>
<p>10. &nbsp;The ability to insert fields into the Text data for the message is now functional. &nbsp;With the Alerts Notification webhook from CenturyLink Cloud there are 3 fields available to be inserted into the event. &nbsp;In this sample, we input standard
  text for Account Alias, Server Name &amp; Event Details paired with fields located in the webhook. &nbsp;</p>
<p><img src="https://t3n.zendesk.com/attachments/token/M00gY85RCLrb4Ru9Yas0ROLDm/?name=07.png" alt="07.png" />
</p>
<p>11. &nbsp;Finally, perform a test of the newly created Zap. &nbsp;Select the test webhook trigger and select a sample.&nbsp;</p>
<p><img src="https://t3n.zendesk.com/attachments/token/PnKnZIXgQGuorcnyLTAACuZkh/?name=08.png" alt="08.png" />
</p>
<p><img src="https://t3n.zendesk.com/attachments/token/cnMejts5lywOt4z0D5QOTAXvU/?name=09.png" alt="09.png" />
</p>
<p>This test will result in a message being sent to Slack.</p>
<p>12. &nbsp;Provide a name for this new Zap and enable it.&nbsp;</p>
<p><img src="https://t3n.zendesk.com/attachments/token/6K8b7lMhiPgU0kx9W0yIVkQU7/?name=10.png" alt="10.png" />
</p>
<p>13. &nbsp;Your Zapier dashboard will show all Zaps currently deployed and active. &nbsp;</p>
<p><img src="https://t3n.zendesk.com/attachments/token/pqCDwDI68ezrJHn4bc5qwVODg/?name=11.png" alt="11.png" />
</p>
<h3>Testing Alert Notifications</h3>
<p>&nbsp;If you'd like to do a live production test of the new Zap and verify data you can follow the steps below. &nbsp;</p>
<p>1. &nbsp;RDP into a Windows VM with your alert policies applied, &nbsp;use a tool like <a href="http://sourceforge.net/projects/max-cpu/" target="_blank">Max CPU</a>&nbsp;or <a href="http://technet.microsoft.com/en-us/library/cc753059.aspx" target="_blank">fsutil </a>to
  max CPU or fill disk space.&nbsp;</p>
<p><strong>Sample CPU Max Tool</strong>
</p>
<p><img src="https://t3n.zendesk.com/attachments/token/mtMYhlgmTFy0YSa6sfKJnQWtx/?name=max+cpu.png" alt="max_cpu.png" />
</p>
<p><strong>Sample FSUTIL Command Line Code</strong>
</p>
<p>"fsutil file createnew largefile.txt 48318382080"</p>
<p>This command creates a file named largefile.txt that is 45 GB in size (<a href="http://www.convertunits.com/from/GB/to/byte" target="_blank">Bytes to GB tool</a>)</p>
<p>2. &nbsp;Check your slack notifications and events will be posted based on CPU, Disk or Both in this sample.</p>
<p><img src="https://t3n.zendesk.com/attachments/token/LxGDXgJ27qYBITKZkjmQnBkgw/?name=CPU.png" alt="CPU.png" />
</p>
<p><img src="https://t3n.zendesk.com/attachments/token/5io3ZAPhziJ6RimBgNA73aCH7/?name=disk.png" alt="disk.png" />
</p>
<p>&nbsp;</p>