{{{
  "title": "DisableAlias",
  "date": "12-26-2012",
  "author": "jw@tier3.com",
  "attachments": []
}}}

This method will disable an existing SMTP Relay alias.

## URL

    https://api.ctl.io/REST/SMTPRelay/DisableAlias/<format>

## Request

### Attributes
  
<table>
  <tbody>
    <tr>
      <thead>
      <tr>
        <th>Name</th>
        <th>Type</th>
        <th>Description</th>
        <th>Req.</th>
      </tr>
    </thead>
    <tbody>
    </tr>
    <tr>
      <td>RelayAlias</td>
      <td>String</td>
      <td>The the SMTP relay alias to disable.</td>
      <td>Yes</td>
    </tr>
  </tbody>
</table>

### Examples

#### JSON

    {

      "RelayAlias":"ZZZ1-relay@t3mx.com"

    }

#### XML

    <SMTPUserRequest>

        <RelayAlias>ZZZ1-relay@t3mx.com</RelayAlias>

    </SMTPUserRequest>

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
  </tbody>
</table>

### Examples

#### JSON

    {

      "Success":true,

      "Message":"Alias has been disabled.",

      "StatusCode":0 

    }

#### XML

    <APIResponse Success="true" Message="Alias has been disabled." StatusCode="0" />

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
      <td>DisableAlias request was successfully processed</td>
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
      <td>SMTP Relay alias does not exist for your account.</td>
    </tr>
    <tr>
      <td>100</td>
      <td>Authentication Failed - You must logon to the API prior to calling this method.</td>
    </tr>
    <tr>
      <td>401</td>
      <td>RelayAlias attribute is required.</td>
    </tr>
    <tr>
      <td>402</td>
      <td>Relay alias was previously deleted.</td>
    </tr>
    <tr>
      <td>403</td>
      <td>Relay alias has already been disabled.</td>
    </tr>
  </tbody>
</table>