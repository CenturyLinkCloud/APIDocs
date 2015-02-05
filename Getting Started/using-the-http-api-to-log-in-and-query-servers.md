{{{
  "title": "Using the HTTP API to Log In and Query Servers",
  "date": "10-13-2014",
  "author": "Richard Seroter",
  "attachments": []
}}}

### Description

The Tier 3 API offers SOAP and HTTP web service endpoints. Users of the API must first authenticate themselves and acquire a session cookie before interacting with the servers and services in the Tier 3 cloud.

In this article, we'll walk through the steps necessary to authenticate a user account and use the session cookie to invoke a subsequent service in the Tier 3 API. This demonstration is done via the C# programming language, but the principles remain the same in any language.

### Audience

- Developers

### Prerequisites

- Must have an API user created in the Tier 3 account.

### Detailed Steps

1. Create variables to hold the API credentials used to call the Tier 3 API.

    ```
    //set API credentials

    string key = "[API key]";

    string pw = "[API password]";
    ```

2. Create an HTTP request object that points to the API's Login URL. Set the method of the request to the HTTP POST verb.
    
    ```
    //set URL for login operation

    HttpWebRequest req = WebRequest.Create("https://api.tier3.com/REST/Auth/Logon/") as HttpWebRequest;

    req.Method = "POST";
    ```

3. Users of the Tier 3 HTTP API can use either XML or JSON to interact with the service endpoints. The next step is to create the payload for the Login service. In the example below, both an XML and JSON payload are shown. Notice that the "content type" of the HTTP request must match the data format being sent to the service.

    ```
    //build up payload message (XML)

    //string payload = string.Format("<LogonRequest><APIKey>{0}</APIKey><Password>{1}</Password></LogonRequest>", key, pw); ;

    //req.ContentType = "text/xml";

                

    //build up payload message (JSON)

    string payload = string.Format("{'APIKey':'0}', 'Password':'{1}}'}", key, pw);

    req.ContentType = "application/json";

    4. Send the payload to the Login operation.

    //convert message to send to byte array

    byte[] byteData = UTF8Encoding.UTF8.GetBytes(payload.ToString());

    req.ContentLength = byteData.Length;



    //put request into stream

    using (Stream postStream = req.GetRequestStream())

    {

        postStream.Write(byteData, 0, byteData.Length);

    }
    ```


4. Parse the response and save the cookie for future API calls. A valid cookie looks like: <strong>Tier3.API.Cookie=Seed=[seed value]; expires=Fri, 01-Mar-2013 21:59:58 GMT; path=/; HttpOnly</strong>

    ```
    //create variable to hold cookie; there is a shortcut in .NET, but this demo uses the most basic technique

    string authCookie = string.Empty;



    //get response and process it

    using (HttpWebResponse resp = req.GetResponse() as HttpWebResponse)

    {

         authCookie = resp.Headers["Set-Cookie"];

    }
    ```

5. With an authentication cookie handy, you can now invoke an API operation such as GetServers, which returns the servers within a particular Tier 3 group. First, create a reference to the HTTP URL of the operation. Notice that the method is set to POST and the authentication cookie is added to the HTTP header of the request.

    ```
    //create new web request

    HttpWebRequest reqQuery = WebRequest.Create("https://api.tier3.com/REST/Server/GetServers/") as HttpWebRequest;

    reqQuery.Method = "POST";

    reqQuery.Headers.Add("Cookie", authCookie);
    ```

6. As with above, requests to the service can be done with JSON or XML payloads. Both examples are shown below.

    ```
    //set query variables

    string groupId = "[group ID]";

    string acctAlias = "[alias]";



    //build up payload message (XML)

    //string queryPayload = string.Format("<GetServersRequest><AccountAlias>{0}</AccountAlias><HardwareGroupID>{1}</HardwareGroupID></GetServersRequest>", acctAlias, groupId);

    //reqQuery.ContentType = "text/xml";



    //build up payload message (JSON)

    string queryPayload = string.Format("{'AccountAlias':'{0}', 'HardwareGroupID':'{1}'}", acctAlias, groupId);

    reqQuery.ContentType = "application/json";
    ```

7. Send the request message to the endpoint and retrieve the response payload.

    ```
    //convert message to send to byte array

    byte[] byteDataQuery = UTF8Encoding.UTF8.GetBytes(queryPayload.ToString());

    reqQuery.ContentLength = byteDataQuery.Length;



    string queryResponse = string.Empty;



    //put request into stream

    using (Stream postStream = reqQuery.GetRequestStream())

    {

       postStream.Write(byteDataQuery, 0, byteDataQuery.Length);

    }



    //invoke service

    using (HttpWebResponse resp = reqQuery.GetResponse() as HttpWebResponse)

    {

        // Get the response stream  

        using (StreamReader reader = new StreamReader(resp.GetResponseStream()))

        {

           //load response

           queryResponse = reader.ReadToEnd();

         }

    }
    ```

8. Process the response as XML or JSON, depending on how it was returned.
