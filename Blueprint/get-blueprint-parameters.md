{{{
  "title": "Get Blueprint Parameters",
  "date": "9-15-2014",
  "author": "Troy Schneringer",
  "attachments": []
}}}

Gets a the full list of parameters that are required to deploy a Blueprint.

## URL

    REST: https://api.ctl.io/REST/Blueprint/GetBlueprintParameters/<format>
    SOAP: https://api.ctl.io/SOAP/Blueprints.asmx?op=GetBlueprintParamatersResponseMsg

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
      <td>ID</td>
      <td>Int</td>
      <td>
        <p>The ID of the Blueprint to retrieve parameters for.</p>
      </td>
      <td>
        <p>Yes</p>
      </td>
    </tr>
  </tbody>
</table>

### Examples

#### JSON

    { "ID":1 }

#### XML

    <BlueprintRequest>

        <ID>1</ID>

    </BlueprintRequest>

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
      <td>Parameters</td>
      <td>List (see below)</td>
      <td>A list of the parameters required to deploy the Blueprint (see below)</td>
    </tr>
  </tbody>
</table>

### Parameter Attributes

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
      <td>Name</td>
      <td>String</td>
      <td>
        <p>The name of the Parameter.</p>
      </td>
    </tr>
    <tr>
      <td>Options</td>
      <td>List</td>
      <td>
        <p>A list of options to choose from if the Parameter is an Option or MultiSelect type.</p>
        <p>Each option has 2 attributes:
          <br />Name = The name of the option
          <br />Value = The value of the option&nbsp;</p>
      </td>
    </tr>
    <tr>
      <td>Regex</td>
      <td>String</td>
      <td>
        <p>A regular expression defining any additional validation that the Parameter value must pass.&nbsp;</p>
        <p>This value is supplied by the Blueprint author.</p>
      </td>
    </tr>
    <tr>
      <td>Type</td>
      <td>
        <p>JSON: Int
          <br />XML: String&nbsp;</p>
      </td>
      <td>
        <p>The data type of the Parameter</p>
        <p>1/Network = &nbsp;internal name of an existing network
          <br />2/Numeric = numeric value
          <br />3/Option = constrained to only one of the listed options
          <br />4/Password = password value
          <br />5/Server = name of an existing server
          <br />6/ServerIP = IP address of an existing server
          <br />7/String = string value
          <br />8/MultiSelect = value constrained to one or more of the listed options</p>
      </td>
    </tr>
  </tbody>
</table>

### Examples

#### JSON

    {

      "ID":1,

      "Parameters":[

        {

          "Name":"T3.ScriptTask.Parameter01",

          "Regex":null,

          "Type":7,

          "Options":[]

        },

        {

          "Name":"T3.ScriptTask.Parameter02",

          "Regex":null,

          "Type":3,

          "Options":[

            {"Name":"Option 1","Value":"1"},

            {"Name":"Option 2","Value":"2"}

          ]

        }

      ],

      "Success":true,

      "Message":"Success",

      "StatusCode":0

     }

#### XML

    <GetBlueprintParamatersResponse Success="true" Message="Success" StatusCode="0">

        <ID>46</ID>

        <Parameters>

              <Parameter Name="T3.ScriptTask.Parameter01" Type="String" />

              <Parameter Name="T3.ScriptTask.Parameter02" Type="Option">

                  <Option Name="Option 1" Value="1"/>

                  <Option Name="Option 2" Value="1"/>

              </Parameter>

          </Parameters>

    </GetBlueprintParamatersResponse>

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
      <td>5</td>
      <td>Resource Not Found. &nbsp;A Blueprint with the specified ID cannot be found.</td>
    </tr>
    <tr>
      <td>100</td>
      <td>Authentication Failed. &nbsp;You must logon to the API prior to calling this method.</td>
    </tr>
  </tbody>
</table>
