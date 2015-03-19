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

    POST https://api.ctl.io/v2/authentication/login

## Request

### Content Properties

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| username | string | Control Portal user name value | Yes |
| password | string | Control Portal password value. | Yes |

### Examples

#### JSON

    {
       "username":"demouser1",
       "password":"mypassword"
    }

## Response

### Entity Definition

| Name | Type | Description |
| --- | --- | --- |
| userName | string | Control Portal user name value |
| accountAlias | string | Account that contains this user record |
| locationAlias | string | Default data center of the user |
| roles | array | Permission roles associated with this user |
| bearerToken | string | Security token for this user that is included in all other API requests |

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
