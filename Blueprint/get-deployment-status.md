{{{
  "title": "Get Deployment Status",
  "date": "7-14-2014",
  "author": "Troy Schneringer",
  "attachments": []
}}}

GetDeploymentStatus
<p>Gets the status of the specified Blueprint deployment.</p>
URL
<pre>REST: <code>https://api.tier3.com/REST/Blueprint/GetBlueprintStatus/&lt;format&gt;</code><br />SOAP: <code>https://api.tier3.com/SOAP/Blueprints.asmx?op=GetDeploymentStatusMsg</code></pre> Request
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
      <td>RequestID</td>
      <td>Int</td>
      <td>
        <p>The ID of the Blueprint Deployment to retrieve status for.</p>
      </td>
      <td>
        <p>Yes</p>
      </td>
    </tr>
    <tr>
      <td>LocationAlias</td>
      <td>String</td>
      <td>
        <p>The location of the Blueprint Deployment to retrieve status for. &nbsp;If not provided, will default to the API user's default data center.</p>
      </td>
      <td>
        <p>No&nbsp;</p>
      </td>
    </tr>
    <tr>
      <td>AccountAlias</td>
      <td>String</td>
      <td>
        <p>ID of the account</p>
      </td>
      <td>
        <p>Yes</p>
      </td>
    </tr>
  </tbody>
</table>
<h3>Examples</h3>
<h4>JSON</h4>
<pre>{<br />    "RequestID": "1",<br />    "LocationAlias": "WA1"<br />}</pre>
<h4>XML</h4>
<pre>&lt;GetDeploymentStatusRequest&gt;<br />    &lt;RequestID&gt;1&lt;/RequestID&gt;<br />    &lt;LocationAlias&gt;WA1&lt;/LocationAlias&gt;<br />&lt;/GetDeploymentStatusRequest&gt;&nbsp;</pre> Response
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
      <td>The ID of the Blueprint deployment request. (Obtained from <a href="http://t3n.zendesk.com/entries/20451642-deploy-blueprint">DeployBlueprint</a> )</td>
    </tr>
    <tr>
      <td>CurrentStatus</td>
      <td>String</td>
      <td>
        <p>The status of the Blueprint deployment. &nbsp;Valid values are:</p>
        <p>- NotStarted&nbsp;
          <br />- Executing&nbsp;
          <br />- Succeeded&nbsp;
          <br />- Failed&nbsp;
          <br />- Resumed</p>
      </td>
    </tr>
    <tr>
      <td>Description</td>
      <td>String</td>
      <td>A detailed description of the current status.</td>
    </tr>
    <tr>
      <td>PercentComplete</td>
      <td>Int</td>
      <td>The percentage of the work that has been completed on the request.</td>
    </tr>
    <tr>
      <td>StatusDate</td>
      <td>DateTime</td>
      <td>The timestamp (UTC) that the most recent status was recorded on the Request.</td>
    </tr>
    <tr>
      <td>Step</td>
      <td>String</td>
      <td>The current step being executed.</td>
    </tr>
    <tr>
      <td>Servers</td>
      <td>Array</td>
      <td>
        <p>An array of strings with the names of any servers built as part of the Blueprint. &nbsp;</p>
        <p>This element is only populated when the Request was originally for server creation.</p>
      </td>
    </tr>
  </tbody>
</table>
<h3>Examples</h3>
<h4>JSON</h4>
<pre>{<br />    "RequestID":210,<br />    "CurrentStatus":"Failed",<br />    "Description":"Error Building Blueprint",<br />    "StatusDate":"\/Date(1318480463790)\/",<br />    "Step":"0",<br />    "PercentComplete":0,<br />    "Success":true,<br />    "Message":"Success",<br />    "StatusCode":0,<br />    "Servers":["WA1T3NWEB01"]<br />}</pre>
<h4>XML</h4>
<pre>&lt;GetDeploymentStatusResponse <br />    Success="true" Message="Success" StatusCode="0" <br />    RequestID="210" CurrentStatus="Failed" Description="Error Building Blueprint" StatusDate="2011-10-12T21:34:23.79" Step="0" PercentComplete="0"&gt;<br />    &lt;Servers&gt;<br />        &lt;string&gt;WA1T3NWEB01&lt;/string&gt;<br />    &lt;/Servers&gt;<br />&lt;GetDeploymentStatusResponse&gt;&nbsp;</pre>
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
      <td>Unknown Error. &nbsp;An application error occurred processing your request, contact Tier3 support to resolve the issue.</td>
    </tr>
    <tr>
      <td>3</td>
      <td>Invalid Request Format. This value indicates that the XML or JSON requests do not match the expected format.</td>
    </tr>
    <tr>
      <td>5</td>
      <td>Resource Not Found. &nbsp;A Blueprint with the specified ID cannot be found.</td>
    </tr>
    <tr>
      <td>100</td>
      <td>Authentication Failed. &nbsp;You must logon to the API prior to calling this method.</td>
    </tr>
  </tbody>
</table>