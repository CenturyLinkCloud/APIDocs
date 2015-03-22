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

| Status Code | Description |
| --- | --- |
| 0 | Request was successfully processed |
| 2 | Unknown Error.  An application error occurred processing your request, contact support to resolve the issue. |
| 3 | Invalid Request Format. This value indicates that the XML or JSON requests do not match the expected format. |
| 100 | Authentication Failed.  You must logon to the API prior to calling this method. |
