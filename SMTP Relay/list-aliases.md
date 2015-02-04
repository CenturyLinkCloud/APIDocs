{{{
  "title": "ListAliases",
  "date": "8-8-2011",
  "author": "jw@tier3.com",
  "attachments": []
}}}


This method will s list of all SMTP Relay aliases for your account.

## URL

    https://api.tier3.com/REST/SMTPRelay/ListAliases/<format>

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
      <td>SMTPRelayAliases</td>
      <td>List</td>
      <td>A list of RelayAlias objects.</td>
    </tr>
    <tr>
      <td>RelayAlias</td>
      <td>Complex</td>
      <td>The details of a Relay Alias instance.</td>
    </tr>
    <tr>
      <td>Alias</td>
      <td>String</td>
      <td>The new Relay Alias created for your account.</td>
    </tr>
    <tr>
      <td>Password</td>
      <td>String</td>
      <td>The password associated with the new Relay Alias.</td>
    </tr>
    <tr>
      <td>Status</td>
      <td>String</td>
      <td>The current status of the Relay Alias (expected values are 'Active', 'Deleted', and 'Disabled)</td>
    </tr>
  </tbody>
</table>

### Examples

#### XML

    <ListAliasesResponse Success="true" Message="ListAliases completed successfully" StatusCode="0">

      <SMTPRelayAliases>

        <RelayAlias Alias="ZZZ1-relay@t3mx.com" Password="password" Status="Active" />

        <RelayAlias Alias="ZZZ2-relay@t3mx.com" Password="password" Status="Deleted" />

        <RelayAlias Alias="ZZZ3-relay@t3mx.com" Password="password" Status="Disabled" />

      </SMTPRelayAliases>

    </ListAliasesResponse>

#### JSON

    {

      "SMTPRelayAliases":[

        {

          "Alias":"ZZZ1-relay@t3mx.com",

          "Password":"password",

          "Status":"Active"

        },

        {

          "Alias":"ZZZ2-relay@t3mx.com",

          "Password":"password",

          "Status":"Deleted"

        },

        {

          "Alias":"ZZZ3-relay@t3mx.com",

          "Password":"password",

          "Status":"Disabled"

        }    

      ],

      "Success":true,

      "Message":"ListAliases completed successfully",

      "StatusCode":0

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
      <td>ListAliases request was successfully processed</td>
    </tr>
    <tr>
      <td>2</td>
      <td>Unknown Error - An application error occurred processing your request, contact Tier3 support to resolve the issue.</td>
    </tr>
    <tr>
      <td>100</td>
      <td>Authentication Failed - You must logon to the API prior to calling this method.</td>
    </tr>
  </tbody>
</table>