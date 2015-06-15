{{{
  "title": "API v2.0 Authentication Overview",
  "date": "10-13-2014",
  "author": "Richard Seroter",
  "attachments": []
}}}

### Summary

Authentication to the API v2 is done with the same credentials used to access the CenturyLink Cloud Control Portal. The username and password are provided to the API and in return, the user gets back a credentials object that contains a valid bearer token. This token -- which can be reused for up to 2 weeks -- must be provided on each subsequent API request.

### Walkthrough

#### .NET Framework Example

Below is a brief demonstration of using the .NET framework to retrieve a valid token from the API authentication service.

1. Reference the assemblies needed to make HTTP requests.

  ```
  using System.Net.Http;
  using System.Net.Http.Headers;
  ```

2. Create an instance of the HttpClient object.

  ```
  HttpClient authClient = new HttpClient();
  ```

3. Add an `Accept` header to indicate that returning JSON as a response is ok.

  ```
  authClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));
  ```

4. Create an HttpContent object to hold the JSON payload (`{"username": "[username]", "password": "[password]"}`) sent to the API. Also, note that the content type `application/json` is set.

  ```
  HttpContent content =
     new StringContent("{ \"username\":\"[username]\", \"password\":\"[password]\" }", null, "application/json");
  ```

5. Invoke the API and send the HTTP content using a POST command.

  ```
  HttpResponseMessage message =
      await authClient.PostAsync("https://api.ctl.io/v2/authentication/login", content);
  ```

6. Load the response into a string for parsing.

  ```
  string responseString = await message.Content.ReadAsStringAsync();
  ```

  If valid credentials are provided, an HTTP 200 status is returned along with the following JSON payload:

  ```
    {
       "userName":"user@company.com",
       "accountAlias":"RLS1",
       "locationAlias":"WA1",
       "roles":[
          "ServerAdmin",
          "AccountAdmin"
       ],
       "bearerToken":"[LONG TOKEN VALUE]"
    }
  ```

  These results show the user's parent account, default data center location, and assigned platform roles. The __bearerToken__ is the value that must be added to the HTTP `Authorization` header when calling any other API service. This token identifies who the user is and what they are allowed to do in the API.

  If you provide invalid credentials, you will get an HTTP 400 (Bad Request) and the following response message:

    {"message":"We didn't recognize the username or password you entered. Please try again."}

7. Submit a request: the following .NET code demonstrates how a user can make a secure API request to retrieve the root Group in a particular data center. Note that the __bearerToken__ is added to the header of the request, with a prefix of "Bearer ".

  ```
    HttpClient authClient = new HttpClient();

    authClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

    // Add bearer token to the header
    authClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", "Bearer [LONG TOKEN VALUE]");

    HttpResponseMessage message = await authClient.GetAsync("https://api.ctl.io/v2/datacenters/DEMO/CA1");

    string responseString = await message.Content.ReadAsStringAsync();
  ```

#### PowerShell Example

Below is a brief demonstration of how PowerShell can be used to retrieve a valid token from the API authentication service. Users will need to start PowerShell v4+ as an administrator.


1. Log into the API.

  ```
  $body = @{
    username = 'ControlUsername'
    password = 'ControlPassword'
  }
  $body = $body | ConvertTo-Json

  $headers = New-Object "System.Collections.Generic.Dictionary[[String],[String]]"
  ```

2. Log in to the Platform and get back a `bearerToken`.

  ```
  $logonUrl = "https://api.ctl.io/v2/authentication/login"
  $logonResponse = Invoke-RestMethod -Method Post -Headers $headers -Uri $logonUrl -Body $body -ContentType "application/json" -SessionVariable "theSession"
  ```

3. Pull the BearerToken out of the response and format it correctly. Note that a prefix of "Bearer " is required.

  ```
  $bearer = $logonResponse.bearerToken
  $bearer = " Bearer " + $bearer
  ```

4. Add the Token to the Headers to be used on future requests.

  ```
  $headers.Add("Authorization",$bearer)
  ```

You can now use the session variable for authenticating further API calls. Example:

Here's an example of pulling server credentials:

```
$servercredsURL = "https://api.ctl.io/v2/servers/$AccountName/$servername/credentials"
$serverCreds = Invoke-RestMethod -Method GET -Headers $Headers -Uri $servercredsURL -ContentType "application/json" -SessionVariable "theSession"
```

#### Raw HTTP Example

Below is an example of the raw HTTP request and response messages when retrieving a valid token from the API authentication service.

**Request**

    POST https://api.ctl.io/v2/authentication/login HTTP/1.1
    Host: api.ctl.io
    Content-Type: application/json
    Content-Length: 54

    {
      "username": "[username]",
      "password": "[password]"
    }

**Response**

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Pragma: no-cache
    Content-Type: application/json; charset=utf-8
    Expires: -1
    Date: Fri, 03 Jan 2015 21:23:45 GMT
    Content-Length: 149

    {
      "userName": "user@company.com",
      "accountAlias": "RLS1",
      "locationAlias": "WA1",
      "roles": [
        "ServerAdmin",
        "AccountAdmin"
      ],
      "bearerToken": "[LONG TOKEN VALUE]"
    }

These results show the user's parent account, default data center location, and assigned platform roles. The bearerToken is the value that must be added to the HTTP `Authorization` header when calling any other API service. This token identifies who the user is and what they are allowed to do in the API.

If you provide invalid credentials, you will get an HTTP 400 (Bad Request) and the following response message:

    HTTP/1.1 400 Bad Request
    Cache-Control: no-cache
    Pragma: no-cache
    Content-Type: application/json; charset=utf-8
    Expires: -1
    Date: Fri, 03 Jan 2015 21:26:45 GMT
    Content-Length: 89

    {"message":"We didn't recognize the username or password you entered. Please try again."}

The following raw HTTP request message shows how a user can make a secure API request to retrieve the root Group in a particular data center. Note that the bearerToken is added to the header of the request, with a prefix of "Bearer ".

    GET https://api.ctl.io/v2/datacenters/RLS1/WA1 HTTP/1.1
    Host: api.ctl.io
    Content-Type: application/json
    Content-Length: 0
    Authorization: Bearer [LONG TOKEN VALUE]
