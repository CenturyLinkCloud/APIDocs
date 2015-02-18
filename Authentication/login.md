{{{
  "title": "Login",
  "date": "11-21-2014",
  "author": "Richard Seroter",
  "attachments": []
}}}

Acquires an authentication token used for subsequent queries to the API.

### When to Use It

Use this API operation before you call any other API operation. It shows a user's roles, primary data center, and a valid bearer token.

## URL

### Structure

    POST https://api.tier3.com/v2/authentication/login

## Request

### Content Properties

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
      <td>username</td>
      <td>string</td>
      <td>Control Portal user name value</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>password</td>
      <td>string</td>
      <td>Control Portal password value.</td>
      <td>Yes</td>
    </tr>
  </tbody>
</table>

### Examples

#### JSON Request

    {
       "username":"demouser1",
       "password":"mypassword"
    }

## Response

### Entity Definition

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
      <td>userName</td>
      <td>string</td>
      <td>Control Portal user name value</td>
    </tr>
    <tr>
      <td>accountAlias</td>
      <td>string</td>
      <td>Account that contains this user record</td>
    </tr>
    <tr>
      <td>locationAlias</td>
      <td>string</td>
      <td>Default data center of the user</td>
    </tr>
    <tr>
      <td>roles</td>
      <td>array</td>
      <td>Permission roles associated with this user</td>
    </tr>
    <tr>
      <td>bearerToken</td>
      <td>string</td>
      <td>Security token for this user that is included in all other API requests</td>
    </tr>
  </tbody>
</table>

### Examples

#### JSON

    {
        "userName": "user@email.com",
        "accountAlias": "ALIAS",
        "locationAlias": "DC1",
        "roles": [
            "AccountAdmin",
            "ServerAdmin"
        ],
        "bearerToken": "ABCDEF"
    }
