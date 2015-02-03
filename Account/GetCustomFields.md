{{{
  "title": "GetCustomFields",
  "date": "5-1-2013",
  "author": "Cale Hoopes",
  "attachments": []
}}}

GetCustomFields
<p>Gets the account custom field definitions.</p>
URL
<pre>REST: https://api.tier3.com/REST/Account/GetCustomFields/&lt;format&gt;<br />SOAP: https://api.tier3.com/SOAP/Account.asmx?op=GetCustomFields</pre> Request
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
      <td>AccountAlias</td>
      <td>String</td>
      <td>The Account Alias that has custom fields
        <br />configured on it.</td>
      <td>Yes</td>
    </tr>
  </tbody>
</table>
<h3>Examples</h3>
<h4>JSON</h4>
<pre>{ "AccountAlias": "ACCT" }</pre>
<h4>XML</h4>
<pre>&lt;GetCustomFieldsRequest&gt;

    &lt;AccountAlias&gt;ACCT&lt;/AccountAlias&gt;

&lt;/GetCustomFieldsRequest&gt;</pre> Response
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
      <td>AccountCustomField</td>
      <td>Complex</td>
      <td>Account Custom Field complex object</td>
    </tr>
  </tbody>
</table>
<h3>Examples</h3>
<h4>JSON</h4>
<pre>{

    "AccountCustomFields": [

        {

            "ID": 100,

            "CustomFieldTypeID": 1,

            "CustomFieldType": "Text",

            "Name": "Name",

            "IsRequired": true,

            "AccountCustomFieldOptions": null

        },

        {

            "ID": 104,

            "CustomFieldTypeID": 2,

            "CustomFieldType": "Option",

            "Name": "Type",

            "IsRequired": true,

            "AccountCustomFieldOptions": [

                {

                    "ID": 48,

                    "Name": "My Type",

                    "Value": "1"

                },

                {

                    "ID": 49,

                    "Name": "Your Type",

                    "Value": "2"

                }

            ]

        },

        {

            "ID": 108,

            "CustomFieldTypeID": 3,

            "CustomFieldType": "Checkbox",

            "Name": "Enabled",

            "IsRequired": true,

            "AccountCustomFieldOptions": []

        },

        {

            "ID": 116,

            "CustomFieldTypeID": 1,

            "CustomFieldType": "Text",

            "Name": "Not required",

            "IsRequired": false,

            "AccountCustomFieldOptions": null

        }

    ],

    "Success": true,

    "Message": "Custom Fields retrieved successfully.",

    "StatusCode": 0

}</pre>
<h4>XML</h4>
<pre>&lt;AccountCustomFieldsResponse 

  Success="true"

  Message="Custom Fields retrieved successfully."

  StatusCode="0"&gt;

    &lt;AccountCustomFields&gt;

        &lt;AccountCustomField ID="100" CustomFieldTypeID="1" CustomFieldType="Text" Name="Name" IsRequired="true" /&gt;

        &lt;AccountCustomField ID="104" CustomFieldTypeID="2" CustomFieldType="Option" Name="Type" IsRequired="true"&gt;

            &lt;AccountCustomFieldOptions ID="48" Name="My Type" Value="1" /&gt;

            &lt;AccountCustomFieldOptions ID="49" Name="Your Type" Value="2" /&gt;

        &lt;/AccountCustomField&gt;

        &lt;AccountCustomField ID="108" CustomFieldTypeID="3" CustomFieldType="Checkbox" Name="Enabled" IsRequired="true" /&gt;

        &lt;AccountCustomField ID="116" CustomFieldTypeID="1" CustomFieldType="Text" Name="Not required" IsRequired="false" /&gt;

    &lt;/AccountCustomFields&gt;

&lt;/AccountCustomFieldsResponse&gt;</pre>
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
      <td>Unknown Error. &nbsp;An application error occurred processing your request, contact Tier3 support to resolve the issue.</td>
    </tr>
    <tr>
      <td>3</td>
      <td>Invalid Request Format. This value indicates that the XML or JSON requests do not match the expected format.</td>
    </tr>
    <tr>
      <td>100</td>
      <td>Authentication Failed. &nbsp;You must logon to the API prior to calling this method.</td>
    </tr>
  </tbody>
</table>