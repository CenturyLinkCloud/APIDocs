{{{
  "title": "Delete Anti-Affinity Policy",
  "date": "11-20-2014",
  "author": "Bryan Friedman",
  "attachments": []
}}}

Deletes a given anti-affinity policy by ID. Calls to this operation must include a token acquired from the authentication endpoint. See the <a href="/api-docs/v2#authentication-login">Login API</a> for information on acquiring this token.

### When to Use It

Use this API operation when you want to delete a specific anti-affinity policy within a given account.

### Supported HTTP Verbs

Requests to this endpoint are done via HTTP DELETE.

## URL

### Structure

```
https://api.tier3.com/v2/antiAffinityPolicies/{accountAlias}/{policyId}
```

### Example

```
https://api.tier3.com/v2/antiAffinityPolicies/ALIAS/80a7bf90b199454b859399bff54f4173
```

## Request

### URI Parameters

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
      <td>AccountAlias</td>
      <td>string</td>
      <td>Short code for a particular account</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>PolicyId</td>
      <td>string</td>
      <td>ID of the anti-affinity policy being queried.</td>
      <td>Yes</td>
    </tr>
  </tbody>
</table>

## Response

The response will not contain JSON content, but should return a standard HTTP 200 OK response upon deletion of the policy.
