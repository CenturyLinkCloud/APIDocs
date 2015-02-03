{{{
  "title": "GetAccountDetails",
  "date": "7-9-2014",
  "author": "Richard Seroter",
  "attachments": []
}}}

Gets all of the contact information and settings for a given account. Calls to this operation must include an authorization cookie acquired from the <a href="http://help.tier3.com/entries/20339862-logon">Logon operation.</a>

## URL

    REST: https://api.tier3.com/REST/Account/GetAccountDetails/&lt;format&gt; (format = XML | JSON)
    SOAP: https://api.tier3.com/SOAP/Account.asmx?op=GetAccountDetails

##Request
### Attributes

<table>
    <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
      <th>Description</th>
      <th>Required</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>AccountAlias</td>
      <td>String</td>
      <td>Short code for a particular account.</td>
      <td>Yes</td>
    </tr>
  </tbody>
</table>

### Examples
<h4>JSON (REST)</h4>
<pre>{ <br />    "AccountAlias": "1000"<br />}</pre>
<h4>XML (REST)</h4>
<pre>&lt;GetAccountDetailsRequest&gt;<br />     &lt;AccountAlias&gt;1000&lt;/AccountAlias&gt;<br />&lt;/GetAccountDetailsRequest&gt;</pre>
<h4>XML (SOAP)</h4>
<pre>&lt;soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 

        xmlns:xsd="http://www.w3.org/2001/XMLSchema" 

        xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/"&gt;

  &lt;soap:Body&gt;

    &lt;GetAccountDetails xmlns="http://www.tier3.com/"&gt;

      &lt;request&gt;

         &lt;AccountAlias&gt;1000&lt;/AccountAlias&gt;

      &lt;/request&gt;

    &lt;/GetAccountDetails&gt;

  &lt;/soap:Body&gt;

&lt;/soap:Envelope&gt;    

</pre> 

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
      <td>AccountDetails</td>
      <td>Complex</td>
      <td>The account details</td>
    </tr>
  </tbody>
</table>
<h3>AccountDetails Attributes</h3>
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
      <td>AccountAlias</td>
      <td>String</td>
      <td>Short name associated with the account.</td>
    </tr>
    <tr>
      <td>ParentAlias</td>
      <td>String</td>
      <td>Short name associated with parent account of the queried account.</td>
    </tr>
    <tr>
      <td>Location</td>
      <td>String</td>
      <td>Data center location alias associated with this account.</td>
    </tr>
    <tr>
      <td>BusinessName</td>
      <td>String</td>
      <td>Full name of the business that the account is registered under.</td>
    </tr>
    <tr>
      <td>Address1</td>
      <td>String</td>
      <td>Street address of the business associated with this account.</td>
    </tr>
    <tr>
      <td>Address2</td>
      <td>String</td>
      <td>Secondary street address (if any) of the business associated with this account.</td>
    </tr>
    <tr>
      <td>City</td>
      <td>String</td>
      <td>City of the business associated with this account.</td>
    </tr>
    <tr>
      <td>StateProvince</td>
      <td>String</td>
      <td>State or province of the business associated with this account.</td>
    </tr>
    <tr>
      <td>PostalCode</td>
      <td>String</td>
      <td>Postal code of the business associated with this account.</td>
    </tr>
    <tr>
      <td>Country</td>
      <td>String</td>
      <td>Country of the business associated with this account.</td>
    </tr>
    <tr>
      <td>Telephone</td>
      <td>String</td>
      <td>Telephone number of the business associated with this account.</td>
    </tr>
    <tr>
      <td>Fax</td>
      <td>String</td>
      <td>Fax number (if any) of the business associated with this account.</td>
    </tr>
    <tr>
      <td>TimeZone</td>
      <td>String</td>
      <td>Time zone of the business associated with this account.</td>
    </tr>
    <tr>
      <td>Status</td>
      <td>Int</td>
      <td>Indicator of whether the account is active or not.
        <p>Active&nbsp;=&nbsp;1,
          <br />Disabled&nbsp;=&nbsp;2,
          <br />Deleted&nbsp;=&nbsp;3,
          <br />Demo&nbsp;=&nbsp;4</p>
      </td>
    </tr>
    <tr>
      <td>ShareParentNetworks</td>
      <td>Boolean</td>
      <td>True/false flag indicating whether this account shares the networks of its parent.</td>
    </tr>
  </tbody>
