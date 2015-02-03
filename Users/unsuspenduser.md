{{{
  "title": "UnsuspendUser",
  "date": "5-3-2013",
  "author": "Brent Heinz",
  "attachments": []
}}}

<div>
  UnsuspendUser
  <p>Reactivate a user associated with a given account. Calls to this operation must include an authorization cookie acquired from the <a href="http://help.tier3.com/entries/20339862-logon">Logon operation.</a>
  </p>
  URL
  <pre>REST: https://api.tier3.com/REST/User/UnsuspendUser/&lt;format&gt; (format = XML | JSON) <br />SOAP: https://api.tier3.com/SOAP/User.asmx?op=UnsuspendUser </pre> Request
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
        <td>UserName</td>
        <td>String</td>
        <td>User name, which is could be their email address.</td>
        <td>Yes</td>
      </tr>
    </tbody>
  </table>
  <h3>Examples</h3>
  <h4>JSON (REST)</h4>
  <pre>{ <br />     "UserName": "user3@company.com"<br />}</pre>
  <h4>XML (REST)</h4>
  <pre>&lt;UserRequest&gt;&lt;UserName&gt;user3@company.com&lt;/UserName&gt;&lt;/UserRequest&gt;</pre>
  <h4>XML (SOAP)</h4>
  <pre>&lt;soap12:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 

        xmlns:xsd="http://www.w3.org/2001/XMLSchema" 

        xmlns:soap12="http://www.w3.org/2003/05/soap-envelope"&gt;

  &lt;soap12:Body&gt;

    &lt;UnsuspendUser xmlns="http://www.tier3.com/"&gt;

      &lt;request&gt;

        &lt;UserName&gt;user3@company.com&lt;/UserName&gt;

      &lt;/request&gt;

    &lt;/UnsuspendUser&gt;

  &lt;/soap12:Body&gt;

&lt;/soap12:Envelope&gt;   

</pre> Response
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
    </tbody>
  </table>
  <h3>Examples</h3>
  <h4>JSON (REST)</h4>
  <pre>{"Success":true,"Message":"User unsuspended.","StatusCode":0}

    </pre>
  <h4>XML (REST)</h4>
  <pre>&lt;APIResponse Success="true" Message="User unsuspended." StatusCode="0" /&gt;

    </pre>
  <h4>XML (SOAP)</h4>
  <pre>&lt;soap:Envelope xmlns:soap="http://www.w3.org/2003/05/soap-envelope" 

    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 

    xmlns:xsd="http://www.w3.org/2001/XMLSchema"&gt;

    &lt;soap:Body&gt;

        &lt;UnsuspendUserResponse xmlns="http://www.tier3.com/"&gt;

            &lt;UnsuspendUserResult Success="true" Message="User unsuspended." StatusCode="0"/&gt;

        &lt;/UnsuspendUserResponse&gt;

    &lt;/soap:Body&gt;

&lt;/soap:Envelope&gt;

</pre>
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
</div>