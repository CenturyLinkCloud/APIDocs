{{{
  "title": "Authentication Overview",
  "date": "10-13-2014",
  "author": "jw@tier3.com",
  "attachments": []
}}}

Authentication for the Public API will be handled differently than the Tier3 Control System, &nbsp;To create an API user you must access the Control Portal and create an API user <a href="https://control.tier3.com/Organization/Api" target="_blank">here</a>. The credentials for the API consist of a string based API key and a password.&nbsp;
 
Prior to calling into the API, consumers must first call into the Authentication API to Logon. On successful login, the API will write a persistent cookie as part of its response. The encrypted cookie will be evaluated as part of each subsequent request, this will prevent the need of providing credentials with each API call.
  
The URL to the SOAP version of the Authentication API can be found at <a href="https://api.tier3.com/soap/auth.asmx" target="_blank">https://api.tier3.com/soap/auth.asmx</a>&nbsp;and the WSDL can be found <a href="https://api.tier3.com/soap/auth.asmx?wsdl"
target="_blank">here</a>.

For a complete walkthrough of the authentication process with the REST/HTTP API, see the KB article <a href="http://help.tier3.com/entries/23220626-Using-the-HTTP-API-to-Log-In-and-Query-Servers">Using the HTTP API to Log In and Query Servers</a>

<strong>Authentication API Methods:</strong>

<ul>
  <li><a href="http://help.tier3.com/entries/20339862-logon">Logon</a>
  </li>
  <li><a href="http://help.tier3.com/entries/20345428-logout">Logout</a>
  </li>
</ul>