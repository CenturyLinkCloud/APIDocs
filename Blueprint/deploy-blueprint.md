{{{
  "title": "Deploy Blueprint",
  "date": "1-31-2014",
  "author": "Troy Schneringer",
  "attachments": []
}}}

<div>
  DeployBlueprint
  <p>Deploys a Blueprint with the given set of parameter values.</p>
  URL
  <pre>REST: <code>https://api.tier3.com/REST/Blueprint/DeployBlueprint/&lt;format&gt;</code><br />SOAP: <code>https://api.tier3.com/SOAP/Blueprints.asmx?op=DeployBlueprint</code></pre> Request
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
        <td>ID</td>
        <td>Int</td>
        <td>
          <p>The ID of the Blueprint to deploy.</p>
        </td>
        <td>
          <p>Yes</p>
        </td>
      </tr>
      <tr>
        <td>LocationAlias</td>
        <td>string</td>
        <td>
          <p>The alias of the Datacenter where you would like to deploy the blueprint to. If not provided, it will default to your primary datacenter.</p>
        </td>
        <td>
          <p>No</p>
        </td>
      </tr>
      <tr>
        <td>Parameters</td>
        <td>List</td>
        <td>
          <p>A list of Parameter values to use during the deployment of the Blueprint</p>
        </td>
        <td>
          <p>Yes</p>
        </td>
      </tr>
      <tr>
        <td>CustomFields</td>
        <td>Complex</td>
        <td>
          <p>Custom Fields that need to be set on each server created during blueprint deployment</p>
        </td>
        <td>
          <p>No</p>
        </td>
      </tr>
    </tbody>
  </table>
</div>
<div>
  <h3>Parameter Attributes</h3>
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
        <td>Name</td>
        <td>String</td>
        <td>
          <p>The name of the Parameter being set.</p>
        </td>
      </tr>
      <tr>
        <td>Value</td>
        <td>String</td>
        <td>
          <p>The value for the Parameter.</p>
          <p><em>This value will be validated based on the type and validation rules specified by the Blueprint Parameter definition.</em>
          </p>
        </td>
      </tr>
    </tbody>
  </table>
  <h3>CustomField Attributes</h3>
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
        <td>CustomFieldID</td>
        <td>Int</td>
        <td>Identifier that is associated with the Account Custom Field (Call Account/GetCustomFields for a list of all custom fields set at the account level)</td>
      </tr>
      <tr>
        <td>Value</td>
        <td>String</td>
        <td>For Text: Any value;&nbsp;For Option values, call Account/GetCustomFields to see possible values to pass in. Checkbox values should be "true" or "false".
          <br />
          <br />
        </td>
      </tr>
    </tbody>
  </table>
</div>
<h3>Examples</h3>
<h4>JSON</h4>
<pre>{ <br />    "ID": "1",<br />    "LocationAlias": "WA1",<br />    "Parameters":[<br />        { "Name":"T3.BuildServerTask.Password", "Value":"password" },<br />        { "Name":"T3.BuildServerTask.Network","Value":"VLAN_XXX" },<br />        { "Name":"T3.BuildServerTask.PrimaryDNS","Value":"192.168.64.19" },<br />        { "Name":"T3.BuildServerTask.SecondaryDNS","Value":"192.168.64.20" }<br />    ],

    "CustomFields":[<br />                { "CustomFieldID": 100,"Value": "A test"},<br />                { "CustomFieldID": 101,"Value": "2"},<br />                { "CustomFieldID": 102,"Value": "true"},]<br /> }</pre>
<h4>XML</h4>
<pre>&lt;DeployBlueprintRequest&gt;<br />    &lt;ID&gt;107&lt;/ID&gt;<br />    &lt;LocationAlias&gt;WA1&lt;/LocationAlias&gt;<br />    &lt;Parameters&gt;<br />        &lt;Parameter Name="T3.BuildServerTask.Password" Value="Pass@word1" /&gt;<br />        &lt;Parameter Name="T3.BuildServerTask.Network" Value="VLAN_XXX" /&gt;<br />        &lt;Parameter Name="T3.BuildServerTask.PrimaryDNS" Value="192.168.64.19" /&gt;<br />        &lt;Parameter Name="T3.BuildServerTask.SecondaryDNS" Value="192.168.64.20" /&gt;<br />    &lt;/Parameters&gt;

    &lt;CustomFields CustomFieldID="100" Value="Test text" /&gt;

    &lt;CustomFields CustomFieldID="104" Value="2" /&gt;

    &lt;CustomFields CustomFieldID="108" Value="true" /&gt;<br /> &lt;/DeployBlueprintRequest&gt;</pre> Response
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
      <td>
        <p>The ID of the Queued request to deploy the Blueprint.</p>
        <p>Status of the request can be obtained by calling the&nbsp;<a href="http://help.tier3.com/entries/20561586-get-deployment-status">GetDeploymentStatus</a>&nbsp;method.</p>
      </td>
    </tr>
  </tbody>
</table>
<h3>Examples</h3>
<h4>JSON</h4>
<pre>{<br />&nbsp; &nbsp; "RequestID": 1,<br />&nbsp; &nbsp; "Success":true,<br />&nbsp; &nbsp; "Message":"Success",<br />&nbsp; &nbsp; "StatusCode":0<br />}</pre>
<h4>XML</h4>
<div>
  <div>
    <pre>&lt;QueuedItemResponse Success="true" Message="Success" StatusCode="0"&gt;<br />&nbsp; &nbsp; &lt;RequestID&gt;1&lt;/RequestID&gt;<br />&lt;/QueuedItemResponse&gt;</pre>
  </div>
</div>
<h4>Status Codes</h4>
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
      <td>100</td>
      <td>Authentication Failed - You must logon to the API prior to calling this method.</td>
    </tr>
    <tr>
      <td>1210</td>
      <td>A required Parameter is missing.</td>
    </tr>
    <tr>
      <td>1211</td>
      <td>A Parameter value is invalid. &nbsp;Ensure that the supplied value meets the validation rules of the Blueprint Parameter.
        <br />
        <br />
      </td>
    </tr>
    <tr>
      <td>1212</td>
      <td>A Parameter type is invalid. &nbsp;Ensure that the supplied value is convertible to the type defined by the Blueprint Parameter.</td>
    </tr>
  </tbody>
</table>