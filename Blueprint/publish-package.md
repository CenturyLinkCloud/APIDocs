{{{
  "title": "Publish Package",
  "date": "12-2-2014",
  "author": "Troy Schneringer",
  "attachments": []
}}}


Publishes a Blueprint Package for use within the Blueprint Designer.

## URL

    REST: https://api.tier3.com/REST/Blueprint/PublishPackage/&lt;format&gt;
    SOAP: https://api.tier3.com/SOAP/Blueprints.asmx?op=PublishPackage

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
      <td>Classification</td>
      <td>Int</td>
      <td>
        <p>The type of Packages that should be returned</p>
        <p>1 = System (reserved by Tier3)
          <br />2 = Script
          <br />3 = Software</p>
      </td>
      <td>
        <p>Yes</p>
      </td>
    </tr>
    <tr>
      <td>Name</td>
      <td>String</td>
      <td>
        <p>The name of the Package file to publish.</p>
        <p>Obtained via the <a href="http://help.tier3.com/entries/20428161-get-pending-packages">GetPendingPackages</a> method.</p>
      </td>
      <td>
        <p>Yes</p>
      </td>
    </tr>
    <tr>
      <td>OperatingSystems</td>
      <td>Int[]</td>
      <td>
        <p>A list of operating systems that this Package can be deployed to</p>
        <p>* The most recent list is always available from the <a href="https://t3n.zendesk.com/entries/23102683-List-Available-Server-Templates">ListAvailableServerTemplates</a> API call.&nbsp;</p>
        <pre>+-----------------+---------------------------------------------+

| OperatingSystem | Description                                 |

+-----------------+---------------------------------------------+

| 2               | Windows 2003 R2 Standard | 32-bit           |

| 3               | Windows 2003 R2 Standard | 64-bit           |

| 5               | Windows 2008 R2 Standard | 64-bit           |

| 15              | Windows 2003 R2 Enterprise | 32-bit         |

| 16              | Windows 2003 R2 Enterprise | 64-bit         |

| 18              | Windows 2008 R2 Enterprise | 64-bit         |

| 20              | BOSH Stemcell Template                      |

| 20              | Stemcell | Micro-BOSH                       |

| 25              | RedHat Enterprise Linux 5 | 64-bit          |

| 26              | Windows 2008 R2 Datacenter Edition | 64-bit |

| 27              | Windows 2012 Datacenter Edition | 64-bit    |

| 28              | Windows 2012 R2 Datacenter Edition | 64-bit |

| 29              | Ubuntu 10 | 32-bit                          |

| 30              | Ubuntu 10 | 64-bit                          |

| 30              | Web Fabric Ubuntu x64 Template              |

| 30              | Web Fabric Ubuntu x64 Template V2           |

| 31              | Ubuntu 12 | 64-bit                          |

| 32              | CentOS 5 | 32-bit                           |

| 33              | CentOS 5 | 64-bit                           |

| 34              | CentOS 6 | 32-bit                           |

| 35              | CentOS 6 | 64-bit                           |

| 36              | Debian 6 | 64-bit                           |

| 37              | Debian 7 | 64-bit                           |

| 38              | RedHat Enterprise Linux 6 | 64-bit          |

| 40              | PXE Boot [EXPERIMENTAL]                     |

| 41              | Ubuntu 14 | 64-bit                          |

+-----------------+---------------------------------------------+

</pre>
      </td>
      <td>
        <p>Yes</p>
      </td>
    </tr>
    <tr>
      <td>Visibility</td>
      <td>Int</td>
      <td>
        <p>The visibility of Packages that should be returned</p>
        <p>1 = Public
          <br />2 = Private
          <br /> 3 = Shared</p>
      </td>
      <td>
        <p>Yes</p>
      </td>
    </tr>
  </tbody>
</table>

### Examples

<h4>JSON</h4>
<pre>{ <br />    "Classification": "2",<br />    "Name":"Script01.zip",<br />    "OperatingSystems":[4,5],<br />    "Visibility": "1" <br />}&nbsp;</pre>

<h4>XML</h4>
<pre>&lt;PublishPackageRequest&gt;<br />&nbsp; &nbsp; &lt;Classification&gt;2&lt;/Classification&gt;<br />    &lt;Name&gt;Script01.zip&lt;/Name&gt;<br />    &lt;OperatingSystems&gt;<br />        &lt;OS&gt;4&lt;/OS&gt;<br />        &lt;OS&gt;5&lt;/OS&gt;&nbsp;

  &lt;/OperatingSystems&gt;<br />&nbsp; &nbsp; &lt;Visibility&gt;1&lt;/Visibility&gt;<br />&lt;/PublishPackageRequest&gt;&nbsp;</pre> 

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
      <td>RequestID</td>
      <td>Int</td>
      <td>
        <p>The ID of the Queued request to publish the Package.</p>
        <p>Status of the request can be obtained by calling the <a href="http://help.tier3.com/entries/20345638-get-request-status">GetRequestStatus</a> method.</p>
      </td>
    </tr>
  </tbody>
</table>

### Examples
<h4>JSON</h4>
<pre>{<br />&nbsp; &nbsp; "RequestID": 1,<br />&nbsp; &nbsp; "Success":true,<br />&nbsp; &nbsp; "Message":"Success",<br />&nbsp; &nbsp; "StatusCode":0<br />}</pre>
<h4>XML</h4>
<div>
  <div>
    <pre>&lt;QueuedItemResponse Success="true" Message="Success" StatusCode="0"&gt;<br />&nbsp; &nbsp; &lt;RequestID&gt;1&lt;/RequestID&gt;<br />&lt;/QueuedItemResponse&gt;</pre>
  </div>
</div>

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
      <td>Unknown Error - An application error occurred processing your request, contact Tier3 support to resolve the issue.</td>
    </tr>
    <tr>
      <td>3</td>
      <td>Invalid Request Format. This value indicates that the XML or JSON requests do not match the expected format.</td>
    </tr>
    <tr>
      <td>100</td>
      <td>Authentication Failed - You must logon to the API prior to calling this method.</td>
    </tr>
    <tr>
      <td>1200</td>
      <td>The Classification value is missing or invalid.</td>
    </tr>
    <tr>
      <td>1201</td>
      <td>The Visibility value is missing or invalid.
        <br />
        <br />
      </td>
    </tr>
    <tr>
      <td>1202</td>
      <td>The supplied operating system values are missing or invalid.</td>
    </tr>
  </tbody>
</table>
