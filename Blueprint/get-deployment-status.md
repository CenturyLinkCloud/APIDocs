{{{
  "title": "Get Deployment Status",
  "date": "7-14-2014",
  "author": "Troy Schneringer",
  "attachments": []
}}}

Gets the status of the specified Blueprint deployment.

## URL

    REST: https://api.tier3.com/REST/Blueprint/GetBlueprintStatus/<format>
    SOAP: https://api.tier3.com/SOAP/Blueprints.asmx?op=GetDeploymentStatusMsg

## Request

### Attributes

<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
      <th>Description</th>
      <th>Req.</th>
    </tr>
  </thead>
  <tbody>
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

### Examples

#### JSON

    {

      "RequestID": "1",

      "LocationAlias": "WA1"

    }

#### XML

    <GetDeploymentStatusRequest>

        <RequestID>1</RequestID>

        <LocationAlias>WA1</LocationAlias>

    </GetDeploymentStatusRequest>

## Response

### Attributes

<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
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

### Examples

#### JSON

    {

      "RequestID":210,

      "CurrentStatus":"Failed",

      "Description":"Error Building Blueprint",

      "StatusDate":"\/Date(1318480463790)\/",

      "Step":"0",

      "PercentComplete":0,

      "Success":true,

      "Message":"Success",

      "StatusCode":0,

      "Servers":["WA1T3NWEB01"]

    }


#### XML

    <GetDeploymentStatusResponse

      Success="true"

      Message="Success"

      StatusCode="0"

      RequestID="210"

      CurrentStatus="Failed" 

      Description="Error Building Blueprint" 

      StatusDate="2011-10-12T21:34:23.79" 

      Step="0" 

      PercentComplete="0"
    >

        <Servers>

          <string>WA1T3NWEB01</string>

        </Servers>

    </GetDeploymentStatusResponse>

### Status Codes

<table>
    <thead>
  <tr>
    <th>Status Code</th>
    <th>Description</th>
  </tr>
  </thead>
  <tbody>
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