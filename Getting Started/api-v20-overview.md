{{{
  "title": "API v2.0 Overview",
  "date": "10-13-2014",
  "author": "Richard Seroter",
  "attachments": []
}}}

The CenturyLink Cloud has a new, improved API for performing the same actions programmatically as you can with the Control Portal. The API is RESTful and works with JSON messages over HTTP. It relies on the standard HTTP verbs including GET, POST, PUT, DELETE.

The URI format of the service is: `https://api.tier3.com/v2/[resource]/[account alias]`. As an example, to retrieve the top level Group for a given data center, you would issue a GET request to `https://api.tier3.com/v2/datacenters/ALIAS/WA1`. The HTTP request must includ __Content__ and __Accepts__ headers set to __application/json__.

Service authentication is done via bearer tokens and is outlined in the <a href="/api-docs/v2#authentication-login">Login API</a> description.

The service responds to requests using <a href="http://en.wikipedia.org/wiki/List_of_HTTP_status_codes" target="_blank">standard HTTP codes</a>, and if applicable, a JSON payload.

<table>
  <thead>
    <tr>
      <th>HTTP Code</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>200</td>
      <td>OK. Sent when requests are immediately successful and did NOT create a new URL-addressable resource.</td>
    </tr>
    <tr>
      <td>201</td>
      <td>CREATED. Sent when requests are immediately successful and DID create a new URL-addressable resource.</td>
    </tr>
    <tr>
      <td>202</td>
      <td>ACCEPTED. Sent when requests result in a scheduled activity. Response body will include a URL for them to get the response.</td>
    </tr>
    <tr>
      <td>400</td>
      <td>BAD REQUEST. Sent when something is wrong with the query string or message body.</td>
    </tr>
    <tr>
      <td>401</td>
      <td>UNAUTHORIZED. Sent when a bearer token is not provided.</td>
    </tr>
    <tr>
      <td>403</td>
      <td>FORBIDDEN. Sent if the requests violates the security demands of the service.</td>
    </tr>
    <tr>
      <td>404</td>
      <td>NOT FOUND. Sent if the URL points to a non-existent resource.</td>
    </tr>
    <tr>
      <td>500</td>
      <td>INTERNAL SERVER ERROR. Sent if the service experiences an error through no fault of the user.</td>
    </tr>
  </tbody>
</table>