</table>

### Examples 
<h4>JSON (REST)</h4>
<pre>{<br />     "AccountDetails":{<br />              "AccountAlias":"1001",<br />              "ParentAlias":"1000",<br />              "Location":"WA1",<br />              "BusinessName":"Example Business Name",<br />              "Address1":"110 110th Avenue",<br />              "Address2":null,<br />              "City":"Bellevue",<br />              "StateProvince":"WA",<br />              "PostalCode":"98004",<br />              "Country":"USA",<br />              "Telephone":"877-388-4373",<br />              "Fax":null,<br />              "TimeZone":"Pacific Standard Time",<br />              "Status":2,<br />              "ShareParentNetworks":true},<br />     "Success":true,<br />     "Message":"Account details successfully queried.",<br />     "StatusCode":0<br />}</pre>
<h4>XML (REST)</h4>
<pre>&lt;AccountDetailsResponse Success="true" Message="Account details successfully queried." StatusCode="0"&gt;

        &lt;AccountDetails AccountAlias="1001" ParentAlias="1000" Location="WA1" TimeZone="Pacific Standard Time" Status="2" ShareParentNetworks="true"&gt;

            &lt;BusinessName&gt;Example Business Name&lt;/BusinessName&gt;

            &lt;Address1&gt;110 110th Avenue&lt;/Address1&gt;

            &lt;City&gt;Bellevue&lt;/City&gt;

            &lt;StateProvince&gt;WA&lt;/StateProvince&gt;

            &lt;PostalCode&gt;98004&lt;/PostalCode&gt;

            &lt;Country&gt;USA&lt;/Country&gt;

            &lt;Telephone&gt;877-388-4373&lt;/Telephone&gt;

        &lt;/AccountDetails&gt;

&lt;/AccountDetailsResponse&gt;

    </pre>
<h4>XML (SOAP)</h4>
<pre>&lt;soap:Envelope xmlns:soap="http://www.w3.org/2003/05/soap-envelope" 

        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 

        xmlns:xsd="http://www.w3.org/2001/XMLSchema"&gt;

     &lt;soap:Body&gt;

        &lt;GetAccountDetailsResponse xmlns="http://www.tier3.com/"&gt;

            &lt;GetAccountDetailsResult Success="true" Message="Account details successfully queried." StatusCode="0"&gt;

                &lt;AccountDetails AccountAlias="1001" ParentAlias="1000" Location="WA1" TimeZone="Pacific Standard Time" Status="2" ShareParentNetworks="true"&gt;

                    &lt;BusinessName&gt;Example Business Name&lt;/BusinessName&gt;

                    &lt;Address1&gt;110 110th Avenue&lt;/Address1&gt;

                    &lt;City&gt;Bellevue&lt;/City&gt;

            	    &lt;StateProvince&gt;WA&lt;/StateProvince&gt;

                    &lt;PostalCode&gt;98004&lt;/PostalCode&gt;

                    &lt;Country&gt;USA&lt;/Country&gt;

                    &lt;Telephone&gt;877-388-4373&lt;/Telephone&gt;

                &lt;/AccountDetails&gt;

            &lt;/GetAccountDetailsResult&gt;

        &lt;/GetAccountDetailsResponse&gt;

      &lt;/soap:Body&gt;

&lt;/soap:Envelope&gt;

</pre>

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
      <td>Request was successfully processed</td>
    </tr>
    <tr>
      <td>2</td>
      <td>Unknown Error. &nbsp;An application error occurred processing your request, contact Tier3 support to resolve the issue.</td>
    </tr>
    <tr>
      <td>5</td>
      <td>Resource Not Found. &nbsp;Provided account alias does not exist.</td>
    </tr>
    <tr>
      <td>100</td>
      <td>Authentication Failed. &nbsp;You must logon to the API prior to calling this method.</td>
    </tr>
    <tr>
      <td>1600</td>
      <td>Account Alias Required. &nbsp;You must provide an account alias when calling this method.</td>
    </tr>
  </tbody>
</table>