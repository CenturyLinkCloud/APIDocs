{{{
  "title": "Get Status",
  "date": "10-13-2014",
  "author": "Bryan Friedman",
  "attachments": []
}}}

Gets the status of a particular job in the queue, which keeps track of any long-running asynchronous requests (such as server power operations or provisioning tasks). Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](..Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to check the status of a specific job in the queue. It is usually called after running a batch job and receiving the job identifier from the status link (e.g. [Power On Server](../Power Operations/power-on-server.md), [Create Server](../Servers/create-server.md), etc.) and will typically continue to get called until a "succeeded" or "failed" response is returned.

## URL

### Structure

    GET https://api.ctl.io/v2/operations/{acctAlias}/status/{statusId}

### Example

    GET https://api.ctl.io/v2/operations/ALIAS/status/wa1-12345

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
      <td>Short code for a particular account.</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>Status ID</td>
      <td>string</td>
      <td>ID of the job to query. Retrieved from the status link in the response to a batch job request.</td>
      <td>Yes</td>
    </tr>
  </tbody>
</table>

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
      <td>Status</td>
      <td>string</td>
      <td>The status of the operation. Will be one of the following: "notStarted", "executing", "succeeded", "failed", "resumed" or "unknown".</td>
    </tr>
  </tbody>
</table>

### Examples

#### JSON

    {
      "status":"succeeded"
    }
