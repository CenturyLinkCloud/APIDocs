{{{
  "title": "API v2.0 Overview",
  "date": "10-13-2014",
  "author": "Richard Seroter",
  "sticky": true,
  "attachments": []
}}}

The CenturyLink Cloud has a new, improved API for performing the same actions programmatically as you can with the Control Portal. The API is RESTful and works with JSON messages over HTTP. It relies on the standard HTTP verbs including GET, POST, PUT, DELETE, and PATCH.

The URL format of the service is: `https://api.ctl.io/v2/{resource}/{account alias}`. As an example, to retrieve the top level Group for a given data center, you would issue a GET request to `https://api.ctl.io/v2/datacenters/ALIAS/WA1`. The HTTP request must include `Content-Type` and `Accepts` headers set to `application/json`.

### Authentication

Service authentication is done via bearer tokens and is outlined in the [Authentication Overview](api-v20-authentication-overview.md) and also the [Login API](../Authentication/login.md) description.

### Links Framework

The CenturyLink Cloud v2 REST API utilizes the concept of "linking" to reference other related entities from within JSON response payloads. See more information in our overview of the [Links Framework](api-v20-links-framework.md).

### HTTP Response Codes

The service responds to requests using [standard HTTP codes](http://en.wikipedia.org/wiki/List_of_HTTP_status_codes), and if applicable, a JSON payload.

|HTTP Code|Description|
|---|---|
|200|OK. Sent when requests are immediately successful and did NOT create a new URL-addressable resource.|
|201|CREATED. Sent when requests are immediately successful and DID create a new URL-addressable resource.|
|202|ACCEPTED. Sent when requests result in a scheduled activity. Response body will include a URL for them to get the status of the activity.|
|204|NO CONTENT. Sent when requests are immediately successful but return no additional information about the resource.|
|400|BAD REQUEST. Sent when something is wrong with the query string or message body.|
|401|UNAUTHORIZED. Sent when a bearer token is not provided.|
|403|FORBIDDEN. Sent if the request violates the security demands of the service.|
|404|NOT FOUND. Sent if the URL points to a non-existent resource.|
|500|INTERNAL SERVER ERROR. Sent if the service experiences an error through no fault of the user.|
