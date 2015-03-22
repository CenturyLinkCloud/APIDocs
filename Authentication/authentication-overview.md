{{{
  "title": "Authentication Overview",
  "date": "10-13-2014",
  "author": "jw@tier3.com",
  "attachments": []
}}}

Authentication for the Public API will be handled differently than the CenturyLink Cloud Control System,  To create an API user you must access the Control Portal and create an API user [here](https://control.ctl.io/Organization/Api). The credentials for the API consist of a string based API key and a password.

Prior to calling into the API, consumers must first call into the Authentication API to Logon. On successful login, the API will write a persistent cookie as part of its response. The encrypted cookie will be evaluated as part of each subsequent request, this will prevent the need of providing credentials with each API call.

The URL to the SOAP version of the Authentication API can be found at [https://api.ctl.io/soap/auth.asmx](https://api.ctl.io/soap/auth.asmx) and the WSDL can be found [here](https://api.ctl.io/soap/auth.asmx?wsdl).

For a complete walkthrough of the authentication process with the REST/HTTP API, see [Using the HTTP API to Log In and Query Servers](../Getting Started/using-the-http-api-to-log-in-and-query-servers.md).

### Authentication API Methods

- [Logon](logon.md)
- [Logout](logout.md)
