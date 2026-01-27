{{{
  "title": "Get Alert Policies",
  "date": "03-25-2015",
  "author": "Bryan Friedman",
  "attachments": []
}}}

Gets a list of alert policies within a given account. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to get a list of alert policies within a given account and what servers are part of these policies. You can also use the IDs provided in this list to add a server to that alert policy using the API.

## URL

### Structure

    GET https://api.ctl.io/v2/alertPolicies/{accountAlias}

### Example

    GET https://api.ctl.io/v2/alertPolicies/ALIAS

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | string | Short code for a particular account | Yes |

## Response

The response will be an `items` objects referencing an array containing one entity for each alert policy in the given account.

### Entity Definition

| Name | Type | Description |
| --- | --- | --- |
| id | string | ID of the alert policy. |
| name | string | Name of the alert policy. |
| actions | array | The actions to perform when the alert is triggered. |
| triggers | array | The definition of the triggers that fire the alert. |
| links | array | Collection of [entity links](../Getting Started/api-v20-links-framework.md) that point to resources related to this policy. |

### Actions Entity

| Name | Type | Description |
| --- | --- | --- |
| action | string | The only action currently supported by alerts is `email`. |
| settings | complex | The only setting currently supported is the `recipients` list, which is an array of email addresses to be notified when the alert is triggered. |

### Triggers Entity

| Name | Type | Description |
| --- | --- | --- |
| metric | string | The metric on which to measure the condition that will trigger the alert: `cpu`, `memory`, or `disk`. |
| duration | string | The length of time in minutes that the condition must exceed the threshold: `00:05:00`, `00:10:00`, `00:15:00`. |
| threshold | number | The threshold that will trigger the alert when the metric equals or exceeds it. This number represents a percentage and must be a value between 5.0 - 95.0 that is a multiple of 5.0. |

### Examples

#### JSON

    {
      "items":[
        {
          "id":"999de90f25ab4308a6c346cd03602fef",
          "name":"Memory Above 90%",
          "actions":[
            {
              "action":"email",
              "settings":{
                "recipients":[
                  "user@company.com"
                ]
              }
            }
          ],
          "links":[
            {
              "rel":"self",
              "href":"/v2/alertPolicies/ALIAS/999de90f25ab4308a6c346cd03602fef",
              "verbs":[
                "GET",
                "DELETE",
                "PUT"
              ]
            }
          ],
          "triggers":[
            {
              "metric":"memory",
              "duration":"00:10:00",
              "threshold":90.0
            }
          ]
        },
        {
          "id":"175c3b5743d64cea952a5cca03bdb2da",
          "name":"CPU Above 75%",
          "actions":[
            {
              "action":"email",
              "settings":{
                "recipients":[
                  "user@company.com"
                ]
              }
            }
          ],
          "links":[
            {
              "rel":"self",
              "href":"/v2/alertPolicies/ALIAS/175c3b5743d64cea952a5cca03bdb2da",
              "verbs":[
                "GET",
                "DELETE",
                "PUT"
              ]
            }
          ],
          "triggers":[
            {
              "metric":"cpu",
              "duration":"00:05:00",
              "threshold":75.0
            }
          ]
        }
      ],
      "links":[
        {
          "rel":"self",
          "href":"/v2/alertPolicies/ALIAS",
          "verbs":[
            "GET",
            "POST"
          ]
        }
      ]
    }
