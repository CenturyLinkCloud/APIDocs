{{{
  "title": "Consuming Webhook Alerts with 3rd party web apps",
  "date": "11-24-2014",
  "author": "Chris Little",
  "attachments": []
}}}

Customers may wish to leverage the alert notification webhook services built into CenturyLink Cloud with 3rd party web apps or services. While clients could [build their own webhook listener platform](configuring-webhooks-and-consuming-notifications.md), there are various services on the market that make consuming webhooks and sending them into other web app or services point and click. In this example we are going to leverage <a href="http://zapier.com">Zapier</a>in conjunction with <a href="http://slack.com/">Slack</a>.

### Sample Use Case

The Operations team wishes to integrate alert notifications from the CenturyLink cloud into their real time Slack chat system used by the NOC. Slack provides the NOC teamsone-on-one messaging, private groups, persistent chat rooms, direct messaging as well as group chats organized by topic. By pushing alerts into slack the operations organization hopes to be more responsive and collaborative to events occurring in the CenturyLink Cloud.

The organization does not wish to build an integration system from scratch to consume and push notifications into slack. Instead they choose Zapier which connects web apps to easily move your data and automate tedious tasks. In this case Zapier will consume an alert webhook from CenturyLink Cloud and move that data into the NOC Slack channel for immediate action.

### Prerequisites

* A CenturyLink Cloud Account</li>
* <a href="http://www.zapier.com">A Zapier Account</a>
* <a href="http://www.slack.com">A Slack Account</a>

### Exceptions

This sample use case will not detail the process to setup a #slack domain and associated #channels. We will simply illustrate the events being pushed into these respective areas after Zapier configuration.

### Configuring Zapier
1. Login to the Zapier dashboard and select <strong>Make a New Zap</strong>
<img src="https://t3n.zendesk.com/attachments/token/OK4lR5ujJXXROLpMShvuZMq8n/?name=00.png" alt="00.png" />
2. Choose a trigger and action. For this use case we want to catch a webhook and send a message to Slack.
<img src="https://t3n.zendesk.com/attachments/token/kSgv8yaBXVSkK3d1JoB8silkK/?name=01.png" alt="01.png" />
3. Zapier will generate a unique webhook URL for this new Zap. Copy this to clipboard.</p>
<img src="https://t3n.zendesk.com/attachments/token/tS6zWlON1SuoGr2zHAxvEZAaV/?name=02.png" alt="02.png" />
4. Open the CenturyLink Cloud Control Portal, navigate to API, Webhooks. Input the Zapier URL provided previously into the Alert Notifications field. Optionally, cloud administrators can choose to include any sub accounts in this webhook configuration.
<img src="https://t3n.zendesk.com/attachments/token/zUbmvzFwXjdzxkntKqWoVsbzD/?name=webhook.png" alt="webhook.png" />
5. Select a Slack account for the webhook event to be sent to. If you are setting up your first Zap to Slack you will need to connect and authorize Zapier to connect to your slack account. These steps are not shown.
<img src="https://t3n.zendesk.com/attachments/token/i9pvEQVTxNLoTZHFChjxojHvu/?name=03.png" alt="03.png" />
6. Optional: Add key or filters (not required)
<img src="https://t3n.zendesk.com/attachments/token/3ipLnDTLacNGaNS2m6C5owKPk/?name=04.png" alt="04.png" />
7. Input the Slack channel or user you wish to send Alert Notifications. Typically, if pushing to an operations group you'd want to use a channel (i.e. #operations) as the destination for events. However, events can be pushed via the Slack bot to individual users as well (i.e. @username).
<p>In the Text area of the form select the 'Insert Fields' button. </p>
<img src="https://t3n.zendesk.com/attachments/token/6jdOLv9Eb73vQ57IhiVx0l61E/?name=07a.png" alt="07a.png" />
<p>If this is the first time you've added an alert notification webhook from CenturyLink Cloud a dialog box will pop up saying "We Couldn't get any samples from Web Hook. As you have already 1) taken the URL and added it to control 2) are creating a new hook you can skip right to #3. The Zapier interface will wait until a valid Alert Webhook (don't close browser) arrives from CenturyLink Cloud.</p>
<img src="https://t3n.zendesk.com/attachments/token/U5stj1xY7cjRYwWOh6VWBMb2g/?name=05.png" alt="05.png" />
8. In order to generate an Alert Notification from CenturyLink Cloud you can use various tools to max out a CPU, fill disk space etc on a test VM with an <a href="https://t3n.zendesk.com/entries/27202824-Cloud-Server-Alerting-FAQ" target="_blank">alert policy configured</a>.
In this example, I used <a href="http://sourceforge.net/projects/max-cpu/" target="_blank">Max CPU</a>on a Windows 2012 VM to max out the CPU for the 5 minute duration configured in the alert policy.</p>
<img src="https://t3n.zendesk.com/attachments/token/BjgoVoLsdu4GVSDXruLdCECiK/?name=alert.png" alt="alert.png" />
<img src="https://t3n.zendesk.com/attachments/token/oxlbPAKqHWna6BO8PUj500LmO/?name=13.png" alt="13.png" />
9. Once the webhook from CenturyLink Cloud fires to Zapier the Zap configuration tool will state 'We found your changes!
<img src="https://t3n.zendesk.com/attachments/token/Ek0aNEaCD55VqoIOsVtkEzoGf/?name=06.png" alt="06.png" />
10. The ability to insert fields into the Text data for the message is now functional. With the Alerts Notification webhook from CenturyLink Cloud there are 3 fields available to be inserted into the event. In this sample, we input standard text for Account Alias, Server Name &amp; Event Details paired with fields located in the webhook.
<img src="https://t3n.zendesk.com/attachments/token/M00gY85RCLrb4Ru9Yas0ROLDm/?name=07.png" alt="07.png" />
11. Finally, perform a test of the newly created Zap. Select the test webhook trigger and select a sample.</p>
<img src="https://t3n.zendesk.com/attachments/token/PnKnZIXgQGuorcnyLTAACuZkh/?name=08.png" alt="08.png" />
<img src="https://t3n.zendesk.com/attachments/token/cnMejts5lywOt4z0D5QOTAXvU/?name=09.png" alt="09.png" />
This test will result in a message being sent to Slack.
12. Provide a name for this new Zap and enable it.</p>
<img src="https://t3n.zendesk.com/attachments/token/6K8b7lMhiPgU0kx9W0yIVkQU7/?name=10.png" alt="10.png" />
13. Your Zapier dashboard will show all Zaps currently deployed and active.
<img src="https://t3n.zendesk.com/attachments/token/pqCDwDI68ezrJHn4bc5qwVODg/?name=11.png" alt="11.png" />

### Testing Alert Notifications

If you'd like to do a live production test of the new Zap and verify data you can follow the steps below.

RDP into a Windows VM with your alert policies applied, use a tool like <a href="http://sourceforge.net/projects/max-cpu/">Max CPU</a>

<strong>Sample CPU Max Tool</strong>

<img src="https://t3n.zendesk.com/attachments/token/mtMYhlgmTFy0YSa6sfKJnQWtx/?name=max+cpu.png" alt="max_cpu.png" />
