{{{
  "title": "GetGroups",
  "date": "2-7-2013",
  "author": "Troy Schneringer",
  "attachments": []
}}}

Gets a list of all groups with the specified search criteria.

## URL

    REST: https://api.ctl.io/REST/Group/GetGroups/<format> (format = XML | JSON)
    SOAP: https://api.ctl.io/SOAP/Group.asmx?op=GetGroups

## Request

### Attributes

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | String | The alias of the account that owns the groups. If not provided it will assume the account to which the API user is mapped. Providing this value gives you the ability to access groups in your sub accounts. | No |
| Location | String | The data center location to query for groups. | Yes |

### Examples

#### JSON

    {
      "AccountAlias": "UNK",
      "Location": "DC1"
    }

#### XML

    <GetGroupsRequest>
        <AccountAlias>ACCT</AccountAlias>
        <Location>WA1</Location>
    </GetGroupsRequest>

## Response

### Attributes

| Name | Type | Description |
| --- | --- | --- |
| AccountAlias | String | The alias of the account that owns the groups. |
| Success | Boolean | True if the request was successful, otherwise False. |
| Message | String | A description of the result. The contents of this field does not contain any actionable information, it is purely intended to provide a human readable description of the result. |
| StatusCode | Int | This value will help to identify any errors which were encountered while processing the request. The value of '0' indicates success, all non-zero StatusCodes indicate an error state. |
| HardwareGroups | Complex | A list of Hardware Groups (see below) |

### Hardware Group Attributes

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
      "AccountAlias":"UNK",
      "HardwareGroups": [
        {
          "ID":5,
          "UUID":"3d30a6ab6c1243388b7bc966d073e353",
          "ParentID":2,
          "ParentUUID":"b7e44f0391824d408732f215a91a0578"
          "Name":"Group 01",
          "IsSystemGroup":false
        },
        {
          "ID":2,
          "UUID":"b7e44f0391824d408732f215a91a0578",
          "ParentID":1,
          "ParentUUID":"8a03fcae8ddfe321b05f00505682315a",
          "Name":"Group 02",
          "IsSystemGroup":false
        }
      ],
      "Success":true,
      "Message":"Success",
      "StatusCode":0
    }

#### XML

    <GetGroupsResponse AccountAlias="UNK" Success="true" Message="Success" StatusCode="0">
      <HardwareGroups>
        <HardwareGroup ID="5" UUID="3d30a6ab6c1243388b7bc966d073e353"
          ParentID="2" ParentUUID="b7e44f0391824d408732f215a91a0578"
          Name="Group 01" IsSystemGroup="false" />
        <HardwareGroup ID="2" UUID="b7e44f0391824d408732f215a91a0578"
          ParentID="1" ParentUUID="8a03fcae8ddfe321b05f00505682315a"
          Name="Group 02" IsSystemGroup="false" />
      </HardwareGroups>
    </GetGroupsResponse>

### Status Codes

| Status Code | Description |
| --- | --- |
| 0 | Request was successfully processed |
| 2 | Unknown Error - An application error occurred processing your request, contact support to resolve the issue. |
| 3 | Invalid Request Format. This value indicates that the XML or JSON requests do not match the expected format. |
| 100 | Authentication Failed - You must logon to the API prior to calling this method. |
