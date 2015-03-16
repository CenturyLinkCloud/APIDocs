{{{
  "title": "GetSnapshots",
  "date": "2-7-2013",
  "author": "Troy Schneringer",
  "attachments": []
}}}

Gets the list of Snapshots associated with the server.

## URL

    REST: https://api.ctl.io/REST/Server/GetSnapshots/<format>
    SOAP: https://api.ctl.io/SOAP/Server.asmx?op=GetSnapshots

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
      <td>AccountAlias</td>
      <td>String</td>
      <td>The alias of the account that owns the server. If not provided it will assume the account to which the API user is mapped. Providing this value gives you the ability to access servers in your sub accounts</td>
      <td>No</td>
    </tr>
    <tr>
      <td>Name</td>
      <td>String</td>
      <td>The name of the Server to get Snapshots for.</td>
      <td>Yes</td>
    </tr>
  </tbody>
</table>

### Examples

#### JSON

    {

      "Name": "DEMOFIRST01",

      "AccountAlias": "UNK"

    }

#### XML

    <ServerRequest>

        <AccountAlias>ACCT</AccountAlias>

        <Name>SERVER01</Name>

    </ServerRequest>

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
      <td>Snapshots</td>
      <td>Complex (see below)</td>
      <td>
        <p>A list of Snapshots (see below)</p>
      </td>
    </tr>
  </tbody>
</table>

### Snapshot Attributes

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
      <td>Name</td>
      <td>String</td>
      <td>The full name of the Snapshot.</td>
    </tr>
    <tr>
      <td>Description</td>
      <td>String</td>
      <td>The description of the Snapshot.</td>
    </tr>
    <tr>
      <td>DateCreated</td>
      <td>DateTime</td>
      <td>The time (in UTC) when the Snapshot was created.</td>
    </tr>
  </tbody>
</table>

### Examples

#### JSON

    {
        "RequestID:1,
        "Success":true,
        "Message":"Success",
        "StatusCode":0,
        "Snapshots":[
            {"Name":"2012-01-01-12:00:00","Description":"Snapshot (2012-01-01-12:00:00)","DateCreated":"\/Date(1330047404893)\/"}]
    }

#### XML

    <GetSnapshotsResponse Success="true" Message="Successfully retrieved snapshots" StatusCode="0">
        <Snapshots>
            <Snapshot>
                <Name>2012-01-01-12:00:00</Name>
                <Description>Snapshot (2012-01-01-12:00:00)</Description>
                <DateCreated>2012-01-01T12:00:00.000</DateCreated>
            </Snapshot>
        </Snapshots>
    </GetSnapshotsResponse>

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
      <td>5</td>
      <td>Resource Not Found. &nbsp;A server with the specified name could not be found.</td>
    </tr>
    <tr>
      <td>6</td>
      <td>Invalid Operation. &nbsp;Server must be in an active state.</td>
    </tr>
    <tr>
      <td>100</td>
      <td>Authentication Failed. &nbsp;You must logon to the API prior to calling this method.
        <br />
        <br />
      </td>
    </tr>
    <tr>
      <td>1410</td>
      <td>Name is required.</td>
    </tr>
  </tbody>
</table>