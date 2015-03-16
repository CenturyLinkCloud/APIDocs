{{{
  "title": "API v2.0 Authentication Overview",
  "date": "10-13-2014",
  "author": "Richard Seroter",
  "attachments": []
}}}

### Summary

Authentication to the API v2 is done with the same credentials used to access the CenturyLink Cloud Control Portal. The username and password are provided to the API and in return, the user gets back a credentials object that contains a valid bearer token. This token -- which can be reused for up to 2 weeks -- must be provided on each subsequent API request.

### Walkthrough

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

These results show the user's parent account, default data center location, and assigned platform roles. The __bearerToken__ is the value that must be added to the HTTP `Authorization` header when calling any other API service. This token identifies who the user is and what they are allowed to do in the API.

If you provide invalid credentials, you will get an HTTP 400 (Bad Request) and the following response message:

    {"message":"We didn't recognize the username or password you entered. Please try again."}

The following .NET code demonstrates how a user can make a secure API request to retrieve the root Group in a particular data center. Note that the __bearerToken__ is added to the header of the request.

    HttpClient authClient = new HttpClient();

    authClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

    // Add bearer token to the header
    authClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", "[LONG TOKEN VALUE]");

    HttpResponseMessage message = await authClient.GetAsync("https://api.ctl.io/v2/datacenters/DEMO/CA1");
    
    string responseString = await message.Content.ReadAsStringAsync();

