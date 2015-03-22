{{{
  "title": "CreateHardwareGroup",
  "date": "10-24-2013",
  "author": "Troy Schneringer",
  "attachments": []
}}}

Creates a new Hardware Group.

## URL

    REST: https://api.ctl.io/REST/Group/CreateHardwareGroup/<format> (format = XML | JSON)
    SOAP: https://api.ctl.io/SOAP/Group.asmx?op=CreateHardwareGroup

## Request

### Attributes

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | String | The alias of the account to owns the group. Can be the parent alias or a sub-account alias. | Yes |
| ParentID | Int | The ID of the parent group. | Yes |
| Name | String | The name of the Hardware Group | Yes |
| Description | String | A description of the Hardware Group.If none is supplied, the Name will be used. | No |

### Examples

#### JSON

    {
      "AccountAlias": "UNK",
      "ParentID": "2",
      "Name": "Group 01",
      "Description": "My new group"
    }

#### XML

    <CreateHardwareGroupRequest>
        <AccountAlias>ACCT</AccountAlias>
        <ParentID>2</ParentID>
        <Name>Group 01</Name>
        <Description>My new group</Description>
    </CreateHardwareGroupRequest>

## Response

### Attributes

| Name | Type | Description |
| --- | --- | --- |
| Success | Boolean | True if the request was successful, otherwise False. |
| Message | String | A description of the result. The contents of this field does not contain any actionable information, it is purely intended to provide a human readable description of the result. |
| StatusCode | Int | This value will help to identify any errors which were encountered while processing the request. The value of '0' indicates success, all non-zero StatusCodes indicate an error state. |
| Group | Complex | The created group (see below). |

### Group Attributes

| Name | Type | Description |
| --- | --- | --- |
| ID | Int | The ID of the Group. |
| Name | String | The name of the Group. |
| ParentID | Int | The ID of the Parent Group. |

### Examples

#### JSON

    {
      "Group":
        {
          "ID":5,
          "Name":"Group 01",
          "ParentID":2
        },
      "Success":true,
      "Message":"Success",
      "StatusCode":0
    }

#### XML

    <CreateHardwareGroupResponse Success="true" Message="Success" StatusCode="0">
      <Group ID="5" Name="Group 01" ParentID="2"/>
    </CreateHardwareGroupResponse>

### Status Codes

| Status Code | Description |
| --- | --- |
| 0 | Request was successfully processed |
| 2 | Unknown Error - An application error occurred processing your request, contact support to resolve the issue. |
| 3 | Invalid Request Format. This value indicates that the XML or JSON requests do not match the expected format. |
| 5 | Resource Not Found.  A Parent Group with the specified ID cannot be found. |
| 100 | Authentication Failed - You must logon to the API prior to calling this method. |
| 1310 | The Name attribute is missing. |
