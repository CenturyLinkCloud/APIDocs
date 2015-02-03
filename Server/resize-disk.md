{{{
  "title": "Resize Disk",
  "date": "5-1-2013",
  "author": "Luke Bakken",
  "attachments": []
}}}

ResizeDisk
<p>Resizes a disk on a Server.</p>
URL
<pre>REST: https://api.tier3.com/REST/Server/ResizeDisk/&lt;format&gt;<br />SOAP: https://api.tier3.com/SOAP/Server.asmx?op=ResizeDisk</pre> Request
<h3>Attributes</h3>
<table>
  <tbody>
    <tr>
      <td><strong>Name</strong>
      </td>
      <td><strong>Type</strong>
      </td>
      <td><strong>Description</strong>
      </td>
      <td><strong>Required</strong>
      </td>
    </tr>
    <tr>
      <td>AccountAlias</td>
      <td>String</td>
      <td>The alias of the account that owns the server. If not provided it will assume the Account the API user is mapped to. Providing this value gives you the ability to manage servers in your sub accounts.</td>
      <td>No</td>
    </tr>
    <tr>
      <td>Name</td>
      <td>String</td>
      <td>The name of the server. &nbsp;</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>ScsiBusID</td>
      <td>String</td>
      <td>The SCSI bus ID of the disk.</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>ScsiDeviceID</td>
      <td>String</td>
      <td>The SCSI device ID of the disk.</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>ResizeGuestDisk</td>
      <td>Boolean</td>
      <td>Set to 'True' to attempt to expand the file system on the disk after the resize.</td>
      <td>No</td>
    </tr>
    <tr>
      <td>NewSizeGB</td>
      <td>Int</td>
      <td>The expanded size of the disk. Must be greater than the existing disk size.</td>
      <td>Yes</td>
    </tr>
  </tbody>
</table>
<h3>Examples</h3>
<h4>JSON</h4>
<pre>{

  "AccountAlias": "UNK",

  "Name": "WA1T3NWEB01",

  "ScsiBusID": "0",

  "ScsiDeviceID": "2",

  "ResizeGuestDisk": true,

  "NewSizeGB": 50

}</pre>
<h4>XML</h4>
<pre>&lt;ResizeDiskRequest&gt;

    &lt;AccountAlias&gt;UNK&lt;/AccountAlias&gt;

    &lt;Name&gt;WEB&lt;/Name&gt;

    &lt;ScsiBusID&gt;0&lt;/ScsiBusID&gt;

    &lt;ScsiDeviceID&gt;2&lt;/ScsiDeviceID&gt;

    &lt;ResizeGuestDisk&gt;true&lt;/ResizeGuestDisk&gt;

    &lt;NewSizeGB&gt;50&lt;/NewSizeGB&gt;

&lt;/ResizeDiskRequest&gt;</pre> Response
<h3>Attributes</h3>
<table>
  <tbody>
    <tr>
      <td><strong>Name</strong>
      </td>
      <td><strong>Type</strong>
      </td>
      <td><strong>Description</strong>
      </td>
    </tr>
    <tr>
      <td>Success</td>
      <td>Boolean</td>
      <td>True if the request was successful, otherwise False.</td>
    </tr>
    <tr>
      <td>Message</td>
      <td>String</td>
      <td>A description of the result. The contents of this field does not contain any actionable information, it is purely intended to provide a human readable description of the result.</td>
    </tr>
    <tr>
      <td>StatusCode</td>
      <td>Int</td>
      <td>This value will help to identify any errors which were encountered while processing the request. The value of '0' indicates success, all non-zero StatusCodes indicate an error state.</td>
    </tr>
    <tr>
      <td>RequestID</td>
      <td>Int</td>
      <td>The ID of the Queued request.Status of the request can be obtained by calling the&nbsp;<a href="http://help.tier3.com/entries/20561586-get-deployment-status">GetDeploymentStatus</a>&nbsp;method.</td>
    </tr>
  </tbody>
</table>
<h3>Examples</h3>
<h4>JSON</h4>
<pre>{<br />    "RequestID":1,<br />    "Success":true,<br />    "Message":"Success",<br />    "StatusCode":0<br />}</pre>
<h4>XML</h4>
<pre>&lt;QueuedItemResponse Success="true" Message="Success" StatusCode="0"&gt;<br />&nbsp; &nbsp; &lt;RequestID&gt;1&lt;/RequestID&gt;<br />&lt;/QueuedItemResponse&gt;</pre>
<h3>Status Codes</h3>
<table>
  <tbody>
    <tr>
      <td><strong>Status Code</strong>
      </td>
      <td><strong>Description</strong>
      </td>
    </tr>
    <tr>
      <td>0</td>
      <td>Request was successfully processed</td>
    </tr>
    <tr>
      <td>2</td>
      <td>Unknown Error - An application error occurred processing your request, contact Tier3 support to resolve the issue.</td>
    </tr>
    <tr>
      <td>3</td>
      <td>Invalid Request Format. This value indicates that the XML or JSON requests do not match the expected format.</td>
    </tr>
    <tr>
      <td>5</td>
      <td>Resource Not Found. &nbsp;A Hardware Group with the specified ID cannot be found.
        <br />- OR -
        <br />A Server with the specified Name cannot be found&nbsp;</td>
    </tr>
    <tr>
      <td>6</td>
      <td>Invalid Operation. &nbsp;Server must be in an active state, and must not have snapshots.</td>
    </tr>
    <tr>
      <td>100</td>
      <td>Authentication Failed - You must logon to the API prior to calling this method.</td>
    </tr>
    <tr>
      <td>1410</td>
      <td>Name Required.</td>
    </tr>
    <tr>
      <td>1415</td>
      <td>Unknown snapshot state.</td>
    </tr>
  </tbody>
</table>