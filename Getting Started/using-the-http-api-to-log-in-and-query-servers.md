{{{
  "title": "Using the HTTP API to Log In and Query Servers",
  "date": "10-13-2014",
  "author": "Richard Seroter",
  "attachments": []
}}}

<h3>Description</h3>
<p>The Tier 3 API offers SOAP and HTTP web service endpoints. Users of the API must first authenticate themselves and acquire a session cookie before interacting with the servers and services in the Tier 3 cloud.</p>
<p>In this article, we'll walk through the steps necessary to authenticate a user account and use the session cookie to invoke a subsequent service in the Tier 3 API. This demonstration is done via the C# programming language, but the principles remain the
  same in any language.</p>
<h3>Audience</h3>
<ul>
  <li>Developers</li>
</ul>
<h3>Prerequisites</h3>
<ul>
  <li>Must have an API user created in the Tier 3 account.</li>
</ul>
<h3>Detailed Steps</h3>
<ol>
  <li>Create variables to hold the API credentials used to call the Tier 3 API.
    <div>
      <pre>//set API credentials

string key = "[API key]";

string pw = "[API password]";

</pre>
    </div>
  </li>
  <li>Create an HTTP request object that points to the API's Login URL. Set the method of the request to the HTTP POST verb.
    <div>
      <pre>//set URL for login operation

HttpWebRequest req = WebRequest.Create("https://api.tier3.com/REST/Auth/Logon/") as HttpWebRequest;

req.Method = "POST";

</pre>
    </div>
  </li>
  <li>Users of the Tier 3 HTTP API can use either XML or JSON to interact with the service endpoints. The next step is to create the payload for the Login service. In the example below, both an XML and JSON payload are shown. Notice that the "content type"
    of the HTTP request must match the data format being sent to the service.
    <div>
      <pre>//build up payload message (XML)

//string payload = string.Format("&lt;LogonRequest&gt;&lt;APIKey&gt;{0}&lt;/APIKey&gt;&lt;Password&gt;{1}&lt;/Password&gt;&lt;/LogonRequest&gt;", key, pw); ;

//req.ContentType = "text/xml";

            

//build up payload message (JSON)

string payload = string.Format("{\"APIKey\":\"{0}\", \"Password\":\"{1}}\"}", key, pw);

req.ContentType = "application/json";

</pre>
    </div>
  </li>
  <li>Send the payload to the Login operation.
    <div>
      <pre>//convert message to send to byte array

byte[] byteData = UTF8Encoding.UTF8.GetBytes(payload.ToString());

req.ContentLength = byteData.Length;



//put request into stream

using (Stream postStream = req.GetRequestStream())

{

    postStream.Write(byteData, 0, byteData.Length);

}

</pre>
    </div>
  </li>
  <li>Parse the response and save the cookie for future API calls. A valid cookie looks like: <strong>Tier3.API.Cookie=Seed=[seed value]; expires=Fri, 01-Mar-2013 21:59:58 GMT; path=/; HttpOnly</strong>
    <div>
      <pre>//create variable to hold cookie; there is a shortcut in .NET, but this demo uses the most basic technique

string authCookie = string.Empty;



//get response and process it

using (HttpWebResponse resp = req.GetResponse() as HttpWebResponse)

{

     authCookie = resp.Headers["Set-Cookie"];

}

</pre>
    </div>
  </li>
  <li>With an authentication cookie handy, you can now invoke an API operation such as GetServers, which returns the servers within a particular Tier 3 group. First, create a reference to the HTTP URL of the operation. Notice that the method is set to POST
    and the authentication cookie is added to the HTTP header of the request.
    <div>
      <pre>//create new web request

HttpWebRequest reqQuery = WebRequest.Create("https://api.tier3.com/REST/Server/GetServers/") as HttpWebRequest;

reqQuery.Method = "POST";

reqQuery.Headers.Add("Cookie", authCookie);

</pre>
    </div>
  </li>
  <li>As with above, requests to the service can be done with JSON or XML payloads. Both examples are shown below.
    <div>
      <pre>//set query variables

string groupId = "[group ID]";

string acctAlias = "[alias]";



//build up payload message (XML)

//string queryPayload = string.Format("&lt;GetServersRequest&gt;&lt;AccountAlias&gt;{0}&lt;/AccountAlias&gt;&lt;HardwareGroupID&gt;{1}&lt;/HardwareGroupID&gt;&lt;/GetServersRequest&gt;", acctAlias, groupId);

//reqQuery.ContentType = "text/xml";



//build up payload message (JSON)

string queryPayload = string.Format("{{\"AccountAlias\":\"{0}\", \"HardwareGroupID\":\"{1}\"}}", acctAlias, groupId); ;

reqQuery.ContentType = "application/json";

</pre>
    </div>
  </li>
  <li>Send the request message to the endpoint and retrieve the response payload.
    <div>
      <pre>//convert message to send to byte array

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

</pre>
    </div>
  </li>
  <li>Process the response as XML or JSON, depending on how it was returned.</li>
</ol>