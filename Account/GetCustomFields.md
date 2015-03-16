{{{
  "title": "GetCustomFields",
  "date": "5-1-2013",
  "author": "Cale Hoopes",
  "attachments": []
}}}

Gets the account custom field definitions.

## URL

    REST: https://api.ctl.io/REST/Account/GetCustomFields/<format>
    SOAP: https://api.ctl.io/SOAP/Account.asmx?op=GetCustomFields

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
      <td>The Account Alias that has custom fields
        <br />configured on it.</td>
      <td>Yes</td>
    </tr>
  </tbody>
</table>

### Examples

#### JSON

    { 

      "AccountAlias": "ACCT" 

    }

#### XML

    <GetCustomFieldsRequest>

        <AccountAlias>ACCT</AccountAlias>

    </GetCustomFieldsRequest>

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
      <td>AccountCustomField</td>
      <td>Complex</td>
      <td>Account Custom Field complex object</td>
    </tr>
  </tbody>
</table>

### Examples

#### JSON

    {

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

    }


#### XML

    <AccountCustomFieldsResponse 

      Success="true"

      Message="Custom Fields retrieved successfully."

      StatusCode="0">

        <AccountCustomFields>

            <AccountCustomField ID="100" CustomFieldTypeID="1" CustomFieldType="Text" Name="Name" IsRequired="true" />

            <AccountCustomField ID="104" CustomFieldTypeID="2" CustomFieldType="Option" Name="Type" IsRequired="true">

                <AccountCustomFieldOptions ID="48" Name="My Type" Value="1" />

                <AccountCustomFieldOptions ID="49" Name="Your Type" Value="2" />

            </AccountCustomField>

            <AccountCustomField ID="108" CustomFieldTypeID="3" CustomFieldType="Checkbox" Name="Enabled" IsRequired="true" />

            <AccountCustomField ID="116" CustomFieldTypeID="1" CustomFieldType="Text" Name="Not required" IsRequired="false" />

        </AccountCustomFields>

    </AccountCustomFieldsResponse>


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
      <td>100</td>
      <td>Authentication Failed. &nbsp;You must logon to the API prior to calling this method.</td>
    </tr>
  </tbody>
</table>