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
| ParentUUID | String | The unique identifier of the parent group. | Yes |
| Name | String | The name of the Hardware Group | Yes |
| Description | String | A description of the Hardware Group.If none is supplied, the Name will be used. | No |

### Examples

#### JSON

    {
      "AccountAlias": "UNK",
      "ParentUUID": "b7e44f0391824d408732f215a91a0578",
      "Name": "Group 01",
      "Description": "My new group"
    }

#### XML

    <CreateHardwareGroupRequest>
        <AccountAlias>ACCT</AccountAlias>
        <ParentUUID>b7e44f0391824d408732f215a91a0578</ParentUUID>
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
| ID | Int | The legacy ID of the Group.<br/>_Deprecated. Not available after May 6, 2015. Use UUID instead._ |
| UUID | String | The unique identifier of the Group. |
| ParentID | Int | The legacy ID of the parent Group.<br/>_Deprecated. Not available after May 6, 2015. Use ParentUUID instead._ |
| ParentUUID | String | The unique identifier of the Parent Group. |
| Name | String | The name of the Group. |
| IsSystemGroup | Bool | Denotes a required system Group. |

### Examples

#### JSON

    {
      "Group":
        {
          "ID":5,
          "UUID":"3d30a6ab6c1243388b7bc966d073e353",
          "ParentID":2,
          "ParentUUID":"b7e44f0391824d408732f215a91a0578"
          "Name":"Group 01",
          "IsSystemGroup":false
        },
      "Success":true,
      "Message":"Success",
      "StatusCode":0
    }


#### XML

    <CreateHardwareGroupResponse Success="true" Message="Success" StatusCode="0">
      <Group ID="5" UUID="3d30a6ab6c1243388b7bc966d073e353"
        ParentID="2" ParentUUID="b7e44f0391824d408732f215a91a0578"
        Name="Group 01" IsSystemGroup="false" />
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
