{{{
  "title": "CreateAlias",
  "date": "8-8-2011",
  "author": "jw@tier3.com",
  "attachments": []
}}}

This method will create a new SMTP Relay alias.

## URL

    REST: https://api.ctl.io/REST/SMTPRelay/CreateAlias/<format>

## Request

### Attributes

None.

### Examples

#### JSON

N/A

#### XML

N/A

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
      <td>RelayAlias</td>
      <td>String</td>
      <td>The new Relay Alias created for your account.</td>
    </tr>
    <tr>
      <td>Password</td>
      <td>String</td>
      <td>The password associated with the new Relay Alias.</td>
    </tr>
  </tbody>
</table>

### Examples

#### XML

    <CreateAliasResponse Success="true" Message="Alias has been created." StatusCode="0" RelayAlias="ZZZ1-relay@t3mx.com" Password="password" />

#### JSON

    {

      "Success":true,

      "Message":"Alias has been disabled.",

      "StatusCode":0,

      "RelayAlias":"ZZZ1-relay@t3mx.com",

      "Password":"password"

    }

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
      <td>CreateAlias request was successfully processed</td>
    </tr>
    <tr>
      <td>2</td>
      <td>Unknown Error - An application error occurred processing your request, contact Tier3 support to resolve the issue.</td>
    </tr>
    <tr>
      <td>100</td>
      <td>Authentication Failed - You must logon to the API prior to calling this method.</td>
    </tr>
    <tr>
      <td>400</td>
      <td>You have reached the SMTP Relay Alias limit set on your account. Contact the&nbsp;<a href="mailto:noc@tier3.com">NOC</a>&nbsp;to increase your account limit if you need more.</td>
    </tr>
  </tbody>
</table>