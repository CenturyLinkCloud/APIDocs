{{{
  "title": "GetCustomFields",
  "date": "5-1-2013",
  "author": "Cale Hoopes",
  "attachments": []
}}}

Gets the account custom field definitions.

## URL

    REST: https://api.ctl.io/REST/Account/GetCustomFields/<format> (format = XML | JSON)
    SOAP: https://api.ctl.io/SOAP/Account.asmx?op=GetCustomFields

## Request

### Attributes

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | String | The Account Alias that has custom fields configured on it. | Yes |

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

| Name | Type | Description |
| --- | --- | --- |
| Success | Boolean | True if the request was successful, otherwise False. |
| Message | String | A description of the result. The contents of this field does not contain any actionable information, it is purely intended to provide a human readable description of the result. |
| StatusCode | Int | This value will help to identify any errors which were encountered while processing the request. The value of '0' indicates success, all non-zero StatusCodes indicate an error state. |
| AccountCustomField | Complex | Account Custom Field complex object |

### AccountCustomField Attributes

| Name | Type | Description |
| --- | --- | --- |
| ID | Int | _Deprecated. Value is -1. Use UUID instead._ |
| UUID | String | Unique identifier of the Account Custom Field. |
| CustomFieldTypeID | Int | _Deprecated. Value is -1. Use CustomFieldType instead._ |
| CustomFieldType | String | The type of field: "Text", "Option", or "Checkbox". |
| Name | String | Friendly name of the Custom Field. |
| IsRequired | Boolean | Whether or not the Custom Field is required. |
| AccountCustomFieldOptions | Complex | Options for the Account Custom Field, specific to the field type. |

### Examples

#### JSON

    {
      "AccountCustomFields": [
        {
          "ID": -1,
          "CustomFieldTypeID": -1,
          "CustomFieldType": "Text",
          "Name": "Name",
          "IsRequired": true,
          "UUID":"dba67b15-6e77-4e1f-b413-ddfa3dc4ac1d"
          "AccountCustomFieldOptions": null
        },
        {
          "ID": -1,
          "CustomFieldTypeID": -1,
          "CustomFieldType": "Option",
          "Name": "Type",
          "IsRequired": true,
          "UUID":"d61daab2-e99f-40c2-a4b5-820c3d97eea4"
          "AccountCustomFieldOptions": [
            {
              "Name": "My Type",
              "Value": "1"
            },
            {
              "Name": "Your Type",
              "Value": "2"
            }
          ]
        },
        {
          "ID": -1,
          "CustomFieldTypeID": -1,
          "CustomFieldType": "Checkbox",
          "Name": "Enabled",
          "IsRequired": true,
          "UUID": "de775088-8b94-4e9f-b64b-416623477cf8"
          "AccountCustomFieldOptions": []
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
            <AccountCustomField ID="-1" CustomFieldTypeID="-1" CustomFieldType="Text" Name="Name" UUID="dba67b15-6e77-4e1f-b413-ddfa3dc4ac1d" IsRequired="true" />
            <AccountCustomField ID="-1" CustomFieldTypeID="-1" CustomFieldType="Option" Name="Type" UUID="d61daab2-e99f-40c2-a4b5-820c3d97eea4" IsRequired="true">
                <AccountCustomFieldOptions Name="My Type" Value="1" />
                <AccountCustomFieldOptions Name="Your Type" Value="2" />
            </AccountCustomField>
            <AccountCustomField ID="-1" CustomFieldTypeID="-1" CustomFieldType="Checkbox" Name="Enabled" UUID="de775088-8b94-4e9f-b64b-416623477cf8" IsRequired="true" />
        </AccountCustomFields>
    </AccountCustomFieldsResponse>

### Status Codes

| Status Code | Description |
| --- | --- |
| 0 | Request was successfully processed |
| 2 | Unknown Error.  An application error occurred processing your request, contact support to resolve the issue. |
| 3 | Invalid Request Format. This value indicates that the XML or JSON requests do not match the expected format. |
| 100 | Authentication Failed.  You must logon to the API prior to calling this method. |
