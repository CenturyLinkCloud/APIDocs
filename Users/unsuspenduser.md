{{{
  "title": "UnsuspendUser",
  "date": "5-3-2013",
  "author": "Brent Heinz",
  "attachments": []
}}}

Reactivate a user associated with a given account. Calls to this operation must include an authorization cookie acquired from the <a href="http://help.tier3.com/entries/20339862-logon">Logon operation.</a>

## URL

    REST: https://api.tier3.com/REST/User/UnsuspendUser/<format>
    SOAP: https://api.tier3.com/SOAP/User.asmx?op=UnsuspendUser

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
      <td>UserName</td>
      <td>String</td>
      <td>User name, which is could be their email address.</td>
      <td>Yes</td>
    </tr>
  </tbody>
</table>

### Examples

#### JSON

    { 

      UserName": "user3@company.com"

    }

#### XML (REST)

    <UserRequest><UserName>user3@company.com</UserName></UserRequest>

#### XML (SOAP)

    <soap12:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 

          xmlns:xsd="http://www.w3.org/2001/XMLSchema" 

          xmlns:soap12="http://www.w3.org/2003/05/soap-envelope">

    <soap12:Body>

      <UnsuspendUser xmlns="http://www.tier3.com/">

        <request>

          <UserName>user3@company.com</UserName>

        </request>

      </UnsuspendUser>

    </soap12:Body>

    </soap12:Envelope> 

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

    {"Success":true,"Message":"User unsuspended.","StatusCode":0}

#### XML (REST)

    <APIResponse Success="true" Message="User unsuspended." StatusCode="0" />

#### XML (SOAP)

    <soap:Envelope xmlns:soap="http://www.w3.org/2003/05/soap-envelope" 

      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 

      xmlns:xsd="http://www.w3.org/2001/XMLSchema">

      <soap:Body>

          <UnsuspendUserResponse xmlns="http://www.tier3.com/">

              <UnsuspendUserResult Success="true" Message="User unsuspended." StatusCode="0"/>

          </UnsuspendUserResponse>

      </soap:Body>

    </soap:Envelope>

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
      <td>Unknown Error. &nbsp;An application error occurred processing your request, contact support to resolve the issue.</td>
    </tr>
    <tr>
      <td>100</td>
      <td>Authentication Failed. &nbsp;You must logon to the API prior to calling this method.</td>
    </tr>
    <tr>
      <td>1704</td>
      <td>Username Required. &nbsp;You must provide a valid user name when calling this method.</td>
    </tr>
    <tr>
      <td>1705</td>
      <td>User Not Found. &nbsp;Provided user name does not exist.</td>
    </tr>
  </tbody>
</table>
