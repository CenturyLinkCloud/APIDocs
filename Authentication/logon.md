{{{
  "title": "Logon",
  "date": "10-13-2014",
  "author": "jw@tier3.com",
  "attachments": []
}}}

This method is required to be called prior to calling any other method exposed by the Tier3 API. This method validates your credentials and writes the Encrypted cookie required to be present for all subsequent calls into the API.

## URL

    REST: https://api.tier3.com/REST/Auth/Logon/

## Request
### Attributes

<table>
  <tbody>
    <tr>
      <td><strong>Attribute Name</strong>
      </td>
      <td><strong>Type</strong>
      </td>
      <td><strong>Required</strong>
      </td>
      <td><strong>Description</strong>
      </td>
    </tr>
    <tr>
      <td>APIKey</td>
      <td>String</td>
      <td>Yes</td>
      <td>The API access key provided by Tier3.</td>
    </tr>
    <tr>
      <td>Password</td>
      <td>String</td>
      <td>Yes</td>
      <td>The API password provided by Tier3.</td>
    </tr>
  </tbody>
</table>

### Examples
<pre>&lt;LogonRequest&gt;

  &lt;APIKey&gt;apikey&lt;/APIKey&gt;

  &lt;Password&gt;password&lt;/Password&gt;

&lt;/LogonRequest&gt;</pre>
      <br />
      <br /><strong>JSON</strong>:
      <br />
      <pre>{

  "APIKey":"apikey",

  "Password":"password"

}</pre>

## Response
### Attributes
<table>
  <tbody>
    <tr>
      <td><strong>Attribute Name</strong>
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
  </tbody>
</table>

### Examples
<strong>XML</strong>:
<pre>&lt;LogonResponse Success="true" Message="Login Successful" StatusCode="0" /&gt;</pre>

<strong>JSON</strong>:
<pre>{

  "Success":true,

  "Message":"Login Successful",

  "StatusCode":0

}</pre>

### Status Codes
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
      <td>Logon was successful</td>
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
      <td>Authentication Failed - The APIKey &amp; Password combination were not valid. Verify that the values provided in your message match the values given to you by Tier3.</td>
    </tr>
  </tbody>
</table>
